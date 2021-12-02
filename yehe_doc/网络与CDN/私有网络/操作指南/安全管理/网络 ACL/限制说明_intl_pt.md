### Limites de uso
- Uma ACL de rede pode ser vinculada a várias sub-redes.
- As ACLs de rede não têm estado. Portanto, é necessário definir regras de saída e regras de entrada, respectivamente.
- As ACLs de rede não afetam a intercomunicação de rede privada entre as instâncias do CVM nas sub-redes associadas.

### Limites de cota
| Recurso | Limite |
| -------------- | ----------------- |
| Quantidade de ACLs de rede em cada VPC | 50 |
| Quantidade de regras por ACL de rede | Entrada: 20<br/>Saída: 20 |
| Quantidade de ACLs de rede associadas a cada sub-rede | 1 |

