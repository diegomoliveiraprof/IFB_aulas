# Experimento - ICMP e TCP.



## Objetivo

Utilizar um _sniffer_ de rede como Wireshark para estudar o funcionamento dos protocolos TCP e ICMP.

Executar o experimento e responder às questões em um relatório, utilizar _print_ das telas sempre que possível para justificar suas respostas.



## Experimento

1. Iniciar uma captura no Wireshark, abrir o navegador e acessar algum site para coletar informações sobre a conexão TCP.

2. Acesse algum site de sua preferência.

3. Abra o CMD da sua máquina e efetue um `tracert` para algum site ou endereço IP na internet.



## Questões

1. Identifique pacotes _tree way handshake_ utilizados pelo TCP para estabelecer conexão com o site acessado anteriormente.

   a. Evidencie  as portas utilizadas na conexão.

   b. Evidencie as _flags_ ativas em cada pacote.

2. Mostrar a saída do comando `tracert` e responder aos seguintes itens:

   a. Quantos saltos até o destino?
   b. Foi possível obter informações de algum roteador no caminho?
   c. Analisando a captura, quais os protocolos foram utilizados pelo Tracert?
   d. Quais os tipos e códigos dos pacotes ICMP utilizados?

   

## Observações

Utilizar _print_ da tela para justificar as respostas das questões.

   
