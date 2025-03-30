# Escalonamento de CPU

O escalonamento de CPU é um dos conceitos fundamentais dos sistemas operacionais multiprogramados. Ele permite que o sistema operacional gerencie a alocação da CPU entre os processos (ou threads), tornando o computador mais produtivo e responsivo. Nesta seção, exploramos os conceitos básicos do escalonamento de CPU, os principais algoritmos utilizados e os critérios para selecionar o algoritmo mais adequado para um sistema específico.

![](../images/EscalonamentoDeProcessos1.jpg)

---

### **Conceitos Básicos do Escalonamento de CPU**

1. **O que é Escalonamento de CPU?**
   - O escalonamento de CPU é o processo de decidir qual processo (ou thread) deve receber a CPU para execução em um determinado momento.
   - Em sistemas multiprogramados, vários processos competem pela CPU, e o escalonador (scheduler) é responsável por gerenciar essa competição.

2. **Objetivos do Escalonamento**:
   - **Maximizar a utilização da CPU**: Garantir que a CPU esteja sempre ocupada, evitando ociosidade.
   - **Garantir justiça**: Todos os processos devem ter uma chance justa de usar a CPU.
   - **Minimizar o tempo de resposta**: Reduzir o tempo que os processos levam para serem executados.
   - **Maximizar o throughput**: Executar o maior número possível de processos em um determinado período.

3. **Tipos de Escalonamento**:
   - **Escalonamento de Processos**: Quando o sistema operacional gerencia processos.
   - **Escalonamento de Threads**: Quando o sistema operacional gerencia threads no nível do kernel.

---

### **Algoritmos de Escalonamento de CPU**

Aqui estão alguns dos principais algoritmos de escalonamento de CPU:

#### **1. First-Come, First-Served (FCFS)**
   - **Funcionamento**: O primeiro processo que chega é o primeiro a ser executado.
   - **Vantagem**: Simples de implementar.
   - **Desvantagem**: Pode causar o problema do "convoy effect", onde processos longos atrasam processos curtos.

#### **2. Shortest-Job-First (SJF)**
   - **Funcionamento**: O processo com o menor tempo de execução é selecionado primeiro.
   - **Vantagem**: Minimiza o tempo médio de espera.
   - **Desvantagem**: Difícil de prever o tempo de execução dos processos.

#### **3. Round-Robin (RR)**
   - **Funcionamento**: Cada processo recebe um "quantum" de tempo para executar. Se não terminar, é colocado no final da fila.
   - **Vantagem**: Justo e adequado para sistemas interativos.
   - **Desvantagem**: Pode aumentar o tempo de resposta se o quantum for muito grande ou muito pequeno.

#### **4. Priority Scheduling**
   - **Funcionamento**: Cada processo tem uma prioridade, e o processo com a prioridade mais alta é executado primeiro.
   - **Vantagem**: Permite priorizar processos importantes.
   - **Desvantagem**: Pode causar "starvation" (processos de baixa prioridade nunca são executados).

#### **5. Multilevel Queue Scheduling**
   - **Funcionamento**: Divide os processos em várias filas com prioridades diferentes. Cada fila pode usar um algoritmo de escalonamento diferente.
   - **Vantagem**: Flexível e adequado para sistemas com diferentes tipos de processos.
   - **Desvantagem**: Complexo de implementar.

#### **6. Multilevel Feedback Queue**
   - **Funcionamento**: Similar ao multilevel queue, mas permite que processos mudem de fila com base em seu comportamento.
   - **Vantagem**: Adapta-se dinamicamente ao comportamento dos processos.
   - **Desvantagem**: Ainda mais complexo que o multilevel queue.

---

### **Critérios de Avaliação para Seleção de Algoritmos**

Ao escolher um algoritmo de escalonamento, os seguintes critérios devem ser considerados:

1. **Utilização da CPU**:
   - O algoritmo deve maximizar o uso da CPU, evitando ociosidade.

2. **Throughput**:
   - O número de processos concluídos por unidade de tempo deve ser maximizado.

3. **Tempo de Resposta**:
   - O tempo que um processo leva para começar a ser executado deve ser minimizado.

4. **Tempo de Espera**:
   - O tempo total que um processo passa esperando na fila de prontos deve ser minimizado.

5. **Tempo de Retorno**:
   - O tempo total que um processo leva desde sua submissão até sua conclusão deve ser minimizado.

6. **Justiça**:
   - Todos os processos devem ter uma chance justa de usar a CPU.

7. **Previsibilidade**:
   - O comportamento do algoritmo deve ser previsível para garantir consistência.

---

### **Escalonamento de Threads**

- Em sistemas que suportam threads no nível do kernel, o escalonamento é feito no nível das threads, não dos processos.
- **Benefícios**:
  - Threads são mais leves que processos, permitindo maior concorrência.
  - O escalonamento de threads pode ser mais eficiente, especialmente em sistemas com múltiplos núcleos de CPU.
- **Desafios**:
  - O escalonador deve garantir que threads do mesmo processo sejam tratadas de forma justa.
  - A sincronização entre threads pode ser complexa.
