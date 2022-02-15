Os data centers do TencentDB são hospedados em vários locais em todo o mundo. Esses locais são conhecidos como regiões. Cada região é uma área geográfica independente.
O nome da região pode incorporar mais diretamente a cobertura de um data center. Para sua conveniência, a seguinte convenção de nomenclatura é usada:
Um nome de região é composto pela **região + cidade**. A `região` indica a área geográfica que o data center abrange, já a `cidade` representa a cidade na qual, ou perto da qual, o data center está localizado.


>?O TcaplusDB não divide instâncias por zonas de disponibilidade.

## Como selecionar a região
As regiões do Tencent Cloud são completamente isoladas. Isso garante a máxima estabilidade entre regiões e tolerância a falhas. Ao adquirir os serviços do Tencent Cloud, recomendamos escolher a região mais próxima dos seus usuários finais para minimizar a latência de acesso e aumentar a velocidade de download. Operações como iniciar ou exibir instâncias são executadas no nível da região.
Observações sobre a comunicação de rede privada:
- Os recursos do Tencent Cloud na mesma região (na mesma conta e no mesmo VPC) comunicam entre si pela rede privada. Eles também podem ser acessados por meio de [IPs privados](https://intl.cloud.tencent.com/document/product/213/5225).
- As redes de regiões diferentes são totalmente isoladas umas das outras, e os serviços do Tencent Cloud em regiões diferentes não podem se comunicar uns com os outros por meio de uma rede privada por padrão.
- Os serviços do Tencent Cloud em regiões diferentes podem se comunicar uns com os outros, acessando a internet por meio de [IPs públicos](https://intl.cloud.tencent.com/document/product/213/5224), e os serviços Tencent Cloud em VPCs diferentes podem se comunicar por meio do [CCN](https://intl.cloud.tencent.com/document/product/1003), que é mais rápido e estável.


## Lista de regiões
O TcaplusDB divide as instâncias apenas por região e está disponível nas seguintes regiões:

### China
| Região | Identificador | 
|---------|---------|
| Leste da China (Xangai) | ap-shanghai | 
| Hong Kong/Macau/Taiwan (Hong Kong, China) | ap-hongkong |

### Outros países/regiões
| Região | Identificador | 
|---------|---------|
| Sudeste da Ásia-Pacífico (Singapura) | ap-singapore | 
| Nordeste da Ásia-Pacífico (Seul) | ap-seoul |
| Nordeste da Ásia-Pacífico (Tóquio) | ap-tokyo |
| Oeste dos EUA (Vale do Silício) | na-siliconvalley |
| Leste dos EUA (Virgínia) | na-ashburn |
| Europa (Frankfurt) | eu-frankfurt |


