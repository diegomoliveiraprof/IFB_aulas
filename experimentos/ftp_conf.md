# FTP Configuração



## 1. Objetivo

- Entender o funcionamento básico do FTP e suas variações (ativo e passivo).

- Identificar riscos de segurança e alternativas mais seguras (FTPS, SFTP).

- Configurar usuários e diretórios de trabalho de forma segura.

- Restringir portas passivas e ajustar firewall.

- Realizar operações práticas de upload e download com clientes FTP.

  

## 2. Conceitos envolvidos

- **FTP (File Transfer Protocol):** protocolo de rede usado para transferência de arquivos entre cliente e servidor.

- **Modelo Cliente-Servidor:** o cliente envia comandos e o servidor responde, estabelecendo canais de controle e dados.

- **Porta 21 (controle):** utilizada para comandos e respostas.

- **Portas de dados:** variam conforme o modo (ativo → porta 20; passivo → intervalo configurável).

- **Modo Ativo vs. Passivo:** diferença na forma como a conexão de dados é estabelecida.

- **Usuário FTP:** conta dedicada para acesso, sem privilégios administrativos.

- **DefaultRoot:** diretiva que define o diretório de trabalho padrão no servidor FTP.

- **PassivePorts:** configuração que restringe o intervalo de portas usadas no modo passivo.

- **Firewall/NAT:** necessidade de liberar portas específicas para permitir conexões.

- **FTPS e SFTP:** alternativas seguras que adicionam criptografia à transferência de arquivos.

  

## 3. Instalando o serviço de FTP

Existem vários *softwares* que funcionam como servidores FTP, neste experimento será utilizado o servidor chamado ProFTPd, para Linux.

A instalação é relativamente simples.

* Instalação:

  ```
  apt-get update
  apt-get install proftpd-basic
  ```

  

**Após a instalação, o serviço FTP já estará ativo.**   No entanto, é recomendável realizar algumas configurações adicionais para garantir maior segurança e controle de acesso.

Por motivos de segurança, **o usuário utilizado para o FTP não deve pertencer ao grupo** `sudoers`, evitando que ele tenha privilégios administrativos no sistema.

**Criação de usuário dedicado para o FTP:**   Criar um usuário específico para o acesso ao serviço, restrito apenas às operações de transferência de arquivos, ajuda a manter o ambiente isolado e reduz riscos de comprometimento do sistema.

**Criar o usuário**

```
sudo adduser ftpuser
```

- O sistema pedirá senha e alguns dados adicionais (podem ser ignorados com Enter).
- Esse usuário será usado apenas para acessar o FTP.



**Aplicar restrições**

- Não adicione o usuário ao grupo `sudo`.
- Isso garante que ele não terá permissões administrativas.



* **Remover acesso do usuário à linha de comando.** 

  * O novo usuário criado, por padrão terá acesso à máquina servidora não só via FTP mas também por SSH, e poderá executar comandos no seu servidor, uma das maneiras de tratar isso é retirando dele o acesso ao shell.

  * **Teste**: Tentar acessar o servidor via CLI com o usuário.

    * Remover o **shell** do usuário:

    ```
    usermod -s /bin/false ftpuser
    ```

    



* **Configurar o servidor para aceitar usuários sem shell.**
  * Editar o arquivo `/etc/proftpd/proftpd.conf`, encontrar a linha:
    *  `# RequireValidShell		off`
  * Remover o símbolo de comentário `#`
    *  `RequireValidShell		off`



* **Restringir a navegação do usuário nas pastas do servidor**

  * **Teste**: Tentar mudar/navegar para uma pasta fora da **home** do usuário.

  * Impedir que o usuário tenha acesso a arquivos de outros usuários ou do sistema.

  * Editar o arquivo `/etc/proftpd/proftpd.conf`, encontrar a linha:

    *  `# DefaultRoot		~`

  * Remover o símbolo de comentário `#`

    *  `DefaultRoot		~`

    



* **Restringir as portas do modo passivo**
  * Editar o arquivo `/etc/proftpd/proftpd.conf`, encontrar a linha:
    *  `# PassivePorts	49152 65534`
  * Remover o símbolo de comentário `#` e acertar as portas desejadas
    *  `PassivePorts 	50000 50100`

Após as modificações no arquivo de configuração, é necessário reiniciar o serviço.

```
systemctl restart proftpd
systemctl status proftpd
```



Desativar o **iptables**

Caso tenha regras restitivas de bloqueio na tabela filter.

```
iptables -L			#ver as regras atuais da tabela filter
iptables -F			#limpar as regras da tabela filter
iptables -L			#verificar novamente as regras
```

**Teste**: Tentar acessar o servidor via CLI novamente.

**Teste**: Tentar mudar/navegar para uma pasta fora da **home** do usuário novamente.





## 4. Testar o acesso



### **Acesso via interface gráfica:** 

Utilize os programas

* WinSCP (Windows)
* FileZilla (Linux e Windows)
* Explorador de arquivos (Linux e Windows)



### **Acesso via CLI:**

* **Iniciando a Conexão**

  No terminal, digite o comando seguido do IP ou domínio do servidor:

  ```
  ftp 192.168.1.50
  ```

  O servidor responderá pedindo o **usuário** e depois a **senha**.

  

* **Comandos de Navegação e Visualização**

  * Uma vez logado, os comandos lembram muito o terminal Linux:
    - **`ls`**: Lista os arquivos e pastas no servidor.
    - **`cd <diretorio>`**: Entra em uma pasta específica.
    - **`pwd`**: Mostra em qual diretório você está dentro do servidor.
    - **`lcd <caminho>`**: (**Local CD**) Altera a pasta de trabalho no **seu computador** (onde os arquivos baixados serão salvos).




* **Transferência de Arquivos**

  * Estes são os comandos principais para a aula prática:

    - **`get <arquivo>`**: Baixa um arquivo do servidor para o seu PC.

    - **`put <arquivo>`**: Envia um arquivo do seu PC para o servidor.

    - **`mget \*.jpg`**: (**Multiple Get**) Baixa vários arquivos de uma vez usando máscaras.

    - **`mput \*.pdf`**: (**Multiple Put**) Envia vários arquivos de uma vez.




* **Configuração da Sessão**

  * Antes de transferir, é importante definir o "tipo" de arquivo:

    - **`binary`**: (Ou apenas `bin`) Essencial para fotos, vídeos, executáveis ou PDFs. Garante que o arquivo não seja corrompido.

    - **`ascii`**: Para arquivos de texto simples (.txt, .html).

    - **`passive`**: Ativa ou desativa o **Modo Passivo** (muito útil se o `ls` travar).

      

* **Finalizando**

  - **`bye`** ou **`quit`** ou **`exit`**: Encerra a sessão e fecha o terminal FTP.



## 5. Acesso anônimo

**Também é possível configurar o servidor para aceitar acessos anônimos**, ou seja, sem exigir usuário e senha. Essa opção pode ser útil quando se deseja disponibilizar arquivos para múltiplos usuários de forma simples.

**Por questões de segurança, recomenda-se que os usuários anônimos tenham apenas permissão de leitura**, ou seja, possam apenas baixar arquivos, sem a possibilidade de enviar ou modificar conteúdos no servidor. Não se sabe o tipo de conteúdo que os usuários podem hospedar no servidor.

**Permitir acesso anônimo**

* Editar o arquivo `/etc/proftpd/proftpd.conf`, encontrar o bloco:

  ```
  #<Anonymous ~ftp>
  #  User              ftp
  #  Group             nogroup
  #  # We want clients to be able to login "aninymous" as well as "ftp"
  #  UserAlias         anonymous ftp
  # ...
  #</Anonymous>
  ```

  

* Remover os comentários da primeira coluna, do início ao fim do bloco (apenas da primeira coluna/início da linha)

  ```
  <Anonymous ~ftp>
    User              ftp
    Group             nogroup
    # We want clients to be able to login "aninymous" as well as "ftp"
    UserAlias         anonymous ftp
   ...
  </Anonymous>
  ```

* Os arquivos deste usuário ficam em:

  ```
  /srv/ftp
  ```

* Reiniciar os serviço após as aliterações.

  

## 6. Desafio

Acesso via firewall:

1. Ative novamente as regras de firewall.

   ```
   iptables -L													#ver as regras atuais da tabela filter
   iptables-restore < /etc/iptables/rules.v4					#restaurar regras anteriores
   iptables -L													#verificar novamente as regras
   ```

2. Crie regras para permitir o acesso ao FTP.

   Pesquise quais regras devem ser aplicadas.

   Explique as regras.

3. Teste o acesso.

4. Salve as novas regras.
