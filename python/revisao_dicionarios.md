# Revisão de dicionários

## 1. Declarar um dicionário

### Vazio

```python
estoque = {}
```

### Com valores

```python
estoque = {"caneta azul": 10, "caderno": 10, "lapis": 40}
```



## Imprimir dicionário

```python
print("==Criado o Dicionario==")
print(f"{estoque}")
```

---



## 2. Adicionar / Modificar itens

### Adicionar novo par de chave e valor

```python
print("\n==Adicionar==")
chave = "cola"
quantidade = 23

estoque[chave] = quantidade
print(estoque)
```

### Modificar valor de chave existente

```python
print("\n==Modificar==")
chave = "cola"
quantidade = 1
estoque[chave] = quantidade
print(estoque)
```

---



## 3. Remover itens

```python
print("\n==Remover==")
item_remover = "caneta azul"
if item_remover in estoque:
    estoque.pop(item_remover)
else:
    print("Item não encontrado")
print(estoque)
```

---



## 4. Listar itens – iterar sobre um dicionário

### `dic.keys()` – retorna lista com chaves

```python
print("\n==Chaves==")
for chave in estoque.keys():
    print(f"{chave}")
```



### `dic.values()` – retorna lista com valores

```python
print("\n==Valores==")
for valor in estoque.values():
    print(f"{valor}")
```



### `dic.items()` – retorna tupla (chave, valor)

```python
print("\n==Itens em tupla==")
for item in estoque.items():
    print(f"{item}")
```



### Desempacotar tupla

```python
print("\n==Itens==")
for chave, valor in estoque.items():
    print(f"{chave}: {valor}")
```



### Usando `enumerate` para obter índice

```python
print("\n==Itens com índice==")
for indice, item in enumerate(estoque.items(), start=1):
    chave, valor = item
    print(f"{indice} - {chave}: {valor}")
```

---


   

# Exercício de revisão

1. Atividades básicas com dicionários - com base na revisão sobre dicionários crie um programa em Python que:   
    a. Crie um menu interativo com as seguintes opções:
         
   		1 Adicionar Item   
   		2 Remover Item   
   		3 Listar Estoque   
   		4 Sair   

      O menu deve ser repetir até que o usuário escolha a opção "Sair", e deve mostrar mensagem caso o usuário escolha uma opção inválida.   

	b. Comece com um dicionário chamado `estoque`.   

      ​	Ex.: `estoque={"caneta azul":10,"caderno":10, "lapis":40}`   

	c. Imprima o estoque atualizado na tela.   
	d. Permita ao usuário **adicionar** um item com sua quantidade.   
	e. Permita ao usuário **remover** um item do estoque.   
	f. Mostre todos os item e quantidades.   

---



2. Baseado no enunciado, complete o código fornecido:

   1. Lista de exercícios de Python Básico, Exercício 14 :

      

      Uma livraria quer controlar seu estoque usando um dicionário onde as chaves são os títulos dos livros e os valores são a quantidade disponível em estoque. Implemente um programa com as seguintes funcionalidades:
      
      1. Adicionar um livro ao estoque: o usuário informa o título e a quantidade (se o livro já existir, some a quantidade nova à existente).
      2. Remover unidades de um livro: o usuário informa o título e a quantidade a remover; o programa deve atualizar o estoque e avisar se o estoque ficar zerado ou se o livro não existir.
      3. Consultar quantidade de um livro: o usuário digita o título e o programa mostra a quantidade disponível ou informa que o livro não está no estoque.
      4. Mostrar todos os livros com suas quantidades, ordenados alfabeticamente.
      5. Sair - O programa deve repetir o menu até que o usuário escolha sair. Utilizar função.
   
   
   
   Código inicial:
   
   ```python
   def removeLivro(dicLivros):
       print("==Remove Livro==")
   
       titulo = input("Titulo: ").lower().strip()
       if titulo not in dicLivros:
           print("Titulo não cadastrado!")
   
       else:
           if dicLivros[titulo] == 0:
               print("Estoque zerado para este titulo!")
           else:
               quantidade = int(input("Quantidade: "))
               if quantidade > dicLivros[titulo]:
                   print(f"Quantidade atual insuficiente: {dicLivros[titulo]}")
               else:
                   dicLivros[titulo] -= quantidade
                   print(f"Quantidade atualizada: {dicLivros[titulo]}")
   
   def addLivro(dicLivros):
       print("==Adiciona Livro==")
   
       titulo = input("Titulo: ").lower().strip()
       quantidade = int( input("Quantidade: "))
       if titulo in dicLivros:
           dicLivros[titulo] += quantidade
       else:
           dicLivros[titulo] = quantidade
       print(dicLivros)
   
   def menu(dicLivros):
       print("\n==Livraria==")
       
       while True:
           print("1. Adicionar um livro\n2. Remover unidades\n3. Consultar quantidade\n4. Mostar todos\n5. sair")
           op = input("Escolha: ")
           if op == '5':
               print("Saindo..")
               break
           elif op == '4':
               pass
           elif op == '3':
               pass
           elif op == '2':
               removeLivro(dicLivros)
           elif op =='1':
               addLivro(dicLivros)
           else:
               print("Opção inválida")
   
   
   def main():
       dicLivros={    
           "assassinato no expresso oriente": 12,
      		"morte no nilo": 8,
       	"o caso dos dez negrinhos": 15,
       	"um corpo na biblioteca": 6,
       	"a casa torta": 10,
       	"o assassinato de roger ackroyd": 9,
       	"os crimes abc": 7,
       	"convite para um homicidio": 5,
       	"a noite das bruxas": 4,
       	"cai o pano": 11
       }
       
       menu(dicLivros)
   
   if __name__ == "__main__":
       main()
   ```
   
   
