#include <stdio.h>
#include <stdint.h>

// Função para inicializar o LFSR com um valor de semente
uint32_t inicializa_lfsr32(uint32_t semente) {
    return semente;
}

// Função para realizar um passo do LFSR
uint32_t passo_lfsr32(uint32_t lfsr) {
    // Polinômio gerador específico: x^32 + x^22 + x^2 + x + 1
    // O feedback é calculado com base nos bits 31, 21, 1 e 0 (considerando a indexação 0)
    uint32_t feedback = ((lfsr >> 31) ^ (lfsr >> 21) ^ (lfsr >> 1) ^ (lfsr >> 0)) & 1;
    // Desloca todos os bits para a direita e insere o feedback no bit mais baixo
    return (lfsr >> 1) | (feedback << 31);
}

int main() {
    uint32_t lfsr = inicializa_lfsr32(0xFFFFFFFF); // Inicializa o LFSR com um valor não zero

    // Simula o LFSR por um número definido de ciclos
    for (int i = 0; i < 10; i++) {
        printf("Valor do LFSR: 0x%08X\n", lfsr);
        lfsr = passo_lfsr32(lfsr);
    }

    return 0;
}

