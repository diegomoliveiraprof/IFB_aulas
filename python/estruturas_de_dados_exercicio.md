# Estruturas de Dados e Funções em Python



Exercício:

Criar um programa que gerencia uma lista de tarefas. 

O programa deve:

1. Permitir que o usuário adicione tarefas. Cada tarefa deve ter: Descrição (string), Prioridade (inteiro de 1 a 5, onde 1 é a prioridade mais alta) e Status (inicialmente “pendente”);
2. Armazenar cada tarefa como um dicionário com as chaves "descrição", "prioridade" e "status";
3. Manter todas as tarefas numa lista;
4. Criar funções para: Adicionar tarefas, Mostrar todas as tarefas ordenadas por prioridade (da maior para a menor) e Marcar uma tarefa como concluída (alterar o status para “concluída”);
5. Criar uma função `main()` que permita ao usuário escolher opções num menu para: Adicionar tarefa, Listar tarefas, Marcar tarefa como concluída e Sair do programa.



```python
def adicionar_tarefa(lista, descricao, prioridade):
    """Adiciona uma nova tarefa à lista.

    Args:
        lista (list): Lista de tarefas onde a nova tarefa será armazenada.
        descricao (str): Texto descrevendo a tarefa.
        prioridade (int): Valor da prioridade (1 = mais alta, 5 = mais baixa).
    """
    tarefa = {
        "descrição": descricao,
        "prioridade": prioridade,
        "status": "pendente"
    }
    lista.append(tarefa)
    # Ordena as tarefas pela prioridade (1 = mais alta)
    return sorted(lista, key=lambda x: x["prioridade"])


def listar_tarefas(lista):
    """Exibe todas as tarefas ordenadas por prioridade."""

    print("\n--- Lista de Tarefas ---")

    # Percorre cada tarefa ordenada e imprime os detalhes
    for i, tarefa in enumerate(lista, start=1):
        print(
            f"{i}. Descrição: {tarefa['descrição']} | Prioridade: {tarefa['prioridade']} | Status: {tarefa['status']}"
        )


def concluir_tarefa(lista, indice):
    """Marca a tarefa escolhida como concluída.

    Args:
        lista (list): Lista de tarefas.
        indice (int): Número da tarefa apresentado ao usuário.
    """
    # Ajusta o índice para o inciar em 0
    indice -= 1

    # Verifica se o índice está dentro do intervalo válido da lista
    if 0 <= indice < len(lista):
        #print(lista)
        lista[indice]["status"] = "concluída"
        print("Tarefa marcada como concluída!")
    else:
        print("Índice inválido.")


def main():
    """Função principal do programa que exibe o menu e trata a interação com o usuário."""
    lista_tarefas = []

    while True:
        print("\n--- Menu ---")
        print("1. Adicionar tarefa")
        print("2. Listar tarefas")
        print("3. Marcar tarefa como concluída")
        print("4. Sair")

        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            descricao = input("Digite a descrição da tarefa: ")
            prioridade = int(input("Digite a prioridade (1 a 5): "))
            lista_tarefas = adicionar_tarefa(lista_tarefas, descricao, prioridade)
            print("Tarefa adicionada com sucesso!")

        elif opcao == "2":
            listar_tarefas(lista_tarefas)

        elif opcao == "3":
            listar_tarefas(lista_tarefas)
            indice = int(input("Digite o número da tarefa a concluir: "))
            concluir_tarefa(lista_tarefas, indice)

        elif opcao == "4":
            print("Saindo do programa...")
            break

        else:
            print("Opção inválida. Tente novamente.")


#if __name__ == "__main__":
main()
```



- **Uso do enumerate**

  

  ```python
  for i, tarefa in enumerate(tarefas_ordenadas, start=1):
  ```

  O `enumerate` percorre a lista e retorna **dois valores**: o índice e o elemento.

  - `i` → posição da tarefa (começando em 1 por causa do parâmetro `start=1`).
  - `tarefa` → o dicionário da tarefa. Isso permite imprimir a posição junto com os dados da tarefa, de forma organizada para o usuário.

- **Verificação de intervalo**

  ```python
  if 0 <= indice < len(lista):
  ```

  Essa condição garante que o índice fornecido pelo usuário está dentro dos limites da lista.

  - `0 <= indice` → impede índices negativos.
  - `indice < len(lista)` → impede índices maiores que o tamanho da lista. Assim, evitamos erros de acesso fora da lista.

- **Ordenação de lista de dicionários**

  ```python
  return sorted(lista, key=lambda x: x["prioridade"])
  ```

  O `sorted` cria uma nova lista ordenada.

  - `key=lambda x: x["prioridade"]` → define que a ordenação será feita pelo valor da chave `"prioridade"`. Como prioridade 1 é mais alta, as tarefas aparecem primeiro.

- **Ajuste de índice**

  ```python
  indice -= 1
  ```

  O usuário vê as tarefas numeradas a partir de 1 (mais intuitivo). Mas as listas começam no índice 0. Por isso, subtraímos 1 para alinhar o número escolhido pelo usuário com o índice real da lista.
