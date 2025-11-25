# 📚 Sistema-de-Biblioteca---UFU
Sistema simples de gerenciamento de biblioteca desenvolvido em C.

## Descrição do Projeto

Este projeto consiste em um sistema simples de gerenciamento de acervo e usuários para uma biblioteca, desenvolvido como parte dos estudos de Algoritmos e Programação 1 na Universidade Federal de Uberlândia (UFU).
O projeto focou na aplicação intensiva da **lógica computacional** para criar um sistema completo sem a utilização de estruturas de dados avançadas, como `structs` e alocação dinâmica, nem funções de biblioteca para manipulação de strings (`strcmp`, `strcpy`, etc.)
O objetivo principal foi exercitar os conhecimentos em estruturas de dados, lógica de programação e manipulação de estruturas condicionais e laços de repetição na linguagem C.

## Funcionalidades Principais

O sistema é operado via console e permite que o usuário realize as seguintes operações:

* **Cadastro de Livros:** Inclusão de novos livros com validação de campos (ID, Ano, etc.).
* **Listagem:** Visualização do acervo completo em formato de tabela ou listagem detalhada (com filtros por status Ativo/Inativo).
* **Atualização de Dados:** Modificação de Título, Autor, Ano e Status (Ativo/Inativo) de um livro específico por ID.
* **Busca:** Pesquisa de livros por **substring** no Título ou no Autor (lógica de busca implementada manualmente).
* **Estatísticas e Relatórios:** Geração de dados como média de ano, percentual de inativos e contagem por década.
* **Ordenação:** Organização do acervo por Título (ASC/DESC) e por Ano (ASC/DESC) utilizando a implementação manual do algoritmo **Bubble Sort**.

## Linguagem e Conceitos Aplicados

* **Linguagem:** C
*  **IDE/Ambiente:** Code::Blocks.
* **Estrutura de Dados:** Utilização de **Arrays Paralelos** para gerenciar os dados de cada livro (ID, Título, Autor, Ano, Status).
* **Lógica de Controle de Fluxo:** Implementação extensiva de laços (`for`, `while`, `do-while`) e estruturas condicionais (`if-else`, `switch-case`) para todo o controle do menu e das operações.
* **Manipulação Manual de Strings:** Implementação de rotinas de leitura, busca e comparação de strings sem o uso das funções padrões da biblioteca `string.h`.


