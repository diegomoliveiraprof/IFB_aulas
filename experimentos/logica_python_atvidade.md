1. Solicite ao usuário dois números inteiros. O programa deve comparar os dois valores e exibir qual deles é o maior.

```Python
num1 = int(input("Digite o primeiro número: "))
num2 = int(input("Digite o segundo número: "))

if num1 > num2:
    print(f"O maior número é: {num1}")
else:
    print(f"O maior número é: {num2}")
```

---


2. Solicite ao usuário 1 número e informe se este é par ou ímpar.

```Python
num = float(input("Insira um número: "))
   
if num % 2 == 0:
	print("Número PAR")
else:
    print("Número IMPAR")
```

---


3. Solicite ao usuário o nome do estudante e 3 notas, retorne a média ponderada das notas (com pesos 1,1 e 2), o nome do estudante e se reprovado (media 6 aprovado).

```python
nome = input("Nome do estudante: ")
nota1= float(input("Nota 1: "))
nota2= float(input("Nota 2: "))
nota3= float(input("Nota 3: "))

#pesos
p1=1
p2=1
p3=2

#media ponderada
media = (nota1*p1 + nota2*p2 + nota3*p3) / (p1+p2+p3)

print(f"\nEstudante: {nome}")
print(f"Média: {media:.2f}")

if (media < 6):
  print("Situação: Reprovado")
else:
  print("Situação: Aprovado")
```

---


4. Leia o ano de nascimento de uma pessoa e o ano atual. Com base nisso, calcule a idade da pessoa e informe se ela é maior de idade (18 anos ou mais) ou menor de idade.

```Python
ano_nascimento = int(input("Ano de nascimento: "))
ano_atual = int(input("Ano atual: "))

idade = ano_atual - ano_nascimento
print(f"Esta pessoa tem ou completará: {idade} anos")

if idade < 18:
    print("Situação: Menor de idade")
else:
    print("Situação: Maior de idade")
```

---


5. Leia o salário atual de um funcionário e o percentual de reajuste. Calcule e exiba o valor do aumento e o novo salário após o reajuste.

```Python
salario = float(input("Salário atual: "))
percentual = float(input("Percentual de reajuste %: "))

percentual = percentual / 100
reajuste = salario * percentual
salario_atualizado = salario + reajuste

print(f"\\nReajuste: R$ {reajuste:.2f}")
print(f"Salário atualizado: R$ {salario_atualizado:.2f}")
```

----


6. Leia a idade de duas pessoas e calcule a diferença absoluta de idade entre elas (sem exibir valores negativos).

```Python
idade1 = int(input("Idade 1: "))
idade2 = int(input("Idade 2: "))

diferenca = idade1 - idade2

if diferenca < 0:
    diferenca = diferenca * -1

print(f"Diferença: {diferenca} anos")
```

----


7. Leia o valor de um produto. Se o valor for maior que R$ 100,00, aplique um desconto de 10%. Caso contrário, aplique um desconto de apenas 5%. Exiba o valor do desconto calculado e o preço final que o cliente irá pagar.

```Python
valor_produto = float(input("Digite o valor do produto R$: "))

if valor_produto > 100:
    percentual = 0.10
else:
    percentual = 0.05

desconto = valor_produto * percentual
valor_final = valor_produto - desconto

print(f"Desconto aplicado: R$ {desconto:.2f}")
print(f"Valor final a pagar: R$ {valor_final:.2f}")
```

----


8. Solicite ao usuário que digite um nome de usuário e uma senha. O sistema deve verificar se o usuário é exatamente "admin" e se a senha é "1234". Se ambos estiverem corretos, exiba "Acesso liberado". Caso contrário, exiba "Acesso negado".

```Python
usuario = input("Digite o usuário: ")
senha = input("Digite a senha: ")

if usuario == "admin" and senha == "1234":
    print("Acesso liberado")
else:
    print("Acesso negado. Usuário ou senha incorretos.")
```

----


9. Solicite a distância total percorrida por um carro (em km) e o total de combustível gasto (em litros). Calcule o consumo médio do veículo (km/l). Se o consumo for menor que 10 km/l, exiba a mensagem "Situação: Consumo alto". Caso contrário, exiba "Situação: Consumo dentro do esperado".

```Python
distancia = float(input("Distância percorrida (em km): "))
litros = float(input("Combustível gasto (em litros): "))

consumo_medio = distancia / litros
print(f"Consumo médio: {consumo_medio:.2f} km/l")

if consumo_medio < 10:
    print("Situação: Consumo alto")
else:
    print("Situação: Consumo dentro do esperado")
```

---


10. Conversor de Sistema Métrico para Americano: 
    Escreva um programa que receba do usuário uma medida em centímetros (cm). Em seguida, o programa deve exibir um menu para que o usuário escolha para qual unidade do sistema americano deseja converter, utilizando as seguintes fórmulas:

* Polegadas (in): $Polegadas = \frac{Centímetros}{2.54}$
* Jardas (yd): $Jardas = \frac{Centímetros}{91.44}$
* Milhas (mi): $Milhas = \frac{Centímetros}{160934.4}$

O programa deve calcular e exibir o valor convertido com duas casas decimais. Caso o usuário selecione uma opção inválida, exiba uma mensagem de erro.

```Python
# Solicitando a entrada do valor em centímetros
cm = float(input("Digite o valor em centímetros (cm): "))

# Exibindo as opções de conversão
print("\nEscolha a unidade para conversão:")
print("1 - Polegadas (in)")
print("2 - Jardas (yd)")
print("3 - Milhas (mi)")
opcao = input("Digite o número da opção desejada: ")

# Processando a escolha do usuário
if opcao == "1":
    resultado = cm / 2.54
    print(f"\nResultado: {cm:.2f} cm equivalem a {resultado:.2f} polegadas (in).")

elif opcao == "2":
    resultado = cm / 91.44
    print(f"\nResultado: {cm:.2f} cm equivalem a {resultado:.2f} jardas (yd).")

elif opcao == "3":
    resultado = cm / 160934.4
    # Usamos 5 casas decimais para milhas porque o valor costuma ser muito pequeno
    print(f"\nResultado: {cm:.2f} cm equivalem a {resultado:.5f} milhas (mi).")

else:
    print("\nErro: Opção inválida! Por favor, escolha 1, 2 ou 3.")
```
