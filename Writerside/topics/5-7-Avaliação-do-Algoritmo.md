# 5.8 Avaliação de Algoritmos de Escalonamento

Escolher o algoritmo de escalonamento de CPU ideal para um sistema específico é uma tarefa complexa, pois envolve a análise de diversos fatores, como utilização da CPU, tempo de resposta, throughput e justiça. Nesta seção, exploramos os métodos de avaliação de algoritmos de escalonamento, desde modelos determinísticos até simulações e implementações reais.


<note>

**Escolha do Método de Avaliação:**
   - Use **modelagem determinística** para análises rápidas e cenários controlados.
   - Use **modelos de enfileiramento** para análises teóricas e tendências gerais.
   - Use **simulações** para cenários complexos e realistas.
   - A **implementação real** é a mais precisa, mas também a mais cara e complexa.

</note>


---

## **5.8.1 Modelagem Determinística**
A modelagem determinística é uma técnica analítica que utiliza uma carga de trabalho específica para avaliar o desempenho de diferentes algoritmos de escalonamento. Ela é útil para comparar algoritmos em cenários controlados.

### **Exemplo Prático:**
Considere a seguinte carga de trabalho, onde todos os processos chegam no tempo 0:

| Processo | Tempo de Burst (ms) |
|----------|---------------------|
| P1       | 10                  |
| P2       | 29                  |
| P3       | 3                   |
| P4       | 7                   |
| P5       | 12                  |

Avaliamos três algoritmos: **FCFS (First-Come, First-Served)**, **SJF (Shortest Job First)** e **RR (Round Robin com quantum = 10 ms)**.

1. **FCFS:**
   - Ordem de execução: P1 → P2 → P3 → P4 → P5.
   - Tempos de espera: P1 (0 ms), P2 (10 ms), P3 (39 ms), P4 (42 ms), P5 (49 ms).
   - Tempo de espera médio:  $\frac{0 + 10 + 39 + 42 + 49}{5} = 28$  ms.

2. **SJF (não preemptivo):**
   - Ordem de execução: P3 → P4 → P1 → P5 → P2.
   - Tempos de espera: P1 (10 ms), P2 (32 ms), P3 (0 ms), P4 (3 ms), P5 (20 ms).
   - Tempo de espera médio:  $\frac{10 + 32 + 0 + 3 + 20}{5} = 13$  ms.

3. **RR (quantum = 10 ms):**
   - Ordem de execução: P1 → P2 → P3 → P4 → P5 → P2 → P5.
   - Tempos de espera: P1 (0 ms), P2 (32 ms), P3 (20 ms), P4 (23 ms), P5 (40 ms).
   - Tempo de espera médio:  $\frac{0 + 32 + 20 + 23 + 40}{5} = 23$  ms.


<note>

**Trade-offs:**
   - Algoritmos como **SJF** minimizam o tempo de espera, mas podem causar starvation.
   - Algoritmos como **RR** são justos, mas podem aumentar o tempo de resposta.

</note>


### **Conclusão:**
- O **SJF** fornece o menor tempo de espera médio (13 ms).
- O **RR** oferece um equilíbrio entre tempo de resposta e justiça.
- O **FCFS** é o menos eficiente nesse cenário.

<note>

- A modelagem determinística é simples e rápida, mas só se aplica a cargas de trabalho específicas.
- Ela é útil para ilustrar tendências e comparar algoritmos em cenários controlados.

</note>


---

## **5.8.2 Modelos de Enfileiramento**
Os modelos de enfileiramento são usados para analisar sistemas onde os processos chegam e são atendidos de acordo com distribuições de probabilidade. Eles são úteis para calcular métricas como utilização da CPU, tempo médio de espera e tamanho médio da fila.

### **Fórmula de Little:**
A fórmula de Little relaciona o tamanho médio da fila ( $n$ ), o tempo médio de espera ( $W$ ) e a taxa de chegada de processos ( $\lambda$ ):

$$
n = \lambda \times W
$$

### **Exemplo:**
- Se $\lambda = 7$ processos/segundo e  $n = 14$  processos na fila, então:
  $$
  W = \frac{n}{\lambda} = \frac{14}{7} = 2 \text{ segundos.}
  $$

### **Limitações:**
- Os modelos de enfileiramento assumem distribuições matemáticas simplificadas, que podem não refletir cenários reais.
- Eles são mais úteis para análises teóricas do que para previsões precisas.

---

## **5.8.3 Simulações**
As simulações são usadas para avaliar algoritmos de escalonamento em cenários mais realistas. Elas envolvem a criação de um modelo computacional do sistema, onde os processos são gerados de acordo com distribuições de probabilidade ou fitas de rastreamento (trace tapes).

### **Tipos de Simulações:**
1. **Simulação Controlada por Distribuição:**
   - Usa geradores de números aleatórios para criar processos com base em distribuições (exponencial, Poisson, etc.).
   - Útil para cenários genéricos, mas pode não capturar correlações entre eventos.

2. **Simulação com Fitas de Rastreamento:**
   - Usa dados reais coletados de um sistema em operação.
   - Fornece resultados precisos para cenários específicos.

### **Vantagens:**
- Permite a avaliação de algoritmos em cenários complexos e realistas.
- Pode ser usada para comparar múltiplos algoritmos com as mesmas entradas.

### **Desvantagens:**
- Pode ser computacionalmente cara e demorada.
- Requer grande quantidade de dados e espaço de armazenamento.

---

## **5.8.4 Implementação**
A implementação real de um algoritmo de escalonamento em um sistema operacional é a forma mais precisa de avaliar seu desempenho. No entanto, essa abordagem tem desafios significativos.

### **Desafios:**
1. **Custo:**
   - Modificar o sistema operacional para incluir um novo algoritmo é caro e complexo.
   - Requer testes extensivos para garantir que o sistema continue estável.

2. **Reação dos Usuários:**
   - Usuários podem ajustar seu comportamento para se beneficiar do novo algoritmo (por exemplo, dividindo processos longos em menores).
   - Isso pode distorcer os resultados da avaliação.

3. **Ambiente Dinâmico:**
   - O desempenho do algoritmo pode variar conforme o ambiente de trabalho muda.

### **Exemplo:** {id="exemplo_1"}
- No Solaris, o comando `dispadmin` permite ajustar os parâmetros de escalonamento.
- APIs como as do Java, POSIX e Win32 permitem modificar prioridades de threads, mas isso pode não ser eficaz em cenários genéricos.


<note>

**Simulações vs. Implementação:**
   - Simulações são úteis para testes preliminares, mas a implementação real é necessária para validação final.

</note>




---

## **Mapa mental**

```
Avaliação de Algoritmos de Escalonamento
├── **Modelagem Determinística**
│   ├── Carga de trabalho específica
│   ├── Exemplo: FCFS, SJF, RR
│   └── Útil para comparações controladas
│
├── **Modelos de Enfileiramento**
│   ├── Fórmula de Little (n = λ × W)
│   ├── Análise teórica
│   └── Limitações: simplificações matemáticas
│
├── **Simulações**
│   ├── Simulação controlada por distribuição
│   ├── Simulação com fitas de rastreamento
│   ├── Vantagens: cenários realistas
│   └── Desvantagens: custo computacional
│
└── **Implementação**
    ├── Desafios: custo, reação dos usuários
    ├── Exemplo: Solaris (dispadmin)
    └── APIs para ajuste de prioridades
```

---

## **Conclusão** {id="conclus-o_1"}
A escolha do algoritmo de escalonamento ideal depende dos critérios de desempenho desejados (tempo de resposta, throughput, justiça) e do ambiente de trabalho. A combinação de modelagem, simulação e implementação real é essencial para tomar decisões informadas. 

<note>

**Adaptação ao Ambiente:**
   - Algoritmos de escalonamento devem ser ajustados conforme o ambiente de trabalho muda.
   - Sistemas operacionais modernos permitem ajustes dinâmicos (por exemplo, prioridades de threads).

</note>