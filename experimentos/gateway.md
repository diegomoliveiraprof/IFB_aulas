# Gateway


## 1. Objetivo

- Entender os conceitos relacionados a um **Gateway**  
- Reforçar os conhecimentos de Linux, incluindo manipulação de arquivos e diretórios, arquivos de configuração, editores e comandos  
- Utilizar um Linux Ubuntu Server para criar um gateway  

### 2. Conceitos envolvidos
* IP público e privado  
* Gateway  
* Encaminhamento de pacotes  
* Network Address Translation (NAT)  
* Shell Script  
* IP estático e dinâmico  

---

## 3. Diagrama do Experimento

![Diagrama do Gateway](../img/crs_gateway_diagrama.png)

---
## 4. Configurar placas de rede

* Uma máquina gateway (gw), precisa ter duas placas de rede (reais ou virtuais), uma fica ligada na rede interna e outra fica ligada na saída para a internet.
* A placa 0 será a saída e fica com ip automático (dhcp).
* A placa 1 será a ligação com a rede interna e ficará com ip estático.
* É preciso modificar o arquivo de configuração das interfaces de rede.
* Seguem os comandos e um exemplo de arquivo de configuração.

---

## 5. Configuração de rede

Para configurar a rede, é necessário editar o arquivo de configuração. No Ubuntu, esse arquivo geralmente está localizado em:
`/etc/netplan/00-installer-config.yaml ou /etc/netplan/01-netcfg.yaml`

O editor de texto que utilizaremos será o `nano` (nano).

Como se trata de um arquivo de configuração do sistema, é preciso ter permissões de superusuário. Para isso, você pode:

Logar diretamente como usuário `root`, ou

Utilizar o comando `sudo` antes das instruções no terminal.

### Editando o arquivo de configuração de rede

O comando `ls /etc/netplan` deve ser utilizado para verificar qual o nome correto do arquivo antes de tentar editar.   

Ainda antes de editar o arquivo de configuração de rede é necessário saber o nome das interfaces disponíveis na máquina.   
Isso pode ser feito com o comando `networkclt`, que em sua saída, mostrará o nome das interfaces.
Comando:
```
networkcl

```   
Saída
<img width="450" height="179" alt="crs_netwokclt" src="https://github.com/user-attachments/assets/806a70c0-03b2-44d8-8f97-c22769bf3794" />   

Neste caso a interface `ensp03 é a primeira e ensp8 é segunda inteface física`    
Comando:   
```
nano /etc/netplan/00-installer-config.yaml
ou
nano /etc/netplan/01-netcfg.yaml
```


_**Obs.:** Arquivos com extensão `.yaml` NÃO suportam tabulação.   
Portanto, não utilize a tecla `TAB` ao editar esses arquivos;    
use apenas espaços para indentar corretamente._   

