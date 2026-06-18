# Exercícios 1 - python Básico 

1. Crie uma função que recebe uma lista de nomes e imprime cada nome em maiúsculas.

   ```python
   def imprime(nomes):
     for item in nomes:
       # Imprime o nome em maiúsculas
       print(item.upper())
       # Imprime o nome com a primeira letra de cada palavra em maiúscula
       print(item.title())
       print('\n')
   
   # Inicializa uma lista de nomes para teste
   nomes=["fulano1 da costa","fulano2 de almeida","fulano3 da silva"]
   
   # Chama a função 'imprime' com a lista 'nomes'
   imprime(nomes)
   ```

   

2. Crie uma função que recebe um dicionário chamado **turma** que recebe o nome do estudante como chave e a nota como valor ex. `turma={"Fulano": 9}` , o dicionário deve conter 5 itens no mínimo. A função deve calcular e retornar a média das notas da turma.

   2.1. Solução com `for`

      ```python
   def calc_media(turma):
     # Inicializa a soma dos valores
     soma=0
     # Itera sobre os valores (notas) no dicionário 'turma'
     for valor in turma.values():
       # Adiciona cada valor a 'soma'
       soma+=valor
   
     # Calcula a média dividindo a soma pelo número de itens
     m = soma/len(turma)
     return m
   
   # Define um dicionário 'turma' com nomes de alunos e notas
   turma={"Fulano1": 9,"Fulano2": 9,"Fulano3": 9,"Fulano4": 9,"Fulano5": 9}
   
   # Chama a função 'calc_media' e armazena o resultado
   media = calc_media(turma)
   # Imprime a média calculada
   print(media)
      ```

      

   2.2. Solução sem `for`

      ```python
   def calc_media(turma):
     # Calcula a média usando as funções internas sum() e len()
     return sum(turma.values())/len(turma)
   
   # Define um dicionário 'turma' com nomes de alunos e notas
   turma={"Fulano1": 9,"Fulano2": 9,"Fulano3": 9,"Fulano4": 9,"Fulano5": 9}
   
   # Chama a função 'calc_media' e armazena o resultado
   media = calc_media(turma)
   # Imprime a média calculada
   print(media)
      ```

   

   2.3. Solução com dicionário de tamanho variável

      ```python
   # Obtém o tamanho desejado do dicionário do usuário
   tamanho = int(input("Tamanho do dicionario: "))
   
   # Inicializa um dicionário vazio
   turma={}
   # Loop para obter nomes e notas dos alunos do usuário e preencher o dicionário
   for i in range(tamanho):
     chave = input("Nome estudante: ")
     valor = float(input("Nota: "))
     turma[chave]= valor
   
   # Imprime o dicionário preenchido
   print(turma)
   
   def calc_media(turma):
     # Calcula a média usando as funções internas sum() e len()
     return sum(turma.values())/len(turma)
   
   # Chama a função 'calc_media' e armazena o resultado
   media = calc_media(turma)
   # Imprime a média calculada
   print(media)
      ```

      

3. Crie um programa com um menu que permita:

   1 - Adicionar um item a uma lista.   
   2 - Remover um item da lista.   
   3 - Mostrar todos os itens.   
   4 - Sair.   

   ```python
   # Inicializa uma lista vazia
   lista=[]
   
   # Função para adicionar um item à lista
   def add_items(lista):
     item = input("Item: ")
     lista.append(item)
   
   # Função para remover um item da lista
   def remove_items(lista):
     # Verifica se a lista está vazia
     if len(lista)==0:
       print("Não possui itens")
     else:
       item = input("Item a remover: ")
       # Verifica se o item existe na lista
       if item in lista:
         lista.remove(item)
         print("Item removido!")
       else:
         print("Item não encontrado!")
   
   # Função para listar todos os itens na lista
   def listar_items(lista):
     # Verifica se a lista está vazia
     if len(lista)==0:
       print("Não possui itens")
     else:
       # Itera com índice e item para imprimi-los formatados
       for indice, item in enumerate(lista, start=1):
         print(f"{indice} - {item}")
   
   # Inicia um loop infinito para o menu
   while True:
     # Exibe as opções do menu
     print("\n==Menu==")
     print("1 - Adicionar")
     print("2 - Remover")
     print("3 - Listar")
     print("4 - Sair\n")
   
     # Obtém a escolha do usuário
     op = input("Escolha: ")
   
     # Usa uma instrução match para lidar com diferentes opções
     match op:
       case "1":
         # Chama a função add_items
         print("==Adiciona==")
         add_items(lista)
       case "2":
         # Chama a função remove_items
         print("==Remove==")
         remove_items(lista)
       case "3":
         # Chama a função listar_items
         print("==Lista==")
         listar_items(lista)
       case "4":
         # Sai do loop
         print("Saindo....")
         break
       case _:
         # Lida com entrada inválida
         print("Opção inválida!!")
   ```

   

4. Crie um programa que permita ao usuário gerenciar uma lista de produtos. Cada produto será representado por um **dicionário** com as chaves: `"nome"`, `"preço"` e `"quantidade"`. O programa deve ter um **menu** com as opções: (utilize funções sempre que possível)

   1 - Adicionar produto   
   2 - Listar produtos   
   3 - Buscar produto por nome   
   4 - Remover produto   
   5 - Sair   

   ```python
   lista=[{"nome":"caderno","preco":5.00, "quant":10},{"nome":"lapis","preco":2.00, "quant":20}]
   
   def add_produto(lista):
     
     produto={
         "nome":input("Nome: "),
         "preco": float(input("Preço: ")),
         "quant": int(input("Quantidade: "))
     }
     lista.append(produto)
   
   
   def lista_produto(lista):
     
     for indice, item in enumerate(lista, start=1):
       print(f"{indice} - Nome: {item["nome"]} - Preço: {item["preco"]} - Quantidade: {item["quant"]}")
   
   def busca_produto(lista):
     
     nome = input("Nome produto: ")
     for i in lista:
       if i["nome"] == nome:
         print("Produdo encotrado")
         print(f"Nome: {i["nome"]} - Preço: {i["preco"]} - Quantidade: {i["quant"]}")
         return i
     print("Produto não encontrado")
     return None
   
   def remove_produto(lista):
     
     i = busca_produto(lista)
     if i:
       lista.remove(i)
       print("produto removido")
   
   while True:
     print("\n==Menu==")
     print("1 - Adicionar")
     print("2 - Listar")
     print("3 - Buscar")
     print("4 - Remover")
     print("5 - Sair\n")
   
     op = input("Escolha: ")
   
     match op:
       case "1":
         print("\n==Adicionar==")
         add_produto(lista)
       case "2":
         print("\n==Listar==")
         lista_produto(lista)
       case "3":
         print("\n==Buscar==")
         busca_produto(lista)
         
       case "4":
         print("\n==Remover==")
         remove_produto(lista)
       case "5":
         print("Saindo.....")
         break
       case _:
         print("Opção inválida!")
   ```

   

5. Faça um programa para cadastro de agenda. 

   O programa deve utilizar dicionários para cadastrar os contatos, usando como chaves,**nome, endereço, e-mail e telefone**. 

   Os dicionários devem ser guardados em uma lista.

   O menu deve oferecer as seguintes opções: 

   1 - Adicionar contato - deve verificar se o contato já existe antes de adicionar.

   2 - Editar contato - deve solicitar o nome de um contato, verificar sua existência e solicitar que o usuário entre com os dados do contato novamente, menos o nome.

   3 - Buscar contato - deve solicitar o nome de um contato e mostrar os dados.

   4 - Listar contatos - deve listar os contatos em ordem alfabética.

   5 - Remover contato - deve remover um contato existente.

   6 - Sair.

   ```python
         def adicionar(lista):
           """Cria um novo contato via input e o adiciona à lista."""
           contato={
               "nome": input("Nome: "),
               "end": input("Endereço: "),
               "email": input("E-mail: "),
               "tel": input("Telefone: ")
           }
           lista.append(contato)
           print("Novo contato adicionado: ")
           # Ajustado aspas internas para ' para evitar erro de sintaxe
           print(f"Nome: {contato['nome']} - Endereço: {contato['end']} - E-mail: {contato['email']} - Telefone: {contato['tel']} ")
         
         
         def editar(lista):
           """Busca um contato e atualiza seus dados (exceto o nome)."""
           if not lista:
               print("Lista vazia!")
               return
         
           contato = buscar(lista)
         
           if not contato:
             return
           else:
             contato["end"] = input("Novo endereço: ")
             contato["email"] = input("Novo e-mail: ")
             contato["tel"] = input("Novo telefone: ")
             print("Contato editado:")
             print(f"Nome: {contato['nome']} - Endereço: {contato['end']} - E-mail: {contato['email']} - Telefone: {contato['tel']} ")
         
         def remove(lista):
           """Busca um contato pelo nome e o remove da lista."""
           if not lista:
               print("Lista vazia!")
               return
         
           contato = buscar(lista)
           if not contato:
             return
           else:
             lista.remove(contato)
             print(f"Contato: {contato['nome']} - REMOVIDO")
         
         
         def buscar(lista):
           """Procura um contato pelo nome. Retorna o dicionário se achar, ou None."""
           if not lista:
             print("Lista vazia!")
             return
         
           nome = input("Nome contato: ")
         
           for contato in lista:
             if contato["nome"] == nome:
               print("Contato Encontrado:")
               print(f"Nome: {contato['nome']} - Endereço: {contato['end']} - E-mail: {contato['email']} - Telefone: {contato['tel']} ")
               return contato # Retorna a referência direta do contato encontrado
         
           print("Contato não encontrado...")
           return None
         
         def listar(lista):
           """Exibe todos os contatos ordenados alfabeticamente pelo nome."""
           if not lista:
             print("Lista vazia!")
             return
         
           # Ordena a lista temporariamente para exibição usando uma função lambda
           lista_ordenada = sorted(lista, key=lambda contato: contato["nome"])
           for indice, item in enumerate(lista_ordenada, start=1):
             print(f"{indice}- Nome: {item['nome']} - Endereço: {item['end']} - E-mail: {item['email']} - Telefone: {item['tel']} ")
         
         
         def main():
           """Fluxo principal do programa e menu de navegação."""
           # Dados de teste
           lista=[{"nome":"Fulano3","end":"rua 1","email":"fulano1@teste.com","tel":"1111111"},
                  {"nome":"Fulano2","end":"rua 2","email":"fulano2@teste.com","tel":"2222222"},
                  {"nome":"Fulano1","end":"rua 3","email":"fulano3@teste.com","tel":"33333333"}
                  ]
         
           while True:
             print("\n==Menu==")
             print("1- Adicionar")
             print("2- Editar")
             print("3- Buscar")
             print("4- Listar")
             print("5- Remover")
             print("6- Sair")
         
             op = input("Escolha uma opção: ")
         
             # ESTRUTURA CONDICIONAL 
             match op:
               case "1":
                 print("\nAdicionar")
                 adicionar(lista)
               case "2":
                 print("\nEditar")
                 editar(lista)
               case "3":
                 print("\nBuscar")
                 buscar(lista)
               case "4":
                 print("\nListar")
                 listar(lista)
               case "5":
                 print("\nRemover")
                 remove(lista)
               case "6":
                 print("\nSair")
                 print("Saindo....")
                 break
               case _:
                 print("Opção inválida!")
         
         main()
   ```

   
