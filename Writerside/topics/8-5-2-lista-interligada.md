# 8.5.2 Lista Interligada

## Conceito Básico

A lista interligada é uma técnica alternativa para gerenciamento de espaço livre onde:
- Blocos livres são conectados através de ponteiros
- O primeiro bloco livre é mantido em cache na memória
- Cada bloco livre contém o endereço do próximo bloco livre

### Representação Visual

```ascii
Primeiro Bloco Livre
      ↓
    +---+     +---+     +---+     +---+
    | 2 | --> | 3 | --> | 4 | --> | 5 | ...
    +---+     +---+     +---+     +---+
```

## Implementação Prática

```java
public class GerenciadorEspacoLivreLista {
    private static class BlocoLivre {
        int numeroBloco;
        int proximoBloco;
        
        BlocoLivre(int numeroBloco, int proximoBloco) {
            this.numeroBloco = numeroBloco;
            this.proximoBloco = proximoBloco;
        }
    }
    
    private int primeiroBlocoLivre;
    private Map<Integer, BlocoLivre> blocosLivres;
    private static final int BLOCO_NULO = -1;
    
    public GerenciadorEspacoLivreLista() {
        this.blocosLivres = new HashMap<>();
        this.primeiroBlocoLivre = BLOCO_NULO;
    }
    
    public void adicionarBlocoLivre(int numeroBloco) {
        BlocoLivre novoBloco = new BlocoLivre(numeroBloco, primeiroBlocoLivre);
        blocosLivres.put(numeroBloco, novoBloco);
        primeiroBlocoLivre = numeroBloco;
    }
    
    public int alocarBloco() {
        if (primeiroBlocoLivre == BLOCO_NULO) {
            return BLOCO_NULO; // Sem blocos livres
        }
        
        BlocoLivre blocoAlocado = blocosLivres.get(primeiroBlocoLivre);
        primeiroBlocoLivre = blocoAlocado.proximoBloco;
        blocosLivres.remove(blocoAlocado.numeroBloco);
        
        return blocoAlocado.numeroBloco;
    }
    
    public List<Integer> listarBlocosLivres() {
        List<Integer> lista = new ArrayList<>();
        int atual = primeiroBlocoLivre;
        
        while (atual != BLOCO_NULO) {
            lista.add(atual);
            BlocoLivre bloco = blocosLivres.get(atual);
            atual = bloco.proximoBloco;
        }
        
        return lista;
    }
}
```

### Exemplo de Uso

```java
public static void main(String[] args) {
    GerenciadorEspacoLivreLista gerenciador = new GerenciadorEspacoLivreLista();
    
    // Adicionar blocos livres em sequência
    gerenciador.adicionarBlocoLivre(2);
    gerenciador.adicionarBlocoLivre(3);
    gerenciador.adicionarBlocoLivre(4);
    gerenciador.adicionarBlocoLivre(5);
    
    // Listar blocos livres
    List<Integer> blocosLivres = gerenciador.listarBlocosLivres();
    System.out.println("Blocos livres: " + blocosLivres);
    
    // Alocar alguns blocos
    int blocoAlocado1 = gerenciador.alocarBloco();
    int blocoAlocado2 = gerenciador.alocarBloco();
    
    System.out.println("Bloco alocado 1: " + blocoAlocado1);
    System.out.println("Bloco alocado 2: " + blocoAlocado2);
    
    // Verificar blocos restantes
    blocosLivres = gerenciador.listarBlocosLivres();
    System.out.println("Blocos livres restantes: " + blocosLivres);
}
```

## Considerações de Implementação

### Vantagens
1. **Simplicidade Conceitual**: Fácil de entender e implementar
2. **Sem Fragmentação Externa**: Todos os blocos livres são utilizáveis
3. **Flexibilidade**: Fácil adicionar ou remover blocos

### Limitações
1. **Performance de E/S**:
   - Necessidade de leitura de cada bloco para travessia
   - Tempo substancial de E/S para operações de busca

2. **Overhead de Armazenamento**:
   - Cada bloco livre precisa armazenar um ponteiro
   - Espaço adicional para gerenciamento da lista

### Otimizações Possíveis
1. **Cache de Blocos**: Manter blocos frequentemente acessados em memória
2. **Agrupamento**: Gerenciar grupos de blocos consecutivos como uma unidade
3. **Lista Duplamente Encadeada**: Para operações mais flexíveis de gerenciamento