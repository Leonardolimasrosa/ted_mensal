# ted_mensal

#include <stdio.h>
#include <stdlib.h>

typedef struct {
    void **dados;      // Ponteiro genérico para os elementos da fila
    int inicio;        // Índice do primeiro elemento
    int fim;           // Índice do último elemento
    int tamanho;       // Capacidade atual da fila
    int capacidade;    // Capacidade total da fila
} Fila;

// Função para criar a fila
Fila* criarFila(int capacidadeInicial) {
    Fila *fila = (Fila *) malloc(sizeof(Fila));
    if (fila == NULL) return NULL;  // Verifica se a alocação foi bem-sucedida

    fila->dados = (void **) malloc(sizeof(void*) * capacidadeInicial);
    fila->inicio = 0;
    fila->fim = -1;
    fila->tamanho = 0;
    fila->capacidade = capacidadeInicial;

    return fila;
}

// Função para limpar e liberar a fila
void limparFila(Fila *fila) {
    if (fila != NULL) {
        free(fila->dados);  // Libera a memória alocada para os dados
        free(fila);         // Libera a memória da estrutura da fila
    }
}

void dobrarCapacidade(Fila *fila){
    fila->capacidade = fila->capacidade * 2 ;
    fila->
}

void inserirNaFila(Fila *fila, void *elemento) {
    if (fila->tamanho == fila->capacidade) {
        dobrarCapacidade(fila);
    }
    fila->fim = (fila->fim + 1) % fila->capacidade;
    fila->dados[fila->fim] = elemento;
    fila->tamanho++;
}

void removerDaFila(Fila *fila){
    if(fila->){
        return NULL;
    }
    fila->inicio = fila->inicio - 1;
    fila->dados[fila->inicio];
}

