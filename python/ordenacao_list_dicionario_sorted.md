# Ordenação de listas de dicionários com `lambda` e `sorted`



Ordenar listas de itens que também podem ser iterados, como dicionários requer alguns cuidados.



## Ordenação "na unha"

Sem o uso da função `sorted()` seria necessário a utilização de algum algoritmo de ordenação diretamente no código, como o **Bubble Sort** por exemplo:

```python
lista = [
    {"nome": "Fulano3", "idade": 20, "telefone": '000000'},
    {"nome": "Fulano2", "idade": 29, "telefone": '1111111'},
    {"nome": "Fulano1", "idade": 16, "telefone": '444444'}
]

# Bubble Sort pela idade
n = len(lista)
for i in range(n):
    for j in range(0, n - i - 1):
        if lista[j]["idade"] > lista[j + 1]["idade"]:
            # troca de posição
            lista[j], lista[j + 1] = lista[j + 1], lista[j]

print("Ordenada por idade:", lista)
```

No exemplo apresentado, é necessário percorrer toda a lista original, e ao mesmo tempo, percorrer cada item da lista a procura do subitem com maior valor, e realizar uma série de trocas de posição até que a lista esteja ordenada.



## Ordenação com `sorted()`

No exemplo anterior, foi necessário usar um `for` para percorrer a lista e outro para percorrer cada elemento da lista.

A função `sorted()` faz o trabalho de percorrer a lista e seus elementos, e nos permite ordenar listas de dicionários, baseada em uma **chave** do dicionário.

A chave deve ser informada (de forma indireta) no parâmetro **key** da função:

Sintaxe:

```python
lista_ordenada = sorted(lista, key=???)
```



Neste caso, o parâmetro **key=** , não recebe diretamente o valor da chave, mas sim o "caminho/modo/lógica" de como encontrar essa chave.

Fazemos isso passando uma função para o **key=**, mas não o resultado de uma função e sim a lógica da função para encontrar o valor da chave desejada.

Exemplo:

```python
lista=[{"nome":"Carlos","idade": 20, "telefone":'000000'},
 {"nome":"Ana","idade": 29, "telefone":'1111111'},
  {"nome":"Beto","idade": 16, "telefone":'444444'}]

print(lista)

def get_idade(pessoa):
  return pessoa["idade"]

ordenada2 = sorted(lista, key=get_idade) #key=get_idade sem ( )

print(ordenada2)
```

Neste exemplo, temos uma lista de dicionários que deve ser organizada pela chave **idade**.

* Criamos uma função que recebe um dicionário chamado **pessoa** e retorna o valor da chave **idade**.

* Passamos para  **key=** , o objeto dessa função e não seu retorno, por isso o nome da função sem os parênteses.

  ```python
  ordenada2 = sorted(lista, key=get_idade) #key=get_idade sem ( )
  ```

  * Neste caso  **key=** recebe não o resultado da função mas sua lógica de como encontrar o resultado.

  * Fazemos isso porque quem executa a função **get_idade()** ou seu "miolo", sua lógica, não é o nosso código e sim o próprio `sorted()` que vai executar essa lógica em todos os elementos da lista que foi passada para ele, dispensando o uso de um `for` .



## Ordenação com `sorted()`  e `lambda`

No exemplo anterior, criamos a função **get_idade()** só para mostrar o valor de uma chave dentro do dicionário.

Em seguida, usamos apenas o **"miolo"/lógica** dessa função para que o `sorted()` consiga fazer a ordenação.

Sabemos que o **lambda** nos permite criar uma função, apenas com sua lógica e sem um nome específico.

```python
dobro =  lambda x: x*2			# onde lambda é função anônima (sem nome), atribuida a uma variável (dentro da variável)
print(dobro(2))        			# a função dentro da variável sendo executada
```

Logo, se apresentarmos apenas um **lambda** com sua lógica para o parâmetro **key=** da função `sorted()`, isso será suficiente para realizar a ordenação.

```python
ordenada2 = sorted(lista, key=lambda pessoa: pessoa["idade"]) #a lógica da função get_idade é atribuida diretamente à key sem nome
```

Comparando:

```python
# Função nomeada
def get_idade(pessoa):
    return pessoa["idade"]

ordenada1 = sorted(lista, key=get_idade)

# Função anônima (lambda)
ordenada2 = sorted(lista, key=lambda pessoa: pessoa["idade"])
```



Exemplo completo:

```python
lista=[{"nome":"Carlos","idade": 20, "telefone":'000000'},
 {"nome":"Ana","idade": 29, "telefone":'1111111'},
  {"nome":"Beto","idade": 16, "telefone":'444444'}]

print(lista)

ordenada2 = sorted(lista, key=lambda pessoa: pessoa["idade"]) # lógica direto com lambda, sem criar a função

print(ordenada2)
```

Neste exemplo a lógica vai direto no parâmetro **key** sem criar a necessidade de criar função inteira.

O algoritmo de ordenação utilizado pelo `sorted()`é o **Timsort**.

