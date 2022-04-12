Os data centers do TencentDB são hospedados em várias localizações globalmente. Essas localizações são conhecidas como regiões. Cada região contém várias zonas de disponibilidade (AZs, na sigla em inglês).
Cada região é uma área geográfica independente contendo várias AZs isoladas. As AZs diferentes na mesma região são conectadas por meio de redes privadas de baixa latência. A Tencent Cloud proporciona a capacidade de distribuir recursos da Tencent Cloud em localizações diferentes. Recomendamos colocar os recursos em AZs diferentes para eliminar pontos únicos de falha que podem levar à indisponibilidade do serviço.

O nome da região e o nome da AZ podem incorporar mais diretamente a cobertura de um data center. A seguinte convenção de nomenclatura é usada para sua conveniência:
- Um nome de região é composto por **região + cidade**. A `região` indica a área geográfica que o data center abrange, já a `cidade` representa a cidade na qual ou perto da qual o data center está localizado.
- Os nomes de AZs utilizam o formato de **cidade + número**.

## Regiões
As regiões da Tencent Cloud são totalmente isoladas. Isso garante a máxima estabilidade entre regiões diferentes e tolerância a falhas. Ao adquirir os serviços da Tencent Cloud, recomendamos escolher a região mais próxima dos seus usuários finais para minimizar a latência de acesso e melhorar a velocidade de download. As operações como iniciar ou exibir as instâncias são executadas no nível da região.
Comunicação de rede privada:

- Os recursos da Tencent Cloud na mesma VPC, região e conta podem se comunicar por meio de uma rede privada. Também é possível acessá-los por meio de [IPs privados](https://intl.cloud.tencent.com/document/product/213/5225).
- As redes de regiões diferentes são totalmente isoladas umas das outras, e os serviços da Tencent Cloud em regiões diferentes não podem se comunicar usando as redes privadas por padrão.
- Os serviços da Tencent Cloud entre regiões diferentes podem se comunicar por meio de [IPs públicos](https://intl.cloud.tencent.com/document/product/213/5224) pela Internet, já aqueles em VPCs diferentes comunicam-se por meio do [CCN](https://intl.cloud.tencent.com/document/product/1003) que é mais rápido e estável.
- Atualmente, o [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) permite o encaminhamento de tráfego dentro da região por padrão. Se você ativar a funcionalidade [vinculação entre regiões](https://intl.cloud.tencent.com/document/product/214/38441), uma instância do CLB poderá ser vinculada a instâncias da CVM em outra região.

## Zonas de disponibilidade
Uma zona de disponibilidade (AZ, na sigla em inglês) é um IDC físico da Tencent Cloud com fonte de alimentação e rede independentes na mesma região. Ela pode garantir a estabilidade dos negócios, pois as falhas (exceto grandes desastres ou falhas de energia) em uma AZ são isoladas sem afetar outras AZs na mesma região. Ao iniciar uma instância em uma zona de disponibilidade independente, os usuários podem proteger suas aplicações de serem afetadas por um ponto único de falha.
Ao iniciar uma instância, você pode escolher qualquer AZ na região especificada. Para alta confiabilidade, você pode adotar uma solução de implantação entre AZs diferentes para garantir que o serviço permaneça disponível quando uma instância em uma única localização falhar. Exemplos de tais soluções incluem o [CLB](https://intl.cloud.tencent.com/document/product/214) e o [EIP](https://intl.cloud.tencent.com/document/product/213/5733).

## Detalhes de regiões e AZs
As regiões e as AZs existentes são as seguintes:
>?Atualmente, o acesso à rede pública é permitido apenas nas seguintes regiões:
>Guangzhou, Xangai, Nanjing, Pequim, Chengdu, Chongqing, Hong Kong (China), Singapura, Seul, Tóquio, Vale do Silício e Frankfurt

### China
<table class="table-striped">
<tbody>
<tr><th>Região</th><th>Zona de disponibilidade</th></tr>
<tr>
<td rowspan="6">Sul da China (Guangzhou)<br>ap-guangzhou</td>
<td>Zona 1 de Guangzhou (esgotada)<br> ap-guangzhou-1</td></tr>	
<tr>
<td>Zona 2 de Guangzhou<br> ap-guangzhou-2</td></tr>
<tr>
<td>Zona 3 de Guangzhou<br> ap-guangzhou-3</td></tr>
<tr>
<td>Zona 4 de Guangzhou<br> ap-guangzhou-4</td></tr>
<tr>
<td>Zona 6 de Guangzhou<br> ap-guangzhou-6</td></tr>
<tr>
<td>Zona 7 de Guangzhou<br> ap-guangzhou-7</td></tr>
<tr>
<td rowspan="5">Leste da China (Xangai)<br>ap-shanghai</td>
<td>Zona 1 de Xangai<br>ap-shanghai-1</td></tr>
<tr>
<td>Zona 2 de Xangai<br>ap-shanghai-2</td></tr>
<tr>
<td>Zona 3 de Xangai<br>ap-shanghai-3</td></tr>
<tr>
<td>Zona 4 de Xangai<br>ap-shanghai-4</td></tr>
<tr>
<td>Zona 5 de Xangai<br>ap-shanghai-5</td></tr>
<td rowspan="3">Leste da China (Nanquim)<br>ap-nanjing</td>
<td>Zona 1 de Nanquim<br>ap-nanjing-1</td></tr>
<tr>
<td>Zona 2 de Nanquim<br>ap-nanjing-2</td></tr>
<tr>
<td>Zona 3 de Nanquim<br>ap-nanjing-3</td></tr>
<tr>
<td rowspan="7">Norte da China (Pequim)<br>ap-beijing</td>
<td>Zona 1 de Pequim<br>ap-beijing-1</td></tr>
<tr>
<td>Zona 2 de Pequim<br>ap-beijing-2</td></tr>
<tr>
<td>Zona 3 de Pequim<br>ap-beijing-3</td></tr>
<tr>
<td>Zona 4 de Pequim<br>ap-beijing-4</td></tr>
<tr>
<td>Zona 5 de Pequim<br>ap-beijing-5</td></tr>
<tr>
<td>Zona 6 de Pequim<br>ap-beijing-6</td></tr>
<tr>
<td>Zona 7 de Pequim<br>ap-beijing-7</td></tr>
<tr>
<td rowspan="2">Sudoeste da China (Chengdu)<br>ap-chengdu</td>
<td>Zona 1 de Chengdu<br>ap-chengdu-1</td></tr>
<tr>
<td>Zona 2 de Chengdu<br>ap-chengdu-2</td></tr>    
<tr>
<td>Sudoeste da China (Chongqing)<br>ap-chongqing</td>
<td>Zona 1 de Chongqing<br>ap-chongqing-1</td></tr>
<tr>
<td rowspan="3">Hong Kong/Macau/Taiwan (Hong Kong, China)<br>ap-hongkong</td>
<td>Zona 1 de Hong Kong (Os nós de Hong Kong abrangem os serviços nas regiões da China de Hong Kong, Macau e Taiwan)<br>ap-hongkong-1</td></tr>
<tr>
<td>Zona 2 de Hong Kong (Os nós de Hong Kong abrangem os serviços nas regiões da China de Hong Kong, Macau e Taiwan)<br>ap-hongkong-2</td></tr>
<tr>
<td>Zona 3 de Hong Kong (Os nós de Hong Kong abrangem os serviços nas regiões da China de Hong Kong, Macau e Taiwan)<br>ap-hongkong-3</td></tr>
</tbody></table>	


### [Outros países e regiões](id:InternationalArea)
<table class="table-striped">
<tbody>
<tr><th>Região</th><th>Zona de disponibilidade</th></tr>
<tr>
<td rowspan="4">Sudeste da Ásia (Singapura)<br>ap-singapore</td>
<td>Zona 1 de Singapura (Os nós em Singapura podem abranger os serviços no Sudeste da Ásia)<br>ap-singapore-1</td></tr>
<tr>
<td>Zona 2 de Singapura (Os nós em Singapura podem abranger os serviços no Sudeste da Ásia)<br>ap-singapore-2</td></tr>
<tr>
<td>Zona 3 de Singapura (Os nós em Singapura podem abranger os serviços no Sudeste da Ásia)<br>ap-singapore-3</td></tr>
<tr>
<td>Zona 4 de Singapura (Os nós em Singapura podem abranger os serviços no Sudeste da Ásia)<br>ap-singapore-4</td></tr>
<tr>
<td>Sudeste da Ásia (Jacarta)<br>ap-jakarta</td>
<td>Zona 1 de Jacarta (Os nós em Jacarta podem abranger os serviços no Sudeste da Ásia)<br>ap-jakarta-1</td></tr>
<tr>
<td rowspan="2">Sudeste da Ásia (Bangkok)<br>ap-bangkok</td>
<td>Zona 1 de Bangkok (Os nós em Bangkok podem abranger os serviços no Sudeste da Ásia)<br>ap-bangkok-1</td>
<tr>
<td>Zona 2 de Bangkok (Os nós em Bangkok podem abranger os serviços no Sudeste da Ásia)<br>ap-bangkok-2</td>
<tr>
<td  rowspan="2">Sul da Ásia (Mumbai)<br>ap-mumbai</td>
<td>Zona 1 de Mumbai (Os nós em Mumbai podem abranger os serviços no Sul da Ásia)<br>ap-mumbai-1</td></tr>
<tr>
<td>Zona 2 de Mumbai (Os nós em Mumbai podem abranger os serviços no Sul da Ásia)<br>ap-mumbai-2</td></tr>		
<tr>
<td  rowspan="2">Nordeste da Ásia (Seul)<br>ap-seoul</td>
<td>Zona 1 de Seul (Os nós em Seul podem abranger os serviços no Nordeste da Ásia)<br>ap-seoul-1</td></tr>
<tr>
<td>Zona 2 de Seul (Os nós em Seul podem abranger os serviços no Nordeste da Ásia)<br>ap-seoul-2</td></tr>
<tr>
<td rowspan="2">Nordeste da Ásia (Tóquio)<br>ap-tokyo</td>
<td>Zona 1 de Tóquio (Os nós em Tóquio podem abranger os serviços no Nordeste da Ásia)<br>ap-tokyo-1</td></tr>
<tr>
<td>Zona 2 de Tóquio (Os nós em Tóquio podem abranger os serviços no Nordeste da Ásia)<br>ap-tokyo-2</td></tr>
<tr>
<td rowspan="2">Oeste dos EUA (Vale do Silício)<br>na-siliconvalley</td>
<td>Zona 1 do Vale do Silício (Os nós do Vale do Silício abrangem os serviços no Oeste dos EUA)<br>na-siliconvalley-1</td></tr>
<tr>
<td>Zona 2 do Vale do Silício (Os nós do Vale do Silício abrangem os serviços no Oeste dos EUA)<br>na-siliconvalley-2</td></tr>
<tr>
<td rowspan="2">Leste dos EUA (Virgínia) <br>na-ashburn</td>
<td>Zona 1 de Virgínia (Os nós de Virgínia abrangem os serviços no Leste dos EUA)<br>na-ashburn-1</td></tr>
<tr>
<td>Zona 2 de Virgínia (Os nós de Virgínia abrangem os serviços no Leste dos EUA)<br>na-ashburn-2</td></tr>
<tr>
<td>América do Norte (Toronto)<br>na-toronto</td>
<td>Zona 1 de Toronto (Os nós de Toronto abrangem os serviços na América do Norte)<br>na-toronto-1</td></tr>
<tr>
<td rowspan="2">Europa (Frankfurt)<br>eu-frankfurt</td>
<td>Zona 1 de Frankfurt (Os nós de Frankfurt abrangem os serviços na Europa)<br>eu-frankfurt-1</td></tr>
<tr>
<td>Zona 2 de Frankfurt (Os nós de Frankfurt abrangem os serviços na Europa)<br>eu-frankfurt-2</td></tr>
<tr>
<td >Europa (Moscou)<br>eu-moscow</td>
<td>Zona 1 de Moscou (Os nós de Moscou abrangem os serviços na Europa)<br>eu-moscow-1</td></tr>
</tbody></table>

## Escolha de regiões e AZs
Ao adquirir os serviços da Tencent Cloud, recomendamos escolher a região mais próxima dos seus usuários finais para minimizar a latência de acesso e melhorar a velocidade de download.
