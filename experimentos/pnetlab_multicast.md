# Experimento de demonstração de laboratório no pnetlab





## Objetivo

O objetivo deste laboratório é projetar, configurar e validar uma infraestrutura de rede complexa que integre serviços essenciais de conectividade e transmissão de mídia. O foco principal é demonstrar a viabilidade do **roteamento multicast** em uma topologia com múltiplos saltos (multi-hop), garantindo a eficiência da rede através do protocolo **PIM (Protocol Independent Multicast)**. Além disso, o experimento visa consolidar o conhecimento em roteamento dinâmico com **OSPF** para alta disponibilidade e a implementação de **NAT (PAT)** para permitir que redes privadas acessem recursos na internet de forma simultânea.



## Conceitos envolvidos

* **Endereçamento IPv4:** Planejamento de sub-redes utilizando máscaras de tamanho fixo para organização dos ativos.
* **OSPF (Open Shortest Path First):** Protocolo de roteamento *Link-State* utilizado para convergência rápida e escolha do melhor caminho baseado em custo, permitindo redundância (anel de roteamento).
* **Tradução NAT (Overload/PAT):** Técnica para mapear múltiplos endereços privados (RFC 1918) para um único endereço público global, economizando o espaço de endereçamento IP.
* **Transmissão Multicast (PIM Sparse-Mode):** Método de entrega de dados "um para muitos", onde o tráfego só é enviado para segmentos de rede que possuem receptores ativos, economizando largura de banda.
* **IGMP (Internet Group Management Protocol):** Protocolo utilizado por hosts e roteadores adjacentes para estabelecer membros de grupos multicast.
* **RP (Rendezvous Point):** Ponto de encontro central em redes PIM Sparse-Mode para a coordenação entre fontes e receptores.
* dentre outros.



## Cenário


<img width="1699" height="775" alt="Captura de tela de 2026-04-11 22-58-45" src="https://github.com/user-attachments/assets/9afde004-acf4-4c97-9079-5281353c15c8" />





## Dispositivos

| Dispositivo   | Tipo       | Imagem/Versão | Quantidade                                        |
| ------------- | ---------- | ---------------------------------------------------- |----------|
| Roteador    | Router     | i86bi_Linux-L3-AdvEnterpriseK9- M2_157_3_May_2018.bin | 6 |
| Switch      | Switch L2  | i86bi_Linux-L2-AdvEnterpriseK9-M_152_May_2018.bin    |4|
| VPCs           | PC virtual       | VPCs                                                  |4|
| VM Xubuntu    | Máquina VM | Xubuntu completa                                     |1|
| VM Linux MATE | Máquina VM | Linux MATE completa                                  |1|
| MATE Docker.io | Container Docker | pnetlab/linux-desktio:latest |2|





## Endereçamento

## 🌐 Roteador R0
| Interface | Endereço IP     |
|-----------|-----------------|
| e0/0      | 192.168.73.1/24 |
| e0/1      | 192.168.71.2/24 |
| e0/2      | 192.168.72.1/24 |

## 🌐 Roteador R1
| Interface | Endereço IP     |
|-----------|-----------------|
| e0/0      | 192.168.71.1/24 |
| e0/1      | 192.168.70.1/24 |

## 🌐 Roteador R2
| Interface | Endereço IP     |
|-----------|-----------------|
| e0/0      | 192.168.70.2/24 |
| e0/1      | 172.16.20.1/24  |
| e0/2      | 172.16.30.2/24  |

## 🌐 Roteador R3
| Interface | Endereço IP              |
|-----------|--------------------------|
| e0/0      | 172.16.20.2/24           |
| e0/1      | 172.16.40.1/24           |
| e0/2      | DHCP Cloud_nat/pnetlab   |

## 🌐 Roteador R4
| Interface | Endereço IP     |
|-----------|-----------------|
| e0/0      | 172.16.50.2/24  |
| e0/1      | 172.16.30.1/24  |

## 🌐 Roteador R5
| Interface | Endereço IP     |
|-----------|-----------------|
| e0/0      | 172.16.40.2/24  |
| e0/1      | 172.16.50.1/24  |
| e0/2      | 172.16.60.1/24  |

## 🌐 Roteador R6
| Interface | Endereço IP     |
|-----------|-----------------|
| e0/0      | 172.16.60.2/24  |
| e0/1      | 192.168.74.1/24 |
| e0/2      | 192.168.75.1/24 |

---

# 🖥️ Servidores e Hosts

| Dispositivo     | Interface | Endereço IP     |
|-----------------|-----------|-----------------|
| MATE VLC Server | e0        | 192.168.73.10/24 |
| Xubuntu         | e0        | 192.168.74.20/24 |
| Lunux.d1        | eth1      | 192.168.72.20/24 |
| Lunux.d1        | eth1      | 192.168.75.10/24 |

---

# 💻 VPCs

| Dispositivo | Interface | Endereço IP     |
|-------------|-----------|-----------------|
| VPC_1       | eth0      | 192.168.73.20/24 |
| VPC_2       | eth0      | 192.168.72.10/24 |
| VPC_3       | eth0      | 192.168.74.30/24 |
| VPC_4       | eth0      | 192.168.75.20/24 |




## Configuração



### Roteador R0

```
en
conf t
hostname R0
ip multicast-routing
ip pim rp-address 192.168.73.1
interface Ethernet0/0
ip address 192.168.73.1 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/1
ip address 192.168.71.2 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/2
ip address 192.168.72.1 255.255.255.0
ip pim sparse-mode
no shutdown
exit
router ospf 1
network 192.168.71.0 255.255.255.0 area 0
network 192.168.72.0 255.255.255.0 area 0
network 192.168.73.0 255.255.255.0 area 0
exit
```



### Roteador R1

```
en
conf t
hostname R1
ip multicast-routing
ip pim rp-address 192.168.73.1
interface Ethernet0/0
ip address 192.168.71.1 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/1
ip address 192.168.70.1 255.255.255.0
ip pim sparse-mode
no shutdown
exit
router ospf 1
network 192.168.70.0 255.255.255.0 area 0
network 192.168.71.0 255.255.255.0 area 0
exit
```



### Roteador R2

```
en
conf t
hostname R2
ip multicast-routing
ip pim rp-address 192.168.73.1
interface Ethernet0/0
ip address 192.168.70.2 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/1
ip address 172.16.20.1 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/2
ip address 172.16.30.2 255.255.255.0
ip pim sparse-mode
no shutdown
exit
router ospf 1
network 192.168.70.0 255.255.255.0 area 0
network 172.16.20.0 255.255.255.0 area 0
network 172.16.30.0 255.255.255.0 area 0
exit
```



### Roteador R3

```
en
conf t
hostname R3
ip multicast-routing
ip pim rp-address 192.168.73.1
interface Ethernet0/0
ip address 172.16.20.2 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/1
ip address 172.16.40.1 255.255.255.0
ip pim sparse-mode
no shutdown
exit
router ospf 1
network 172.16.20.0 255.255.255.0 area 0
network 172.16.40.0 255.255.255.0 area 0
exit
```



### Roteador R4

```
en
conf t
hostname R4
ip multicast-routing
ip pim rp-address 192.168.73.1
interface Ethernet0/0
ip address 172.16.50.2 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/1
ip address 172.16.30.1 255.255.255.0
ip pim sparse-mode
no shutdown
exit
router ospf 1
network 172.16.30.0 255.255.255.0 area 0
network 172.16.50.0 255.255.255.0 area 0
exit
```



### Roteador R5

```
en
conf t
hostname R5
ip multicast-routing
ip pim rp-address 192.168.73.1
interface Ethernet0/0
ip address 172.16.40.2 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/1
ip address 172.16.50.1 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/2
ip address 172.16.60.1 255.255.255.0
ip pim sparse-mode
no shutdown
exit
router ospf 1
network 172.16.40.0 255.255.255.0 area 0
network 172.16.50.0 255.255.255.0 area 0
network 172.16.60.0 255.255.255.0 area 0
exit
```



### Roteador R6

```
en
conf t
hostname R6
ip multicast-routing
ip pim rp-address 192.168.73.1
interface Ethernet0/0
ip address 172.16.60.2 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/1
ip address 192.168.74.1 255.255.255.0
ip pim sparse-mode
no shutdown
interface Ethernet0/2
ip address 192.168.75.1 255.255.255.0
ip pim sparse-mode
no shutdown
exit
router ospf 1
network 172.16.60.0 255.255.255.0 area 0
network 192.168.74.0 255.255.255.0 area 0
network 192.168.75.0 255.255.255.0 area 0
exit
```



### Roteador R3 - Configuração extra

Saída para internet e NAT.

```
conf t
interface Ethernet0/2
description SAIDA_INTERNET_NAT
ip address dhcp          
ip nat outside           
no shutdown
interface Ethernet0/0
ip nat inside
interface Ethernet0/1
ip nat inside
exit
access-list 10 permit 172.16.0.0 0.0.255.255
access-list 10 permit 192.168.0.0 0.0.255.255
ip nat inside source list 10 interface Ethernet0/2 overload

```



Rota padrão para toda a rede OSPF

```
conf t
router ospf 1
default-information originate
```



### Switch sw_1

Apenas no switch 1 é necessário desativar o `igmp snooping`

```
no ip igmp snooping 
```



### Salvar a configuração

Salvar a configuração em todos os roteadores e no switch sw_1

```
en
conf t
write
```



#### Configuração dos dispositivos finais

Configurar todos os dispositivos finais (VMs, Linux_docker e VPCs), com:

* Endereço IPv4
* Máscara
* Gateway
* DNS (8.8.8.8 ou de sua preferência)

De acordo com tabela anterior.



## Trafego multicast com VLC



Usando o player VLC para funcionar como servidor e cliente de streaming de vídeo em multicast.

**Servidor**:

Na máquina VLC - Stream Server (192.168.73.10).

* Abrir vlc

* Mídia > Abrir Transmissão de Rede > Arquivo > Adicionar

* Não clicar em Reproduzir

* Clicar na seta do botão Reproduzir e escolher Transmissão

  


  <img width="587" height="558" alt="Captura de tela de 2026-04-11 23-10-14" src="https://github.com/user-attachments/assets/c2874d57-cb89-4f33-a4dd-c8ae3cc87919" />


* Próximo > marcar: exibir localmente > selecionar: RTP/MPEG Transport Stream > Adicionar

* Utilizar um endereço multicast Ex.: 224.1.1.1 

* Deixar porta padrão > Próximo

* Desmarcar Habilitar Transcodificação > Próximo

* No campo: Linha para saída da transmissão gerada, adicionar o parâmetro `ttl=10` 


  <img width="778" height="263" alt="Captura de tela de 2026-04-11 23-28-50" src="https://github.com/user-attachments/assets/632d3ff8-183e-400c-83ab-3f8af2d46b50" />


* Transmissão

A transmissão irá iniciar, se o vídeo for curto, pode se marcar a opção de loop.



<img width="995" height="682" alt="Captura de tela de 2026-04-11 23-21-33" src="https://github.com/user-attachments/assets/56486bf2-6263-44e2-9eda-99d9c276d96f" />



**Cliente**:

Em uma máquina de outra rede.  

* Abrir vlc
* Mídia > Abrir Transmissão de Rede > Rede > URL rtp://224.1.1.1:5004 > Reproduzir

​

  <img width="1180" height="769" alt="Captura de tela de 2026-04-11 23-29-55" src="https://github.com/user-attachments/assets/b58a98a6-5e4e-4662-ad02-15f51a5d00be" />



**Testes:**

* Pausar a transmissão no servidor e ver o vídeo parar no cliente;

* Retomar a transmissão no servidor e verificar o cliente;

* Com o Wireshark:

  * Verificar em diferentes pontos da rede e ver os quadros IGM e UDP trafegando;

  * Verificar que nos enlaces das máquinas que não solicitaram o vídeo, o multicast não transmite os quadros;

  * Parar de consumir no cliente, ver os quadros de **IGMP Leave** e notar que a transmissão UDP deve parar.

    

## Roteamento dinâmico e recuperação de falhas

Com o protocolo de roteamento dinâmico OSPF ativo, no caso de haver enlaces redundantes, é possível continuar a trafegar na rede mesmo que haja uma falha em um enlace.



**Testes:**

* Em uma máquina da rede, utilize a aplicação `traceroute`  para disparar contra uma máquina de outra rede do outro lado do anel de roteamento para descobrir por qual caminho os quadros passarão.

* Dispare um `ping` contra a mesma máquina de destino usada anteriormente.
* Desative ou desconecte o enlace do anel de roteamento por onde os quadros estão passando e veja o `ping` parar (mantenha o `ping`).
* Aguarde a rede convergir e veja que a transmissão irá continuar  (mantenha o `ping`).
* Ative novamente o enlace e veja se o parâmetro `time` do `ping` irá mudar.



## Navegação externa

Com o roteador R3 funcionando como **default Gatway** da rede, todo trafego que não for para as redes do cenário será encaminhado para o R3 e ele encaminhará para a rede externa (Internet).

**Testes**

* Verifique a tabela de rotas de um dos roteadores como R0 ou R6 e tente identificar a rota padrão.

  ```
  en
  show ip route
  ```

  

* Na tabela dos roteadores R2 e R5 verifique se existe mais de uma rota para o mesmo destino.

* Teste a navegação via navegador nos PCs.

* No R3, verifique as traduções ativas: `show ip nat translations`.

* Dispare `ping` e `traceroute` para sites na Internet.



## Conclusões

Ao final da execução deste laboratório, espera-se consolidar os seguintes aprendizados e resultados:

- **Eficiência do multicast em cenários multi-hop:**   A transmissão de vídeo via VLC demonstrou que o tráfego multicast é entregue apenas às redes com receptores ativos, evitando desperdício de largura de banda e validando o funcionamento do **PIM Sparse-Mode** e do **IGMP**.
- **Resiliência da rede com OSPF:**   O protocolo de roteamento dinâmico garantiu convergência rápida em situações de falha de enlace. Os testes com `ping` e `traceroute` mostraram que o tráfego foi redirecionado automaticamente por caminhos alternativos, comprovando a alta disponibilidade da topologia.
- **Tradução de endereços com NAT/PAT:**   A configuração de NAT no R3 permitiu que múltiplos dispositivos privados acessassem a internet simultaneamente. A verificação das traduções ativas (`show ip nat translations`) confirmou o funcionamento correto da sobrecarga de endereços.
- **Validação prática de serviços de rede:**   A integração entre roteamento dinâmico, multicast e NAT mostrou como diferentes tecnologias podem coexistir em uma infraestrutura complexa, simulando cenários reais de redes corporativas e acadêmicas.
- **Ferramentas de análise e monitoramento:**   O uso do **Wireshark** e de comandos como `show ip route` e `traceroute` reforçou a importância de validar o comportamento da rede em diferentes pontos, garantindo que a teoria se confirme na prática.
