# Experimento PnetLab - rede inicial e conexão com a Internet



## OBJETIVO

O objetivo desta atividade é permitir que os estudantes criem uma rede simples no **PNETLab** e, em seguida, conectem-na à Internet, reforçando conceitos de endereçamento IP, DHCP e testes de conectividade.

Com este experimento, o aluno irá:

- **Adicionar e configurar dispositivos básicos** (switch e VPCs).

- **Configurar endereçamento IPv4 manualmente** em uma rede local.

- **Testar conectividade interna** entre máquinas virtuais.

- **Experimentar a configuração automática via DHCP** para acesso externo.

- **Validar a conexão com a Internet real**, diferenciando tráfego interno e externo.

  

## Experimento

Nesta atividade, o estudante deverá:

### Parte 1 - Criando rede inicial
<img width="495" height="277" alt="Captura de tela de 2026-04-09 08-27-06" src="https://github.com/user-attachments/assets/949e1eda-33fe-4f1e-bd35-f3c47e8fbe52" />

- Adicionar um **switch**: *`node > Cisco IOL > Image: L2-ADVENTER...`*

- Adicionar duas máquinas do tipo **Virtual PC (VPC)**: *`node > Virtual PC (VPC)`*

- Configurar **endereçamento IPv4 manualmente** dentro da rede 192.168.1.0/24. 

  Exemplo na CLI do VPC 1:

  ```
  ip 192.168.1.10 255.255.255.0
  ```

  Fazer o mesmo no outro VPC usando outro endereço IPv4.

  

- Verificar as configurações de rede. 

  Exemplo na CLI do VPC 1:

  ```
  ip show
  ```

  

- Testar a **conexão interna** entre as máquinas via CLI. 

  Exemplo na CLI do VPC 2:

  ```
  ping 192.168.1.10
  ```

  Ping do VPC 2 para o VPC 1.

  

---



### Parte 2 - Conectando a rede à Internet
<img width="483" height="430" alt="Captura de tela de 2026-04-09 08-31-46" src="https://github.com/user-attachments/assets/e4733b90-b9d3-475c-81b8-e741ddd0b059" />

- Adicionar uma **Network** do tipo *Cloud_nat*: *`node > Network > Type: Cloud_nat`*   

- Conectar os dispositivos.

- Configurar os VPCs para obter configurações de rede via **DHCP**. 

  Exemplo na CLI do VPC 1:

  ```
  ip dhcp
  ```

  

- Verificar as configurações de rede. 

  Exemplo na CLI do VPC 1:

  ```
  ip show
  ```

  

- Testar a **conexão interna ** via CLI. 

  Exemplo na CLI do VPC 2:

  ```
  ping x.x.x.x
  ```

  (utilizar o endereço obtido pelas máquinas no passo anterior) Ping do VPC 1 para o VPC 2.

  

- Testar **conexão externa** via CLI (para uma máquina/site na Internet):

  Exemplo na CLI de um VPC :

  ```
  ping www.google.com
  ```



## Validação

Mostrar ao professor o cenário configurado funcionando, com conectividade interna e acesso à Internet.



## Importância

- Esta atividade é **fundamental para compreender a integração de redes locais com a Internet**.
- Permite que os estudantes pratiquem tanto a configuração manual quanto a automática (DHCP).
- Demonstra como o PNETLab pode simular ambientes próximos ao real, incluindo acesso externo.
- Serve como base para práticas mais avançadas, como configuração de serviços de rede, protocolos dinâmicos e análise de tráfego.
