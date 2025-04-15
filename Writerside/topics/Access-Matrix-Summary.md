# Matriz de Acesso (Access Matrix)

## Estrutura Básica
- **Linhas**: Representam domínios (Di)
- **Colunas**: Representam objetos (Oj)
- **Entradas**: access(i,j) define operações permitidas para processos no domínio Di sobre objeto Oj

## Direitos Especiais

### 1. Switch
- Permite troca entre domínios
- Se switch ∈ access(i,j), processo pode mudar do domínio Di para Dj

### 2. Copy (*)
- Indicado por asterisco após o direito
- Permite copiar direitos dentro da mesma coluna
- Variantes:
  - Transferência (remove direito original)
  - Cópia limitada (copia sem direito de propagação)

### 3. Owner
- Controla adição/remoção de direitos
- Proprietário pode modificar qualquer direito na coluna do objeto

### 4. Control
- Aplica-se apenas a objetos de domínio
- Permite remover direitos de acesso de uma linha específica

## Características
- Implementa políticas de proteção dinâmicas
- Permite criação de novos objetos e domínios
- Controla mudanças de domínio
- Gerencia propagação de direitos

## Limitações
- Não resolve o problema de confinamento (impedir vazamento de informações)
- Requer decisões políticas dos projetistas e usuários do sistema