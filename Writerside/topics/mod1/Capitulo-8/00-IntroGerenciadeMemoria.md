# 6.1 Introdução - Gerenciamento de Memória

> Confira os slides para esse Domus: [](https://www.canva.com/design/DAGieRxxG70/22yP_5cv_423fYTQGbqMGA/edit?utm_content=DAGieRxxG70&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

Os sistemas computacionais têm como **principal finalidade a execução de programas**. Para que esses programas possam ser executados, é essencial que estejam armazenados na memória, pelo menos parcialmente, durante sua execução.

![Estrutura de Armazenamento](003 - Estrutura de Armazenamento.png)

Dessa forma, a importância do gerenciamento de memória reside no fato de que, além de fornecer espaço para armazenamento, é necessário um sistema eficiente para administrar as demandas relacionadas à memória. Esse sistema deve garantir que os recursos de memória sejam alocados, liberados e otimizados de maneira adequada, permitindo que múltiplos programas sejam executados de forma eficaz e sem conflitos.


![Estrutura de Armazenamento Hierarquia Dispositivos De Armazenamento](003 - Estrutura de Armazenamento-Hierarquia-Dispositivos-De-Armazenamento.png)

---

```
Gerenciamento de Memória
├── Objetivo Principal
│   ├── Execução de Programas
│   └── Alocação Eficiente
├── Componentes
│   ├── Memória Principal (RAM)
│   ├── Memória Secundária (HD/SSD)
│   └── Memória Cache
├── Funções
│   ├── Alocação de Memória
│   ├── Liberação de Memória
│   ├── Otimização de Uso
│   └── Proteção de Memória
├── Técnicas
│   ├── Paginação
│   ├── Segmentação
│   ├── Memória Virtual
│   └── Alocação Contígua/Não Contígua
├── Desafios
│   ├── Fragmentação
│   ├── Sobrecarga de Gerenciamento
│   └── Concorrência de Processos
└── Benefícios
    ├── Melhor Desempenho
    ├── Execução Simultânea
    └── Uso Eficiente de Hardware
```
