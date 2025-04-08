# 8.5.1 Vetor de Bits

## Conceito Básico

O vetor de bits é uma técnica eficiente para gerenciar espaço livre em disco, onde:
- Cada bloco é representado por 1 bit
- Bit 1 = bloco livre
- Bit 0 = bloco alocado

### Exemplo Visual

```ascii
Blocos:    0  1  2  3  4  5  6  7  8  9  10
Estado:    A  A  L  L  L  L  A  A  L  L   L
Bits:      0  0  1  1  1  1  0  0  1  1   1
```
A = Alocado, L = Livre

## Implementação Prática

```java
public class GerenciadorEspacoLivre {
    private BitSet vetorBits;
    private int totalBlocos;
    private static final int BITS_POR_PALAVRA = 32;

    public GerenciadorEspacoLivre(int numBlocos) {
        this.totalBlocos = numBlocos;
        this.vetorBits = new BitSet(numBlocos);
        // Inicialmente, todos os blocos estão livres
        this.vetorBits.set(0, numBlocos);
    }

    public int encontrarPrimeiroBlocoLivre() {
        for (int i = 0; i < totalBlocos; i++) {
            if (vetorBits.get(i)) {
                return i;
            }
        }
        return -1; // Nenhum bloco livre encontrado
    }

    public int[] encontrarBlocosConsecutivos(int quantidade) {
        int contador = 0;
        int inicio = -1;

        for (int i = 0; i < totalBlocos; i++) {
            if (vetorBits.get(i)) {
                if (contador == 0) inicio = i;
                contador++;
                if (contador == quantidade) {
                    return new int[]{inicio, i};
                }
            } else {
                contador = 0;
            }
        }
        return null; // Não encontrou blocos consecutivos suficientes
    }

    public void alocarBloco(int numeroBloco) {
        if (numeroBloco >= 0 && numeroBloco < totalBlocos) {
            vetorBits.clear(numeroBloco);
        }
    }

    public void liberarBloco(int numeroBloco) {
        if (numeroBloco >= 0 && numeroBloco < totalBlocos) {
            vetorBits.set(numeroBloco);
        }
    }

    public double calcularFragmentacao() {
        int blocosLivres = vetorBits.cardinality();
        int sequenciasLivres = 0;
        boolean emSequencia = false;

        for (int i = 0; i < totalBlocos; i++) {
            if (vetorBits.get(i) && !emSequencia) {
                sequenciasLivres++;
                emSequencia = true;
            } else if (!vetorBits.get(i)) {
                emSequencia = false;
            }
        }

        return sequenciasLivres > 0 ? 
               (double) blocosLivres / sequenciasLivres : 
               0.0;
    }
}
```

### Exemplo de Uso

```java
public static void main(String[] args) {
    GerenciadorEspacoLivre gerenciador = new GerenciadorEspacoLivre(1000);
    
    // Alocar alguns blocos
    gerenciador.alocarBloco(0);
    gerenciador.alocarBloco(1);
    gerenciador.alocarBloco(6);
    gerenciador.alocarBloco(7);
    
    // Encontrar espaço para um novo arquivo
    int[] blocos = gerenciador.encontrarBlocosConsecutivos(4);
    if (blocos != null) {
        System.out.println("Encontrado espaço livre do bloco " + 
                          blocos[0] + " até " + blocos[1]);
    }
    
    // Verificar fragmentação
    double fragmentacao = gerenciador.calcularFragmentacao();
    System.out.println("Índice de fragmentação: " + fragmentacao);
}
```

## Considerações de Implementação

### Vantagens
1. **Simplicidade**: Fácil de implementar e manter
2. **Eficiência de Memória**: 1 bit por bloco
3. **Rápida Localização**: Operações bitwise eficientes

### Limitações
1. **Consumo de Memória para Discos Grandes**:
   - 1 TB (blocos 4 KB) = 32 MB de bitmap
   - 1 PB (blocos 4 KB) = 32 GB de bitmap

2. **Necessidade de Manter em Memória**:
   - Para eficiência máxima
   - Sincronização periódica com disco

### Otimizações Possíveis
1. **Agrupamento de Blocos**: Reduzir overhead de bitmap
2. **Cache Parcial**: Manter apenas partes ativas em memória
3. **Compressão**: Para regiões com muitos blocos livres/ocupados consecutivos