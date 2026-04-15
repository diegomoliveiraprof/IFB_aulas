
# Experimento HTTP / Wireshark

---

## OBJETIVO
​	Observar o funcionamento do protocolo da camada de aplicação HTTP.

## Experimento

▪ Inicie o wireshark e digite o seguinte endereço em seu navegador: http://httpforever.com/ . Será exibida uma página HTML simples.

Responda as seguintes questões:



**Parte 1: A interação básica em resposta “HTTP GET/”.**

Para facilitar a resposta da Parte 1, utilize a opção Analize →Follow TCP Stream

1. Qual a versão seu browser está rodando do HTTP, 1.0 ou 1.1? E qual versão roda o servidor?

2. Que línguas (se houver alguma), seu browser indica ao servidor, que pode aceitar?

3. Qual o endereço IP de seu PC? E do servidor?

4. Ao fazer a requisição, qual é o status code retornado pelo servidor?

5. Quando foi a última vez que o arquivo HTML requisitado foi modificado no servidor?

6. Quantos bytes de conteúdo foram retornados pelo servidor, ao fazer-se a requisição?

  



**Parte 2: A interação básica em resposta “HTTP CONDITIONAL GET/”.**

Com o cache do browser vazio (limpe o cache), requisite a página http://httpforever.com/, e rapidamente, requisite a página novamente.

1. Inspecione o conteúdo da primeira resposta do servidor. Qual o status code retornado pelo
    servidor em resposta a requisição? O servidor retorna explicitamente o conteúdo do arquivo
    HTML? Como é possível verificar?

Qual o status code retornado pelo servidor em resposta à segunda requisição? O servidor
explicitamente retorna o conteúdo do arquivo pela segunda vez? Explique



**Parte 3: Recuperando arquivos longos**

Acesse a página web com conteúdo extenso (maior que o MTU de 1500 bytes):
http://altoro.testfire.net/index.jsp?content=inside_contact.htm.

1. Quantas requisições GET foram enviadas pelo browser?
2. Quantos segmentos TCP contendo dados HTTP foram enviados em resposta ao GET?





**Parte 4: Autenticação HTTP**
Acesse: http://altoro.testfire.net/login.jsp

```
Login: admin		

Senha: admin
```

1. Qual a resposta (status code e frase) do servidor, em resposta ao primeiro GET enviado pelo
   browser?
2. Quando o browser envia a segunda requisição GET ao servidor, que campo agora está incluído
   na mensagem desta requisição?
