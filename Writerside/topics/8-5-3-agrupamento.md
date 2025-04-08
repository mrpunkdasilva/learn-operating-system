# 8.5.3 Agrupamento

## Conceito Básico

O agrupamento é uma otimização da lista interligada onde cada bloco livre armazena múltiplos endereços de outros blocos livres, melhorando a eficiência da gestão de espaço.

### Representação Visual

```ascii
Primeiro Bloco (n=4)
+----------------+
| Bloco 2        |
| Bloco 3        |
| Bloco 4        |
| → Próx. Grupo  |
+----------------+
       ↓
Próximo Grupo
+----------------+
| Bloco 7        |
| Bloco 8        |
| Bloco 9        |
| → Próx. Grupo  |
+----------------+
```

## Implementação

```java
public class GerenciadorEspacoLivreGrupo {
    private static final int TAMANHO_GRUPO = 4; // n blocos por grupo
    
    private static class BlocoGrupo {
        int[] blocosLivres;      // n-1 blocos livres
        int proximoGrupo;        // Endereço do próximo grupo
        
        BlocoGrupo() {
            this.blocosLivres = new int[TAMANHO_GRUPO - 1];
            this.proximoGrupo = -1;
        }
    }
    
    private Map<Integer, BlocoGrupo> grupos;
    private int primeiroGrupo;
    private int blocosDisponiveis;
    
    public GerenciadorEspacoLivreGrupo() {
        this.grupos = new HashMap<>();
        this.primeiroGrupo = -1;
        this.blocosDisponiveis = 0;
    }
    
    public void adicionarBlocosLivres(int[] blocos) {
        int indiceBloco = 0;
        
        while (indiceBloco < blocos.length) {
            BlocoGrupo novoGrupo = new BlocoGrupo();
            
            // Preenche o grupo atual com blocos livres
            for (int i = 0; i < TAMANHO_GRUPO - 1 && indiceBloco < blocos.length; i++) {
                novoGrupo.blocosLivres[i] = blocos[indiceBloco++];
                blocosDisponiveis++;
            }
            
            // Conecta o novo grupo à lista
            novoGrupo.proximoGrupo = primeiroGrupo;
            primeiroGrupo = blocos[indiceBloco - 1];
            grupos.put(primeiroGrupo, novoGrupo);
        }
    }
    
    public int alocarBloco() {
        if (primeiroGrupo == -1 || blocosDisponiveis == 0) {
            return -1; // Sem blocos livres
        }
        
        BlocoGrupo grupo = grupos.get(primeiroGrupo);
        
        // Aloca o primeiro bloco livre disponível
        int blocoAlocado = grupo.blocosLivres[0];
        
        // Reorganiza os blocos restantes
        for (int i = 0; i < TAMANHO_GRUPO - 2; i++) {
            grupo.blocosLivres[i] = grupo.blocosLivres[i + 1];
        }
        
        blocosDisponiveis--;
        
        // Se o grupo ficou vazio, move para o próximo
        if (blocosDisponiveis % (TAMANHO_GRUPO - 1) == 0) {
            int proximoGrupo = grupo.proximoGrupo;
            grupos.remove(primeiroGrupo);
            primeiroGrupo = proximoGrupo;
        }
        
        return blocoAlocado;
    }
    
    public List<Integer> listarBlocosLivres() {
        List<Integer> blocos = new ArrayList<>();
        int grupoAtual = primeiroGrupo;
        
        while (grupoAtual != -1) {
            BlocoGrupo grupo = grupos.get(grupoAtual);
            for (int bloco : grupo.blocosLivres) {
                if (bloco != 0) { // Ignora posições vazias
                    blocos.add(bloco);
                }
            }
            grupoAtual = grupo.proximoGrupo;
        }
        
        return blocos;
    }
}
```

### Exemplo de Uso

```java
public static void main(String[] args) {
    GerenciadorEspacoLivreGrupo gerenciador = new GerenciadorEspacoLivreGrupo();
    
    // Adiciona vários blocos livres
    int[] blocosLivres = {2, 3, 4, 7, 8, 9, 12, 13, 14};
    gerenciador.adicionarBlocosLivres(blocosLivres);
    
    // Lista todos os blocos livres
    System.out.println("Blocos livres iniciais: " + 
        gerenciador.listarBlocosLivres());
    
    // Aloca alguns blocos
    int bloco1 = gerenciador.alocarBloco();
    int bloco2 = gerenciador.alocarBloco();
    
    System.out.println("Bloco alocado 1: " + bloco1);
    System.out.println("Bloco alocado 2: " + bloco2);
    
    // Verifica blocos restantes
    System.out.println("Blocos livres restantes: " + 
        gerenciador.listarBlocosLivres());
}
```

## Vantagens e Desvantagens

### Vantagens
1. **Acesso Mais Rápido**: Localiza múltiplos blocos livres com menos operações de I/O
2. **Menor Overhead de Travessia**: Reduz o número de leituras necessárias
3. **Melhor Utilização de Cache**: Aproveita melhor o cache de memória

### Desvantagens
1. **Complexidade Adicional**: Implementação mais complexa que lista simples
2. **Overhead de Memória**: Cada grupo precisa manter array de endereços
3. **Fragmentação do Grupo**: Grupos parcialmente preenchidos podem desperdiçar espaço