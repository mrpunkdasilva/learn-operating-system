# Revogação de Direitos de Acesso

## Aspectos da Revogação

### 1. Imediata versus Adiada
- **Imediata**: Efeito instantâneo
- **Adiada**: Aplicação posterior
  - Necessidade de previsibilidade
  - Controle do momento da aplicação

### 2. Seletiva versus Geral
- **Seletiva**: Afeta usuários específicos
- **Geral**: Afeta todos os usuários com acesso

### 3. Parcial versus Total
- **Parcial**: Revoga subconjunto de direitos
- **Total**: Revoga todos os direitos

### 4. Temporária versus Permanente
- **Temporária**: Permite recuperação futura
- **Permanente**: Revogação definitiva

## Implementações

### Lista de Acesso (ACL)
- Revogação simplificada
- Pesquisa e exclusão direta
- Suporta todos os tipos de revogação
- Implementação eficiente

### Capacidades (Capabilities)
Apresenta desafios devido à distribuição pelo sistema.

#### Métodos de Implementação

1. **Reaquisição**
   - Exclusão periódica de capacidades
   - Processo de readquirição
   - Verificação de validade

2. **Ponteiros de Apoio**
   - Lista de ponteiros por objeto
   - Implementado no MULTICS
   - Flexível mas custoso

3. **Indireção**
   - Tabela global intermediária
   - Implementado no sistema CAL
   - Não permite revogação seletiva

4. **Chaves**
   - Padrões de bits exclusivos
   - Chave mestra por objeto
   - Comparação na execução

#### Sistema de Chaves Avançado
- Lista de chaves por objeto
- Tabela global de chaves
- Máxima flexibilidade
- Controle granular

## Considerações de Segurança

### Gerenciamento de Chaves
- Operações restritas
- Controle pelo proprietário
- Políticas flexíveis

### Políticas de Implementação
- Definidas pelo sistema
- Configuráveis por objeto
- Baseadas em propriedade