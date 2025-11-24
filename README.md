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

#include <stdio.h>
#include <stdlib.h>
#include <string.h<

int main()
{
  
    int id[300];
    int ano[300];
    int status[300];
    char titulo[300][100];
    char autor[300][100];

    int opcao, qtdId = 0;
    char confirmacao;

    do
    {
        printf("\nMenu:\n");
        printf("1 - Cadastrar.\n");
        printf("2 - Listar por tabela\n");
        printf("3 - Listar separado\n");
        printf("4 - Buscar\n");
        printf("5 - Atualizar livro\n");
        printf("6 - Ativar/Inativar\n");
        printf("7 - Relatorios/Estatisticas\n");
        printf("8 - Ordenar\n");
        printf("0 - Sair.\n");
        printf("Opcao escolhida: ");
        scanf("%d", &opcao);
        while(getchar() != '\n');

        switch(opcao)
        {
            case 1: 
                {
                    if (qtdId < 300) {
                        int duplicado;

                        do {
                            printf("\nDigite o ID: ");
                            scanf("%d", &id[qtdId]);
                            while(getchar() != '\n');
                            
                            duplicado = 0;
                            if (id[qtdId] > 0) {
                                for (int i = 0; i < qtdId; i++) {
                                    if (id[qtdId] == id[i]) {
                                        duplicado = 1;
                                    }
                                }
                                if (duplicado) {
                                    printf("ID ja existente! Digite outro.\n");
                                }
                            } else {
                                printf("ID invalido. O ID deve ser um numero maior que 0.\n");
                            }
                        } while (id[qtdId] <= 0 || duplicado);

                        do {
                            printf("Insira o titulo: ");
                            fgets(titulo[qtdId], 100, stdin);
                            int i = 0;
                            while(titulo[qtdId][i] != '\n' && titulo[qtdId][i] != '\0') {
                                i++;
                            }
                            if (titulo[qtdId][i] == '\n') {
                                titulo[qtdId][i] = '\0';
                            }

                            int vazio = 1;
                            for(int j = 0; titulo[qtdId][j] != '\0'; j++) {
                                if (titulo[qtdId][j] != ' ' && titulo[qtdId][j] != '\t') {
                                    vazio = 0;
                                }
                            }
                            
                            if (vazio) {
                                printf("Titulo nao pode ser vazio. Tente novamente.\n");
                            }
                        } while (titulo[qtdId][0] == '\0');

                        do {
                            printf("Insira o autor: ");
                            fgets(autor[qtdId], 100, stdin);
                            int i = 0;
                            while(autor[qtdId][i] != '\n' && autor[qtdId][i] != '\0') {
                                i++;
                            }
                            if (autor[qtdId][i] == '\n') {
                                autor[qtdId][i] = '\0';
                            }

                            int vazio = 1;
                            for(int j = 0; autor[qtdId][j] != '\0'; j++) {
                                if (autor[qtdId][j] != ' ' && autor[qtdId][j] != '\t') {
                                    vazio = 0;
                                }
                            }
                            
                            if (vazio) {
                                printf("Autor nao pode ser vazio. Tente novamente.\n");
                            }
                        } while (autor[qtdId][0] == '\0');
                        
                        do {
                            printf("Insira o ano (entre 1500 e 2025): ");
                            scanf("%d", &ano[qtdId]);
                            while(getchar() != '\n');
                            if (ano[qtdId] < 1500 || ano[qtdId] > 2025) {
                                printf("Ano invalido. O ano deve estar entre 1500 e 2025.\n");
                            }
                        } while (ano[qtdId] < 1500 || ano[qtdId] > 2025);

                        status[qtdId] = 1;
                        qtdId++;
                        printf("\nLivro cadastrado com sucesso!\n");
                    } else {
                        printf("\nAcervo de livros cheio. Nao e possivel cadastrar mais.\n");
                    }
                }
                break;

            case 2:
                if (qtdId == 0) {
                    printf("\nNenhum livro cadastrado.\n");
                } else {
                    printf("\n--- Livros Cadastrados ---\n");
                    printf("ID | Titulo | Autor | Ano | Status\n");
                    printf("----------------------------------\n");
                    for(int i = 0; i < qtdId; i++) {
                        printf("%d | %s | %s | %d | %s\n", id[i], titulo[i], autor[i], ano[i], status[i] == 1 ? "Ativo" : "Inativo");
                    }
                    printf("----------------------------------\n");
                }
                break;

            case 3: 
                if (qtdId == 0) {
                    printf("\nNenhum livro cadastrado.\n");
                } else {
                    int escolha;
                    printf("\n--- Submenu de Listagem ---\n");
                    printf("0 - Listar todos\n");
                    printf("1 - Listar apenas ativos\n");
                    printf("2 - Listar apenas inativos\n");
                    printf("Opcao selecionada: ");
                    scanf("%d", &escolha);
                    while(getchar() != '\n');

                    int livros_encontrados = 0;
                    for(int i = 0; i < qtdId; i++) {
                        if (escolha == 0) { 
                            printf("\nID: %d | Titulo: %s | Autor: %s | Ano: %d | Status: %s\n", id[i], titulo[i], autor[i], ano[i], status[i] == 1 ? "Ativo" : "Inativo");
                            livros_encontrados = 1;
                        } else if (escolha == 1 && status[i] == 1) { // Listar apenas ativos
                            printf("\nID: %d | Titulo: %s | Autor: %s | Ano: %d | Status: Ativo\n", id[i], titulo[i], autor[i], ano[i]);
                            livros_encontrados = 1;
                        } else if (escolha == 2 && status[i] == 0) { // Listar apenas inativos
                            printf("\nID: %d | Titulo: %s | Autor: %s | Ano: %d | Status: Inativo\n", id[i], titulo[i], autor[i], ano[i]);
                            livros_encontrados = 1;
                        }
                    }
                    if (!livros_encontrados && escolha != 0) {
                        printf("\nNenhum livro encontrado para o criterio selecionado.\n");
                    }
                }
                break;

            case 4: 
                {
                    if (qtdId == 0) {
                        printf("\nNenhum livro para buscar.\n");
                    } else {
                        int buscaOpcao;
                        char termoBusca[100];
                        int encontrado = 0;

                        printf("\n--- Buscar Livro ---\n");
                        printf("1 - Buscar por Titulo\n");
                        printf("2 - Buscar por Autor\n");
                        printf("Opcao: ");
                        scanf("%d", &buscaOpcao);
                        while(getchar() != '\n');

                        printf("Digite o termo de busca: ");
                        fgets(termoBusca, 100, stdin);
                        
                        int i = 0;
                        while(termoBusca[i] != '\n' && termoBusca[i] != '\0') {
                            i++;
                        }
                        if (termoBusca[i] == '\n') {
                            termoBusca[i] = '\0';
                        }
                        
                        for (int i = 0; i < qtdId; i++) {
                            int j, k, match;
                            if (buscaOpcao == 1) { 
                                match = 0;
                                for (j = 0; titulo[i][j] != '\0'; j++) {
                                    if (titulo[i][j] == termoBusca[0]) {
                                        match = 1;
                                        for (k = 0; termoBusca[k] != '\0'; k++) {
                                            if (titulo[i][j+k] == '\0' || titulo[i][j+k] != termoBusca[k]) {
                                                match = 0;
                                                k = 100; 
                                            }
                                        }
                                        if (match) {
                                            j = 100; 
                                        }
                                    }
                                }
                                if (match) {
                                    printf("\nEncontrado: ID %d | Titulo: %s | Autor: %s | Ano: %d | Status: %s\n", id[i], titulo[i], autor[i], ano[i], status[i] == 1 ? "Ativo" : "Inativo");
                                    encontrado = 1;
                                }
                            } else if (buscaOpcao == 2) { 
                                match = 0;
                                for (j = 0; autor[i][j] != '\0'; j++) {
                                    if (autor[i][j] == termoBusca[0]) {
                                        match = 1;
                                        for (k = 0; termoBusca[k] != '\0'; k++) {
                                            if (autor[i][j+k] == '\0' || autor[i][j+k] != termoBusca[k]) {
                                                match = 0;
                                                k = 100; 
                                            }
                                        }
                                        if (match) {
                                            j = 100; 
                                        }
                                    }
                                }
                                if (match) {
                                    printf("\nEncontrado: ID %d | Titulo: %s | Autor: %s | Ano: %d | Status: %s\n", id[i], titulo[i], autor[i], ano[i], status[i] == 1 ? "Ativo" : "Inativo");
                                    encontrado = 1;
                                }
                            }
                        }
                        if (!encontrado) {
                            printf("\nNenhum livro encontrado com o termo de busca.\n");
                        }
                    }
                }
                break;

            case 5:
                {
                    if (qtdId == 0) {
                        printf("\nNenhum livro para atualizar.\n");
                    } else {
                        int idBusca, livroIndex = -1, i;
                        printf("Digite o ID do livro para atualizar: ");
                        scanf("%d", &idBusca);
                        while(getchar() != '\n');
                        for (i = 0; i < qtdId; i++) {
                            if (id[i] == idBusca) {
                                livroIndex = i;
                            }
                        }

                        if (livroIndex == -1) {
                            printf("\nID nao encontrado. Operacao cancelada.\n");
                        } else {
                            int updateOpcao;
                            printf("\nLivro encontrado: %s - %s\n", titulo[livroIndex], autor[livroIndex]);
                            printf("O que deseja atualizar?\n");
                            printf("1 - Titulo\n");
                            printf("2 - Autor\n");
                            printf("3 - Ano\n");
                            printf("4 - Status\n");
                            printf("Opcao: ");
                            scanf("%d", &updateOpcao);
                            while(getchar() != '\n');

                            if (updateOpcao == 1) {
                                printf("Novo titulo: ");
                                fgets(titulo[livroIndex], 100, stdin);
                                int j = 0;
                                while(titulo[livroIndex][j] != '\n' && titulo[livroIndex][j] != '\0') {
                                    j++;
                                }
                                if (titulo[livroIndex][j] == '\n') {
                                    titulo[livroIndex][j] = '\0';
                                }
                                printf("Titulo atualizado com sucesso.\n");
                            } else if (updateOpcao == 2) {
                                printf("Novo autor: ");
                                fgets(autor[livroIndex], 100, stdin);
                                int j = 0;
                                while(autor[livroIndex][j] != '\n' && autor[livroIndex][j] != '\0') {
                                    j++;
                                }
                                if (autor[livroIndex][j] == '\n') {
                                    autor[livroIndex][j] = '\0';
                                }
                                printf("Autor atualizado com sucesso.\n");
                            } else if (updateOpcao == 3) {
                                int novoAno;
                                do {
                                    printf("Novo ano (1500-2025): ");
                                    scanf("%d", &novoAno);
                                    while(getchar() != '\n');
                                    if (novoAno < 1500 || novoAno > 2025) {
                                        printf("Ano invalido. O ano deve estar entre 1500 e 2025.\n");
                                    }
                                } while (novoAno < 1500 || novoAno > 2025);
                                ano[livroIndex] = novoAno;
                                printf("Ano atualizado com sucesso.\n");
                            } else if (updateOpcao == 4) {
                                status[livroIndex] = (status[livroIndex] == 1) ? 0 : 1;
                                printf("Status do livro alterado para %s.\n", status[livroIndex] == 1 ? "Ativo" : "Inativo");
                            } else {
                                printf("Opcao invalida.\n");
                            }
                        }
                    }
                }
                break;

            case 6: 
                {
                    if (qtdId == 0) {
                        printf("\nNenhum livro para alterar o status.\n");
                    } else {
                        int idBusca, livroIndex = -1, i;
                        printf("Digite o ID do livro para alterar o status: ");
                        scanf("%d", &idBusca);
                        while(getchar() != '\n');

                        for (i = 0; i < qtdId; i++) {
                            if (id[i] == idBusca) {
                                livroIndex = i;
                            }
                        }

                        if (livroIndex == -1) {
                            printf("\nID nao encontrado.\n");
                        } else {
                            status[livroIndex] = (status[livroIndex] == 1) ? 0 : 1;
                            printf("Status do livro alterado para %s.\n", status[livroIndex] == 1 ? "Ativo" : "Inativo");
                        }
                    }
                }
                break;

            case 7:
                {
                    if (qtdId == 0) {
                        printf("\nNenhum livro para gerar relatorios.\n");
                    } else {
                        int ativos = 0, inativos = 0, anoMaisAntigo = 9999, anoMaisRecente = 0;
                        double somaAnos = 0;
                        int decadas[100] = {0};

                        for (int i = 0; i < qtdId; i++) {
                            if (status[i] == 1) {
                                ativos++;
                                if (ano[i] < anoMaisAntigo) anoMaisAntigo = ano[i];
                                if (ano[i] > anoMaisRecente) anoMaisRecente = ano[i];
                                somaAnos += ano[i];
                                if (ano[i] >= 1500 && ano[i] <= 2025) {
                                    decadas[(ano[i] - 1500) / 10]++;
                                }
                            } else {
                                inativos++;
                            }
                        }

                        printf("\n--- Relatorios e Estatisticas ---\n");
                        printf("Quantidade de livros ativos: %d\n", ativos);
                        printf("Quantidade de livros inativos: %d\n", inativos);
                        
                        if (ativos > 0) {
                            printf("Ano mais antigo (ativos): %d\n", anoMaisAntigo);
                            printf("Ano mais recente (ativos): %d\n", anoMaisRecente);
                            printf("Media dos anos (ativos): %.1f\n", somaAnos / ativos);
                        } else {
                            printf("Ano mais antigo (ativos): N/A\n");
                            printf("Ano mais recente (ativos): N/A\n");
                            printf("Media dos anos (ativos): N/A\n");
                        }
                        
                        if (qtdId > 0) {
                            printf("Percentual de inativos: %.2f%%\n", (float)inativos / qtdId * 100);
                        }
                       
                        printf("\nContagem de livros por decada (ativos):\n");
                        for (int i = 0; i < 100; i++) {
                            if (decadas[i] > 0) {
                                printf("Decada %d-%d: %d livros\n", 1500 + i*10, 1500 + i*10 + 9, decadas[i]);
                            }
                        }
                    }
                }
                break;
                {
                    if (qtdId <= 1) {
                        printf("\nHa menos de 2 livros para ordenar.\n");
                    } else {
                        int ordenacaoOpcao;
                        printf("\n--- Ordenar Livros ---\n");
                        printf("1 - Por Titulo (ASC)\n");
                        printf("2 - Por Titulo (DESC)\n");
                        printf("3 - Por Ano (ASC)\n");
                        printf("4 - Por Ano (DESC)\n");
                        printf("Opcao: ");
                        scanf("%d", &ordenacaoOpcao);
                        while(getchar() != '\n');
                        for (int i = 0; i < qtdId - 1; i++) {
                            for (int j = 0; j < qtdId - i - 1; j++) {
                                int trocar = 0;
                                if (ordenacaoOpcao == 1) {
                                    int k = 0;
                                    while(titulo[j][k] != '\0' && titulo[j+1][k] != '\0' && titulo[j][k] == titulo[j+1][k]) {
                                        k++;
                                    }
                                    if (titulo[j][k] > titulo[j+1][k]) trocar = 1;
                                }
                                else if (ordenacaoOpcao == 2) {
                                    int k = 0;
                                    while(titulo[j][k] != '\0' && titulo[j+1][k] != '\0' && titulo[j][k] == titulo[j+1][k]) {
                                        k++;
                                    }
                                    if (titulo[j][k] < titulo[j+1][k]) trocar = 1;
                                }
                                else if (ordenacaoOpcao == 3) {
                                    if (ano[j] > ano[j+1]) trocar = 1;
                                } else if (ordenacaoOpcao == 4) {
                                    if (ano[j] < ano[j+1]) trocar = 1;
                                }

                                if (trocar) {
                                    int tempId = id[j]; id[j] = id[j+1]; id[j+1] = tempId;
                                    int tempAno = ano[j]; ano[j] = ano[j+1]; ano[j+1] = tempAno;
                                    int tempStatus = status[j]; status[j] = status[j+1]; status[j+1] = tempStatus;
                                    
                                    char tempTitulo[100];
                                    int k = 0;
                                    while(titulo[j][k] != '\0') {
                                        tempTitulo[k] = titulo[j][k];
                                        k++;
                                    }
                                    tempTitulo[k] = '\0';
                                    k = 0;
                                    while(titulo[j+1][k] != '\0') {
                                        titulo[j][k] = titulo[j+1][k];
                                        k++;
                                    }
                                    titulo[j][k] = '\0';
                                    k = 0;
                                    while(tempTitulo[k] != '\0') {
                                        titulo[j+1][k] = tempTitulo[k];
                                        k++;
                                    }
                                    titulo[j+1][k] = '\0';

                                    char tempAutor[100];
                                    k = 0;
                                    while(autor[j][k] != '\0') {
                                        tempAutor[k] = autor[j][k];
                                        k++;
                                    }
                                    tempAutor[k] = '\0';
                                    k = 0;
                                    while(autor[j+1][k] != '\0') {
                                        autor[j][k] = autor[j+1][k];
                                        k++;
                                    }
                                    autor[j][k] = '\0';
                                    k = 0;
                                    while(tempAutor[k] != '\0') {
                                        autor[j+1][k] = tempAutor[k];
                                        k++;
                                    }
                                    autor[j+1][k] = '\0';
                                }
                            }
                        }
                        printf("Acervo ordenado com sucesso!\n");
                        printf("\n--- Lista ordenada ---\n");
                        printf("ID | Titulo | Autor | Ano | Status\n");
                        for(int i = 0; i < qtdId; i++) {
                            printf("%d | %s | %s | %d | %s\n", id[i], titulo[i], autor[i], ano[i], status[i] == 1 ? "Ativo" : "Inativo");
                        }
                    }
                }
                break;

            case 0:
                printf("Tem certeza que deseja sair? (S/N): ");
                scanf(" %c", &confirmacao);
                if (confirmacao != 'S' && confirmacao != 's') {
                    opcao = -1;
                }
                break;
            
            default:
                printf("\nOpcao invalida. Por favor, tente novamente.\n");
        }
    } while(opcao != 0);

    return 0;
}


