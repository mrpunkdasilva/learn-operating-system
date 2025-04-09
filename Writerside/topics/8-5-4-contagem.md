# 8.5.4 Contagem

## Conceito Básico

A técnica de contagem otimiza o gerenciamento de espaço livre armazenando pares de (endereço, quantidade), onde:
- Endereço indica o primeiro bloco livre de uma sequência
- Quantidade indica o número de blocos contíguos livres

### Representação Visual

```ascii
Lista de Espaço Livre
+----------------+----------------+----------------+
| Bloco 2, n=3   | Bloco 8, n=4   | Bloco 15, n=2  |
+----------------+----------------+----------------+
     ↓                 ↓                ↓
Disco
[XX][▢▢▢][XX][XX][▢▢▢▢][XX][▢▢][XX]
     ↑         ↑          ↑
   2,n=3     8,n=4     15,n=2
```
X = Ocupado, ▢ = Livre

## Implementação

```java
public class GerenciadorEspacoLivreContagem {
    private static class BlocoContagem implements Comparable<BlocoContagem> {
        int enderecoInicial;
        int quantidade;
        
        BlocoContagem(int enderecoInicial, int quantidade) {
            this.enderecoInicial = enderecoInicial;
            this.quantidade = quantidade;
        }
        
        @Override
        public int compareTo(BlocoContagem outro) {
            return Integer.compare(this.enderecoInicial, outro.enderecoInicial);
        }
    }
    
    private TreeSet<BlocoContagem> blocosLivres;
    private int totalBlocos;
    
    public GerenciadorEspacoLivreContagem(int totalBlocos) {
        this.blocosLivres = new TreeSet<>();
        this.totalBlocos = totalBlocos;
    }
    
    public void adicionarBlocoLivre(int enderecoInicial, int quantidade) {
        // Verifica se pode mesclar com blocos adjacentes
        BlocoContagem anterior = encontrarBlocoAnterior(enderecoInicial);
        BlocoContagem proximo = encontrarBlocoProximo(enderecoInicial + quantidade);
        
        if (anterior != null && anterior.enderecoInicial + anterior.quantidade == enderecoInicial) {
            // Mescla com bloco anterior
            blocosLivres.remove(anterior);
            enderecoInicial = anterior.enderecoInicial;
            quantidade += anterior.quantidade;
        }
        
        if (proximo != null && enderecoInicial + quantidade == proximo.enderecoInicial) {
            // Mescla com bloco próximo
            blocosLivres.remove(proximo);
            quantidade += proximo.quantidade;
        }
        
        blocosLivres.add(new BlocoContagem(enderecoInicial, quantidade));
    }
    
    public int[] alocarBlocos(int quantidadeDesejada) {
        for (BlocoContagem bloco : blocosLivres) {
            if (bloco.quantidade >= quantidadeDesejada) {
                int enderecoAlocado = bloco.enderecoInicial;
                
                // Atualiza ou remove o bloco livre
                if (bloco.quantidade > quantidadeDesejada) {
                    blocosLivres.remove(bloco);
                    blocosLivres.add(new BlocoContagem(
                        bloco.enderecoInicial + quantidadeDesejada,
                        bloco.quantidade - quantidadeDesejada
                    ));
                } else {
                    blocosLivres.remove(bloco);
                }
                
                return new int[]{enderecoAlocado, quantidadeDesejada};
            }
        }
        return null; // Não encontrou espaço suficiente
    }
    
    private BlocoContagem encontrarBlocoAnterior(int endereco) {
        return blocosLivres.floor(new BlocoContagem(endereco, 0));
    }
    
    private BlocoContagem encontrarBlocoProximo(int endereco) {
        return blocosLivres.ceiling(new BlocoContagem(endereco, 0));
    }
    
    public List<String> listarBlocosLivres() {
        List<String> lista = new ArrayList<>();
        for (BlocoContagem bloco : blocosLivres) {
            lista.add(String.format("Endereço: %d, Quantidade: %d", 
                bloco.enderecoInicial, bloco.quantidade));
        }
        return lista;
    }
}
```

### Exemplo de Uso

```java
public static void main(String[] args) {
    GerenciadorEspacoLivreContagem gerenciador = new GerenciadorEspacoLivreContagem(100);
    
    // Adiciona blocos livres
    gerenciador.adicionarBlocoLivre(2, 3);  // Blocos 2-4
    gerenciador.adicionarBlocoLivre(8, 4);  // Blocos 8-11
    gerenciador.adicionarBlocoLivre(15, 2); // Blocos 15-16
    
    System.out.println("Blocos livres iniciais:");
    gerenciador.listarBlocosLivres().forEach(System.out::println);
    
    // Aloca alguns blocos
    int[] alocacao = gerenciador.alocarBlocos(2);
    if (alocacao != null) {
        System.out.println("\nAlocado: Endereço " + alocacao[0] + 
                          ", Quantidade " + alocacao[1]);
    }
    
    System.out.println("\nBlocos livres após alocação:");
    gerenciador.listarBlocosLivres().forEach(System.out::println);
}
```

## Vantagens e Desvantagens

### Vantagens
1. **Lista Mais Compacta**: Menos entradas para representar o mesmo espaço livre
2. **Eficiência em Alocação Contígua**: Ideal para sistemas que usam alocação contígua
3. **Facilita Mesclagem**: Simplifica a identificação de blocos adjacentes livres

### Desvantagens
1. **Maior Complexidade**: Necessidade de manter e atualizar contadores
2. **Overhead por Entrada**: Cada entrada requer mais espaço (endereço + contador)
3. **Fragmentação da Lista**: Pode ocorrer quando há muitos blocos pequenos não contíguos