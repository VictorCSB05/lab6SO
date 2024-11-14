// Os resultados estão no final do arquivo.
#include <stdio.h>
#include <stdlib.h>

struct reg {
    int conteudo;
    struct reg *prox;
};
typedef struct reg celula;

void imprimirLista(celula *inicio) {
    celula *atual = inicio;
    while (atual != NULL) {
        printf("%d -> ", atual->conteudo);
        atual = atual->prox;
    }
    printf("NULL\n");
}

void liberarLista(celula *inicio) {
    celula *atual = inicio;
    celula *temp;
    while (atual != NULL) {
        temp = atual;
        atual = atual->prox;
        free(temp);  
    }
}
int main() {
    // Criando três instâncias da estrutura celula
    celula *c1 = (celula *)malloc(sizeof(celula));
    celula *c2 = (celula *)malloc(sizeof(celula));
    celula *c3 = (celula *)malloc(sizeof(celula));

    if (c1 == NULL || c2 == NULL || c3 == NULL) {
        printf("Erro ao alocar memória.\n");
        return 1;
    }

    c1->conteudo = 10;
    c1->prox = c2;
    c2->conteudo = 20;
    c2->prox = c3;
    c3->conteudo = 30;
    c3->prox = NULL;

    printf("Valores da lista encadeada:\n");
    imprimirLista(c1);

    printf("Memória usada por cada célula: %zu bytes\n", sizeof(celula));

    liberarLista(c1);
    printf("Memória liberada com sucesso.\n");

    return 0;
}


execução: 
Valores da lista encadeada:
10 -> 20 -> 30 -> NULL
Memória usada por cada célula: 16 bytes
Memória liberada com sucesso.
