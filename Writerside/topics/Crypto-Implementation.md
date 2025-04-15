# Implementação da Criptografia em Redes

## 1. Organização em Camadas

- Protocolos organizados em camadas hierárquicas
- Cada camada atua como cliente da camada inferior
- Baseado no modelo ISO de 7 camadas
- Exemplo de fluxo:
  ```
  TCP (Transporte) -> IP (Rede) -> Enlace de Dados
  ```

## 2. Níveis de Implementação

### 2.1 Camada de Transporte
- SSL/TLS
- Proteção fim-a-fim

### 2.2 Camada de Rede
- IPSec
- VPNs (Redes Privadas Virtuais)
- Criptografia de pacotes IP

## 3. Considerações de Implementação

### 3.1 Vantagens da Implementação em Camadas Baixas
- Maior abrangência de proteção
- Proteção automática das camadas superiores
- Exemplo: IPSec protege tanto TCP quanto dados

### 3.2 Limitações
- Pode ser insuficiente para requisitos específicos
- Necessidade de autenticação adicional em nível de aplicação
- Exemplo: necessidade de senha mesmo com IPSec

## 4. Exemplo: SSL/TLS

### 4.1 Componentes Principais
```java
class SSLConnection {
    private byte[] clientRandom;    // 28 bytes
    private byte[] serverRandom;    // 28 bytes
    private byte[] preMasterSecret; // 46 bytes
    private byte[] masterSecret;    // 48 bytes
    
    private Certificate serverCert;
    private KeyPair sessionKeys;
}
```

### 4.2 Processo de Handshake
1. Cliente envia random
2. Servidor responde com random + certificado
3. Cliente verifica certificado
4. Estabelecimento de chave de sessão
5. Comunicação segura