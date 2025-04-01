# 7.1.2 Operação de Arquivos

## **1. Introdução Conceitual (Teoria)**
Um arquivo é uma abstração que representa dados persistentes armazenados em disco. O sistema operacional fornece operações básicas para manipulação, análogas a ações em um mundo Minecraft. Vamos explorar:

### **Analogia Minecraft-Arquivos**
| **Computação**          | **Minecraft**               |
|-------------------------|-----------------------------|
| Sistema de Arquivos     | Mundo do jogo               |
| Arquivo                 | Bloco/Baú                   |
| Operações (create, read)| Craftar/Olhar blocos        |
| Ponteiro de arquivo     | Cursor do jogador           |
| File Lock               | Trancar baú                 |

## **2. Operações Básicas (Teoria + Java)**

### **2.1 Criar Arquivos**
**Teoria**: Aloca espaço no disco e registra no diretório.

**Java**:
```java
Path filePath = Paths.get("inventario.txt");
try {
    Files.createFile(filePath); // Cria arquivo vazio
    System.out.println("Arquivo criado (Bloco craftado!)");
} catch (IOException e) {
    System.err.println("Falha ao criar: " + e.getMessage());
}
```

**Passo a passo**:
1. `Paths.get()` define o local do arquivo
2. `Files.createFile()` realiza a criação física
3. Tratamento de exceções é obrigatório

### **2.2 Escrever em Arquivos**
**Teoria**: Adiciona dados movendo o ponteiro de escrita.

**Java**:
```java
try (FileWriter writer = new FileWriter("inventario.txt")) {
    writer.write("Diamante: 5\nOuro: 10\n"); 
    System.out.println("Dados escritos (Bloco modificado!)");
} catch (IOException e) {
    // Tratamento de erro
}
```

**Melhor prática**:
- Usar `try-with-resources` para fechamento automático
- `\n` para quebra de linha universal

### **2.3 Ler Arquivos**
**Teoria**: Acessa dados sequencialmente ou aleatoriamente.

**Java (leitura linha-a-linha)**:
```java
try (BufferedReader br = Files.newBufferedReader(filePath)) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println("Baú contém: " + line);
    }
}
```

**Métodos alternativos**:
- `Files.readAllLines()` (carrega tudo em memória)
- `Files.lines()` (stream Java 8+)

### **2.4 Seek (Posicionamento)**
**Teoria**: Move o ponteiro sem realizar E/S.

**Java**:
```java
try (RandomAccessFile raf = new RandomAccessFile("inventario.txt", "r")) {
    raf.seek(10); // Posiciona no 11º byte
    byte[] data = new byte[4];
    raf.read(data);
    System.out.println("Conteúdo: " + new String(data));
}
```

**Aplicações**:
- Acesso a registros de tamanho fixo
- Edição parcial de arquivos grandes

### **2.5 Exclusão e Truncamento**
**Java (Excluir)**:
```java
Files.deleteIfExists(filePath); // Remove o arquivo
```

**Java (Truncar)**:
```java
try (RandomAccessFile raf = new RandomAccessFile(filePath, "rw")) {
    raf.setLength(0); // Zera o conteúdo
}
```

## **3. Controle de Acesso (File Locks)**

### **3.1 Tipos de Locks**
| **Tipo**       | **Java**                     | **Minecraft**            |
|----------------|-----------------------------|--------------------------|
| Exclusivo      | `FileChannel.lock()`        | Baú trancado para edição |
| Compartilhado  | `FileChannel.lock(0, Long.MAX_VALUE, true)` | Vários jogadores lendo |

### **3.2 Implementação Profissional**
```java
try (RandomAccessFile file = new RandomAccessFile("registro.txt", "rw");
     FileChannel channel = file.getChannel();
     FileLock lock = channel.lock()) { // Lock exclusivo
    
    // Região crítica
    file.write("Dado exclusivo".getBytes());
    Thread.sleep(2000); // Simula processamento
    
} catch (Exception e) {
    // Tratamento refinado
}
```

**Boas práticas**:
1. Sempre liberar locks (usar try-with-resources)
2. Documentar políticas de acesso
3. Implementar timeouts para evitar deadlocks

## **4. Arquitetura Avançada**

### **4.1 Tabela de Arquivos Abertos**
```java
// Simulação da tabela do SO
Map<String, FileEntry> openFilesTable = new ConcurrentHashMap<>();

class FileEntry {
    int openCount;
    long filePointer;
    FileLock activeLock;
}
```

### **4.2 Gerenciamento de Ponteiros**
```java
// Controle multi-processo
public class FilePointerTracker {
    private static final Map<Long, Map<String, Long>> processPointers = new HashMap<>();
    
    public static void updatePointer(long pid, String file, long position) {
        processPointers.computeIfAbsent(pid, k -> new HashMap<>())
                     .put(file, position);
    }
}
```

## **5. Caso Completo: Sistema de Inventário**
```java
public class InventoryManager {
    private static final Path INVENTORY_FILE = Paths.get("/world/inventory.dat");
    
    public synchronized void addItem(String item, int quantity) {
        try (FileLock lock = acquireLock()) {
            // Lógica de escrita thread-safe
            Files.write(INVENTORY_FILE, 
                       (item + ":" + quantity + "\n").getBytes(),
                       StandardOpenOption.APPEND);
        }
    }
    
    private FileLock acquireLock() throws IOException {
        FileChannel channel = FileChannel.open(INVENTORY_FILE, 
                                     StandardOpenOption.WRITE);
        return channel.tryLock(10, TimeUnit.SECONDS); // Timeout
    }
}
```

## **6. Exercícios Práticos**

1. **Desafio de Seek**:
   ```java
   // Implemente uma função que busca a palavra "Diamante" no arquivo
   // e retorna sua posição (dica: use RandomAccessFile)
   ```

2. **Sistema de Backup**:
   ```java
   // Crie um método que copia apenas as linhas modificadas
   // nos últimos 7 dias (dica: BasicFileAttributes)
   ```

3. **Lock Distribuído**:
   ```java
   // Implemente um lock que funciona entre múltiplas JVMs
   // usando arquivos como semáforos
   ```

## **7. Referências Críticas**

1. **Problemas Comuns**:
   - Esquecer de fechar recursos (vazamentos)
   - Deadlocks por ordem incorreta de locks
   - Race conditions em operações não atômicas

2. **Soluções**:
   ```java
   // Padrão de projeto para operações atômicas
   public interface FileOperation<T> {
       T execute(RandomAccessFile file) throws IOException;
   }
   
   public class AtomicFileExecutor {
       public <T> T execute(String path, FileOperation<T> op) {
           // Implementação com retry e locks
       }
   }
   ```




```
Operações de Arquivo (Minecraft)
│
├── Operações Básicas
│   ├── Criar (Craftar bloco)
│   ├── Escrever (Modificar bloco)
│   ├── Ler (Olhar baú)
│   ├── Seek (Mover cursor)
│   ├── Excluir (Quebrar bloco)
│   └── Truncar (Resetar bloco)
│
├── Arquivos Abertos (Hotbar)
│   ├── Ponteiro (Posição atual)
│   ├── Contador (Usos simultâneos)
│   └── Modo de Acesso (Permissões)
│
└── Locks (Proteção)
    ├── Compartilhado (Leitura múltipla)
    ├── Exclusivo (Escrita única)
    ├── Obrigatório (SO força bloqueio)
    └── Consultivo (Programas cooperam)
```
