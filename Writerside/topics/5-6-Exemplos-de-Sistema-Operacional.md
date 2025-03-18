# 5.6 Exemplos de Sistema Operacional

Vamos explorar como sistemas operacionais modernos, como **Windows 10/11**, **Linux (com foco no kernel 5.x ou superior)** e **macOS**, lidam com o escalonamento de tarefas. Para facilitar o entendimento, vamos usar **Minecraft** como analogia. Imagine que o sistema operacional é o **servidor de Minecraft**, e as tarefas (processos ou threads) são os **jogadores** que precisam realizar atividades no jogo.

---

## **5.6.1 Escalonamento no Windows 10/11**
O Windows 10/11 usa um sistema de **prioridades dinâmicas** e **escalonamento preemptivo** para gerenciar tarefas. Ele é uma evolução do Windows XP, com melhorias para suportar hardware moderno, como processadores multicore e sistemas NUMA.

### **Características Principais:** {id="caracter-sticas-principais_1"}
1. **Prioridades Dinâmicas:**
   - As tarefas são organizadas em **32 níveis de prioridade** (0 a 31).
   - Tarefas de **tempo real** (16-31) têm prioridade máxima e são executadas imediatamente.
   - Tarefas comuns (1-15) têm prioridades ajustadas dinamicamente:
     - Tarefas interativas (como abrir um aplicativo) ganham prioridade.
     - Tarefas que usam muita CPU (como renderização) perdem prioridade.

2. **Balanceamento de Carga:**
   - O Windows distribui tarefas entre **núcleos de processadores** para evitar sobrecarga.
   - Se um núcleo estiver ocioso, ele "puxa" tarefas de outros núcleos ocupados.

3. **Suporte a NUMA:**
   - Em sistemas com múltiplos processadores e memória não uniforme (NUMA), o Windows tenta manter as tarefas próximas à memória que estão usando, para melhorar o desempenho.

4. **Modo de Economia de Energia:**
   - O Windows ajusta o escalonamento para reduzir o consumo de energia em dispositivos móveis, priorizando tarefas em núcleos de baixo consumo.

### **Como Funciona no Minecraft:** {id="como-funciona-no-minecraft_1"}
- Se um jogador estiver construindo algo complexo (uso intenso de CPU), ele pode perder prioridade para outro jogador que está interagindo com o ambiente (abrir baús, clicar em blocos).
- O servidor (escalonador) garante que todos os núcleos do processador sejam usados de forma equilibrada.

---

## **5.6.2 Escalonamento no Linux (Kernel 5.x ou superior)**
O Linux moderno usa o **escalonador CFS (Completely Fair Scheduler)**, que é altamente eficiente e justo. Ele foi projetado para sistemas multicore e grandes cargas de trabalho.

### **Características Principais:** {id="caracter-sticas-principais_2"}
1. **CFS (Completely Fair Scheduler):**
   - O CFS usa um conceito de **tempo virtual** para garantir que todas as tarefas recebam uma fatia justa da CPU.
   - Tarefas com **prioridades mais altas** recebem mais tempo de CPU, mas todas são atendidas de forma equilibrada.

2. **Prioridades:**
   - As tarefas são organizadas em dois grupos:
     - **Tempo Real (0-99):** Prioridade máxima, executadas imediatamente.
     - **Tarefas Comuns (100-139):** Prioridades ajustadas dinamicamente com base no valor **nice** (quanto maior o valor nice, menor a prioridade).

3. **Balanceamento de Carga:**
   - O Linux distribui tarefas entre núcleos de processadores e tenta manter a **afinidade de processador** (evitar migração desnecessária de tarefas entre núcleos).
   - Se um núcleo estiver ocioso, ele "puxa" tarefas de outros núcleos.

4. **Suporte a NUMA:**
   - O Linux é altamente otimizado para sistemas NUMA, garantindo que as tarefas sejam executadas próximas à memória que estão usando.

5. **Escalonamento em Tempo Real:**
   - O Linux suporta tarefas de tempo real com **prioridades estáticas**, garantindo que elas sejam executadas imediatamente.

### **Como Funciona no Minecraft:**
- O servidor (escalonador) garante que todos os jogadores tenham uma fatia justa do tempo de CPU.
- Se um jogador estiver minerando (uso intenso de CPU), ele não dominará o servidor, permitindo que outros jogadores interajam com o ambiente.

---

## **5.6.3 Escalonamento no macOS**
O macOS usa um sistema de escalonamento baseado em **prioridades dinâmicas** e **qualidade de serviço (QoS)**, projetado para oferecer uma experiência suave e responsiva.

### **Características Principais:**
1. **Qualidade de Serviço (QoS):**
   - As tarefas são classificadas em **níveis de QoS**, que determinam sua prioridade:
     - **User Interactive (UI):** Prioridade máxima para tarefas interativas (como animações de interface).
     - **User Initiated:** Para tarefas iniciadas pelo usuário (como abrir um aplicativo).
     - **Utility:** Para tarefas em segundo plano (como downloads).
     - **Background:** Para tarefas de baixa prioridade (como indexação de arquivos).

2. **Prioridades Dinâmicas:**
   - O macOS ajusta as prioridades das tarefas com base no comportamento:
     - Tarefas interativas ganham prioridade.
     - Tarefas que usam muita CPU perdem prioridade.

3. **Grand Central Dispatch (GCD):**
   - O GCD é uma tecnologia que facilita a execução de tarefas em paralelo, distribuindo-as entre núcleos de processadores.

4. **Suporte a NUMA:**
   - O macOS é otimizado para sistemas com múltiplos processadores e memória não uniforme (NUMA).

### **Como Funciona no Minecraft:** {id="como-funciona-no-minecraft_2"}
- Se um jogador estiver interagindo com a interface do jogo (como abrir um menu), ele terá prioridade máxima.
- Tarefas em segundo plano (como carregar chunks do mundo) são executadas com prioridade mais baixa, sem afetar a experiência do jogador.

---

## **Mindmap**

```
Exemplos de Sistemas Operacionais Modernos
├── **Windows 10/11**
│   ├── Prioridades Dinâmicas (0-31)
│   ├── Balanceamento de Carga
│   ├── Suporte a NUMA
│   └── Modo de Economia de Energia
│
├── **Linux (Kernel 5.x ou superior)**
│   ├── CFS (Completely Fair Scheduler)
│   ├── Prioridades (Tempo Real: 0-99, Comuns: 100-139)
│   ├── Balanceamento de Carga
│   ├── Suporte a NUMA
│   └── Escalonamento em Tempo Real
│
└── **macOS**
    ├── Qualidade de Serviço (QoS)
    ├── Prioridades Dinâmicas
    ├── Grand Central Dispatch (GCD)
    └── Suporte a NUMA
```
