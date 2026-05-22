# Estruturas de controle em python
Crie um programa que simule o funcionamento de um caixa eletrônico. O usuário inicia com um saldo fictício e pode realizar as seguintes operações por um menu iterativo:
Consultar saldo
Depositar dinheiro
Sacar dinheiro
Sair

O programa deve repetir o menu até o usuário escolher a opção 4 (sair).

## Solução 1.
Usando a estrutura `match-case`.

```python
# Saldo inicial fictício do usuário
saldo = 1000

# Variável para armazenar a opção escolhida no menu
op = 0

# Loop principal: continua até o usuário escolher a opção 4 (sair)
while op != 4:
    print("\n------Banco------")
    print("Consultar Saldo     - 1")
    print("Sacar Dinheiro      - 2")
    print("Depositar Dinheiro  - 3")
    print("Sair                - 4\n")

    # Solicita ao usuário que escolha uma opção
    # O teste é feito com str para evitar erros caso usuário digite letras
    op = input("Opção: ")

    # Estrutura match-case para tratar cada opção
    match op:
        case "1":# Exibe o saldo formatado com duas casas decimais
            print(f"Saldo: {saldo:.2f}")

        case "2":# Solicita valor para saque
            valor = float(input("Sacar - Valor: "))

            # Verifica se o valor é válido e se há saldo suficiente
            if valor <= saldo and valor > 0:
                saldo = saldo - valor
                print("Saque autorizado!")
            else:
                print("Saldo insuficiente ou valor inválido.")

        case "3":# Solicita valor para depósito
            valor = float(input("Depositar - Valor: "))

            # Verifica se o valor é positivo
            if valor > 0:
                saldo = saldo + valor
                print("Depósito realizado!")
            else:
                print("Valor inválido.")

        case "4":# Finaliza o programa
            print("Saindo!")
            op = 4

        case _:# Caso o usuário digite uma opção inválida
            print("Opção inválida")

```



## Solução 2
Usando `if, elif e else` no lugar do `match-case`.
```python
# Saldo inicial fictício do usuário
saldo = 1000

# Variável para armazenar a opção escolhida no menu
op = 0

# Loop principal: continua até o usuário escolher a opção 4 (sair)
while op != 4:
    print("\n------Banco------")
    print("Consultar Saldo     - 1")
    print("Sacar Dinheiro      - 2")
    print("Depositar Dinheiro  - 3")
    print("Sair                - 4\n")

    # Solicita ao usuário que escolha uma opção
    op = input("Opção: ")

    # Estrutura condicional com if/elif/else
    if op == "1":
        # Exibe o saldo formatado com duas casas decimais
        print(f"Saldo: {saldo:.2f}")

    elif op == "2":
        # Solicita valor para saque
        valor = float(input("Sacar - Valor: "))
        
        # Verifica se o valor é válido e se há saldo suficiente
        if valor <= saldo and valor > 0:
            saldo = saldo - valor
            print("Saque autorizado!")
        else:
            print("Saldo insuficiente ou valor inválido.")

    elif op == "3":
        # Solicita valor para depósito
        valor = float(input("Depositar - Valor: "))
        # Verifica se o valor é positivo
        if valor > 0:
            saldo = saldo + valor
            print("Depósito realizado!")
        else:
            print("Valor inválido.")

    elif op == "4":
        # Finaliza o programa
        print("Saindo!")
        op = 4

    else:
        # Caso o usuário digite uma opção inválida
        print("Opção inválida")

```
