# Parâmetros da função: valores padrão, *args e **kwargs



## Parâmetros com Valores Padrão (Default Arguments)
Em Python, podemos definir valores padrão para parâmetros. Isso permite chamar a função sem precisar passar todos os argumentos.
Permite que a função seja executada mesmo se um arqumento necessário não for passado. Se o valor for omitido, o Python usa o valor padrão definido na criação da função.   

Exemplo:
```python
  def criar_usuario(nome, plano="Gratuito"):
      print(f"Usuário: {nome} | Plano: {plano}")
  
  # Chamando a função sem o segundo argumento
  criar_usuario("Ana")  
  # Saída: Usuário: Ana | Plano: Gratuito
  
  # Mudando o valor padrão
  criar_usuario("Carlos", "Premium")  
  # Saída: Usuário: Carlos | Plano: Premium
```

> **Regra de Ouro:** Parâmetros com valores padrão sempre devem vir depois dos parâmetros obrigatórios na assinatura da função.
`Errado: def func(a=1, b): | Certo: def func(b, a=1):`

---


## *args Argumentos Posicionais Variáveis
E se você não souber quantos argumentos o usuário vai enviar? O `*args` permite que a função receba um número dinâmico de argumentos posicionais.       
O caractere crucial aqui é o asterisco `*`. O Python empacota todos esses valores em uma Tupla.     
`*args` permite passar uma quantidade variável de argumentos posicionais.   

```python
  def soma(*args):
      total = sum(args)
      print(f"Soma: {total}")
  
  soma(1, 2, 3)
  soma(10, 20, 30, 40)
```
> O detalhe aqui é que os argumentos são **posicionais** ou seja devem ser acessados de acordo dua possição na passagem.

---

## O **kwargs Argumentos Nomeados Variáveis
Semelhante ao `*args`, mas para argumentos nomeados (chave=valor). O Python empacota esses argumentos em um Dicionário. Usamos dois asteriscos ().

💡 Analogia: É como uma ficha de cadastro ou um formulário com campos personalizados. Você passa o nome do campo e o valor correspondente.
