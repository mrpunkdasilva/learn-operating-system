# 5.5 Escalonamento em Múltiplos Processadores

Imagine que você está jogando Minecraft em um servidor com vários amigos. Cada amigo é como um **processador**, e as tarefas que vocês fazem no jogo (como minerar, construir ou lutar) são os **processos**. Agora, vamos entender como o jogo (sistema operacional) decide quem faz o quê e como isso funciona quando há vários "amigos" (processadores) disponíveis.

---

## **5.5.1 Técnicas de Escalonamento com Multiprocessadores**
1. **Multiprocessamento Assimétrico (ASMP):**
   - Imagine que um dos seus amigos é o **chefe do servidor**. Ele decide quem faz o quê (escalona as tarefas), enquanto os outros só jogam (executam tarefas).
   - **Vantagem:** Simples, pois só o chefe toma decisões.
   - **Desvantagem:** Se o chefe ficar ocupado, todo o servidor pode ficar lento.

2. **Multiprocessamento Simétrico (SMP):**
   - Aqui, todos os amigos são **chefes** e decidem o que fazer. Eles podem compartilhar uma lista de tarefas ou cada um ter sua própria lista.
   - **Desafio:** Se dois amigos pegarem a mesma tarefa, pode dar confusão. Então, é preciso sincronização.
   - **Exemplo:** Sistemas como Windows, Linux e macOS usam SMP.

---

## **5.5.2 Afinidade de Processador**
- Imagine que você está minerando em uma caverna e já decorou onde estão os minérios (dados na **cache**). Se você for para outra caverna (outro processador), vai perder tempo reaprendendo onde estão os minérios.
- **Afinidade de Processador:** O sistema tenta manter você na mesma caverna (processador) para evitar perda de tempo.
  - **Afinidade Flexível:** O sistema tenta, mas não garante.
  - **Afinidade Rígida:** Você pode dizer "não quero sair daqui!".
- **NUMA (Acesso Não Uniforme à Memória):** Em servidores grandes, algumas cavernas são mais rápidas de acessar do que outras, dependendo da localização.

---

## **5.5.3 Balanceamento de Carga**
- Se um amigo está sobrecarregado (minerando e construindo ao mesmo tempo), enquanto outro está só olhando a paisagem, o sistema tenta **equilibrar** as tarefas.
  - **Migração Push:** O sistema redistribui as tarefas ativamente.
  - **Migração Pull:** O amigo ocioso pega uma tarefa de quem está ocupado.
- **Problema:** Se você mudar de caverna (processador), perde o benefício de já conhecer o local (cache).

---

## **5.5.4 Processadores Multicore**
- Agora imagine que cada amigo tem **várias mãos** (núcleos) para fazer tarefas ao mesmo tempo.
  - **Multithreading:** Cada mão pode fazer uma tarefa diferente.
    - **Coarse-Grained:** Troca de tarefas só quando algo demora muito (como esperar um bloco cair).
    - **Fine-Grained:** Troca de tarefas rapidamente, a cada pequena ação.
- **Exemplo:** Um processador com 8 núcleos e 4 threads por núcleo parece ter 32 "mãos" para o sistema operacional.

---

## **5.5.5 Virtualização e Escalonamento**
- Imagine que você está jogando em um **servidor virtual** (como um Minecraft dentro de outro Minecraft). O servidor real tem que dividir seus recursos entre vários jogos virtuais.
  - **Problema:** Se o servidor real estiver ocupado, seu jogo virtual pode ficar lento, mesmo que você tenha configurado tudo certinho.
  - **Impacto:** Sistemas de tempo real (como mods de redstone) podem falhar porque o tempo não é preciso.

---

## **Mindmap**

```
Escalonamento em Múltiplos Processadores
├── **Técnicas de Escalonamento**
│   ├── Assimétrico (ASMP)
│   │   ├── 1 chefe (processador mestre)
│   │   └── Outros só executam tarefas
│   └── Simétrico (SMP)
│       ├── Todos são chefes
│       ├── Fila de tarefas comum ou privada
│       └── Sincronização necessária
│
├── **Afinidade de Processador**
│   ├── Manter processo no mesmo processador
│   ├── Benefícios: aproveitar a cache
│   ├── Tipos
│   │   ├── Afinidade Flexível
│   │   └── Afinidade Rígida
│   └── NUMA (Acesso Não Uniforme à Memória)
│
├── **Balanceamento de Carga**
│   ├── Distribuir tarefas uniformemente
│   ├── Técnicas
│   │   ├── Migração Push
│   │   └── Migração Pull
│   └── Conflito com afinidade de processador
│
├── **Processadores Multicore**
│   ├── Vários núcleos em um chip
│   ├── Multithreading
│   │   ├── Coarse-Grained
│   │   └── Fine-Grained
│   └── Dois níveis de escalonamento
│       ├── Escalonamento de threads de software
│       └── Escalonamento de threads de hardware
│
└── **Virtualização e Escalonamento**
    ├── CPUs virtuais para máquinas virtuais
    ├── Impacto no desempenho
    └── Desafios para sistemas de tempo real
```
