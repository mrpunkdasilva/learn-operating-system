# Exercícios sobre Sistema de Arquivos

## 11.1 Análise de Operações de E/S em Diferentes Estratégias de Alocação

### Premissas
- Arquivo com 100 blocos
- Bloco de controle e índice já em memória
- Dados do novo bloco em memória
- Alocação contígua tem espaço apenas no final

### Tabela Comparativa de Operações de E/S

| Operação                    | Contígua | Interligada | Indexada |
|----------------------------|----------|-------------|-----------|
| Adicionar no início        | 101      | 2           | 2         |
| Adicionar no meio          | 51       | 2           | 2         |
| Adicionar no final         | 1        | 2           | 2         |
| Remover do início          | 99       | 1           | 1         |
| Remover do meio            | 50       | 2           | 1         |
| Remover do final           | 0        | 2           | 1         |

### Explicação Detalhada

#### Alocação Contígua
- **Adicionar início**: 101 operações
  - Mover 100 blocos uma posição adiante (100 operações)
  - Escrever novo bloco (1 operação)
  
- **Adicionar meio**: 51 operações
  - Mover 50 blocos uma posição (50 operações)
  - Escrever novo bloco (1 operação)
  
- **Adicionar final**: 1 operação
  - Apenas escrever o novo bloco

- **Remover início**: 99 operações
  - Mover 99 blocos uma posição para trás
  
- **Remover meio**: 50 operações
  - Mover 50 blocos uma posição para trás
  
- **Remover final**: 0 operações
  - Apenas atualizar metadados (já em memória)

#### Alocação Interligada
- **Adicionar**: 2 operações para qualquer posição
  - Ler bloco anterior (1 operação)
  - Escrever novo bloco com ponteiro (1 operação)

- **Remover**: 
  - Início: 1 operação (atualizar primeiro ponteiro)
  - Meio/Final: 2 operações (ler anterior e atualizar ponteiro)

#### Alocação Indexada
- **Adicionar**: 2 operações para qualquer posição
  - Escrever novo bloco (1 operação)
  - Atualizar bloco de índice (1 operação)

- **Remover**: 1 operação
  - Apenas atualizar bloco de índice

## 11.2 Problemas com Montagem Simultânea

### Principais Problemas
1. **Inconsistência de Dados**
   - Múltiplas cópias dos mesmos dados em cache
   - Conflitos de escrita entre pontos de montagem

2. **Corrupção do Sistema de Arquivos**
   - Atualizações simultâneas podem corromper estruturas
   - Problemas de sincronização de metadados

3. **Problemas de Cache**
   - Diferentes caches para mesmo arquivo
   - Inconsistência entre pontos de montagem

## 11.3 Mapa de Bits em Armazenamento de Massa

### Razões
1. **Persistência**
   - Informação crítica que deve sobreviver a reinicializações
   - Necessária para recuperação após falhas

2. **Consistência**
   - Garante estado consistente do sistema de arquivos
   - Evita perda de informação sobre blocos livres/ocupados

3. **Tamanho**
   - Mapas de bits podem ser grandes
   - Memória principal é recurso limitado

## 11.4 Critérios para Escolha de Estratégia de Alocação

### Fatores a Considerar

1. **Tamanho do Arquivo**
   - Pequenos: Alocação contígua
   - Grandes: Indexada ou interligada

2. **Padrão de Acesso**
   - Sequencial: Contígua ou interligada
   - Aleatório: Indexada

3. **Frequência de Modificação**
   - Alta: Indexada
   - Baixa: Contígua

4. **Crescimento**
   - Previsível: Contígua
   - Imprevisível: Indexada ou interligada

## 11.5 Análise da Solução de Área de Estouro

### Comparação

1. **Vantagens**
   - Melhor que alocação contígua pura
   - Mantém benefícios de acesso sequencial
   - Flexibilidade para crescimento

2. **Desvantagens**
   - Mais complexo que interligada
   - Fragmentação nas áreas de estouro
   - Overhead de gerenciamento

## 11.6 Caches e Desempenho

### Benefícios
1. **Redução de E/S**
   - Menos acessos ao disco
   - Menor latência

2. **Melhor Throughput**
   - Operações mais rápidas
   - Maior vazão de dados

### Limitações
1. **Custo**
   - Memória RAM é cara
   - Compete com outros recursos

2. **Complexidade**
   - Gerenciamento de consistência
   - Overhead de sincronização

## 11.7 Alocação Dinâmica de Tabelas

### Vantagens
1. **Eficiência**
   - Uso otimizado de memória
   - Adaptação a diferentes cargas

2. **Flexibilidade**
   - Suporte a mais arquivos/processos
   - Melhor utilização de recursos

### Desvantagens
1. **Overhead**
   - Gerenciamento de memória
   - Fragmentação

2. **Complexidade**
   - Implementação mais complexa
   - Debugging mais difícil

## 11.8 Camada VFS

### Funcionamento
1. **Abstração**
   - Interface uniforme
   - Independência de implementação

2. **Modularidade**
   - Separação de responsabilidades
   - Facilidade de extensão

3. **Flexibilidade**
   - Suporte a múltiplos sistemas
   - Transparência para aplicações