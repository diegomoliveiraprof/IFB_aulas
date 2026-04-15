




## Atividade

1. **Captura de ICMP (Ping)**

   - Inicie uma captura no Wireshark na interface interna (`ens4`) e externa (`ens3`).

   - Realize um ping da máquina interna para a internet e outro da internet para o gateway.

   - Pergunta: *Quais pacotes ICMP aparecem em cada interface e como eles refletem as regras configuradas no iptables?

2. **Análise de DNS**

   - Faça uma captura durante uma navegação web (ex.: acessar `www.ifb.edu.br`).

   - Observe os pacotes DNS (porta 53 UDP).

   - Pergunta: *Quais pacotes DNS são vistos indo para o servidor externo e quais respostas retornam? O que aconteceria se a regra de DNS fosse removida?

3. **Tráfego HTTP/HTTPS**
   - Capture pacotes enquanto acessa um site via HTTP (porta 80) e HTTPS (porta 443).
   - Compare os pacotes TCP em cada caso.
   - Pergunta: *Como o Wireshark mostra a diferença entre conexões HTTP e HTTPS? Quais portas são utilizadas e como isso se relaciona com as regras liberadas no iptables?*

Utilize capturas de tela para justificar cada resposta e destaque na imagem o item que está sendo analisado.
Organize bem suas respostas em um arquivo PDF, o arquivo também deve incluir as perguntas.
