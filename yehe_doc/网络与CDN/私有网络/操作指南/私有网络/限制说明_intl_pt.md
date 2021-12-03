### Limites de uso
- Os intervalos de IP de VPCs e sub-redes não podem ser modificados após a criação.
- Para cada sub-rede, o Tencent Cloud reserva seus primeiros dois endereços IP e o último endereço IP para fins de redes de IP. Por exemplo, se o CIDR da sub-rede for `172.16.0.0/24`, então os endereços IP reservados pelo Tencent Cloud serão `172.16.0.0`, `172.16.0.1` e `172.16.0.255`.
- Quando você adiciona um CVM a um VPC, o sistema atribui aleatoriamente um endereço IP privado à sua instância dentro da sub-rede especificada e você pode reatribuí-lo para cada CVM depois que os CVMs forem criados.
- Em um VPC, um IP privado do CVM corresponde a um endereço IP público.
- Os CVMs da rede clássica não aceitam a interconexão com os recursos de nuvem no bloco CIDR auxiliar.
- Atualmente, apenas a Cloud Communication Network (CCN) aceita a passagem do bloco CIDR auxiliar. Isso significa que os serviços no bloco CIDR auxiliar não podem se comunicar por meio do VPN Connection, do Direct Connect ou do Peering Connection.

### Limites de cota
| Recurso | Limite/quantidade |
|---------|---------|
| Quantidade de VPCs por região para cada conta | 20 |
| Quantidade de sub-redes por VPC | 100 |
| Quantidade de blocos CIDR auxiliares por VPC | 5 |

>? Se você precisar aumentar a cota, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) para solicitar.

