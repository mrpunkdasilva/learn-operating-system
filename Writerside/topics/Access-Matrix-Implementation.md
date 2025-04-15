# Implementação da Matriz de Acesso

## 1. Tabela Global

### Características
- Implementação usando triplas `<domínio, objeto, conjunto-de-direitos>`
- Pesquisa sequencial por triplas correspondentes

### Desvantagens
- Tabela muito grande
- Requer E/S adicional
- Difícil aproveitar agrupamentos
- Redundância para direitos comuns

## 2. Listas de Acesso (ACL)

### Estrutura
- Lista por objeto
- Pares `<domínio, conjunto-de-direitos>`
- Suporte a direitos padrão

### Funcionamento
1. Pesquisa entrada específica
2. Verifica conjunto padrão
3. Permite ou nega acesso

## 3. Listas de Capacidade

### Características
- Lista por domínio
- Capacidades como ponteiros seguros
- Proteção inerente do sistema

### Implementação
- Tags/chaves para distinguir capacidades
- Espaço de endereço dividido
- Acesso restrito pelo SO

## 4. Mecanismo Lock-Key

### Funcionamento
- Objetos têm locks (padrões de bits)
- Domínios têm keys
- Acesso permitido se key combina com lock

## Comparação Final

| Método | Vantagens | Desvantagens |
|--------|-----------|--------------|
| Tabela Global | Simplicidade | Tamanho excessivo |
| ACL | Intuitivo para usuários | Pesquisa lenta |
| Capacidades | Verificação eficiente | Revogação complexa |
| Lock-Key | Flexibilidade | Depende do tamanho das chaves |

### Solução Híbrida Comum
- Combina ACL e Capacidades
- ACL na primeira verificação
- Capacidade para acessos subsequentes
- Exemplo: Sistema de arquivos UNIX