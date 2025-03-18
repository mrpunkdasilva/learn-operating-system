# Exercicios Práticos


## **Exercício 5.1**
**Pergunta:**  
Um algoritmo de escalonamento de CPU determina uma ordem para a execução de seus processos escalonados. Com $ n$ processos a serem escalonados em um processador, quantos escalonamentos diferentes são possíveis? Mostre uma fórmula em termos de $ n$.

**Resposta:**  
O número de escalonamentos possíveis é dado pelo número de permutações dos $ n$ processos. Isso ocorre porque cada ordem de execução dos processos é uma permutação única. A fórmula para o número de permutações de $ n$ elementos é:

$$
n! = n \times (n-1) \times (n-2) \times \dots \times 1
$$

**Explicação:**  
- Se houver 3 processos ($n = 3$), os escalonamentos possíveis são $ 3! = 6$:  
  (P1, P2, P3), (P1, P3, P2), (P2, P1, P3), (P2, P3, P1), (P3, P1, P2), (P3, P2, P1).  
- Esse conceito é importante porque mostra que, à medida que o número de processos aumenta, o número de possíveis escalonamentos cresce rapidamente (fatorialmente).

---

## **Exercício 5.2**
**Pergunta:**  
Explique a diferença entre escalonamento preemptivo e não preemptivo.

**Resposta:**  
- **Escalonamento preemptivo:** O sistema operacional pode interromper um processo em execução e substituí-lo por outro, mesmo que o processo atual não tenha terminado. Isso permite maior flexibilidade e melhor uso da CPU, especialmente em sistemas com múltiplos processos.  
- **Escalonamento não preemptivo:** Uma vez que um processo começa a executar, ele só é interrompido quando termina ou bloqueia (por exemplo, para E/S). Isso pode levar a tempos de resposta mais longos, especialmente se processos longos estiverem em execução.

**Explicação:**  
- O escalonamento preemptivo é comum em sistemas modernos, pois permite priorizar processos mais importantes ou curtos.  
- O escalonamento não preemptivo é mais simples, mas pode causar problemas como o "efeito convoy", onde processos curtos ficam esperando processos longos terminarem.

---

## **Exercício 5.3**
**Pergunta:**  
Suponha que os processos a seguir cheguem para execução nos tempos indicados. Cada processo será executado por um período listado. Use escalonamento não preemptivo e responda as perguntas.

| Processo | Tempo de chegada | Tempo de burst |
|----------|------------------|----------------|
| P1       | 0,0              | 8              |
| P2       | 0,4              | 4              |
| P3       | 1,0              | 1              |

a. Qual é o tempo de turnaround médio para estes processos com o algoritmo de escalonamento FCFS?  
b. Qual é o tempo de turnaround médio para estes processos com o algoritmo de escalonamento SJF?  
c. Calcule o tempo de turnaround médio se a CPU ficar ociosa por uma unidade e depois usar SJF.

**Resposta:**  
a. **FCFS (First-Come, First-Served):**  
   - Ordem de execução: P1 (0-8), P2 (8-12), P3 (12-13).  
   - Turnaround: P1 = 8, P2 = 12 - 0,4 = 11,6, P3 = 13 - 1,0 = 12.  
   - Média: $(8 + 11,6 + 12) / 3 = 10,53$.

b. **SJF (Shortest Job First):**  
   - Ordem de execução: P1 (0-8), P3 (8-9), P2 (9-13).  
   - Turnaround: P1 = 8, P2 = 13 - 0,4 = 12,6, P3 = 9 - 1,0 = 8.  
   - Média: $(8 + 12,6 + 8) / 3 = 9,53$.

c. **SJF com CPU ociosa:**  
   - CPU fica ociosa até t = 1.  
   - Ordem de execução: P3 (1-2), P2 (2-6), P1 (6-14).  
   - Turnaround: P1 = 14 - 0 = 14, P2 = 6 - 0,4 = 5,6, P3 = 2 - 1,0 = 1.  
   - Média: $(14 + 5,6 + 1) / 3 = 6,87$.

**Explicação:**  
- O FCFS é simples, mas pode não ser eficiente.  
- O SJF melhora o tempo de turnaround médio, mas depende do conhecimento prévio dos tempos de burst.  
- A ociosidade inicial pode melhorar ainda mais o desempenho, mas aumenta o tempo de espera dos processos que chegam antes.

---

## **Exercício 5.4**
**Pergunta:**  
Qual é a vantagem de haver diferentes tamanhos de quantum de tempo em diferentes níveis de um sistema de enfileiramento multilevel queue?

**Resposta:**  
A vantagem é permitir que processos curtos sejam executados rapidamente (com quanta menores) e processos longos recebam mais tempo de CPU (com quanta maiores). Isso melhora o tempo de resposta para processos interativos e a eficiência para processos de longa duração.

**Explicação:**  
- Filas com quanta menores são ideais para processos interativos (como editores de texto).  
- Filas com quanta maiores são ideais para processos de longa duração (como compiladores).  
- Isso equilibra justiça e eficiência.

---

## **Exercício 5.5**
**Pergunta:**  
Que relação existe entre os seguintes pares de conjuntos de algoritmos?  
a. Prioridade e SJF  
b. Multilevel feedback queues e FCFS  
c. Prioridade e FCFS  
d. RR e SJF

**Resposta:**  
a. **Prioridade e SJF:** O SJF pode ser visto como um caso especial de prioridade, onde a prioridade é inversamente proporcional ao tempo de burst.  
b. **Multilevel feedback queues e FCFS:** O FCFS pode ser uma das filas em um sistema multilevel feedback queue.  
c. **Prioridade e FCFS:** O FCFS pode ser implementado como um caso especial de prioridade, onde todos os processos têm a mesma prioridade.  
d. **RR e SJF:** Não há relação direta, pois o RR é baseado em tempo, enquanto o SJF é baseado no tempo de burst.

**Explicação:**  
- Essas relações mostram como os algoritmos de escalonamento podem ser generalizados ou combinados.

---

## **Exercício 5.6**
**Pergunta:**  
Por que um algoritmo que favorece processos que usaram menos tempo de CPU recentemente favorece programas voltados para E/S e evita starvation?

**Resposta:**  
- Programas voltados para E/S passam a maior parte do tempo esperando por operações de E/S, usando pouco tempo de CPU. Assim, eles são frequentemente favorecidos por esse algoritmo.  
- Programas voltados para CPU, embora possam esperar mais, não sofrem starvation porque, eventualmente, seu tempo de uso recente de CPU se torna baixo, e eles são escalonados novamente.

**Explicação:**  
- Esse equilíbrio é importante para sistemas interativos, onde a responsividade é crucial.

---

## **Exercício 5.7**
**Pergunta:**  
Distinção entre escalonamento PCS e SCS.

**Resposta:**  
- **PCS (Process-Contention Scope):** Escalonamento de threads no nível do processo, onde o sistema operacional não interfere.  
- **SCS (System-Contention Scope):** Escalonamento de threads no nível do sistema, onde o sistema operacional gerencia a competição por recursos.

**Explicação:**  
- PCS é comum em threads de usuário, enquanto SCS é comum em threads de kernel.

---

## **Exercício 5.8**
**Pergunta:**  
É necessário vincular uma thread em tempo real a um LWP?

**Resposta:**  
Sim, threads em tempo real precisam ser vinculadas a LWPs (Lightweight Processes) para garantir que tenham prioridade e recursos adequados, especialmente em sistemas com mapeamento muitos-para-muitos.

**Explicação:**  
- LWPs atuam como intermediários entre threads de usuário e threads de kernel, garantindo que threads em tempo real sejam tratadas com a urgência necessária.

--- 

Espero que essas explicações ajudem a entender os conceitos e as respostas! 😊