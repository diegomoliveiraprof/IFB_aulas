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
> O detalhe aqui é que os argumentos são **posicionais** ou seja devem ser acessados de acordo sua posição na passagem.

---

## O **kwargs Argumentos Nomeados Variáveis
Semelhante ao `*args`, mas para argumentos nomeados (chave=valor).   
O Python empacota esses argumentos em um Dicionário. Usamos dois asteriscos `**`.  
**kwargs vai permitir passar uma quantidade variável de argumentos nomeados.


```python
  def exibir_info(**kwargs):
      for chave, valor in kwargs.items():
          print(f"{chave}: {valor}")
  
  exibir_info(nome="Fulano", idade=30, cidade="Brasília")
```
> **kwargs é tratado como um dicionário dentro da função. 

---

# Fixação

1. Crie uma função saudacao que receba nome (padrão = "Aluno") e mensagem (padrão = "Bem-vindo").    
Teste chamando a função sem argumentos, com apenas um argumento e com os dois.

2. Crie uma função area_retangulo (largura x altura) que receba largura e altura sendo altura(padrão = 1).    
Calcule a área e teste chamando a função com diferentes combinações de parâmetros.

3. Crie uma função media que receba vários números via *args e retorne a média deles.

4. Crie uma função concatenar que receba várias strings via *args e retorne uma única string concatenada.

5. Crie uma função perfil_usuario que receba informações como nome, idade, cidade via **kwargs e exiba formatado.

6. Crie uma função configuracoes que receba parâmetros opcionais como tema, idioma, notificacoes via **kwargs e mostre as configurações escolhidas.


