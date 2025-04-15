# Cryptography as a Security Tool

## 1. Context and Need

### Isolated Computer
- OS can reliably determine sender/receiver of all process communication
- Complete control over communication channels
- Direct trust relationship

### Networked Environment
- Cannot immediately verify message origins
- Network addresses are unreliable for security
- Problems:
  - Address spoofing
  - Multiple receivers
  - Router interception

## 2. Key Challenges

### Trust Issues
- Cannot rely on network addresses for authentication
- Source addresses can be falsified
- Destination addresses don't guarantee exclusive reception

### Security Requirements
- Request validation without trusting source
- Data protection without knowing all receivers
- Message integrity verification

## 3. Cryptographic Solution

### Core Concept
- Based on keys (secrets)
- Selectively distributed to network computers
- Computationally infeasible to derive from public information

### Key Functions
1. **Origin Verification**
   - Verify message creator has specific key
   - Authentication of source

2. **Destination Control**
   - Encode messages for specific key holders
   - Restrict message access

### Advantages
- More reliable than network addresses
- Independent of network infrastructure
- Mathematically verifiable security