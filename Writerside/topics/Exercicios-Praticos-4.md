# Exercícios Pŕaticos - 4


### **4.1. Prepare dois exemplos de programação nos quais o uso de multithreading ofereça melhor desempenho do que uma solução de única thread.**

#### **Exemplo 1: Download de Múltiplos Arquivos**
- **Problema**: Baixar vários arquivos de um servidor.
- **Solução com Multithreading**:
  - Cada thread pode ser responsável por baixar um arquivo individualmente.
  - Enquanto uma thread espera por I/O (download), outras threads podem continuar trabalhando.
- **Vantagem**: O tempo total de download é reduzido, pois os downloads ocorrem em paralelo.

#### **Exemplo 2: Processamento de Imagens**
- **Problema**: Aplicar filtros (como desfoque ou detecção de bordas) em várias imagens.
- **Solução com Multithreading**:
  - Cada thread processa uma imagem independentemente.
  - O processamento é distribuído entre os núcleos da CPU.
- **Vantagem**: O tempo total de processamento é reduzido, especialmente em CPUs multicore.

---

### **4.2. Quais são as duas diferenças entre as threads em nível de usuário e as threads em nível de kernel? Sob quais circunstâncias um tipo é melhor do que o outro?**

#### **Diferenças**
1. **Gerenciamento**:
   - **Threads em nível de usuário**: Gerenciadas pela aplicação (biblioteca de threads).
   - **Threads em nível de kernel**: Gerenciadas diretamente pelo sistema operacional.

2. **Troca de Contexto**:
   - **Threads em nível de usuário**: A troca de contexto é mais rápida, pois não envolve o kernel.
   - **Threads em nível de kernel**: A troca de contexto é mais lenta, pois envolve uma chamada ao sistema.

#### **Circunstâncias**
- **Threads em nível de usuário**:
  - Melhor para aplicações que exigem muitas threads e trocas de contexto frequentes.
  - Exemplo: Servidores web com alta concorrência.
- **Threads em nível de kernel**:
  - Melhor para aplicações que exigem integração com o sistema operacional (ex.: operações de I/O bloqueantes).
  - Exemplo: Aplicações de tempo real.

---

### **4.3. Descreva as ações tomadas por um kernel para a troca de contexto entre as threads em nível de kernel.**

1. **Salvar o estado da thread atual**:
   - O kernel salva os registradores da CPU, o contador de programa e a pilha da thread que está sendo interrompida.

2. **Escolher a próxima thread**:
   - O escalonador do kernel seleciona a próxima thread a ser executada com base em políticas de escalonamento.

3. **Restaurar o estado da próxima thread**:
   - O kernel restaura os registradores, o contador de programa e a pilha da próxima thread.

4. **Retomar a execução**:
   - A CPU começa a executar a próxima thread a partir do ponto onde ela foi interrompida.

---

### **4.4. Quais recursos são usados quando uma thread é criada? Qual a diferença entre eles e aqueles usados quando um processo é criado?**

#### **Recursos usados na criação de uma thread**
1. **Espaço de endereçamento**: Compartilhado com outras threads do mesmo processo.
2. **Pilha**: Cada thread tem sua própria pilha.
3. **Registradores**: Cada thread tem seu próprio conjunto de registradores.
4. **Contexto de execução**: Inclui o contador de programa e o estado da CPU.

#### **Diferença em relação à criação de um processo**
1. **Espaço de endereçamento**: Um processo tem seu próprio espaço de endereçamento, enquanto threads compartilham o mesmo espaço.
2. **Recursos do sistema**: Processos exigem mais recursos, como tabelas de páginas e descritores de arquivos.
3. **Custo**: Criar uma thread é mais rápido e consome menos recursos do que criar um processo.

---

### **4.5. Suponha que um sistema operacional faça um mapeamento entre as threads em nível de usuário e o kernel, usando o modelo muitos para muitos, e que o mapeamento seja feito por meio de LWPs. Além do mais, o sistema permite que os desenvolvedores criem threads em tempo real para uso em sistemas de tempo real. É necessário vincular uma thread em tempo real a um processo leve? Explique.**

#### **Resposta**
- **Não é necessário** vincular uma thread em tempo real a um LWP (Lightweight Process).
- **Motivo**: Threads em tempo real geralmente exigem controle direto sobre o hardware e o escalonamento, o que é melhor gerenciado pelo kernel sem a camada intermediária de LWPs.
- **Benefício**: Isso permite que as threads em tempo real tenham prioridade máxima e sejam escalonadas de forma preemptiva, garantindo atendimento de prazos rígidos.

---

### **4.6. Um programa Pthread que executa a função de somatório foi apresentado abaixo. Reescreva esse programa em Java.**

#### **Código Original em C (Pthreads)**
```c
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

int sum = 0;

void* runner(void* param) {
    int upper = atoi(param);
    for (int i = 1; i <= upper; i++) {
        sum += i;
    }
    pthread_exit(0);
}

int main(int argc, char* argv[]) {
    pthread_t tid;
    pthread_attr_t attr;

    pthread_attr_init(&attr);
    pthread_create(&tid, &attr, runner, argv[1]);
    pthread_join(tid, NULL);

    printf("Somatório = %d\n", sum);
    return 0;
}
```

#### **Código em Java**
```java
class Somatorio implements Runnable {
    private int upper;
    private int sum = 0;

    public Somatorio(int upper) {
        this.upper = upper;
    }

    public void run() {
        for (int i = 1; i <= upper; i++) {
            sum += i;
        }
        System.out.println("Somatório = " + sum);
    }

    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Uso: java Somatorio <valor>");
            return;
        }

        int upper = Integer.parseInt(args[0]);
        Somatorio task = new Somatorio(upper);
        Thread thread = new Thread(task);
        thread.start();

        try {
            thread.join(); // Espera a thread terminar
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

#### **Explicação**
1. **Classe `Somatorio`**:
   - Implementa a interface `Runnable` para definir a tarefa da thread.
   - O método `run()` calcula o somatório.
2. **Thread Principal**:
   - Cria uma instância de `Somatorio` e uma thread associada.
   - Inicia a thread com `start()` e espera seu término com `join()`.
3. **Saída**:
   - O resultado do somatório é exibido após a thread terminar.
