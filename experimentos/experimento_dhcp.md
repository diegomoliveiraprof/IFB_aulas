# Experimento DHCP

## Objetivo

Compreender o processo de **atribuição dinâmica de endereços IP** e a **interação entre protocolos de camada de enlace e rede**, por meio da análise real de pacotes capturados no Wireshark. Identificar as etapas do ciclo **DORA** (Discover, Offer, Request, Acknowledge) e observar como **endereços MAC** e **mensagens ARP** participam da comunicação.



## Experimental

1. **Preparação do ambiente**

   - Abra o **Wireshark** e selecione a interface de rede correta.
   - Inicie a captura de pacotes.

2. **Liberação e renovação do IP**

   - Execute os comandos para liberar e solicitar novamente um endereço IP:

     **Linux**

     bash

     ```
     sudo dhclient -r   # libera o endereço atual
     sudo dhclient -v   # solicita novo endereço ao servidor DHCP
     ```

     **Windows**

     cmd

     ```
     ipconfig /release  # libera o endereço atual
     ipconfig /renew    # solicita novo endereço ao servidor DHCP
     ```

   - Alternativamente, desative e reative a interface de rede via interface gráfica.

   > **Nota:** A liberação do IP não garante que o novo endereço será diferente — o servidor DHCP decide se o mesmo IP será reutilizado.

3. **Análise dos pacotes**

   - No Wireshark, filtre os pacotes DHCP com:

     Filtro

     ```
     DHCP || arp
     ```

     No filtro, o operador lógico `ou` pode ser representado como `or` e como `||` (pipe 2x)

     

   - Localize e analise os quadros:

     - **DHCP Discover**
     - **DHCP Offer**
     - **DHCP Request**
     - **DHCP ACK**

   - Observe também os pacotes **ARP Probe**  e **ARP Announcement** (também chamado de *Gratuitous ARP*) que ocorrem após o ACK do DHCP.

   

## Questões

1. Qual protocolo de **camada de transporte** é utilizado pelo DHCP?
2. Quais são as **portas de origem e destino** de cada quadro DHCP?
3. Descreva a **função** de cada mensagem do ciclo DORA (Discover, Offer, Request, ACK).
4. Observe se há **mensagens ARP** após o DHCP ACK. Qual é o propósito delas?
5. Identifique os **endereços MAC** envolvidos e explique sua importância na comunicação.

Utilize capturas de tela para justificar cada resposta e destaque na imagem o item que está sendo analisado.
Organize bem suas respostas em um arquivo PDF, o arquivo também deve incluir as perguntas.
