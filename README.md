#include <stdio.h>
#include <stdlib.h>

typedef struct {
    void **dados;      // Ponteiro genérico para os elementos da fila
    int inicio;        // Índice do primeiro elemento
    int fim;           // Índice do último elemento
    int tamanho;       // Número atual de elementos na fila
    int capacidade;    // Capacidade total da fila
} Fila;

// Função para criar a fila
Fila* criarFila(int capacidadeInicial) {
    Fila *fila = (Fila *) malloc(sizeof(Fila));
    if (fila == NULL) return NULL; // Verifica se a alocação foi bem-sucedida

    fila->dados = (void **) malloc(sizeof(void *) * capacidadeInicial);
    if (fila->dados == NULL) {
        free(fila);
        return NULL;
    }

    fila->inicio = 0;
    fila->fim = -1;
    fila->tamanho = 0;
    fila->capacidade = capacidadeInicial;

    return fila;
}

// Função para dobrar a capacidade da fila
void dobrarCapacidade(Fila *fila) {
    int novaCapacidade = fila->capacidade * 2;
    void *novosDados = (void *) realloc(fila->dados, sizeof(void *) * novaCapacidade);
    if (novosDados == NULL) return;

    fila->dados = novosDados;
    fila->capacidade = novaCapacidade;
}

// Função para inserir um elemento na fila
void inserirNaFila(Fila *fila, void *elemento) {
    if (fila->tamanho == fila->capacidade) {
        dobrarCapacidade(fila);
    }
    fila->fim = (fila->fim + 1) % fila->capacidade;
    fila->dados[fila->fim] = elemento;
    fila->tamanho++;
}

// Função para remover um elemento da fila
void* removerDaFila(Fila *fila) {
    if (fila->tamanho == 0) return NULL; 

    void *elementoRemovido = fila->dados[fila->inicio];
    fila->inicio = (fila->inicio + 1) % fila->capacidade;
    fila->tamanho--;

    return elementoRemovido;
}

// Função para limpar e liberar a fila
void limparFila(Fila *fila) {
    if (fila != NULL) {
        free(fila->dados); 
        free(fila);        
    }
}

int main() {
    Fila *fila = criarFila(2); 
    int a = 10, b = 20, c = 30;

    inserirNaFila(fila, &a);
    inserirNaFila(fila, &b);
    inserirNaFila(fila, &c); 

    printf("Removido: %d\n", *(int *)removerDaFila(fila)); 
    printf("Removido: %d\n", *(int *)removerDaFila(fila)); 
    printf("Removido: %d\n", *(int *)removerDaFila(fila)); 

    limparFila(fila);
    return 0;
}
