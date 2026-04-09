# DHCP



## 1. Objetivo

* O objetivo deste experimento é instalar, configurar e testar um servidor DHCP em ambiente Linux, compreendendo como o serviço automatiza a atribuição de endereços IP e demais parâmetros de rede para clientes. 

* Busca-se demonstrar na prática como o DHCP facilita a administração de redes, reduz erros de configuração manual e garante maior eficiência na distribuição de recursos.

  

## 2. Conceitos envolvidos

* **DHCP (Dynamic Host Configuration Protocol):** protocolo que permite a atribuição automática de endereços IP e parâmetros de rede (gateway, DNS, máscara de sub-rede) aos dispositivos conectados.

* **Endereço IP:** identificador único de cada dispositivo em uma rede. Pode ser atribuído manualmente (estático) ou dinamicamente (via DHCP).

* **MAC Address:** endereço físico da placa de rede, usado pelo DHCP para identificar dispositivos e, opcionalmente, criar reservas de IP.

* **Lease (concessão):** período de tempo durante o qual um cliente pode usar o IP fornecido pelo servidor DHCP.

* **Reserva de IP:** mecanismo que garante que um dispositivo específico receba sempre o mesmo IP, com base em seu MAC address.



## 3. Instalando o serviço de DHCP



Existem vários serviços de DHCP que podem ser instalados no Linux, dentre eles vamos usar um software chamado **isc-dhcp-server**, parte pela simplicidade na configuração, parte por ser bastante utilizado na comunidade Linux.



* Atualizar a lista de pacotes.

* Instalar a aplicação **isc-dhcp-server**.

  ```
  sudo apt update
  sudo apt install isc-dhcp-server
  ```

  

* Após a instalação é possível verificar o arquivo de configuração do serviço.

  ```
  nano /etc/dhcp/dhcpd.conf
  ```

  Pode se notar que é um arquivo extenso e cheio de exemplos e explicações de diferentes configurações que o serviço permite.

  É possível fazer editar o arquivo e fazer a configuração desejada, porém, como se trata de um arquivo extenso, no caso da necessidade de manutenção, correção ou adição de alguma funcionalidade, um arquivo grande e cheio de opções pode tornar a tarefa mais demorada e passível de erros.

  A alternativa é apagar o arquivo original e criar um arquivo novo com o mesmo nome e adicionar nele apenas a configuração que desejamos.

  

* Criar o novo arquivo de configuração.

  * Apagando o arquivo original.
  * Criando um novo arquivo com mesmo nome.

  ```
  sudo rm /etc/dhcp/dhcpd.conf
  sudo nano /etc/dhcp/dhcpd.conf
  ```

  

* Conteúdo do arquivo de configuração.

  ```
  ddns-update-style none;
  authoritative;
  log-facility local7;
  
  subnet 10.1.1.0 netmask 255.255.255.0 {
          range 10.1.1.150 10.1.1.200;
          option domain-name-servers 8.8.4.4,8.8.8.8;
          option domain-name "minha.net";
          option routers 10.1.1.1;
          option broadcast-address 10.1.1.255;
          default-lease-time 600;
          max-lease-time 7200;
  }
  
  ```

  Ao digitar, atenção ao `;` no final das linhas. 

  Salvar e sair do arquivo.

  ```
  ctrl+o --> salvar
  Enter
  ctrl+x --> sair do arquivo
  ```

  

* Reiniciar o serviço

  * No geral quando um arquivo de configuração de um serviço é modificado é necessário reiniciar o serviço para que as modificações tenham efeito.

  * O serviço deve ser reiniciado coma ferramenta **systemctl**.

  * A opção de `status` pode ser utilizada para verificar se tudo ocorreu bem.

    ```
    systemctl restart isc-dhcp-server
    systemctl status isc-dhcp-server
    ```

  

* Breve explicação sobre as linhas de configuração do arquivo **dhcpd.cof**.

  * `ddns-update-style none;`   Define o estilo de atualização dinâmica de DNS. O valor `none` indica que o servidor DHCP **não vai atualizar registros DNS automaticamente**.

  * `authoritative;`   Informa que este servidor DHCP é **autoridade** para a rede configurada. Isso significa que ele pode negar solicitações incorretas vindas de clientes que tentem usar outro servidor DHCP.

  * `log-facility local7;`   Define a categoria de log usada pelo syslog. Aqui, os registros do DHCP serão enviados para o **local7**, permitindo separar os logs do DHCP dos demais serviços.

  * `subnet 10.1.1.0 netmask 255.255.255.0 { ... }`   Define a rede e máscara de sub-rede que será atendida pelo servidor DHCP.

  * `range 10.1.1.150 10.1.1.200;`   Intervalo de endereços IP que o servidor pode **atribuir dinamicamente** aos clientes.

  * `option domain-name-servers 8.8.4.4,8.8.8.8;`   Especifica os servidores DNS que os clientes devem usar (neste caso, os do Google).

  * `option domain-name "minha.net";`   Define o nome de domínio que será atribuído aos clientes.

  * `option routers 10.1.1.1;`   Informa o **gateway padrão** da rede (roteador).

  * `option broadcast-address 10.1.1.255;`   Define o endereço de broadcast da rede.

  * `default-lease-time 600;`   Tempo padrão de concessão de um IP em segundos (aqui, 10 minutos).

  * `max-lease-time 7200;`   Tempo máximo de concessão de um IP em segundos (aqui, 2 horas).

    

## 4. Cofigurando clientes



* Com o servidor configurado, e o serviço reiniciado, basta configurar a máquina cliente para solicitar end. IP automaticamente.

  * Essa configuração pode variar de um Sistema Operacional para outro.

  * Podendo ainda ser feita via interface gráfica ou linha de comando.

    * Exemplos:

      Windows via CMD:

      ```
      ipconfig /release
      ipconfig /renew
      ```

      `ipconfig /release` → libera o endereço IP atual da interface.

      `ipconfig /renew` → solicita um novo endereço IP ao servidor DHCP.

      

      Linux via CLI

      ```
      sudo dhclient -r
      sudo dhclient -v
      ```

      Na maioria a das distribuições Linux pode se usar o `dhclient`  para obter configuração **DHCP**, caso ele não esteja presente é possível instalar.

      `dhclient -r` → libera o endereço IP atual da interface. 

      `dhclient -v` → solicita um novo endereço IP ao servidor DHCP.

  

  ## 5. Reserva de endereços

  O serviço DHCP vincula o end. MAC da placa de rede ao end. IP atribuído, essa característica pode ser usada para criar **Reservas** de endereços.

  

  A reserva de endereços IP no serviço DHCP consiste em vincular o endereço MAC da placa de rede de um dispositivo a um endereço IP específico. Dessa forma, sempre que o dispositivo solicitar configuração de rede ao servidor DHCP, ele receberá o mesmo IP previamente reservado, garantindo consistência e previsibilidade na rede.

  A diferença em relação ao DHCP dinâmico é que, em vez de o servidor atribuir qualquer IP disponível dentro do intervalo configurado, ele **sempre entrega o mesmo IP ao cliente reservado**. Isso é útil para servidores, impressoras e outros equipamentos que precisam de um endereço fixo, mas ainda querem aproveitar a automação do DHCP.

* Criando uma reserva de endereço IP.

  * Primeiro é necessário saber o endereço MAC da máquina que receberá o endereço.

    Verificando endereço MAC:

    Windows

    ```
    ipconfig /all
    ```

    <img width="1143" height="601" alt="Captura de tela de 2026-04-09 11-43-26" src="https://github.com/user-attachments/assets/d2d6de86-4aaa-4a28-8690-07e8fef68456" />


    Linux
    ```
    ip a
    ```
    <img width="1000" height="235" alt="Captura de tela de 2026-04-09 11-41-25" src="https://github.com/user-attachments/assets/9e5edf75-1dba-41d8-9ee2-d349eabeafd2" />




  * Adicionado reserva no arquivo de configuração

    Exemplo: adicionando reserva para uma máquina chamada MATE com endereço MAC: 08:00:27:99:2d:a3

    ```
    #IP para maquina MATE
    host MATE{
    hardware ethernet 08:00:27:99:2d:a3;
    fixed-address 10.1.1.199;
    }
    ```

    Adicionar esse codigo no final do arquivo **dhcpd.conf**.

    Salvar o arquivo e reiniciar o serviço.

    Na máquina cliente, renovar o endereço IP.

​	
