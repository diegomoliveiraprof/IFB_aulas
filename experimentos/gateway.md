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

## 5. Configuração de rede

Para configurar a rede é necessário editar o arquivo de configuração, que no caso do Ubuntu é `/etc/netplan/00-installer-config.yaml`, o edidor de texto que utilizaremos é o nano `nano`.
Para ser capaz de modificar arquivos de configuração é necessário utilizar permissões de super usuário, neste caso pode se logar diretamente como usuário `root` ou usar o `sudo` antes dos comandos.

