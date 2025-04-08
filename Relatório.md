# Integrantes:

* Gabriel Marques Da Silva Barros - 202402399764
* Letícia Valença Timótio - 202402534351
* Thiago Matias Rodrigues - 202403475171

Este programa foi desenvolvido em Python e utiliza o banco de dados SQLite, devida sua praticidade e por ser completa para o objetivo, com a finalidade de realizar operações de CRUD (Create, Read, Update, Delete) em uma tabela de produtos. Este programa é útil para praticar operações com banco de dados em Python de forma simples e funcional.

## 1. Conectar ao banco de dados:

* A função `conectar()` conecta ao banco chamado `estoque.db`. Se o banco não existir, ele é criado automaticamente.

## 2. Criar tabela:

* A função `criarTabela()` cria a tabela `Produtos` com as colunas: `id` (chave primária), `nome` (texto), e `preco` (número real). A tabela só será criada se ainda não existir.

## 3. Inserir dados:

* A função `inserirDados()` solicita ao usuário que digite o nome e o preço de um produto.
* Os dados são inseridos usando comandos SQL com placeholders (?) para evitar SQL Injection.
* O loop permite inserir vários produtos até o usuário digitar `'n'`.

## 4. Atualizar preço:

* A função `atualizarPreco()` permite que o usuário atualize o preço de um produto existente, informando o ID do produto e o novo valor.

## 5. Deletar produtos:

* A função `deletarProdutos()` pede ao usuário o ID do produto a ser excluído.
* Após excluir, informa se a operação teve sucesso ou se nenhum produto foi encontrado com aquele ID.

## 6. Listar Produtos

## Menu de Opções:

Imagens:

![1](https://github.com/user-attachments/assets/320f5d0a-408e-4fdd-9b85-ab5865efe2b0)

![2](https://github.com/user-attachments/assets/c890dedf-95e9-44f1-ac61-67f8de3107a9)

![3](https://github.com/user-attachments/assets/dd00fe89-00cf-4b7e-918c-aba88346b019)

![4](https://github.com/user-attachments/assets/ac310b90-6d82-44e7-a778-1dc65ff8c0cb)

![5](https://github.com/user-attachments/assets/65b2275b-b7dd-49d5-9ee6-7cbccf06c9e3)
