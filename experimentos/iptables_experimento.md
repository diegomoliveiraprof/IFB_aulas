# Experimento Iptables 

## Objetivo

Compreender como regras de firewall com **iptables** afetam o tráfego de rede e verificar, por meio de capturas no **Wireshark**, o comportamento de protocolos essenciais (ICMP, DNS e HTTP/HTTPS). Relacionar as regras configuradas com os pacotes observados, destacando como o firewall controla a comunicação entre rede interna, gateway e internet.

## Experimento

### Preparação do ambiente

### Configuração inicial do iptables

Utilizando o cenário/laboratório do roteiro de configuração do iptables, certifique se de que as regras no iptables estão de acordo com o que foi estabelecido naquele roteiro:

* Bloquear todo o tráfego não seja explicitamente liberado.

* Liberar tráfego na interface de loopback.

* Liberar tráfego de quadros ICMP.

* Liberar tráfego para navegação *Web* HTTP e HTTPS

* Liberar tráfego de consulta DNS,.
* Bloquear ICMP vindo de redes externas

[Roteiro iptables configuração](https://github.com/diegomoliveiraprof/IFB_aulas/blob/main/experimentos/iptables_conf.md)

### Captura e análise dos pacotes

#### 1. Captura de ICMP (Ping)

- Inicie uma captura no Wireshark nas interfaces `ens4` e `ens3`.

- Realize um **ping da máquina interna para a internet**.

- Realize um  **ping  da internet para o gateway**.

- **Filtro sugerido:**

  ```
  icmp
  ```

#### 2. Análise de DNS

- Durante uma navegação web (ex.: acessar `www.ifb.edu.br`), capture os pacotes.

- Observe o tráfego DNS (porta 53 UDP).

- **Filtro sugerido:**

  ```
  DNS
  ```

#### 3. Tráfego HTTP/HTTPS

- Capture pacotes enquanto acessa um site via HTTP (porta 80) e HTTPS (porta 443).
  - sites HTTP:
    - www.httpforever.com
    - altoro.testfire.net
    - [172.18.1.40](http://172.18.1.40) 

- Compare os pacotes TCP em cada caso.

- **Filtros sugeridos:**

  ```
  tcp.port == 80
  tcp.port == 443
  ```

---



## Questões

1. **ICMP (Ping)**
   - Quais pacotes ICMP aparecem em cada interface?
   - Como eles refletem as regras configuradas no iptables?
2. **DNS**
   - Quais pacotes DNS são vistos indo para o servidor externo e quais respostas retornam?
   - O que aconteceria se a regra de DNS fosse removida?
3. **HTTP/HTTPS**
   - Como o Wireshark mostra a diferença entre conexões HTTP e HTTPS?
   - Quais portas são utilizadas e como isso se relaciona com as regras liberadas no iptables?

---

## Entrega

- Organize suas respostas em um **arquivo PDF**.
- Utilize capturas de tela para justificar cada resposta e destaque na imagem o item que está sendo analisado.
- O arquivo também deve incluir as perguntas e as respostas com os prints.


