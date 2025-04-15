# Soluções dos Exercícios de Proteção

## 1. Diferenças entre Listas de Capacidade e Listas de Acesso

### Análise Comparativa

| Característica | Lista de Capacidade | Lista de Acesso |
|----------------|---------------------|-----------------|
| Estrutura | Por usuário/processo | Por objeto |
| Verificação | Rápida | Pode ser lenta |
| Revogação | Complexa | Simples |
| Delegação | Fácil | Difícil |

### Exemplo Prático
```java
// Lista de Capacidade
class CapabilityList {
    Map<User, Set<Permission>> userCapabilities;
}

// Lista de Acesso
class AccessList {
    Map<Resource, Set<UserPermission>> resourceAccess;
}
```

## 2. Sobrescrita de Arquivos Confidenciais

### Propósito
- **Segurança**: Previne recuperação de dados sensíveis
- **Conformidade**: Atende requisitos regulatórios
- **Proteção**: Evita vazamento de informações após exclusão

### Implementação Moderna
```java
public class SecureFileDelete {
    public void secureDelete(File file) {
        RandomNumberGenerator rng = new SecureRandom();
        byte[] randomData = new byte[(int) file.length()];
        
        // Múltiplas passagens de sobrescrita
        for (int i = 0; i < 3; i++) {
            rng.nextBytes(randomData);
            Files.write(file.toPath(), randomData);
        }
        
        file.delete();
    }
}
```

## 3. Estrutura de Anéis e Capacidades

### Relação de Capacidades
- Se j > i, então Capacidades(j) ⊆ Capacidades(i)
- Nível mais interno (0) tem todas as capacidades
- Cada nível externo tem um subconjunto do nível anterior

```ascii
Ring Structure
Ring 0 (Kernel) → Todas as capacidades
    Ring 1 → Subset de Ring 0
        Ring 2 → Subset de Ring 1
            Ring 3 → Subset de Ring 2
```

## 4. Árvore de Processos RC 4000

### Relação Matemática
Para qualquer objeto y:
A(x,y) ⊆ A(z,y) onde z é ancestral de x

### Implementação
```java
class ProcessNode {
    Set<Permission> permissions;
    ProcessNode parent;
    
    boolean canAccess(Resource resource, Permission permission) {
        if (!permissions.contains(permission)) {
            return false;
        }
        return parent == null || parent.canAccess(resource, permission);
    }
}
```

## 5. Problemas com Pilha Compartilhada

### Riscos de Segurança
1. **Buffer Overflow**: Manipulação maliciosa de limites
2. **Race Conditions**: Acesso concorrente não sincronizado
3. **Information Leakage**: Dados residuais entre chamadas

### Solução Segura
```java
class SecureParameterPassing {
    private static class IsolatedStack {
        private final byte[] data;
        private int pointer;
        
        public void push(byte[] params) {
            // Validação de limites
            if (pointer + params.length > data.length) {
                throw new StackOverflowError();
            }
            // Cópia segura
            System.arraycopy(params, 0, data, pointer, params.length);
            pointer += params.length;
        }
    }
}
```

## 6. Proteção Baseada em Números

### Estrutura
- Sistema de proteção hierárquico unidirecional
- Acesso permitido apenas de números maiores para menores

```python
class HierarchicalAccess:
    def can_access(self, process_num: int, object_num: int) -> bool:
        return process_num > object_num
```

## 7. Acesso Limitado por Contagem

### Implementação
```java
public class CountedAccess {
    private Map<ObjectId, Integer> accessCount = new HashMap<>();
    
    public boolean tryAccess(ObjectId objectId) {
        int remaining = accessCount.getOrDefault(objectId, 0);
        if (remaining > 0) {
            accessCount.put(objectId, remaining - 1);
            return true;
        }
        return false;
    }
}
```

## 8. Remoção Automática de Objetos

### Sistema de Garbage Collection
```java
public class AccessRightManager {
    private Map<ObjectId, Set<AccessRight>> rights;
    private Map<ObjectId, WeakReference<Object>> objects;
    
    public void removeRights(ObjectId objectId) {
        rights.remove(objectId);
        WeakReference<Object> ref = objects.get(objectId);
        if (ref != null && ref.get() == null) {
            objects.remove(objectId);
            // Trigger cleanup
            System.gc();
        }
    }
}
```

## 9. Desafios da E/S Direta

### Problemas
1. Acesso direto ao hardware
2. Bypass de mecanismos de proteção
3. Interferência com outros processos

### Mitigação
```java
class IOController {
    private static final Set<Integer> PROTECTED_PORTS = Set.of(80, 443);
    
    public boolean validateIORequest(IORequest request) {
        return !PROTECTED_PORTS.contains(request.getPort()) &&
               isInUserSpace(request.getAddress());
    }
}
```

## 10. Proteção de Listas de Capacidade

### Mecanismos de Proteção
1. **Hardware**: Bits de proteção em memória
2. **Criptografia**: Assinatura digital das capacidades
3. **Kernel**: Mediação de todas as modificações

### Implementação Segura
```java
public class SecureCapabilityList {
    private final byte[] signature;
    private final List<Capability> capabilities;
    
    public boolean verifyIntegrity() {
        byte[] currentSignature = calculateSignature(capabilities);
        return Arrays.equals(signature, currentSignature);
    }
    
    private byte[] calculateSignature(List<Capability> caps) {
        // Implementação de assinatura criptográfica
        return null; // Placeholder
    }
}
```

## Referências Adicionais

### Bibliografia Recomendada
- Tanenbaum, A. S. "Modern Operating Systems"
- Silberschatz, A. "Operating System Concepts"
- Stallings, W. "Operating Systems: Internals and Design Principles"

### Recursos Online
- NIST Special Publications
- OWASP Security Guidelines
- CWE (Common Weakness Enumeration)