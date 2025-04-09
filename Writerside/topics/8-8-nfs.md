# 8.8 NFS (Network File System)

## 1. Visão Geral
- Sistema cliente-servidor para acesso a arquivos remotos via LAN/WAN
- Parte do ONC+ com suporte em UNIX e alguns sistemas PC
- Versão 3 é a mais utilizada (texto descreve esta versão)
- Permite compartilhamento transparente entre máquinas independentes

```mermaid
graph TD
    subgraph "Cliente NFS"
        A[Aplicação] --> B[Cliente NFS]
        B --> C[RPC Cliente]
    end
    
    subgraph "Servidor NFS"
        D[RPC Servidor] --> E[Servidor NFS]
        E --> F[Sistema de Arquivos Local]
    end
    
    C -->|Rede| D
```

## 2. Características Principais

### 2.1 Montagem
- Cliente precisa executar operação de montagem para acessar diretório remoto
- Diretório remoto aparece como subárvore do sistema local
- Suporta montagens em cascata (montar sobre outro sistema já montado)
- Independente de implementação através de RPC e XDR

```mermaid
graph TD
    subgraph "Sistema de Arquivos Local"
        A["/"] --> B[home]
        B --> C[user]
        A --> D[etc]
        A --> E[var]
    end
    
    subgraph "Sistema de Arquivos Remoto"
        F["/export"] --> G[projetos]
        G --> H[docs]
        G --> I[src]
    end
    
    C -->|mount| G
```

### 2.2 Protocolos

#### 2.2.1 Protocolo de Montagem
- Estabelece conexão inicial cliente-servidor
- Gerencia lista de exportação (/etc/dfs/dfstab)
- Mantém controle de montagens ativas

```mermaid
sequenceDiagram
    Cliente->>Servidor: MOUNT(/export/projetos)
    Servidor-->>Cliente: FileHandle
    Cliente->>Cliente: Monta sistema de arquivos
    Cliente->>Servidor: UNMOUNT
    Servidor-->>Cliente: OK
```

#### 2.2.2 Protocolo NFS
- Operações com arquivos remotos
- Servidor é stateless (sem estado)
- Operações síncronas para garantir consistência

```mermaid
mindmap
  root((Protocolo NFS))
    Operações Básicas
      LOOKUP
      READ
      WRITE
      CREATE
      REMOVE
    Características
      Stateless
      Idempotente
      Síncrono
    Cache
      Cliente
        Dados
        Atributos
      Servidor
        Escritas
        Diretórios
```

## 3. Implementação

### 3.1 Operações Principais
```java
public interface NFSOperations {
    FileHandle lookup(String path);
    DirectoryEntry[] readDirectory(FileHandle dir);
    void manipulateLinks(FileHandle link);
    FileAttributes getAttributes(FileHandle file);
    byte[] readFile(FileHandle file, long offset, int length);
    void writeFile(FileHandle file, long offset, byte[] data);
}
```

### 3.2 Características de Implementação

```mermaid
graph TD
    A[Cliente NFS] -->|1. Requisição| B[Cache Local]
    B -->|2. Cache Miss| C[RPC]
    C -->|3. Chamada Remota| D[Servidor NFS]
    D -->|4. Acesso| E[Sistema de Arquivos]
    E -->|5. Dados| D
    D -->|6. Resposta| C
    C -->|7. Atualização| B
    B -->|8. Retorno| A
```

### 3.3 Estrutura de FileHandle

```mermaid
graph LR
    A[FileHandle] --> B[ID do Sistema de Arquivos]
    A --> C[Número do Inode]
    A --> D[Generation Number]
```

## 4. Considerações de Consistência

### 4.1 Modelo de Consistência
- Novos arquivos podem demorar até 30s para serem visíveis
- Não garante semântica UNIX estrita
- Escritas podem não ser imediatamente visíveis em outras máquinas
- Recomenda-se uso de mecanismos externos para controle de concorrência

```mermaid
sequenceDiagram
    participant C1 as Cliente 1
    participant S as Servidor
    participant C2 as Cliente 2
    
    C1->>S: Escrita
    S-->>C1: OK
    Note over C1,C2: Delay de Propagação
    C2->>S: Leitura
    S-->>C2: Dados Antigos
    Note over C2: Cache Expirado
    C2->>S: Leitura
    S-->>C2: Dados Atualizados
```

### 4.2 Estratégias de Cache

```mermaid
mindmap
  root((Cache NFS))
    Cliente
      Dados
        Validade temporal
        Verificação periódica
      Atributos
        TTL curto
        Consistência fraca
    Servidor
      Write-through
        Garantia de persistência
        Overhead de I/O
      Delayed commits
        Melhor performance
        Risco de perda
```

## 5. Segurança e Autenticação

### 5.1 Mecanismos de Segurança
- Autenticação UNIX (UID/GID)
- Kerberos opcional
- Lista de controle de acesso
- Exportação seletiva

```mermaid
graph TD
    A[Cliente] -->|1. Requisição| B[Autenticação]
    B -->|2. Credenciais| C[Autorização]
    C -->|3. Verificação ACL| D[Acesso]
    D -->|4. Permitido| E[Operação NFS]
    D -->|4. Negado| F[Erro]
```