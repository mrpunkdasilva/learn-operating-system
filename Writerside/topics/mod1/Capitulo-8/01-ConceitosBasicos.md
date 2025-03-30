# 6.2 Conceitos Básicos

## Memória Principal

A memória é um componente essencial para os sistemas computacionais. Sua estrutura básica é composta por uma sequência de **words** (palavras) e **bytes**, cada um com seu próprio endereço único. A **CPU busca as instruções da memória com base no valor do contador de programa**.

Essas instruções podem realizar operações como:
- **Carregamento adicional** de dados.
- **Alocação** em endereços específicos da memória.

Um ciclo comum de execução de instrução envolve as seguintes etapas:
1. **Busca**: A CPU busca uma instrução na memória.
2. **Decodificação**: A instrução é decodificada, e os operandos são buscados na memória.
3. **Execução**: A instrução é executada sobre os operandos.
4. **Armazenamento**: O resultado é guardado de volta na memória.

![Ciclo Comum De Execucao De Instrucao Na Memoria](CicloComumDeExecucaoDeInstrucaoNaMemoria.drawio%20(1).svg)  

**Texto Alternativo**: "Diagrama ilustrando o ciclo comum de execução de instrução na memória, composto por quatro etapas: Busca, Decodificação, Execução e Armazenamento. A CPU busca instruções da memória, decodifica e executa as operações, e armazena os resultados de volta na memória."

> A unidade de memória **enxerga apenas um fluxo de endereços**, sem considerar como eles são gerados (por exemplo, pelo contador de programa).

---

## Hardware Básico

A **memória principal** e os **registradores embutidos** no processador são os **únicos dispositivos de armazenamento diretamente conectados à CPU**. Isso significa que apenas esses componentes podem acessar a CPU diretamente.

Algumas instruções utilizam **endereços de memória** como argumentos, mas não podem acessar **endereços de disco**. Portanto, os dados necessários para a execução das instruções **devem estar na memória principal ou nos registradores** para que a CPU possa processá-los. Caso contrário, os dados precisam ser movidos para a memória antes do processamento.

### Velocidade de Acesso
- **Registradores internos**: Acessíveis em um **único ciclo de clock** da CPU.
- **Memória principal**: O acesso é feito através do **barramento de memória**, podendo levar vários ciclos de clock para ser concluído.

Essa diferença de velocidade pode causar atrasos (stalls) na execução das instruções, já que a CPU pode ficar esperando pelos dados necessários. Para mitigar esse problema, é utilizado um **buffer de memória rápida**, chamado de **08 - Caching**, que fica entre a CPU e a memória principal.

### Proteção e Segurança
Além da velocidade, é crucial garantir a **proteção do sistema operacional** e dos **processos de usuário** uns contra os outros. Essa proteção é implementada em nível de hardware para garantir confiabilidade e segurança.

#### Garantindo Segurança
Para proteger a memória, cada processo tem um **espaço de endereçamento reservado**. Dois registradores são usados para definir os limites desse espaço:
- **Registrador de Base**: Armazena o endereço físico inicial (menor endereço) do processo.
- **Registrador de Limite**: Armazena o endereço físico final (maior endereço) do processo.

Esses registradores garantem que um processo só acesse os endereços de memória dentro do intervalo permitido, prevenindo acessos indevidos.

---

### Mind Map: Conceitos Básicos de Memória

```
Memória
├── Memória Principal
│   ├── Estrutura
│   │   ├── Words e Bytes
│   │   └── Endereços Únicos
│   ├── Ciclo de Execução
│   │   ├── Busca
│   │   ├── Decodificação
│   │   ├── Execução
│   │   └── Armazenamento
│   └── Fluxo de Endereços
│
├── Hardware Básico
│   ├── Componentes Diretos
│   │   ├── Memória Principal
│   │   └── Registradores
│   ├── Velocidade de Acesso
│   │   ├── Registradores: 1 ciclo de clock
│   │   └── Memória Principal: Vários ciclos
│   ├── Buffer de Memória Rápida (Caching)
│   └── Proteção e Segurança
│       ├── Espaço de Endereçamento por Processo
│       ├── Registrador de Base
│       └── Registrador de Limite
│
└── Objetivos
    ├── Execução Eficiente de Programas
    ├── Alocação e Liberação de Memória
    └── Proteção de Dados e Processos
```