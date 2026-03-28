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
  ```ini
  [Service]
  Restart=always  #sempre reiniciar em caso de falha
  RestartSec=5    #tempo de espera antes e reiniciar

Configurações em units permitem definir comportamento em caso de falha (Restart=always).

## 3. Script de controle do NAT

Exemplo de _script_ para controlar a ativação/desativação das regras de NAT no IPTABLES.

Comando:   
```
sudo su
nano /usr/local/bin/nat.sh
```

<img width="1365" height="784" alt="internetNAT (3)" src="https://github.com/user-attachments/assets/9a3d0eaf-bc9c-4531-ad7e-a6c02ba5946c" />


