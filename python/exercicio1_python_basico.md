# Exercício Agenda
## Enunciado
Faça um programa em python para cadastro de agenda. 
O programa deve utilizar dicionários para cadastrar os contatos, usando como chaves, nome, endereço, e-mail e telefone. Os dicionários devem ser guardados em uma lista.
O menu deve oferecer as seguintes opções: 

1. Adicionar contato - deve verificar se o contato já existe antes de adicionar.
2. Editar contato - deve solicitar o nome de um contato, verificar sua existência e solicitar que o usuário entre com os dados do contato novamente, menos o nome.
3. Buscar contato - deve solicitar o nome de um contato e mostrar os dados.
4. Listar contatos - deve listar os contatos em ordem alfabética.
5. Remover contato - deve remover um contato existente.
6. Sair.   
Usar funções.

## Solução
_obs_.:  _esta é apenas uma possível solução!_

### Descrição:

 - O teste `__init__` garante que as funções não serão executadas automaticamente em caso de importação do código.
 - Na função `main`:
   - cria uma lista **agenda** com dados iniciais para facilitar os tetes.
   - chama a função `menu` que irá imprimir as opções
 - Função `menu`:
   - imprime o menu de opções.
   - solicita que o usuário escolha uma
   - quando usuário escolhe a opção, chama a função correspondente e repassa a lista de contatos chamada **agenda**.
   - caso escolha algo não previsto, mostra mensagem de erro e retorna ao menu novamente.
   - caso escolha "Sair" encerra o programa.
 - Função `buscaContato`:
   - recebe a lista de contatos **agenda** e o **nome** do contato que deve ser buscado.
   - percorre a lista comparando o **nome** (digitado) com o valor da chave 'nome' nos dicionários da lista.
   - caso encontre, retorna o dicionário com todos os dados do contato.
   - caso não encontre, retorna falso
 - Função `addContato`:
   - recebe a lista de contatos **agenda**.
   - solicita no nome do novo contato
   - chama a função `buscaContato` para verificar se já existe um contato com o nome fornecido.
   - caso o nome já esteja na agenda, exibe mensagem de erro e retorna ao menu.
   - caso não exista:
     - solicita os dados do novo contato.
     - adiciona em um novo dicionário.
     - adiciona o dicionário a lista **agenda**.
 - Função `editarContato`:
   - recebe a lista de contatos **agenda**.
   - verifica se a lista de contatos está vazia, caso esteja, exibe mensagem de erro e retorna ao menu.
   - solicita o nome do contato a ser editado.
   - chama a função `buscaContato` para verificar se já existe um contato com o nome fornecido, caso não exista, exibe mensagem de erro e retorna ao menu.
   - caso exista, obtém o índice (posição) do contato na lista.
   - solicita dos novos dados do contato.
   - adiciona em um novo dicionário.
   - substitui o dicionario anterior da lista pelo novo, usando o índice como referência.
 - Função `mostraContato`:
   - recebe a lista de contatos **agenda**.
   - verifica se a lista de contatos está vazia, caso esteja exibe mensagem de erro e retorna ao menu.
   - solicita o nome do contato a ser editado.
   - chama a função `buscaContato` para verificar se existe um contato com o nome fornecido, caso não exista, exibe mensagem de erro e retorna ao menu.
   - caso exista, imprime as informações do contato.
 - Função `listaContatos`:
   - recebe a lista de contatos **agenda**.
   - verifica se a lista de contatos está vazia, caso esteja exibe mensagem de erro e retorna ao menu.
   - caso contrário, cria uma nova lista ordenada por ordem alfabética, pela chave 'Nome' dos dicionários.
   - imprime a lista de contatos ordenada.
 - Função `removeContato`:
   - recebe a lista de contatos **agenda**.
   - verifica se a lista de contatos está vazia, caso esteja exibe mensagem de erro e retorna ao menu.
   - solicita o nome do contato a ser editado.
   - chama a função `buscaContato` para verificar se já existe um contato com o nome fornecido, caso não exista, exibe mensagem de erro e retorna ao menu.
   - caso exista, obtém o índice (posição) do contato na lista. 
   - remove o contato pelo índice.
  
### Código:

```python
# Remove um contato da agenda pelo nome
def removeContato(agenda):
    print("\n==Remove Contato==")
    # Verifica se a agenda está vazia
    if not agenda:
        print("Nem um contato cadastrado!")
    else:
        # Solicita o nome do contato a ser removido
        nome = input("Nome: ").lower().strip().title()
        # Verifica se o contato existe
        contato = buscaContato(agenda, nome)
        if contato:
            # Busca o índice do contato na lista
            index = agenda.index(contato)
            # Remove o contato se encontrado (remove pelo índice)
            agenda.pop(index)
            print(f"REMOVIDO contato: {nome}")
        else:
            print("Contato não encontrado!")

# Lista todos os contatos da agenda em ordem alfabética
def listaContatos(agenda):
    print("\n==Listar Contatos==")
    # Verifica se a agenda está vazia
    if not agenda:
        print("Nem um contato cadastrado!")
    else:
        # Ordena a lista de contatos pelo nome
        ordenada = sorted(agenda, key=lambda contato: contato['Nome'])
        # Exibe todos os contatos ordenados
        for contato in ordenada:
            print(f"Contato: {contato['Nome']} - Endereço: {contato['End']} - E-mail: {contato['Email']} - Telefone: {contato['Fone']}")

# Mostra os dados de um contato buscado pelo nome
def mostraContato(agenda):
    print("\n==Buscar Contato==")
    if not agenda:
        print("Nem um contato cadastrado!")
    else:
        # Solicita o nome do contato a ser buscado
        nome = input("Nome: ").lower().strip().title()
        # Verifica se o contato existe
        contato = buscaContato(agenda, nome)
        if contato:
            # Exibe os dados do contato encontrado
            print(f'Nome: {contato['Nome']}\nEndereço: {contato['End']}\nE-mail: {contato['Email']}\nTelefone: {contato['Fone']}')
        else:
            # Se o contato não for encontrado, exibe mensagem
            print("Contato não encontrado!")

# Edita um contato existente na agenda            
def editarConato(agenda):
    print("\n==Editar Contato==")
    # Verifica se a agenda está vazia
    if not agenda:
        print("Nem um contato cadastrado!")
    else:
        # Solicita o nome do contato a ser editado
        nome = input("Nome: ").lower().strip().title()
        # Verifica se o contato existe
        contato = buscaContato(agenda, nome)
        if contato:
            # Busca o índice do contato na lista
            index = agenda.index(contato)
                
            # Cria um novo dicionário com os dados atualizados do contato
            # Solicita os novos dados do contato (exceto o nome)
            novoContato = {
                'Nome': nome,
                'End': input("Endereço: ").lower().strip(),
                'Email': input("E-mail: ").lower().strip(),
                'Fone': input("Telefone: ").lower().strip()
            }
            # Atualiza o contato na agenda pelo índice
            agenda[index] = novoContato
        else:
            # Se o contato não for encontrado, exibe mensagem
            print("Contato não encontrado!")

# Adiciona um novo contato à agenda
def addContato(agenda):
    print("\n==Add Contato==")
    # Solicita o nome do novo contato
    nome = input("Nome: ").lower().strip().title()
    # Verifica se o contato já existe
    if not buscaContato(agenda, nome):
        # Cria um novo dicionário com os dados do contato
        contato = {
            'Nome': nome,
            'End': input("Endereço: ").lower().strip(),
            'Email': input("E-mail: ").lower().strip(),
            'Fone': input("Telefone: ").lower().strip()
        }
        # Adiciona o novo contato à agenda
        agenda.append(contato)
    else:
        print("Contato já cadastrado!")

# Busca um contato pelo nome na agenda
def buscaContato(agenda, nome):
    # Busca um contato pelo nome na agenda
    # Retorna o contato se encontrado, caso contrário retorna False
    for contato in agenda:
        if nome in contato['Nome']:
            return contato
    return False

# Menu principal do programa
def menu(agenda):
    while True:
        print("\n==Menu==")
        print("1. Adicionar contato\n2. Editar contato\n3. Buscar contato\n4. Listar contatos\n5. Remover contato\n6 .Sair")
        op = input("Opção: ")
 
        if op == '1':
            addContato(agenda)
        elif op == '2':
            editarConato(agenda)
        elif op == '3':
            mostraContato(agenda)
        elif op == '4':
            listaContatos(agenda)
        elif op == '5':
            removeContato(agenda)
        elif op == '6':
            print("Saindo...")
            break
        else:
            print("Opção inválida!")

def main():
    # Lista inicial de contatos cadastrados para testes
    agenda = [
        {'Nome': 'Alberto', 'End': 'Santa Maria', 'Email': 'diego@ual.com', 'Fone': '954216502'},
        {'Nome': 'Larissa', 'End': 'Asa Norte', 'Email': 'larissa@exemplo.com', 'Fone': '981234567'},
        {'Nome': 'Carlos', 'End': 'Taguatinga', 'Email': 'carlos@exemplo.com', 'Fone': '992345678'},
        {'Nome': 'Fernanda', 'End': 'Guará', 'Email': 'fernanda@exemplo.com', 'Fone': '993456789'},
        {'Nome': 'Ariel', 'End': 'Guará', 'Email': 'fernanda@exemplo.com', 'Fone': '993456789'},
        {'Nome': 'João', 'End': 'Plano Piloto', 'Email': 'joao@exemplo.com', 'Fone': '994567890'}
    
    ]
    # Inicia o menu 
    menu(agenda)

if __name__ == "__main__":
    main()



