### Limites de uso
- Não é possível modificar os intervalos de IP da VPC e da sub-rede após a criação.
- Para cada sub-rede, a Tencent Cloud reserva os seus dois primeiros IPs e o último para as redes de IP. Por exemplo, se o [bloco CIDR da sub-rede](https://intl.cloud.tencent.com/document/product/215/4925) for `172.16.0.0/24`, então `172.16.0.0`, `172.16.0.1` e `172.16.0.255` serão reservados pela Tencent Cloud.
- Ao adicionar uma CVM a uma VPC, a instância será atribuída aleatoriamente a um IP privado de uma sub-rede especificada. Você pode reatribuir um IP privado a ele depois que a instância for criada.
- Em uma VPC, um IP privado da CVM corresponde a um endereço IP público.
- As CVMs baseadas na rede clássica não podem se interconectar com os recursos de nuvem no bloco CIDR secundário.
- Um Peering Connection não aceita blocos CIDR secundários.
- O Cloud Connect Network, o gateway do VPN e o gateway do Direct Connect padrão aceitam os blocos CIDR secundários.

### Limites de cota
| Recurso | Limites |
|---------|---------|
| Quantidade de instâncias da VPC por região e conta | 20 | 
| Quantidade de sub-redes por VPC | 100 | 
| Quantidade de blocos CIDR secundários por VPC | 5 |

>?Se você quiser aumentar a cota, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1) para solicitar.
