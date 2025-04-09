# 8.7 Recuperação de Sistemas de Arquivos

## 1. Visão Geral
- Arquivos e diretórios são mantidos tanto na memória principal quanto no disco
- Falhas podem causar inconsistências nas estruturas de dados do sistema
- Principais desafios: perda de dados e incoerência após falhas

## 2. Tipos de Inconsistências
- Estruturas de diretório corrompidas
- Ponteiros de blocos livres inconsistentes
- Contadores FCB incorretos
- Dados em cache não sincronizados com disco

## 3. Métodos de Recuperação

### 3.1 Verificação de Consistência
```java
public class ConsistencyChecker {
    private static final int STATUS_OK = 0;
    private static final int STATUS_CORRUPTED = 1;
    
    public int verificarConsistencia(String filesystem) {
        // Verifica bit de status
        if (isMetadataUpdateInProgress(filesystem)) {
            return STATUS_CORRUPTED;
        }
        
        // Verifica estruturas
        boolean diretoriosOk = verificarDiretorios();
        boolean blocosOk = verificarBlocosLivres();
        boolean fcbOk = verificarFCBs();
        
        return (diretoriosOk && blocosOk && fcbOk) 
               ? STATUS_OK 
               : STATUS_CORRUPTED;
    }
}
```

### 3.2 Sistema de Arquivos Estruturado em Log
- Usa técnicas de recuperação baseadas em log
- Todas as mudanças de metadados são registradas sequencialmente
- Transações são confirmadas após escrita no log
- Vantagens:
  - Recuperação mais rápida
  - Maior confiabilidade
  - Melhor desempenho em E/S

### 3.3 Backup e Restauração
```java
public class BackupStrategy {
    public enum BackupType {
        FULL,      // Backup completo
        INCREMENTAL // Backup incremental
    }
    
    public void executarBackup(BackupType tipo, String origem, String destino) {
        switch (tipo) {
            case FULL:
                // Copia todos os arquivos
                copiarTodosArquivos(origem, destino);
                break;
            case INCREMENTAL:
                // Copia apenas arquivos modificados desde último backup
                copiarArquivosModificados(origem, destino);
                break;
        }
    }
}
```

## 4. Ciclo de Backup Recomendado
1. Dia 1: Backup completo
2. Dias 2-N: Backups incrementais
3. Repetir ciclo

## 5. Considerações de Implementação
- Armazenamento de backups permanentes em local seguro
- Monitoramento do desgaste das mídias de backup
- Balanceamento entre frequência de backups e recursos necessários