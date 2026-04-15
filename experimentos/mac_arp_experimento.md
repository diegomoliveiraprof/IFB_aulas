_______________________

# Experimento MAC e ARP



## OBJETIVO
​
Utilizar um sniffer de rede como o Wireshark, para evidenciar o funcionamento das LAN's com
end. MAC e protocolo ARP.
Executar o experimento e responder às questões em um relatório, utilizar print das telas sempre
que possível para justificar suas respostas.

## Experimento

## 1. Inicie a captura no Wireshark
- Abra o **Wireshark**.  
- Selecione a **interface de rede ativa** (aquela conectada à internet ou rede local).  
- Clique em **Start Capture** para começar a coleta de pacotes.

## 2. Visualize e manipule a tabela ARP
- Abra o **Prompt de Comando (CMD)** no Windows ou o **Terminal (CLI)** no Linux.  
- Execute o comando para visualizar a tabela ARP:  
  - **Windows:** `arp -a`  
  - **Linux:** `arp -n`  
- Observe os endereços IP e MAC já presentes na tabela.  
- Escolha **dois endereços IP da rede local** que **não estejam listados** na tabela ARP.  
- Efetue um **ping** para cada um desses endereços.

## 3. Finalize a captura
- Retorne ao **Wireshark**.  
- Clique em **Stop Capture** para encerrar a coleta de


## Questões

1. **Identificação de endereços MAC**
   - Localize **3 endereços MAC diferentes** na captura realizada no Wireshark.  
   - Utilize uma ferramenta de consulta de fabricantes (ex.: [macvendors](https://macvendors.com/), [IEEE OUI Lookup](https://standards-oui.ieee.org/), [OUI Wireshark](https://www.wireshark.org/tools/oui-lookup.html)) para descobrir a qual fabricante cada endereço pertence.  
   - Inclua **prints da tela** para justificar sua resposta.

2. **Comunicação Unicast**
   - Identifique na captura um **quadro (frame)** que evidencie uma comunicação **unicast**.  
   - Explique o que é comunicação unicast.
   - Inclua **prints da tela** para justificar sua resposta.

3. **Comunicação Broadcast**
   - Identifique na captura um **quadro (frame)** que evidencie uma comunicação **broadcast**.  
   - Explique o que é comunicação broadcast.  
   - Inclua **prints da tela** para justificar sua resposta.

4. **Funcionamento básico do protocolo ARP**
   - Explique brevemente como o protocolo ARP funciona.
     
5. **Função da tabela ARP**
   - Explique qual é a função da tabela ARP.  
   - Mostre uma **imagem da tabela ARP** da sua máquina (Windows: `arp -a` / Linux: `arp -n`).

6. **Pacotes ARP na captura**
   - Identifique pacotes ARP na captura.  
   - Explique a principal diferença entre **ARP Request** e **ARP Reply**.  
   - Mostre como identificar cada um no Wireshark.

7. **Camada de enlace**
   - Selecione a **camada de enlace** de um pacote da captura.  
   - Identifique qual protocolo está encapsulado nela.  
   - Inclua **prints da tela** para justificar sua resposta.
