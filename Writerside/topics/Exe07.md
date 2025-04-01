# Exercícios Práticos 

### **Exercício 7.1: Exclusão automática vs. persistência de arquivos**
**Abordagem 1 (Exclusão automática)**  
- *Vantagens*:  
  - Economia de espaço em sistemas com muitos usuários temporários (ex: laboratórios acadêmicos)  
  - Redução de "lixo digital" e arquivos obsoletos  
  - Maior privacidade (dados não persistem após sessão)  
- *Desvantagens*:  
  - Risco de perda acidental de arquivos não salvos  
  - Inconveniência para usuários que precisam de persistência  

**Abordagem 2 (Persistência padrão)**  
- *Vantagens*:  
  - Melhor experiência do usuário (não requer ação explícita)  
  - Adequado para ambientes corporativos/compartilhados  
- *Desvantagens*:  
  - Acúmulo de arquivos não gerenciados  
  - Requer políticas de limpeza manual  

---

### **Exercício 7.2: Tipos de arquivo em sistemas operacionais**
**Sistemas com tipos registrados** (ex: Windows):  
- *Prós*:  
  - Associação automática com aplicativos  
  - Validação de estrutura de dados  
- *Contras*:  
  - Complexidade adicional no SO  

**Sistemas sem tipos** (ex: UNIX):  
- *Prós*:  
  - Flexibilidade total para usuários avançados  
  - Simplicidade de implementação  
- *Contras*:  
  - Requer conhecimento do usuário para interpretação  

**Melhor abordagem**: Depende do contexto. Sistemas para usuários finais beneficiam-se de tipos registrados, enquanto sistemas para desenvolvedores preferem flexibilidade.

---

### **Exercício 7.3: Estruturas de dados vs. fluxo de bytes**
**Estruturas definidas** (ex: bancos de dados):  
- *Vantagens*:  
  - Validação automática de formato  
  - Operações otimizadas (ex: busca indexada)  
- *Desvantagens*:  
  - Rigidez de formato  

**Fluxo de bytes** (ex: arquivos texto):  
- *Vantagens*:  
  - Flexibilidade máxima  
  - Portabilidade entre sistemas  
- *Desvantagens*:  
  - Toda lógica de interpretação fica com a aplicação  

---

### **Exercício 7.4: Simulação de diretórios multinível**
**Com nomes ilimitados**:  
- *Solução*: Usar delimitadores (ex: `pasta_subpasta_arquivo`)  
- *Comparação*:  
  - *Prós*: Não requer estrutura complexa  
  - *Contras*: Dificuldade em gerenciar permissões e links  

**Com nomes de 7 caracteres**:  
- *Problema*: Espaço insuficiente para codificar hierarquia complexa  
- *Solução inviável*: Necessário no mínimo 9 chars (`XX_YY_ZZ`) para 3 níveis  

---

### **Exercício 7.5: Operações open() e close()**
**open()**:  
- Verifica permissões  
- Cria entrada na tabela de arquivos abertos  
- Posiciona ponteiro de leitura/escrita  

**close()**:  
- Libera recursos do sistema  
- Garante que buffers sejam gravados  
- Atualiza metadados (timestamp, tamanho)  

*Exemplo*:  
```c
int fd = open("arquivo.txt", O_RDWR); // Aloca recursos
read(fd, buffer, 100); // Operações de E/S
close(fd); // Libera descritor
```

---

### **Exercício 7.6: Acesso sequencial vs. aleatório**
**a) Acesso sequencial**:  
- *Aplicação*: Streaming de vídeo (ex: Netflix)  
- *Motivo*: Dados são consumidos em ordem linear  

**b) Acesso aleatório**:  
- *Aplicação*: Banco de dados de clientes  
- *Motivo*: Busca por registros específicos (ex: CPF)  

---

### **Exercício 7.7: Subdiretórios como arquivos**
**a) Problemas**:  
1. Corrupção acidental da estrutura hierárquica  
2. Injeção de metadados maliciosos  
3. Dificuldade em auditar alterações  

**b) Soluções**:  
1. Exigir privilégios especiais para escrita  
2. Usar formatos estruturados (ex: JSON) para conteúdo  
3. Implementar journaling para rollback  

---

### **Exercício 7.8: Proteção em larga escala**
**a) Solução UNIX**:  
```bash
chmod 750 arquivo       # Dono: rwx, Grupo: r-x, Outros: ---
chgrp grupo_especial arquivo  # Grupo com 4.990 usuários
```

**b) Alternativa melhor**:  
- *ACL (Access Control List)*:  
  ```bash
  setfacl -m g:grupo_especial:r-x arquivo
  setfacl -m u:user_proibido:--- arquivo
  ```
- *Vantagem*: Controle granular sem criar grupos artificiais  

---

### **Exercício 7.9: Listas de acesso vs. listas de usuário**
**Lista por arquivo (ACL tradicional)**:  
- *Vantagens*:  
  - Fácil visualização de quem tem acesso  
  - Ideal para recursos com poucos usuários  

**Lista por usuário (Capabilities)**:  
- *Vantagens*:  
  - Escalável para usuários com muitos arquivos  
  - Delegação mais simples de permissões  
- *Melhor para*: Sistemas distribuídos ou com milhões de arquivos  

*Exemplo*:  
```java
// Abordagem por capacidade
userPermissions.get("alice").add(
   new FilePermission("/data/report.pdf", "READ")
);
```
