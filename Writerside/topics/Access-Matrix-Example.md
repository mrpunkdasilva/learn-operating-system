# Exemplo de Matriz de Acesso

## Matriz Básica

| Domínio | F1 | F2 | F3 | Impressora |
|---------|----|----|----| ---------- |
| D1      | read | - | read | - |
| D2      | - | read* | - | print |
| D3      | - | - | - | - |
| D4      | read,write | - | read,write | - |

## Matriz com Direitos de Domínio

| Domínio | F1 | F2 | F3 | D1 | D2 | D3 | D4 |
|---------|----|----|----|----|----|----|----| 
| D1      | read | - | read | - | switch | - | - |
| D2      | - | read* | - | - | - | switch | switch |
| D3      | - | - | - | - | - | - | - |
| D4      | read,write | - | read,write | switch | - | - | - |

## Matriz com Direitos de Proprietário

| Domínio | F1 | F2 | F3 |
|---------|----|----|----| 
| D1      | owner,read | - | - |
| D2      | - | owner,read | owner |
| D3      | - | - | - |
| D4      | read,write | - | read,write |