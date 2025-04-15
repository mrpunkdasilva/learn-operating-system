# Criptografia e Codificação

## Conceitos Básicos

A codificação é usada para restringir os possíveis receptores de uma mensagem, permitindo que apenas computadores com determinada chave possam ler a mensagem.

### Componentes de um Algoritmo de Codificação

- Conjunto K de chaves
- Conjunto M de mensagens 
- Conjunto C de cifras
- Função E: K → (M → C) para gerar cifras
- Função D: K → (C → M) para decodificar cifras

## Tipos Principais

### 1. Codificação Simétrica

- Mesma chave usada para codificar e decodificar
- Exemplos:
  - DES (Data Encryption Standard) - 56 bits
  - Triple DES - 168 bits
  - AES (Advanced Encryption Standard) - 128, 192 ou 256 bits
  - Twofish
  - RC4 (cifra de stream)

### 2. Codificação Assimétrica 

- Usa pares de chaves diferentes (pública/privada)
- Exemplo principal: RSA
- Mais lento que algoritmos simétricos
- Usado principalmente para:
  - Autenticação
  - Confidencialidade
  - Distribuição de chaves

## Autenticação

- Complementar à codificação
- Restringe emissores possíveis
- Usa funções hash (MD5, SHA-1)
- Tipos:
  - MAC (Message Authentication Code)
  - Assinatura Digital

## Distribuição de Chaves

### Desafios
- Entrega segura de chaves simétricas
- Gerenciamento de múltiplas chaves
- Proteção contra ataques "homem no meio"

### Soluções
- Certificados digitais
- Autoridades de certificação
- Formato X.509