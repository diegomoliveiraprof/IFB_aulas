# SAMBA - Compartilhamento de arquivos	
Sonre o SAMBA   
Segundo o site samba.org, o Samba é uma suíte de aplicativos que permite que sistemas operacionais não Windows, como Linux, Unix e macOS (baseado em Unix), compartilhem arquivos e impressoras via rede com máquinas Windows. 

O projeto foi iniciado em 1992 por Andrew Tridgell, a partir da necessidade de conectar uma máquina DOS a um servidor Unix. 

O nome “Samba” deriva de SMB (Server Message Block), protocolo usado para compartilhamento de arquivos e dispositivos em rede. O Samba foi desenvolvido inicialmente por meio de engenharia reversa sobre o protocolo SMB e, ao longo dos anos, evoluiu para oferecer também serviços de autenticação e integração com Active Directory.


## 1. Objetivo

Configurar um servidor **SAMBA** para disponibilizar pastas compartilhadas acessíveis por usuários específicos, simulando um ambiente de rede entre sistemas Linux e Windows.

## 2. Conceitos envolvidos

* **SAMBA**: software que permite compartilhamento de arquivos e impressoras entre Linux e Windows.

* **Workgroup**: grupo de computadores que compartilham recursos na mesma rede.

* **smb.conf**: arquivo de configuração principal do SAMBA.

* **Permissões de acesso**: controle de leitura e escrita nas pastas compartilhadas.

* **Autenticação de usuários**: define quem pode acessar cada pasta.

## 3. Compartilhar pasta na rede

Para compartilha pastas na rede é necessário criar a estrutura de pastas e os usuários que vão viabilizar o acesso.

### 3.1 Usuários

Se os usuários `aluno1` e `aluno2` não existirem, primeiro eles devem ser criados. 

Os novos usuários são apenas para acesso ao compartilhamento, por tanto não há necessidade que eles tenham uma pasta `home` (pasta pessoal) no servidor e por questão segurança, eles também não precisam de acesso ao servidor via linha de comandos, ou seja, não precisam de **shell**.

Criar usuário `aluno1` sem `home` e em seguida criar uma senha para ele.

Comando:

```bash
useradd aluno1
passwd aluno1
```

Retira o `shell` do usuário `aluno1`

```shell
usermod -s /bin/false aluno1
```

_**Fazer o mesmo para o usuário aluno2**_

### 3.2 Estrutura de pastas

Criando as pastas a serem compartilhadas.

A estrutura pode ser como o administrador achar melhor.

Neste experimento, por questão de organização vamos criar uma pasta para centralizar os compartilhamentos e dentro dela vamos criar uma pasta para cada usuário.



```bash
compartilhamentos/
├── aluno1
└── aluno2
```

<img width="479" height="365" alt="Captura de tela de 2026-10-13 13-58-38" src="https://github.com/user-attachments/assets/04639d1c-cc76-47f7-8ec9-c0afb497fec9" />


Criando as pastas

Comando:

```bash
mkdir /compartilhamentos
cd /compartilhamentos
mkdir aluno1
mkdir aluno2
```

Verificando

```bash
ls -l /compartilhamentos
```



As pastas **aluno1** e **aluno2** devem ser acessadas somente por seus usuários, por tanto é necessário mudar o proprietário e o grupo de cada pasta.

Comando:

```bash
chown aluno1:aluno1 /compartilhamentos/aluno1
```

_**Fazer o mesmo para a pasta aluno2**_



### 3.3 Instalar e configurar o SAMBA

Instalar o SAMBA.

Comando:

```bash
apt update
apt install samba
```

O arquivo de configuração do samba é o `/etc/samba/smb.conf` 



Apagando o arquivo original e criando um novo apenas com as configurações necessárias.

Comando:

```bash
rm /etc/samba/smb.conf
nano /etc/samba/smb.conf
```

No novo arquivo aberto, digitar as seguintes linhas:

```bash
[global]
    workgroup = workgroup
    server string = srvsamba
    netbios name = srvsamba
    log file = /var/log/samba/log.%m
    
    
[aluno1]
    comment = pasta do usuario aluno1
    path = /compartilhamentos/aluno1
    read only = no
    valid users = aluno1
    browseable = yes

[aluno2]
    comment = pasta do usuario aluno2
    path = /compartilhamentos/aluno2
    read only = no
    valid users = aluno2
    browseable = yes
```

Savar o arquivo e sair.



**Breve descrição das linhas do novo arquivo `smb.conf`**

* **[global]** – é a seção de configurações gerais do servidor.
* **workgroup** – define o grupo de trabalho Windows. Normalmente o padrão é `WORKGROUP`.
* **server string** – descrição do servidor, aparece nos clientes.
* **netbios name** – nome curto do servidor na rede.
* **log file** – caminho do arquivo de log. Pode ser algo como `/var/log/samba/log.%m`.
* **[aluno1]** – define um compartilhamento específico.
* **comment** – comentário descritivo do compartilhamento.
* **path** – caminho da pasta compartilhada.
* **valid users** – lista de usuários autorizados.
* **browseable** – define se o compartilhamento aparece na lista de recursos disponíveis.





Adicionar os usuários no SAMBA

Comando:

```bash
smbpasswd -a aluno1
smbpasswd -a aluno2
```

Repetir as senhas anteriores quando solicitado.

Reiniciar o serviço do SAMBA e verificar se está tudo correto

```bash
systemctl restart smbd.service
systemctl status smbd.service
```



### 3.4 Acessar o compartilhamento

Para acessar o compartilhamento:



**No Linux:**

Abir o explorador de arquivos e digitar o endereço IP do servidor.

```bash
smb://10.1.1.1
```

<img width="965" height="338" alt="Captura de tela de 2026-10-13 14-47-49" src="https://github.com/user-attachments/assets/42a3651e-7635-4380-aca0-cd9a7ed0dc10" />




___

**No Windows:**

Abir o explorador de arquivos e digitar o endereço IP do servidor.

```cmd
\\10.1.1.1
```

<img width="965" height="338" alt="Captura de tela de 2026-10-13 14-59-27" src="https://github.com/user-attachments/assets/213e1ddf-05d7-439a-a244-9e5ff593ffba" />


Após realizar a conexão em um compartilhamento que requer senha, o Windows mantêm a sessão até que se faça *logoff* do usuário, para acessar um  compartilhamento no mesmo servidor mas com outro usuário e senha é necessário encerrar a sessão ativa.

Para encerrar a sessão no Windows.

Abra o CMD, para verificar as sessões ativas digite:

```cmd
net use
```

Para encerrar uma sessão digite:

```cmd
net use /delete \\endereço_do_servidor
```

Exemplo:

```cmd
net use /delete \\10.1.1.1
```

