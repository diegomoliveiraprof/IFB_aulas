# Estruturas de dados e funções

## Exercício

**Criar um programa que gerencia uma lista de tarefas**. 
O programa deve:

* Permitir que o usuário adicione tarefas. Cada tarefa deve ter: 
  * Descrição (string), 
  * Prioridade (inteiro de 1 a 5, onde 1 é a prioridade mais alta) e 
  * Status (inicialmente “pendente”);
* Armazenar cada tarefa como um dicionário com as chaves "descrição", "prioridade" e "status";
* Manter todas as tarefas numa lista;
* Criar funções para: 
  * Adicionar tarefas, 
  * Mostrar todas as tarefas ordenadas por prioridade (da maior para a menor) e 
  * Marcar uma tarefa como concluída (alterar o status para “concluída”);
* Criar uma função `main()` que permita ao usuário escolher opções no menu para: 
  * Adicionar tarefa, Listar tarefas, Marcar tarefa como concluída e Sair do programa.



### Solução 1  - simplificada

```python
def add_tarefas(tarefas):
  # Mostra o cabeçalho para adicionar uma nova tarefa
  print("\n==Adicionar Tarefa==")

  # Cria um dicionário para armazenar as informações da tarefa
  dic_tarefa = {}
  dic_tarefa["Descricao"] = input("Descrição: ")

  # Converte a prioridade para inteiro para permitir ordenação
  dic_tarefa["Prioridade"] = int(input("Prioridade [1 à 5]: "))

  # Todas as tarefas começam com status pendente
  dic_tarefa["Status"] = "Pendente"

  # Adiciona o dicionário à lista de tarefas
  tarefas.append(dic_tarefa)
  print("\nTarefa adicionada!")

def listar_tarefas(tarefas):
  # Verifica se existem tarefas cadastradas
  if len(tarefas) >= 1:
    # Ordena a lista temporária por prioridade (menor valor = mais urgente)
    temp = sorted(tarefas, key=lambda x: x["Prioridade"])

    # Mostra cada tarefa com seu número e informações
    for indice, item in enumerate(temp, start=1):
      print("=" * 100)
      print(f" {indice}-Tarefa ======")

      for chave, valor in item.items():
        print(f"{chave} = {valor}")
  else:
    # Mensagem exibida quando não há tarefas
    print("Não existem tarefas")

def concluir_tarefa(tarefas):
  # Pede ao usuário o número da tarefa a ser concluída
  indice = int(input("\nNumero da tarefa: "))

  # Verifica se o número informado é válido
  if 1 <= indice <= len(tarefas):
    # Usa índice -1 porque a lista começa em 0
    tarefa = tarefas[indice - 1]
    tarefa["Status"] = "Concluida"

    # Informa ao usuário o status atualizado da tarefa selecionada
    print(f"\nDescrição: {tarefa['Descricao']} - Status atual: {tarefa['Status']}")
  else:
    print("Tarefa não cadastrada")



def menu():
  # Exibe as opções do menu principal
  print("=" * 100)
  print("\n1-Adiconar tarefas \n2-Mostrar tarefas \n3-Marcar concluida \n4-Sair\n")


def main():
  # Lista que guarda as tarefas durante a execução do programa
  tarefas = []

  while True:
    menu()
    op = input("Escolha uma opção: ")
    match op:
      case "1":
        add_tarefas(tarefas)
      case "2":
        listar_tarefas(tarefas)
      case "3":
        concluir_tarefa(tarefas)
      case "4":
        print("Saindo!")
        break
      case _:
        print("\nOpção inválida")


# Executa o programa chamando a função principal
main()
```



### Solução 2 - mais elaborada



```python
def add_tarefa():
    # Solicita a descrição da nova tarefa ao usuário
    desc = input("Criando nova tarefa\nDescrição: ")
    tarefa={}
    status = "Pendente"
    tarefa["desc"]= desc
    tarefa["status"]=status

    # Define a prioridade da tarefa chamando a função set_prioridade
    tarefa["prioridade"] = set_prioridade(tarefa)
    return tarefa

def mostrar_tarefas(lista_tarefas):
    # Verifica se a lista de tarefas está vazia
    if len(lista_tarefas) == 0:
        print("\nNenhuma tarefa cadastrada.")
        return
    print("\nLista de tarefas:")

    # Itera sobre a lista de tarefas para exibi-las, começando a contagem do índice em 1
    for i, tarefa in enumerate(lista_tarefas, start=1):
        print(f"{i}. Descrição: {tarefa['desc']} - Prioridade: {tarefa['prioridade']} - Status: {tarefa['status']}")

def set_prioridade(tarefa):
    # Solicita um valor de prioridade ao usuário (de 1 a 5)
    print("Digite um valor de prioridade de 1 a 5:")
    valor = int(input("Prioridade: "))
    
    # Valida o valor da prioridade. Se for inválido, define como 5 (padrão)
    if not (1<= valor <= 5):
      print("\nValor inválido!\nPrioridade definida por padrão com 5.")
      valor = 5
    return valor

def altera_status(lista_tarefas):
    # Verifica se há tarefas para alterar o status
    if len(lista_tarefas) == 0:
        print("\nNenhuma tarefa para alterar o status.")
        return
    # Mostra a lista de tarefas para que o usuário possa escolher
    mostrar_tarefas(lista_tarefas)
    
    # Solicita o número da tarefa e ajusta o índice (lista começa em 0)
    indice = int(input("Digite o número da tarefa que deseja alterar o status: ")) - 1
   
	# Verifica se o índice é válido
    if 0 <= indice < len(lista_tarefas):
        # Chama a função set_status para alterar o status da tarefa específica
        lista_tarefas[indice] = set_status(lista_tarefas[indice])
    else:
        print("Índice inválido.")

def set_status(tarefa):
    # Exibe as opções de status disponíveis
    print("Possíveis status:\n\t1. Pendente\n\t2. Concluida")
    
    # Solicita a escolha do usuário
    valor = int(input("Escolha um status: "))
    
    # Atualiza o status da tarefa com base na escolha do usuário
    if valor == 1:
        tarefa["status"] = "Pendente"
    elif valor == 2:
        tarefa["status"] = "Concluida"
    else:
        print("Valor inválido")
    return tarefa

def menu(lista_tarefas):
    # Exibe o menu principal do gerenciador de tarefas
    print("\nBem vindo ao gerênciador de tarefas: ")
    print("\nOpções: ")
    print("\t1. Adicionar tarefa")
    print("\t2. Alterar status de tarefa")
    print("\t3. Listar tarefas")
    print("\t4. Sair")
    op = input("Escolha uma opção: ")

    # Utiliza o comando match-case para lidar com as opções do menu
    match op:
      case "1":
        # Adiciona uma nova tarefa e a insere na lista
        lista_tarefas.append(add_tarefa())
        # Ordena a lista de tarefas por prioridade
        lista_tarefas.sort(key=lambda x: x['prioridade'])

      case "2":
        # Chama a função para alterar o status de uma tarefa
        altera_status(lista_tarefas)

      case "3":
        # Chama a função para mostrar todas as tarefas
        mostrar_tarefas(lista_tarefas)

      case "4":
        print("Saindo...")
        return False # Retorna False para indicar que o programa deve sair
      case _:
        print("\nOpção inválida")

    return True # Retorna True para continuar o loop do menu

def main():
    # Inicializa uma lista vazia para armazenar as tarefas
    lista_tarefas = []

    # Loop principal que mantém o menu em execução até o usuário escolher sair
    while True:
      if not menu(lista_tarefas):
        break

# Garante que a função main() seja chamada apenas quando o script for executado diretamente
if __name__ == "__main__":

    main()

```

