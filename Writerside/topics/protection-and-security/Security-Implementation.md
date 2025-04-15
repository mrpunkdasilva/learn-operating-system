# Implementando Defesas de Segurança

Existem inúmeras soluções de segurança para combater as diversas ameaças aos sistemas e redes. As abordagens variam desde treinamento de usuários até desenvolvimento de software seguro. A maioria dos profissionais segue o princípio da **defesa em profundidade** - quanto mais camadas de proteção, melhor.

## Política de Segurança

O primeiro passo para melhorar a segurança é estabelecer uma política clara que defina:

- O que está sendo protegido
- Regras e procedimentos obrigatórios
- Responsabilidades e permissões
- Processos de revisão e atualização

A política deve ser:
- Bem documentada e comunicada
- Regularmente atualizada
- Usada como guia prático

## Avaliação de Vulnerabilidade

Inclui:

- Testes de penetração
- Varreduras de sistema procurando:
  - Senhas fracas
  - Programas não autorizados
  - Proteções inadequadas
  - Processos suspeitos
  - Daemons de rede inesperados

### Varreduras de Rede

- Identificam portas abertas
- Detectam serviços vulneráveis  
- Verificam configurações incorretas
- Identificam patches faltantes

## Detecção de Intrusão

Sistemas de detecção (IDS) e prevenção (IPS) de intrusão utilizam duas abordagens principais:

1. **Detecção baseada em assinatura**
   - Procura padrões conhecidos de ataques
   - Eficaz contra ameaças conhecidas
   - Requer atualizações frequentes

2. **Detecção de anomalia** 
   - Monitora comportamentos anormais
   - Pode detectar ataques novos
   - Desafio: definir "comportamento normal"

## Proteção Antivírus

Estratégias principais:

- Varredura de assinaturas
- Análise comportamental
- Execução em sandbox
- Monitoramento em tempo real
- Prevenção proativa

Boas práticas:

- Usar software de fontes confiáveis
- Evitar anexos suspeitos
- Manter sistemas atualizados
- Implementar múltiplas camadas de proteção