# Experimento - protocolo IP.



## Objetivo

Utilizar um simulador de rede como Cisco Packet Tracer,  para evidenciar o funcionamento das LAN's com end. MAC e end. IP, consulta à bases de dados de end. IP para obter informações de endereços públicos.

Executar o experimento e responder às questões em um relatório, utilizar _print_ das telas sempre que possível para justificar suas respostas.



## Experimento

### Parte 1 - configuração de rede

O estudante deverá configurar uma rede no simulador:

* Utilize o arquivo fornecido no ambiente virtual da disciplina.

* Você tem o bloco de endereços IP **10.10.0.0/16**.

* Planeje o endereçamento em uma tabela antes da configuração.

  **Exemplo de tabela de endereçamento:**

  | Dispositivo | IP         | Máscara       | Gateway   |
  | ----------- | ---------- | ------------- | --------- |
  | PC1         | 10.10.1.10 | 255.255.255.0 | 10.10.1.1 |
  | PC2         | 10.10.1.11 | 255.255.255.0 | 10.10.1.1 |
  | R1 - G0/0   | 10.10.2.20 | 255.255.255.0 | -         |

  **Exemplo de configuração:**
  
  Não utiize as redes deste exemplo, utilize a rede 10.10.0.0/16

  ```
   Rede Original
   192.168.0.0/16
   
   Rede divida
   6 redes /24
   
   
   Rede original 192.168.0.0/16
   Rede 1 - 192.168.10.0/24
   
   Rede 2 - 192.168.11.0/24
   
   Rede 3 - 192.168.21.0/24
   
   Rede 4 - 192.168.30.0/24
   
   Rede 5 - 192.168.45.0/24
   
   Rede 6 - 192.168.51.0/24
   
   Configuração dos roteadores
   =============================================
   Roteador 1  -- repita a configuração com R2 e R3 adaptando os endereços

   enable
   conf t
   int g0/0
   ip add 192.168.10.1 255.255.255.0
   no shut
   int g1/0
   ip add 192.168.30.1 255.255.255.0
   no shut
   int g2/0
   ip add 192.168.45.1 255.255.255.0
   no shut

   router rip
   version 2
   network 192.168.10.0
   network 192.168.30.0
   network 192.168.45.0
  ```


### Parte 2 - análise de endereçamento IP e rotas

O estudante irá analisar informações de rede da máquina física que estiver utilizando:

* Verifique o endereço IP privado da máquina que está utilizando. Comando: Windows `ipconfig` / Linux `ifconfig`.

* Descubra qual o endereço público da máquina física que está utilizando, existem sites na internet que oferecem este serviço.

* Utilize o serviço de [_whois_ da LACNIC](http://lacnic.net/cgi-bin/lacnic/whois?lg=pt) ou [ _whois_ do NIC.br](whois.registro.br) para coletar informações sobre seu endereço IP público que descobriu.

* Utilize algum serviço de geolocalização IP para coletar informações de localização do seu endereço IP público.

* Visualize a tabela de rotas da máquina que está utilizando. Comando: Windows `route print` / Linux `route -n`.



## Questões

1. Mostre a tabela de endereços IP que usou para configurar as máquinas da rede na Parte 1 da sessão Experimento. 

2. No espaço de endereçamento IP, quais são as redes consideradas Privadas? Justifique.

3. Sobre o endereço IP que está utilizando, responda: 

  	a. Está utilizando end. IP privado? Se sim, qual o end. e máscara?

  	b. Está utilizando end. IP público? Se sim, quem é proprietário, qual o pais e bloco original do endereço?

4. Qual serviço de geolocalização utilizou? Quais as informações de geolocalização conseguiu coletar do seu endereço IP público?

5. Na tabela de rotas da máquina que está utilizando:

   a. Existe uma rota padrão / _gateway_ ? Qual?

   b. Exite uma rota específica para sua rede? Qual?



## Observações

Enviar o arquivo  ` .pkt` configurado junto com o relatório.

Utilizar _print_ da tela para justificar as respostas das questões: 3, 4 e 5.

   
