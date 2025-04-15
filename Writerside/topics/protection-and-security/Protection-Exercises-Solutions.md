# Soluções dos Exercícios - Proteção e Segurança

## 1. Ataques de Buffer Overflow
Os ataques de buffer overflow podem ser evitados através de:

**Metodologias de Programação:**
- Validação rigorosa de entrada
- Uso de funções seguras (strncpy vs strcpy)
- Verificação de limites de buffer
- Análise estática de código

**Suporte de Hardware:**
- Bits NX (No-Execute)
- ASLR (Address Space Layout Randomization)
- Stack canaries
- Proteção de página de memória

## 2. Detecção de Senha Comprometida
Não existe um método simples e direto para detectar se uma senha foi comprometida. Porém, podem ser implementadas estratégias como:

- Monitoramento de padrões de acesso anormais
- Logs de login de diferentes localizações
- Implementação de autenticação de dois fatores
- Análise de tentativas de login simultâneas

## 3. Uso de Salt em Senhas
O salt é um valor aleatório concatenado à senha antes do hash. Seu propósito é:

- Prevenir ataques de tabela rainbow
- Tornar hashes únicos mesmo para senhas idênticas
- Dificultar ataques de dicionário

O salt deve ser:
- Armazenado junto com o hash da senha
- Único para cada usuário
- Gerado aleatoriamente

## 4. Proteção da Lista de Senhas
Solução proposta:

1. **Representação Externa:**
   - Hash da senha + salt
   - Nunca armazenar senha em texto puro

2. **Representação Interna:**
   - Usar criptografia adicional
   - Fragmentar o armazenamento
   - Implementar controle de acesso em nível de kernel

## 5. Watchdog em Arquivos UNIX

**Prós:**
1. Controle granular de acesso
2. Monitoramento em tempo real

**Contras:**
1. Overhead de performance
2. Complexidade adicional de manutenção

## 6. Riscos do COPS

**Riscos Potenciais:**
1. Pode ser usado por atacantes para identificar vulnerabilidades
2. Falsos negativos podem criar falsa sensação de segurança

**Mitigação:**
- Restringir acesso ao COPS
- Executar em ambiente controlado
- Manter logs de execução

## 7. Prevenção contra Worms
Soluções possíveis:

1. **Segmentação de rede:**
   - DMZs
   - VLANs
   - Microsegmentação

2. **Desvantagens:**
   - Complexidade administrativa
   - Custos adicionais
   - Possível impacto na performance

## 8. Caso Robert Morris Jr.
Argumentos relevantes:

**A Favor da Condenação:**
- Causou danos significativos
- Ação intencional
- Impacto em infraestrutura crítica

**Contra a Condenação:**
- Intenção de pesquisa
- Contribuiu para conscientização
- Impacto não intencional

## 9. Segurança Bancária
Aspectos críticos:

1. **Segurança Física:**
   - Controle de acesso ao datacenter
   - Sistemas de backup

2. **Segurança Humana:**
   - Treinamento de funcionários
   - Políticas de acesso

3. **Segurança do SO:**
   - Criptografia de dados
   - Controle de privilégios
   - Logs de auditoria

## 10. Vantagens da Criptografia
1. Proteção contra acesso não autorizado mesmo com comprometimento físico
2. Conformidade com regulamentações de privacidade

## 11. Ataques Man-in-the-Middle
Programas vulneráveis:
- Navegadores web
- Clientes de email
- Aplicativos de mensagem

Soluções:
- Certificados SSL/TLS
- Verificação de certificados
- Pinning de certificados

## 12. Criptografia Simétrica vs Assimétrica

**Simétrica:**
- Mais rápida
- Ideal para grandes volumes
- Requer canal seguro para troca de chaves

**Assimétrica:**
- Mais segura para distribuição de chaves
- Permite assinatura digital
- Mais lenta

## 13. Análise de D(kd,N)(E(ke,N)(m))
Esta operação não fornece autenticação porque:
- Qualquer pessoa com acesso a ke pode gerar a mensagem
- Não há garantia da origem

Usos possíveis:
- Confidencialidade de dados
- Comunicação segura sem autenticação

## 14. Usos de Criptografia Assimétrica

a) **Autenticação:**
- Emissor assina com chave privada
- Receptor verifica com chave pública

b) **Segredo:**
- Emissor criptografa com chave pública do receptor
- Receptor descriptografa com sua chave privada

c) **Autenticação e Segredo:**
- Combinar assinatura e criptografia
- Usar protocolos como PGP

## 15. Análise de Sistema de Detecção

Dados:
- 10 milhões registros/dia
- 10 ataques/dia (200 registros)
- Taxa alarme verdadeiro: 0,6
- Taxa alarme falso: 0,0005

Cálculo:
1. Alarmes verdadeiros = 0,6 × 10 × 20 = 120
2. Alarmes falsos = 0,0005 × (10.000.000 - 200) = 4.999,9
3. Total alarmes = 120 + 4.999,9 = 5.119,9
4. Porcentagem real = (120 / 5.119,9) × 100 ≈ 2,34%