# Experimento 1 - Wireshark Lab Intro.



## Objetivo

Iniciar a utilização de um _sniffer_ de rede , o Wireshark, evidenciar o conceito de encapsulamento.

Executar o experimento e responder às questões em um relatório, utilizar _print_ das telas sempre que possível para justificar suas respostas.



## Experimento

1. Abra um navegador.

2. Abra o Wireshark e inicie uma captura na interface de rede ativa.

3. No navegador abra o site: <a href="http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html" target="_blank" rel="noopener noreferrer">http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html</a>

4. Depois que seu navegador mostrar a mensagem de parabéns "_Congratulations! You've downloaded the first Wireshark lab file!_", pare a captura no Wireshark.

5. Digite http  no filtro de visualização e tecle ``enter`` , com isso devem aparecer apenas mensagens http na tela, como na Figura 1.

   <img width="959" height="583" alt="wireshark_labintro_01" src="https://github.com/user-attachments/assets/8816aa95-4a12-4dc5-8107-ad1e8c78ce89" />


   <small>Figura 1 - Captura com filtro de visualização http</small>

6. Encontre o HTTP GET enviado pela sua máquina ao servidor, procure na coluna _Info_. Selecione o pacote e veja que é possível ver detalhes das informações das camadas de rede.   





## Questões

1. Liste 3 diferentes protocolos que aparecem na captura antes da utilização do filtro http. Utilize um _print_ da tela para  justificar sua resposta.

   

2. Quanto tempo levou desde o envio do HTTP GET da sua máquina até o HTTP OK do servidor ser recebido? Por padrão a coluna time está em segundos, para ver em formato data-hora, selecione o menu ``View > Time display format > Date and Time of Day`` . Utilize um _print_ da tela para  justificar sua resposta.

 

3. Qual é o endereço IP do servidor e qual é o endereço IP da sua máquina? Utilize um _print_ da tela para  justificar sua resposta.

   

4. Quais os campos nas camadas apresentadas no pacote GET que indicam o tipo de informação presente no _payload_ de cada camada? Utilize um _print_ da tela para  justificar sua resposta.
