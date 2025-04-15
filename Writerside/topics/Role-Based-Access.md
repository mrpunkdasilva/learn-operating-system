# Controle de Acesso Baseado em Posição (RBAC)

O controle de acesso baseado em posição (RBAC - Role-Based Access Control) é uma evolução dos sistemas tradicionais de controle de acesso, implementado notavelmente no Solaris 10.

## Conceitos Fundamentais

### Privilégios
- Direito de executar uma chamada de sistema
- Permissão para usar opções específicas dentro de chamadas de sistema
- Atribuídos diretamente a processos
- Limitação precisa de acesso necessário

### Posições (Roles)
- Agrupam privilégios e programas
- Atribuídas a usuários
- Podem requerer senhas específicas
- Ativação dinâmica de privilégios

## Implementação no Solaris 10

O Solaris 10 implementa o princípio do menor privilégio através do RBAC, oferecendo:

1. **Granularidade Fina**
   - Controle preciso sobre permissões
   - Minimização de riscos de segurança

2. **Flexibilidade**
   - Usuários podem assumir diferentes papéis
   - Papéis podem ser protegidos por senhas

3. **Segurança Aprimorada**
   - Redução de riscos associados a superusuários
   - Alternativa mais segura a programas setuid

## Comparação com Matriz de Acesso

O RBAC pode ser visto como uma implementação prática dos conceitos da matriz de acesso, oferecendo:
- Melhor escalabilidade
- Gerenciamento simplificado
- Maior segurança operacional
