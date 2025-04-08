import sqlite3 as sql

def conectar (): # Cria ou Conecta ao Banco de dados
    return sql.connect('estoque.db')

# Criando a Tabela Produtos
def criarTabela():
    conexao = conectar()
    cursor = conexao.cursor()  # Cia um cursor de execução SQL
    cursor.execute('''
    CREATE TABLE IF NOT EXISTS Produtos (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        nome TEXT NOT NULL,
        preco REAL NOT NULL
    )
    ''')

# Inserindo Dados
def inserirDados():
    conexao = conectar()
    cursor = conexao.cursor()

    while True:
        nome = input('Digite o nome do produto: ')
        try:
            preco = float(input("Digite o preço do produto: R$ "))
        except ValueError:
            print('Preço inválido! Tente novamente.')
            continue

        cursor.execute('INSERT INTO Produtos (nome, preco) VALUES (?, ?)', (nome, preco))
        conexao.commit()  # Confirmando alterações

        continuar = input('Deseja adicionar outro produto? (s/n): ').lower()
        if continuar != 's':
            break

    conexao.close() #Fechando conexão

def atualizarPreco ():
    conexao = conectar()
    cursor = conexao.cursor()

    while True:
        id = int(input('Digite o id do protudo: '))
        try: preco = float(input('Digite o novo preço do produto: R$ '))
        except ValueError:
            print('Preço inválido! Tente novamente.')
            continue

        cursor.execute('UPDATE Produtos SET preco = ? WHERE id = ?', (preco, id))
        conexao.commit()

        continuar = input('Deseja atualizar outro produto? (s/n): ').lower()
        if continuar != 's':
            break

    conexao.close()

def deletarProdutos():
    conexao = conectar()
    cursor = conexao.cursor()
    while True:
        try:
            id_produto = int(input("Digite o ID do produto que deseja deletar: "))
            cursor.execute('DELETE FROM Produtos WHERE id = ?', (id_produto,))
            conexao.commit()

            if cursor.rowcount == 0:
                print(f"Nenhum produto encontrado com ID {id_produto}.")
            else:
                print(f"Produto com ID {id_produto} foi deletado com sucesso.")
        except ValueError:
            print("ID inválido! Digite um número inteiro.")

        continuar = input("Deseja deletar outro produto? (s/n): ").lower()
        if continuar != 's':
            break

    conexao.close()

def listarProdutos():
    conexao = conectar()
    cursor = conexao.cursor()
    cursor.execute('SELECT * FROM Produtos')
    produtos = cursor.fetchall()
    for produto in produtos:
        print(produto)
    conexao.close()

def filtrarProdutos():
    conexao = conectar()
    cursor = conexao.cursor()

    termo = input('Digite o produto: ')
    cursor.execute('SELECT * FROM Produtos WHERE nome LIKE ?',('%' + termo + '%',))
    produtos = cursor.fetchall()

    if produtos:
        for produto in produtos:
            print(f'ID: {produto[0]}| Nome: {produto[1]}| Preço: {produto[2]:.2f}')
    else:
        print('Nenhum produto encontrado')
    conexao.close()

def menu():
    criarTabela()
    while True:
        print("\n1 - Inserir Produtos")
        print("2 - Listar Produtos")
        print("3 - Filtrar Produtos")
        print("4 - Atualizar Preço")
        print("5 - Deletar Produtos")
        print("0 - Sair")

        opcao = input("Escolha uma opção: ")
        if opcao == '1':
            inserirDados()
        elif opcao == '2':
            listarProdutos()
        elif opcao == '3':
            filtrarProdutos()
        elif opcao == '4':
            atualizarPreco()
        elif opcao == '5':
            deletarProdutos()
        elif opcao == '0':
            break
        else:
            print("Opção inválida!")

if __name__ == '__main__':
    menu()
