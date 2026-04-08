# Systemd


## 1. Objetivo

- Compreender o papel do **systemd** como sistema de inicialização e gerenciador de serviços no Linux.  
- Utilizar o comando **systemctl** para iniciar, parar, reiniciar, habilitar e verificar o status de serviços.  
- Analisar o **ciclo de vida de um serviço** e os impactos de ativá-lo ou desativá-lo.  
- Realizar testes práticos de funcionamento de serviços (ex.: consultas DNS com `nslookup`).  
- Interpretar informações de **status e logs** para diagnosticar problemas em serviços.  
- Configurar serviços para inicialização automática e compreender a importância dos **targets**.  
- Desenvolver autonomia na administração de serviços em ambientes Linux.  


## 2. Conceitos envolvidos

* Systemd como init system
- Responsável por inicializar e gerenciar serviços e processos no Linux.

- Units
- Arquivos de configuração que descrevem recursos gerenciados pelo systemd.
- Tipos principais:
  - `.service` → serviços (ex.: `nginx.service`)
  - `.socket` → soquetes de rede
  - `.target` → grupos de serviços (ex.: `multi-user.target`)
  - `.timer` → agendamento de tarefas
  - `.mount` → pontos de montagem

* Serviços (`.service`)
- Programas ou processos que rodam em segundo plano.
- Exemplos: DNS, Apache, SSH.
- Controlados pelo comando `systemctl`.

* Comando systemctl
- Ferramenta para interagir com o systemd.
- Permite:
  - Iniciar (`systemctl start`)
  - Parar (`systemctl stop`)
  - Reiniciar (`systemctl restart`)
  - Verificar status (`systemctl status`)
  - Habilitar na inicialização (`systemctl enable`)
  - Desabilitar da inicialização (`systemctl disable`)

* Status e Logs
- `systemctl status nome.service` → mostra se o serviço está ativo/inativo.
- `journalctl -u nome.service` → exibe logs detalhados do serviço.

* Dependências e Targets
- Targets agrupam serviços (ex.: `multi-user.target`, `graphical.target`).
- Garantem que serviços sejam carregados na ordem correta.

* Teste de funcionamento de serviços
- Uso de ferramentas externas para validar funcionamento:
  - `nslookup` → para DNS

* Ciclo de vida de um serviço
- Ativo → Parado → Teste → Reinício.
- Demonstra como o administrador controla e monitora serviços.

* Habilitação na inicialização
- `systemctl enable nome.service` → inicia automaticamente ao ligar o sistema.
- `systemctl disable nome.service` → remove da inicialização.

* Resiliência e reinício automático
- Configurações em units permitem definir comportamento em caso de falha:
  ```bash
  [Service]
  Restart=always  #sempre reiniciar em caso de falha
  RestartSec=5    #tempo de espera antes e reiniciar

Configurações em units permitem definir comportamento em caso de falha (Restart=always).

## 3. Colocando um serviço na inicialização

Será criado um serviço para controlar e ativar automaticamente o NAT.   
Para colocar um novo serviço ou um _script_ na inicialização via systemctl, é preciso criar um arquivo unit para o serviço/script.   
O script pode ser criado em qualquer parte do sistema, mas vamos adotar um padrão e criar o script e o unit na pasta  `/usr/local/bin/`.   

- Controlando o serviço

  Para controlar o serviço será aproveitado o _script_ criado no experimento anterior.

- Inicializar o serviço automaticamente

  Para criar o serviço, é necessário criar o arquivo unit, que possui as opções do serviço e utiliza o _script_ para controlar as ações necessárias.

#### 3.1 Arquivo Unit

Criando o arquivo na pasta: `/usr/local/bin/`

Comando:

```
nano /usr/local/bin/nat.service
```

Conteúdo:

```bash
[Unit]
Description=gateway

[Service]
Type=simple
RemainAfterExit=yes
ExecStart=/bin/bash /usr/local/bin/nat.sh start
ExecStop=/bin/bash /usr/local/bin/nat.sh stop
ExecReload=/bin/bash /usr/local/bin/nat.sh restart

[Install]
WantedBy=multi-user.target
Alias=nat.service
```
Savar o arquivo e sair.   

**Explicando as linhas do arquivo:**   
```bash
[Unit]
Description=gateway
``` 
  - **[Unit] →** Seção que descreve informações gerais sobre a unit.

  - **Description=gateway →** Texto descritivo que identifica o serviço. É exibido em comandos como `systemctl status`.

```bash
[Service]
Type=simple
RemainAfterExit=yes
ExecStart=/bin/bash /usr/local/bin/nat.sh start
ExecStop=/bin/bash /usr/local/bin/nat.sh stop
ExecReload=/bin/bash /usr/local/bin/nat.sh restart
``` 

  - **[Service] →** Seção que define como o serviço deve ser executado.


  - **Type=simple →** Indica que o processo iniciado pelo `ExecStart` é o próprio serviço e não cria processos filhos complexos. É o tipo mais comum.


  - **RemainAfterExit=yes →** Diz ao systemd para considerar o serviço como ativo mesmo após o _script_ terminar. Útil quando o _script_ configura algo persistente (como rotas ou firewall).


  - **ExecStart →** Comando executado para iniciar o serviço. Aqui, chama o _script_ nat.sh com o parâmetro `start`.


  - **ExecStop →** Comando para parar o serviço, chamando o _script_ com `stop`.


  - **ExecReload →** Comando para recarregar a configuração do serviço, chamando o _script_ com `restart`.

```bash
[Install]
WantedBy=multi-user.target
Alias=nat.service

``` 
  - **[Install] →** Seção que define como o serviço será habilitado na inicialização.

  - **WantedBy=multi-user.target →** Faz com que o serviço seja iniciado automaticamente quando o sistema entra no target `multi-user` (modo texto, sem interface gráfica, equivalente ao runlevel 3).

  - **Alias=internet.service →** Cria um nome alternativo para a unit, permitindo que ela seja referenciada como `nat.service` além do nome original.

  - **Configuração e Habilitação de um Arquivo Unit no systemd**    

  - **Configurar as permissões do arquivo unit**  

```bash
chmod 640 /usr/local/bin/nat.service
```
**Habilitar o novo serviço no systemctl**
```bash
systemctl enable /usr/local/bin/nat.service
systemctl daemon-reload
```

**Reiniciar a máquina e verificar as regras de NAT**
```bash
reboot
iptables -L -t nat
```

## 4. Controle do Serviço nat.service

| Ação                        | Comando                         | Descrição                                      |
|------------------------------|---------------------------------|------------------------------------------------|
| Iniciar o serviço            | `systemctl start nat.service`   | Executa o serviço imediatamente.               |
| Parar o serviço              | `systemctl stop nat.service`    | Interrompe a execução do serviço.              |
| Reiniciar o serviço          | `systemctl restart nat.service` | Para e inicia novamente o serviço.             |
| Verificar o status do serviço| `systemctl status nat.service`  | Mostra se está ativo, inativo ou falhou, <br>além de detalhes do processo. |

## 5. Targets

Em resumo: targets são pontos de controle que definem o estado global do sistema, agrupando serviços de acordo com a necessidade (modo gráfico, modo texto, recuperação, desligamento, etc.).

| Target | Equivalente (runlevel antigo) | Função principal |
| --- | --- | --- |
| ``poweroff.target`` | Runlevel 0 | Desliga o sistema |
| ``rescue.target`` | Runlevel 1 | Modo de recuperação (mínimo de serviços) |
| ``multi-user.target`` | Runlevel 3 | Modo multiusuário, sem interface gráfica |
| ``graphical.target`` | Runlevel 5 | Modo multiusuário com interface gráfica |
| ``reboot.target`` | Runlevel 6 | Reinicia o sistema |

