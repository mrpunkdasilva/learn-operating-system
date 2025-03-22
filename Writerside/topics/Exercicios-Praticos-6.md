# Exercícios Práticos 6


### **Exercício 6.1: Cite duas diferenças entre endereços lógicos e físicos.**

#### Explicação:
- **Endereço Lógico**: É o endereço que o programa usa. Ele é gerado pela CPU e existe no "mundo" do programa. O programa não sabe onde ele está realmente na memória física.
- **Endereço Físico**: É o endereço real na memória RAM. Ele é o local onde os dados ou instruções estão armazenados fisicamente.

#### Diferenças:
1. **Visibilidade**:
   - O **endereço lógico** é visível para o programa.
   - O **endereço físico** é visível apenas para o hardware (CPU e sistema operacional).
2. **Mapeamento**:
   - O endereço lógico é mapeado para o endereço físico pelo sistema operacional (usando tabelas de páginas ou segmentação).
   - O endereço físico é fixo e não muda, enquanto o endereço lógico pode variar dependendo do processo.

#### Exemplo:
- Imagine que você está em um prédio com vários apartamentos (memória física). O endereço lógico é como o número do apartamento que você vê no seu contrato, enquanto o endereço físico é a localização real do apartamento no prédio.

---

### **Exercício 6.2: Discussão sobre registradores de base-limite para código e dados.**

#### Explicação: {id="explica-o_5"}
- O sistema tem dois pares de registradores de base-limite:
  - Um para **código** (instruções).
  - Outro para **dados**.
- Esses registradores são **somente leitura**, o que permite que programas sejam compartilhados entre usuários.

#### Vantagens:
1. **Compartilhamento de Código**:
   - Vários usuários podem rodar o mesmo programa sem precisar de cópias separadas do código.
2. **Proteção**:
   - O código é somente leitura, então ninguém pode alterá-lo acidentalmente ou maliciosamente.

#### Desvantagens:
1. **Complexidade**:
   - O sistema precisa gerenciar dois pares de registradores, o que aumenta a complexidade do hardware.
2. **Limitação de Flexibilidade**:
   - Se o programa precisar modificar o código (por exemplo, em linguagens que permitem auto-modificação), isso não será possível.

#### Exemplo: {id="exemplo_4"}
- Imagine que você tem um livro (código) que várias pessoas podem ler, mas ninguém pode escrever nele. Isso é bom para compartilhar, mas ruim se você quiser fazer anotações.

---

### **Exercício 6.3: Por que os tamanhos de página são sempre potências de 2?**

#### Explicação: {id="explica-o_4"}
- Os tamanhos de página são potências de 2 (por exemplo, 4 KB, 8 KB, 16 KB) porque isso facilita o cálculo de endereços e a divisão da memória.

#### Motivos:
1. **Facilidade de Cálculo**:
   - Em binário, potências de 2 são representadas por um único bit "1" seguido de zeros (ex: 4 KB = 2^12).
   - Isso simplifica a divisão do endereço lógico em número da página e deslocamento.
2. **Alinhamento de Memória**:
   - Potências de 2 garantem que as páginas comecem e terminem em endereços alinhados, o que melhora a eficiência do hardware.

#### Exemplo: {id="exemplo_3"}
- Se o tamanho da página for 4 KB (2^12), os últimos 12 bits do endereço lógico são o deslocamento, e os bits restantes são o número da página. Isso é fácil de calcular em hardware.

---

### **Exercício 6.4: Espaço de endereços lógicos e físicos.**

#### Dados:
- **Páginas lógicas**: 64.
- **Tamanho de cada página**: 1.024 words.
- **Quadros físicos**: 32.

#### a) Quantos bits existem no endereço lógico?
- **Número de páginas**: 64 = 2^6 → 6 bits para o número da página.
- **Tamanho da página**: 1.024 words = 2^10 → 10 bits para o deslocamento.
- **Total**: 6 + 10 = **16 bits**.

#### b) Quantos bits existem no endereço físico?
- **Número de quadros**: 32 = 2^5 → 5 bits para o número do quadro.
- **Tamanho do quadro**: 1.024 words = 2^10 → 10 bits para o deslocamento.
- **Total**: 5 + 10 = **15 bits**.

---

### **Exercício 6.5: Compartilhamento de páginas.**

#### Explicação: {id="explica-o_2"}
- Se duas entradas na tabela de páginas apontam para o mesmo quadro físico, isso significa que duas páginas lógicas compartilham a mesma página física.

#### Vantagens: {id="vantagens_1"}
1. **Economia de Memória**:
   - Reduz a quantidade de memória usada, pois a mesma página física é compartilhada.
2. **Cópia Rápida**:
   - Para copiar uma grande quantidade de memória, basta apontar as entradas da tabela de páginas para o mesmo quadro físico, sem precisar copiar os dados.

#### Efeito de Atualização:
- Se um byte em uma página for atualizado, a outra página também será afetada, pois ambas compartilham o mesmo quadro físico.

#### Exemplo: {id="exemplo_2"}
- Imagine que duas pessoas estão lendo o mesmo livro. Se uma pessoa escrever algo no livro, a outra pessoa verá a alteração.

---

### **Exercício 6.6: Compartilhamento de segmentos entre processos.**

#### Explicação: {id="explica-o_3"}
- Um segmento pode pertencer ao espaço de endereços de dois processos se ambos mapearem o mesmo segmento físico em suas tabelas de segmentos.

#### Mecanismo:
1. **Tabela de Segmentos Compartilhada**:
   - Ambos os processos têm entradas em suas tabelas de segmentos que apontam para o mesmo segmento físico.
2. **Proteção**:
   - O sistema operacional garante que os processos tenham permissão para acessar o segmento compartilhado.

#### Exemplo: {id="exemplo_1"}
- Dois programas podem compartilhar uma biblioteca de funções (como uma biblioteca matemática), sem precisar de cópias separadas.

---

### **Exercício 6.7: Compartilhamento de segmentos e páginas.**

#### a) Compartilhamento de segmentos com vínculo estático:
- O sistema pode usar um **identificador único** para cada segmento compartilhado, em vez de depender do número do segmento. Assim, processos podem compartilhar segmentos sem precisar ter os mesmos números de segmento.

#### b) Compartilhamento de páginas:
- O sistema pode usar uma **tabela de páginas invertida**, onde várias entradas podem apontar para o mesmo quadro físico. Isso permite que páginas sejam compartilhadas sem precisar ter os mesmos números de página.

---

### **Exercício 6.8: Proteção de memória no IBM/370.**

#### Explicação: {id="explica-o_1"}
- O IBM/370 usa **chaves de 4 bits** para proteger a memória. Cada bloco de 2 KB tem uma chave, e a CPU também tem uma chave. Acesso é permitido apenas se as chaves forem iguais ou se uma delas for zero.

#### Esquemas compatíveis:
- **a) Máquina pura**: Sim, pois a proteção é feita por hardware.
- **b) Sistema monousuário**: Sim, mas a proteção é desnecessária.
- **c) Multiprogramação com processos fixos**: Sim, cada processo pode ter uma chave única.
- **d) Multiprogramação com processos variáveis**: Sim, mas a gestão de chaves pode ser complexa.
- **e) Paginação**: Sim, as chaves podem ser usadas para proteger páginas.
- **f) Segmentação**: Sim, as chaves podem ser usadas para proteger segmentos.
