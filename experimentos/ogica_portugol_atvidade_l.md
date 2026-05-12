# Solução Atividade de fixação de lógica com Portugol



1. Solicite ao usuário 3 notas e retorne a média simples das notas.

```portugol
programa {
  funcao inicio() {

  real  nota1, nota2, nota3, media

    escreva("Digite a primeira nota: ")
    leia(nota1)

    escreva("Digite a segunda nota: ")
    leia(nota2)

    escreva("Digite a terceira nota: ")
    leia(nota3)

    media = (nota1 + nota2 + nota3) / 3

    escreva("A média das notas é: ", media)

  }
}
```

**O que pode ser observado neste código:**

**Declaração de variáveis** **com tipagem:** usamos `real` porque notas podem ter casas decimais.

| **Tipo**    | **O que armazena?**        | **Exemplo de Sintaxe**         |
| ----------- | -------------------------- | ------------------------------ |
| **Inteiro** | Números sem frações        | `inteiro idade = 25`           |
| **Real**    | Números com frações        | `real preco = 19.90`           |
| **Cadeia**  | Textos (letras e símbolos) | `cadeia nome = "Ana"`          |
| **Logico**  | Valores binários (V ou F)  | `logico aprovado = verdadeiro` |

**Atribuição:** Quando um valor é armazenado em uma variável com o sinal   `=`.

**Entrada de dados**: `leia()` captura o valor digitado pelo usuário.

**Processamento**: relizando operações com as variáveis `(nota1 + nota2 + nota3) / 3`.

**Saída de dados**: `escreval()` mostra o resultado na tela.

**Prioridade de Operações:** Assim como na matemática, no Portugol a multiplicação acontece antes da adição. Os parênteses são fundamentais para garantir que a soma de todas as notas seja feita **antes** da divisão pelo total dos pesos.

---



2. Altere o código anterior para solicitar o nome do estudante e mostrar na saída junto à média.

```portugol
programa {
  funcao inicio() {

    // Declaração das variáveis, "cadeia" é o tipo ideal para nomes e textos
    cadeia nome
    real nota1, nota2, nota3, media

    // Solicita o nome do estudante
    escreva("Digite o nome do estudante: ")
    leia(nome)

    escreva("Digite a primeira nota: ")
    leia(nota1)

    escreva("Digite a segunda nota: ")
    leia(nota2)

    escreva("Digite a terceira nota: ")
    leia(nota3)

    // Cálculo da média
    media = (nota1 + nota2 + nota3) / 3

    // Saída formatada com o nome e a média
    escreva("\nO estudante ", nome, " obteve a média: ", media)

  }
}
```

**O que pode ser observado neste código:**

**Comentários**: textos explicativos que ajudam a entender partes do código, em portugol usa-se  `//` antes do texto. Também pode usando para "desativar" determinada parte do código.  

**Declaração `cadeia nome`**: Adicionamos o tipo `cadeia` para que o algoritmo consiga reservar um espaço na memória para o texto (o nome).

**Formatação da saída de dados**: No último `escreva`, concatenamos (juntamos) a variável `nome` com a frase de resultado. O `\n` serve apenas para pular uma linha e deixar o console mais organizado.

---



3. Altere o código anterior para utilizar média ponderada.

```portugol
programa {
  funcao inicio() {

    cadeia nome
    real nota1, nota2, nota3, media
    // Definindo os pesos (poderiam ser variáveis também)
    inteiro p1 = 2, p2 = 1, p3 = 1

    escreva("Digite o nome do estudante: ")
    leia(nome)

    escreva("Digite a primeira nota (Peso ", p1, "): ")
    leia(nota1)

    escreva("Digite a segunda nota (Peso ", p2, "): ")
    leia(nota2)

    escreva("Digite a terceira nota (Peso ", p3, "): ")
    leia(nota3)

    // Cálculo da média ponderada: (N1*P1 + N2*P2 + N3*P3) / (P1 + P2 + P3)
    media = (nota1 * p1 + nota2 * p2 + nota3 * p3) / (p1 + p2 + p3)

    escreva("\n--- Boletim ---")
    escreva("\nEstudante: ", nome)
    escreva("\nMédia Ponderada: ", media)

  }
}
```

**O que pode ser observado neste código:**

**Variáveis de Peso:** Note que usamos variáveis `p1`, `p2` e `p3`. Isso é uma boa prática de programação (Clean Code), pois se os pesos da escola mudarem, você só precisa alterar o valor em um lugar, e não em toda a fórmula.

**A Fórmula:** A principal mudança está na expressão matemática. Em vez de apenas somar e dividir pela quantidade, multiplicamos cada nota pelo seu respectivo peso:

`media = (nota1 * p1 + nota2 * p2 + nota3 * p3) / (p1 + p2 + p3)`

Na média ponderada é como se a primeira nota (peso 2) "valesse por 2 notas iguais" no cálculo final, dando mais importância a ela.

---



4. Altere o código para informar se o estudante foi aprovado ou reprovado (média 6).

```portugol
se (media >= 6) {
      escreva("\nStatus: Aprovado")
    } senao {
      escreva("\nStatus: Recuperação")
    }
```

**O que pode ser observado neste código:**

**Estrutura condicional / tomada de decisão**:

* `se (condicao)`

​	O `se` funciona como um teste. Ele avalia o que está dentro dos parênteses e espera um resultado **lógico** (`verdadeiro` ou `falso`).

- **A condição:** `media >= 6` pergunta ao computador: "O valor guardado na variável `media` é maior ou igual a sete?"
- Se a resposta for **verdadeiro**, o computador executa tudo o que estiver dentro das primeiras chaves `{ }`.

* O `senao`

​	O `senao` é o plano B. Ele é executado **apenas se** a condição do `se` for **falsa**.

- Ele não precisa de uma nova pergunta entre parênteses, pois ele captura "todo o resto". Se a média não for maior ou igual a 6, ela é obrigatoriamente menor que 6, caindo aqui.

**Operadores Relacionais e Lógicos**:

1. **`==` (Igual a):** Compara se os valores são idênticos.
2. **`!=` (Diferente de):** Verifica se os valores são distintos.
3. **`e` (E lógico):** Exige que todas as condições sejam verdadeiras.
4. **`ou` (OU lógico):** Exige que pelo menos uma condição seja verdadeira.

---



5. Solicite ao usuário 1 número e informe se este é par ou ímpar.

```portugol
programa {
  funcao inicio() {
    
    inteiro numero

    escreva("Digite um número inteiro: ")
    leia(numero)

    // O símbolo % calcula o resto da divisão
    se (numero % 2 == 0) {
      escreva("O número ", numero, " é PAR.")
    } senao {
      escreva("O número ", numero, " é ÍMPAR.")
    }

  }
}
```

**Lógica do Exercício**

Todo número **par** é divisível por 2, ou seja, o resto da divisão por 2 é sempre **0**. Se o resto for **1**, o número é **ímpar**.

**O que pode ser observado neste código:**

- **`numero % 2`**: O computador divide o número por 2 e "guarda" apenas o que sobrou, com o operador  `%`.
- **`== 0`**: O símbolo `==` é um operador de comparação. Ele verifica se o lado esquerdo é igual ao lado direito. (Cuidado: um único `=` serve para atribuir valor, dois `==` servem para comparar).
- **A Condição**: Se o resto da divisão de `numero` por 2 for exatamente igual a 0, o código entra no bloco do `se`. Caso contrário, o `senao` assume o controle.

**Operadores aritméticos**

| **Operador** | **Operação**   | **Exemplo** | **Resultado** |
| ------------ | -------------- | ----------- | ------------- |
| **`+`**      | Soma           | `5 + 2`     | `7`           |
| **`-`**      | Subtração      | `5 - 2`     | `3`           |
| **`\*`**     | Multiplicação  | `5 * 2`     | `10`          |
| **`/`**      | Divisão        | `5 / 2`     | `2.5`         |
| **`%`**      | Módulo (Resto) | `5 % 2`     | `1`           |

---



6. Leia o ano de nascimento de uma pessoa e o ano atual. Com base nisso, deve calcular a idade da pessoa e informar se ela é maior de idade (18 anos ou mais) ou não.

```portugol
programa {
  funcao inicio() {

    // Declaração das variáveis
    inteiro ano_nascimento, ano_atual, idade

    // Entrada de dados
    escreva("Em que ano você nasceu? ")
    leia(ano_nascimento)

    escreva("Em qual ano estamos? ")
    leia(ano_atual)

    // Processamento: Cálculo da idade
    idade = ano_atual - ano_nascimento

    escreva("\nVocê tem (ou fará) ", idade, " anos.\n")

    // Estrutura de Decisão: Verificação da maioridade
    se (idade >= 18) {
      escreva("Status: Você é MAIOR de idade.")
    } senao {
      escreva("Status: Você é MENOR de idade.")
    }

  }
}
```

**O que pode ser observado neste código:**

**A Ordem da Subtração:** É importante lembrar que, na matemática computacional, a ordem importa. Para a idade ser positiva, subtraímos o `ano_nascimento` (menor) do `ano_atual` (maior).



---



7.  Leia o salário atual de um funcionário e o percentual de reajuste, calcule e exiba o novo salário após o aumento.

```portugol
programa {
  funcao inicio() {

    // Declaração de variáveis
    // Usamos 'real' pois salários e percentuais podem ter casas decimais
    real salario_atual, percentual, aumento, novo_salario

    escreva("Digite o salário atual do funcionário: R$ ")
    leia(salario_atual)

    escreva("Digite o percentual de reajuste (ex: 10 para 10%): ")
    leia(percentual)

    // Cálculo do aumento: (salario * percentual) / 100
    aumento = salario_atual * (percentual / 100)

    // Cálculo do novo salário
    novo_salario = salario_atual + aumento

    // Exibição dos resultados
    escreva("\n--- Resumo do Reajuste ---")
    escreva("\nValor do aumento: R$ ", aumento)
    escreva("\nNovo salário: R$ ", novo_salario)
    
  }
}
```

**O que pode ser observado neste código:**

**Por que dividir por 100?**

Na matemática, 10% é o mesmo que 10 / 100 ou 0.10. Como o usuário digita apenas o número inteiro (ex: 10), precisamos fazer essa conversão no código para que a multiplicação funcione corretamente.

**A ordem das operações:**

Usamos os parênteses em `(percentual / 100)` para deixar o código mais legível, embora no Portugol a multiplicação e a divisão tenham a mesma prioridade e seriam executadas da esquerda para a direita.

---



8. Leia a idade de duas pessoas e calcule a diferença de idade entre elas.

```portugol
programa {
  funcao inicio() {
    
    inteiro idade1, idade2, diferenca

    escreva("Digite a idade da primeira pessoa: ")
    leia(idade1)

    escreva("Digite a idade da segunda pessoa: ")
    leia(idade2)

    // Lógica para garantir que a diferença seja sempre positiva
    se (idade1 > idade2) {
      diferenca = idade1 - idade2
    } senao {
      diferenca = idade2 - idade1
    }

    escreva("\nA diferença de idade entre elas é de: ", diferenca, " anos.")
    
  }
}
```

**O que pode ser observado neste código:**

**O Problema:** Se a primeira pessoa tem 15 anos e a segunda tem 25, o cálculo `15 - 25` resultaria em `-10`.

**A Solução:** Usamos o `se` para descobrir quem é o mais velho e sempre subtrair o **menor do maior**. Isso garante que o resultado seja um número natural.

