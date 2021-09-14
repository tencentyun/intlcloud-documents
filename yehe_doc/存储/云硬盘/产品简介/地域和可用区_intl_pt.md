## Regiões
Uma região é a localização física de um IDC. No Tencent Cloud, regiões diferentes são totalmente isoladas, garantindo a estabilidade entre regiões e a tolerância a falhas. Ao adquirir os serviços do Tencent Cloud, recomendamos escolher a região mais próxima dos seus usuários finais para minimizar a latência de acesso e aumentar a velocidade de download.
As regiões têm estas características:
- As redes de regiões diferentes são totalmente isoladas. Os serviços do Tencent Cloud em regiões diferentes **não podem se comunicar por meio de uma rede privada por padrão**.
- Os serviços do Tencent Cloud em regiões diferentes podem acessar a internet por meio de [IPs públicos](https://intl.cloud.tencent.com/document/product/213/5224), já aqueles em um VPC podem usar a [conexão de emparelhamento](https://intl.cloud.tencent.com/document/product/553) para se comunicarem entre si por meio da rede de alta velocidade do Tencent Cloud, que é mais rápida e estável.
- O [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) agora é compatível com encaminhamento de tráfego intra-região por padrão. Se a [vinculação entre regiões](https://intl.cloud.tencent.com/document/product/214/12014) estiver habilitada, uma instância do CLB pode ser vinculada a instâncias do CVM em outra região.

## Zonas de disponibilidade
Uma zona de disponibilidade (AZ, do inglês "availability zone") é um IDC físico do Tencent Cloud com fonte de alimentação independente e recurso de rede em uma única região. Pode garantir a estabilidade da empresa, já que as falhas (exceto as causadas por desastres de grande escala ou grandes falhas de energia) em uma AZ são isoladas sem afetar outras AZs na mesma região. Ao iniciar uma instância em uma zona de disponibilidade independente, os usuários podem proteger seus aplicativos de serem afetados por um ponto único de falha.
As zonas de disponibilidade têm estas características:
- Os serviços do Tencent Cloud da mesma conta no mesmo [VPC](https://intl.cloud.tencent.com/document/product/215) são interconectados pela rede privada, o que significa que podem se comunicar usando [IPs privados](https://intl.cloud.tencent.com/document/product/213/5225), mesmo que estejam em zonas de disponibilidade diferentes.
- Os recursos em contas diferentes do Tencent Cloud são específicos da zona de disponibilidade, o que significa que não podem se comunicar por uma rede privada, mesmo se estiverem na mesma região.

<span id="MainlandChina"></span>
## China
<table class="table-striped">
<tbody>
	<tr>
		<th>Região</th>
		<th>Zona de disponibilidade</th>
	</tr>
	<tr>
		<td rowspan="5">Sul da China (Guangzhou)<br>ap-guangzhou</td>
		<td>Zona 1 de Guangzhou (esgotada)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>Zona 2 de Guangzhou (esgotada)<br>ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>Zona 3 de Guangzhou<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Zona 4 de Guangzhou<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>Zona 6 de Guangzhou<br> ap-guangzhou-6</td>
	</tr>
	<tr>
		<td rowspan="5">Leste da China (Xangai) <br>ap-shanghai</td>
		<td>Zona 1 de Xangai<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>Zona 2 de Xangai<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Zona 3 de Xangai<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Zona 4 de Xangai<br>ap-shanghai-4</td>
	</tr>
 <tr>
		<td>Zona 5 de Xangai<br>ap-shanghai-5</td>
	</tr>
		<tr>
			<td rowspan="3">Norte da China (Nanquim)<br>ap-nanjing</td>
			<td>Zona 1 de Nanquim<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Nanquim<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td>Zona 3 de Nanquim<br>ap-nanjing-3</td>
	</tr>
	<tr>
			<td rowspan="5">Norte da China (Pequim) <br>ap-beijing</td>
			<td>Zona 1 de Pequim<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Pequim<br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>Zona 3 de Pequim<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>Zona 4 de Pequim<br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>Zona 5 de Pequim<br>ap-beijing-5</td>
	</tr>
	<tr>
		<td rowspan="2">Sudoeste da China (Chengdu)<br>ap-chengdu</td>
		<td>Zona 1 de Chengdu<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Chengdu<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >Sudoeste da China (Chongqing)<br>ap-chongqing</td>
			<td>Zona 1 de Chongqing<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="2">Hong Kong/Macau/Taiwan (Hong Kong, China) <br>ap-hongkong</td>
			<td>Zona 1 de Hong Kong (Os nós de Hong Kong abrangem os serviços nas regiões da China de Hong Kong, Macau e Taiwan)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Hong Kong (Os nós de Hong Kong abrangem os serviços nas regiões da China de Hong Kong, Macau e Taiwan)<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>
## Outros países e regiões	
<table class="table-striped">
	<tbody>
	<tr>
			<th>Região</th>
			<th>Zona de disponibilidade</th>
		</tr>
		<tr>
			<td  rowspan="2">Sudeste da Ásia (Singapura)<br>ap-singapore</td>
			<td>Zona 1 de Singapura (Os nós de Singapura abrangem os serviços no Sudeste da Ásia)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Singapura (Os nós de Singapura abrangem os serviços no Sudeste da Ásia)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td  rowspan="2">Nordeste da Ásia (Seul)<br>ap-seoul</td>
			<td>Zona 1 de Seul (Os nós de Seul abrangem os serviços no Nordeste da Ásia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Seul (Os nós de Seul abrangem os serviços no Nordeste da Ásia)<br>ap-seoul-2</td>
		</tr>
		<tr>
			<td >Nordeste da Ásia (Tóquio)<br>ap-tokyo</td>
			<td>Zona 1 de Tóquio (Os nós de Tóquio abrangem os serviços no Nordeste da Ásia)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td  rowspan="2">Sul da Ásia (Mumbai)<br>ap-mumbai</td>
			<td>Zona 1 de Mumbai (Os nós de Mumbai abrangem os serviços no Sul da Ásia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Zona 2 de Mumbai (Os nós de Mumbai abrangem os serviços no Sul da Ásia)<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td >Sudeste da Ásia (Bangkok)<br>ap-bangkok </td>
				 <td >Zona 1 de Bangkok (Os nós de Bangkok abrangem os serviços no Sudeste da Ásia)<br>ap-bangkok-1</td>
		<tr>
			<td>América do Norte (Toronto)<br>na-toronto</td>
			<td>Zona 1 de Toronto (Os nós de Toronto abrangem os serviços na América do Norte)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">Oeste dos EUA (Vale do Silício)<br>na-siliconvalley</td>
			<td>Zona 1 do Vale do Silício (Os nós de Vale do Silício abrangem os serviços no Oeste dos EUA)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Zona 2 do Vale do Silício (Os nós de Vale do Silício abrangem os serviços no Oeste dos EUA)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">Leste dos EUA (Virgínia) <br>na-ashburn</td>
			<td>Zona 1 de Virgínia (Os nós de Virgínia abrangem os serviços no leste dos EUA)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Virgínia (Os nós de Virgínia abrangem os serviços no leste dos EUA)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>Europa (Frankfurt) <br>eu-frankfurt</td>
			<td>Zona 1 de Frankfurt (Os nós de Frankfurt abrangem os serviços na Europa)<br>eu-frankfurt-1</td>
		</tr>
		<td >Europa (Moscou)<br>eu-moscow</td>
		<td>Zona 1 de Moscou (Os nós de Moscou abrangem os serviços na Europa)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## Como escolher as regiões e as zonas de disponibilidade
Ao selecionar uma região e uma zona de disponibilidade, considere estes fatores:
- Os limites de onde será possível montar os discos em nuvem. Só é possível montar um disco em nuvem em um CVM na mesma zona de disponibilidade.
- A região do CVM em que o disco em nuvem será usado, sua localização e a localização de seus usuários. Recomendamos que você escolha a região mais próxima de seus usuários ao adquirir os serviços do Tencent Cloud para minimizar a latência de acesso e aumentar a velocidade de acesso.
- A relação entre o CVM no qual o disco em nuvem será usado e os outros serviços do Tencent Cloud. Recomendamos que, ao escolher os outros produtos do Tencent Cloud, você tente localizá-los todos na mesma região e zona de disponibilidade para permitir que eles se comuniquem entre si pela rede privada, reduzindo a latência de acesso e aumentando as velocidades de acesso.
- Considerações de alta disponibilidade empresarial e recuperação de desastres. Mesmo que você tenha apenas um VPC, ainda assim recomendamos que mobilize seus negócios em diferentes zonas de disponibilidade, para evitar um ponto único de falha e habilitar a recuperação de desastres entre AZ.
- Pode haver latência de rede mais alta entre zonas de disponibilidade diferentes. Recomendamos que você avalie as necessidades da sua empresa e encontre o equilíbrio ideal entre a alta disponibilidade e a baixa latência.

## Operações relevantes
Ações como o uso e a visualização de discos em nuvem são específicas da zona de disponibilidade e da região. Para migrar facilmente dados e serviços para outras regiões ou criar um sistema de recuperação de desastres entre regiões, basta copiar snapshots para outras regiões. Para obter mais informações, consulte [Replicação de snapshots entre regiões](https://intl.cloud.tencent.com/document/product/362/31623).
