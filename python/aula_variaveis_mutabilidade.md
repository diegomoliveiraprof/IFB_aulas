# Variáveis em python: escopo, mutabilidade e uso em funções



O Python lida com variáveis de um jeito um pouco diferente de outras linguagens (ele não copia valores, ele gerencia referências). Isso pode confundir um pouco no início. 

**Vamos estudar alguns aspectos importantes:**

1. Variáveis e referências

2. Escopo (local e global)
3. Objetos mutáveis e imutáveis
4. Passagem de parâmetros em funções
5. Resumo e caso que pode confundir.

---



## 1. Variáveis e referências

Conceitualmente se imagina que uma variável é como uma caixinha onde se pode guardar um valor, o que não está completamente errado. 

Porém em Python é mais correto pensar que a variável aponta para um objeto.

```python
x = 10
y = x

print(x)
print(y)
#saida: 
#10
#10
#
```

Pode parecer que `y` recebeu valor de `x`, mas na verdade `y ` recebeu uma referência para o mesmo objeto que `x`. Podemos ver isso usando a função `id()`que retorna o identificador do objeto em memória.

```python
print(id(x))
print(id(y))
#saida
#11645640
#11645640
```

Neste ponto `x`e `y`apontam para o mesmo objeto na memória.

O que acontece se eu mudar valor de `x`?

```python
x = 20

print(x)
print(y)

print(id(x))
print(id(y))
#saida
#20
#10
#11645960
#11645640
```

Quando `x`é modificado, ele passa a apontar para um novo objeto na memória.

Quando executamos `x = 20`, o nome `x` deixa de referenciar o objeto de valor `10` e passa a referenciar o objeto de valor `20`.

Imagine que a variável é uma etiqueta colada em um objeto. Quando fazemos `x = 20`, não alteramos o objeto `10`; apenas retiramos a etiqueta `x` do objeto `10` e a colocamos no objeto `20`.

---



## 2. Escopo (local e global)

Escopo é a região do código onde um nome (variável) pode ser acessado.

* Global - todo o codigo (com alguns detalhes)

* Local - dentro de uma estrutura específica, como uma função.

  

### 2.1. Global

Variáveis globais são "visíveis" em todo o código, podem ser acessadas de qualquer parte do código.

Variáveis globais podem ser acessadas a partir de funções e outras partes do programa, desde que não sejam ocultadas por uma variável local com o mesmo nome.

#### Acessando uma variável global

```python
nome = "Maria"

def mostrar():
    print(nome)

mostrar()
#saida
#Maria
```

A função consegue ler a variável global.



#### Modificando uma variável local

Variáveis globais não podem ser modificadas diretamente dentro de estruturas fechadas como funções.

```python
contador = 0

def incrementar():
    contador = contador + 1

incrementar()
#saida
#UnboundLocalError
```

Como tentamos uma atribuição a variável `contador` o  python acha que variável é local.

**Usando a cláusula `global`**

```python
contador = 0

def incrementar():
    global contador
    contador += 1

incrementar()

print(contador)
#saida
#1
```

Com a cláusula `global` informamos ao python que variável foi declarada globalmente.

**Em programas reais, evite o uso excessivo de variáveis globais.**

Prefira o uso de funções com retorno.

```python
def incrementar(valor):
    return valor + 1

contador = 0
contador = incrementar(contador)
print(contador)
#saida
#1
```



### 2.2 Local

Variáveis locais existem apenas no "bloco/espaço" onde foram criadas.

```python
def mostrar():
    idade = 20
    print(idade)

mostrar()
print(idade)
#saida
#NameError: name 'idade' is not defined
```

Uma variável criada em uma função não pode ser acessa fora da função.



### 2.3 Sombreamento de variáveis

Exemplo clássico de **sombreamento de variáveis** (*variable shadowing*).

```python
nome = "Maria"  # variável global

def mostrar():
    nome = "João"  # variável local
    print("Dentro da função:", nome)

mostrar()

print("Fora da função:", nome)

#saida
#Dentro da função: João
#Fora da função: Maria
```

Existe uma variável chamada `nome` no escopo global e uma no escopo local da função `mostrar`.

Dentro da função a variável `nome` local "esconde" a variável global.

---



## 3. Objetos mutáveis e imutáveis

Essa é a base para entender funções e manipulação de variáveis.

Neste caso, entenda como objeto sendo aquilo para onde uma variável aponta, aquilo que é referenciado por uma variável

### 3.1 Imutável

Não podem ser alterados depois de criados.

Exemplos:

- int
- float
- bool
- str
- tuple

```python
nome = "ana"
nome[0] = "A"

#saida
#TypeError: 'str' object....
```

Strings são imutáveis.

Mas, eu consigo alterar a frase dentro da string, como ela pode ser imutável?

O que realmente acontece:

```python
nome = "ana"
#print(id(nome))
print(nome)
nome = "Ana"
#print(id(nome))
print(nome)

#saida sem id()
#ana
#Ana

#Descomente as linhas da função id()
#saida com id()
#139364397325776
#ana
#139364418845792
#Ana
```

À primeira vista parece que alteramos a string, mas na verdade criamos uma nova string e fazemos a variável apontar para ela.

Como os identificadores são diferentes, concluímos que se trata de dois objetos distintos. O objeto `"ana"` não foi modificado; um novo objeto `"Ana"` foi criado e a variável `nome` passou a referenciá-lo.

---



## 4. Passagem de parâmetros em funções

Tecnicamente, **Python é passagem por atribuição** (*pass-by-assignment*) ou, como alguns livros chamam, **passagem por compartilhamento de objeto** (*call-by-sharing*).

Não é exatamente passagem por valor nem exatamente passagem por referência como em C++.

Quando uma função é chamada, o parâmetro recebe uma referência para o mesmo objeto que foi passado como argumento.

Se o objeto for modificado, a alteração pode ser observada fora da função.

Se o parâmetro passar a apontar para outro objeto, isso não afeta a variável usada na chamada.

Em Python, funções recebem referências para os mesmos objetos, mas a reatribuição do parâmetro não altera a variável usada na chamada. 

Isso faz com que objetos mutáveis e imutáveis se comportem de maneira diferente quando passados para funções.

### 4.1. Exemplo com inteiro (imutável)

```python
def dobrar(x):
    print("Dentro da função")
    print("Antes da atribuição:",x)
    x = x * 2
    print("Depois da atribuição:", x)

x = 10

dobrar(x)

print("\n\nFora da função:", x)

#saida
#Dentro da função
#Antes da atribuição: 10
#Depois da atribuição: 20
#
#
#Fora da função: 10
```

Por que não mudou?

Porque inteiros são imutáveis.

A atribuição:

```python
x = x * 2
```

faz `x` apontar para outro objeto.



### 4.2. Exemplo com lista (mutável)

```python
def adicionar(lista):
    lista.append(100)

dados = [1, 2, 3]

adicionar(dados)

print(dados)

#saida
#[1, 2, 3, 100]
```

Mudou fora da função.

Por quê?

Porque a função recebeu uma referência para a mesma lista e a modificou.



### 4.3. Caso que confunde

```python
def alterar(lista):
    lista = [10, 20, 30]

dados = [1, 2, 3]

alterar(dados)

print(f"dados= {dados}")
#verificar a mudança com a função id()
#saida
#[1, 2, 3]
```

Por que?

Porque a variável local `lista` passou a apontar para outra lista.

A lista original não foi modificada.



### 4.3.1. Comparação importante

**Modifica o objeto**

```python
def f(lista):
    lista.append(10)
```

Afeta o argumento original.

**Reatribui a variável**

```python
def f(lista):
    lista = [10]
```

Não afeta o argumento original.



---



# 5. Resumo 

| Conceito | Exemplo | Pode mudar? |
| -------- | ------- | ----------- |
| int      | 10      | Não         |
| float    | 3.14    | Não         |
| str      | "Ana"   | Não         |
| tuple    | (1,2)   | Não         |
| list     | [1,2]   | Sim         |
| dict     | {"a":1} | Sim         |
| set      | {1,2}   | Sim         |

------

## Regra de ouro

Quando uma função recebe um parâmetro:

- Se o objeto for **imutável**, alterações normalmente não afetam a variável original.
- Se o objeto for **mutável**, alterações no objeto podem ser vistas fora da função.
- Reatribuir o parâmetro dentro da função não altera a variável original.
- Modificar o objeto apontado pelo parâmetro pode alterar o valor observado fora da função.



## 5.1. Fixação

Tente prever as saídas antes de executar os códigos:

```python
x = 10

def teste1(x):
    x = x + 5

teste1(x)
print(x)


lista = [1, 2]

def teste2(l):
    l.append(3)

teste2(lista)
print(lista)


lista2 = [1, 2]

def teste3(l):
    l = [9, 9]

teste3(lista2)
print(lista2)

l = [1, 2]

def teste3(l):
    l = [9, 9]

teste3(l)
print(l)
```

