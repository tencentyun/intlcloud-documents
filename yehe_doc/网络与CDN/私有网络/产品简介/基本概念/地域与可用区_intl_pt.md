## Regiões

### Visão geral

Uma região é a localização física de um IDC. Na Tencent Cloud, as regiões são totalmente isoladas umas das outras, garantindo estabilidade entre as regiões e tolerância a falhas. Recomendamos que você escolha a região mais próxima dos seus usuários finais para minimizar a latência de acesso e melhorar a velocidade de acesso.

Você pode consultar a tabela a seguir ou usar a API [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708) para obter uma lista completa das regiões.

### Características

- As redes de regiões diferentes são totalmente isoladas. Os serviços da Tencent Cloud em regiões diferentes **não podem se comunicar por meio de uma rede privada por padrão**.
- Os serviços da Tencent Cloud entre regiões podem se comunicar uns com os outros por meio de [IPs públicos](https://intl.cloud.tencent.com/document/product/213/5224) pela internet, já os serviços em diferentes VPCs se comunicam por meio do [CCN](https://intl.cloud.tencent.com/document/product/1003), que é mais rápido e estável.
- O [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214) agora permite o encaminhamento de tráfego intrarregião por padrão. Se você ativar a funcionalidade [Vinculação entre regiões 2.0 (Nova)](https://intl.cloud.tencent.com/document/product/214/38441), uma instância do CLB pode ser vinculada a instâncias da CVM em outra região.


## Zonas de disponibilidade

### Visão geral

As zonas de disponibilidade se referem aos data centers físicos da Tencent Cloud cuja energia e rede são independentes entre si dentro da mesma região. Elas foram criadas para garantir que as falhas dentro de uma zona de disponibilidade possam ser isoladas (exceto em caso de desastres em grande escala ou grandes falhas de energia) sem se espalhar para outras zonas, de modo a garantir a estabilidade de seus negócios. Ao iniciar uma instância em uma zona de disponibilidade independente, os usuários podem proteger as aplicações de serem afetadas pelas falhas que ocorrem em um único local.
Você pode consultar a tabela a seguir ou usar a API [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) para obter uma lista completa das zonas de disponibilidade.

### Características

Os serviços da Tencent Cloud no mesmo VPC estão interconectados por meio da rede privada, o que significa que podem se comunicar utilizando [IPs privados](https://intl.cloud.tencent.com/document/product/213/5225), mesmo que estejam em zonas de disponibilidade diferentes da mesma região.
>? Interconexão de rede privada se refere à interconexão de recursos da mesma conta. Os recursos de contas diferentes estão totalmente isolados na rede privada.

<span id="MainlandChina"></span>

## China
<table class="table-striped">
<tbody>
	<tr>
		<th>Região</th>
		<th>AZ</th>
	</tr>
	<tr>
		<td rowspan="6">Sul da China (Guangzhou)<br>ap-guangzhou</td>
		<td>Zona 1 de Guangzhou (esgotada)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>Zona 2 de Guangzhou (esgotada)<br>ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>Zona 3 de Guangzhou </br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Zona 4 de Guangzhou</br>ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>Zona 6 de Guangzhou<br>ap-guangzhou-6</td>
	</tr>
	<tr>
		<td>Zona 7 de Guangzhou<br>ap-guangzhou-7</td>
	</tr>
	<tr>
		<td rowspan="5">Leste da China (Xangai)<br>ap-shanghai</td>
		<td>Zona 1 de Xangai<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>Zona 2 de Xangai</br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Zona 3 de Xangai</br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Zona 4 de Xangai</br>ap-shanghai-4</td>
	</tr>
 <tr>
		<td>Zona 5 de Xangai <br>ap-shanghai-5</td>
	</tr>
		<tr>
			<td rowspan="3">Leste da China (Nanquim)<br>ap-nanjing</td>
			<td>Zona 1 de Nanquim<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Nanquim<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td>Zona 3 de Nanquim<br>ap-nanjing-3</td>
	</tr>
	<tr>
			<td rowspan="7">Norte da China (Pequim)<br>ap-beijing</td>
			<td>Zona 1 de Pequim<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Pequim</br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>Zona 3 de Pequim</br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>Zona 4 de Pequim</br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>Zona 5 de Pequim <br>ap-beijing-5</td>
	</tr>
		<tr>
			<td>Zona 6 de Pequim<br>ap-beijing-6</td>
	</tr>
		<tr>
			<td>Zona 7 de Pequim<br>ap-beijing-7</td>
	</tr>
	<tr>
		<td rowspan="2">Sudoeste da China (Chengdu)<br>ap-chengdu</td>
		<td>Zona 1 de Chengdu<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Chengdu</br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >Sudoeste da China (Chongqing)<br>ap-chongqing</td>
			<td>Zona 1 de Chongqing<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="3">Hong Kong, Macao e Taiwan, China (Hong Kong)<br>ap-hongkong</td>
			<td>Zona 1 de Hong Kong (Os nós em Hong Kong, na China, podem abranger os serviços nas regiões de Hong Kong/Macao/Taiwan)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Hong Kong (Os nós em Hong Kong, na China, podem abranger os serviços nas regiões de Hong Kong/Macao/Taiwan)<br>ap-hongkong-2</td>
	</tr>
	<tr>
			<td>Zona 3 de Hong Kong (Os nós em Hong Kong, na China, podem abranger as regiões de Hong Kong/Macao/Taiwan)<br>ap-hongkong-3</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>
## Outros países e regiões	
<table class="table-striped">
	<tbody>
	<tr>
			<th>Região</th>
			<th>AZ</th>
		</tr>
		<tr>
			<td  rowspan="3">Sudeste da Ásia (Singapura)<br>ap-singapore</td>
			<td>Zona 1 de Singapura (Os nós em Singapura podem abranger o Sudeste da Ásia)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Singapura (Os nós em Singapura podem abranger o Sudeste da Ásia)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>Zona 3 de Singapura (Os nós em Singapura podem abranger o Sudeste da Ásia)<br>ap-singapore-3</td>
		</tr>
		<tr>
			<td  rowspan="2">Nordeste da Ásia (Seul)<br>ap-seoul</td>
			<td>Zona 1 de Seul (Os nós em Seul podem abranger o Nordeste da Ásia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Seul (Os nós em Seul podem abranger o Nordeste da Ásia)<br>ap-seoul-2</td>
		</tr>
		<tr >
			<td rowspan="2">Nordeste da Ásia (Tóquio)<br>ap-tokyo</td>
			<td>Zona 1 de Tóquio (Os nós em Tóquio podem abranger o Nordeste da Ásia)<br>ap-tokyo-1</td>
		</tr>
		 <tr>
			<td>Zona 2 de Tóquio (Os nós em Tóquio podem abranger o Nordeste da Ásia)<br>ap-tokyo-2</td>
		</tr>
       <tr>
			<td  rowspan="2">Sul da Ásia (Mumbai)<br>ap-mumbai</td>
			<td>Zona 1 de Mumbai (Os nós em Mumbai podem abranger o Sul da Ásia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Zona 2 de Mumbai (Os nós em Mumbai podem abranger o Sul da Ásia) <br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td rowspan="2">Sudeste da Ásia (Bangkok)<br>ap-bangkok</td>
				 <td>Zona 1 de Bangkok (Os nós em Bangkok podem abranger o Sudeste da Ásia)<br>ap-bangkok-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Bangkok (Os nós em Bangkok podem abranger o Sudeste da Ásia)<br>ap-bangkok-2</td>
		</tr>
			<td>América do Norte (Toronto)<br>na-toronto</td>
			<td>Zona 1 de Toronto (Os nós em Toronto podem abranger a América do Norte)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">Oeste dos EUA (Vale do Silício)<br>na-siliconvalley</td>
			<td>Zona 1 do Vale do Silício (Os nós no Vale do Silício podem abranger o Oeste dos EUA)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Zona 2 do Vale do Silício (Os nós no Vale do Silício podem abranger o Oeste dos EUA)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">Leste dos EUA (Virgínia)<br>na-ashburn</td>
			<td>Zona 1 de Virgínia (Os nós em Virgínia podem abranger o Leste dos EUA)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Virgínia (Os nós em Virgínia podem abranger o Leste dos EUA)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td rowspan="2">Europa (Frankfurt)<br>eu-frankfurt</td>
			<td>Zona 1 de Frankfurt (Os nós em Frankfurt podem abranger a Europa)<br>eu-frankfurt-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Frankfurt (Os nós em Frankfurt podem abranger a Europa)<br>eu-frankfurt-2</td>
		</tr>
		<td >Europa (Moscou)<br>eu-moscow</td>
		<td>Zona 1 de Moscou (Os nós em Moscou podem abranger a Europa)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## Como escolher as regiões e as zonas de disponibilidade

Ao escolher uma região e zona de disponibilidade, leve em consideração o seguinte:
- A sua localização, a localização dos seus usuários e a região das instâncias da CVM.
Recomendamos que opte pela região mais próxima aos seus usuários ao adquirir as instâncias da CVM, para minimizar a latência e melhorar a velocidade de acesso.
- Outros serviços da Tencent Cloud que você usa.
Ao escolher outros serviços da Tencent Cloud, recomendamos que você tente locar todos na mesma região e zona de disponibilidade para permitir que se comuniquem entre si por meio da rede privada, reduzindo a latência e aumentando a velocidade de acesso.
- Alta disponibilidade e recuperação de desastres.
Mesmo que você tenha apenas um VPC, ainda recomendamos que você implante seus negócios em zonas de disponibilidade diferentes, para evitar um ponto único de falha e habilitar a recuperação de desastres entre AZ.
- Pode haver latência de rede entre zonas de disponibilidade diferentes. Recomendamos que você avalie as necessidades da sua empresa e encontre o equilíbrio ideal entre a alta disponibilidade e a baixa latência.

## Disponibilidade de recursos

A tabela a seguir descreve quais recursos da Tencent Cloud são globais, regionais e específicos às zonas de disponibilidade.

<table>
	<tr><th width="14%">Recurso</th><th>Formato da ID do recurso<br>String <Resource Abbreviation>-8 dígitos com números e letras</th><th>Tipo</th><th>Descrição</th></tr>
	<tbody>
	<tr>
	  <td>Conta do usuário</td>
	  <td>Sem limite</td>
	  <td>Globalmente exclusivo</td>
	  <td>Os usuários podem utilizar a mesma conta para acessar os recursos da Tencent Cloud no mundo todo.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">Chaves SSH</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>Global</td>
	  <td>Os usuários podem usar uma chave SSH para vincular uma CVM em qualquer região na conta.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">Instâncias da CVM</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>As instâncias da CVM são específicas de uma zona de disponibilidade</td>
	  <td>Os usuários só podem criar uma instância da CVM em uma zona de disponibilidade específica.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941">Imagens personalizadas</a></td>
	  <td>img-xxxxxxxx</td>
	  <td>Regional</td>
	   <td>Os usuários podem criar uma imagem personalizada para instâncias que podem ser usadas em zonas de disponibilidade diferentes da mesma região. Copie a imagem personalizada para outras regiões usando a função de cópia de imagem para usá-la nessas regiões. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIPs</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>Podem ser usados em várias zonas de disponibilidade em uma região</td>
	  <td>Os EIPs (IPs elásticos) só podem ser criados em uma região e associados a instâncias na mesma região.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">Grupos de segurança</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>Podem ser usados em várias zonas de disponibilidade em uma região</td>
	  <td>O grupo de segurança é criado em uma determinada região e só pode ser associado a uma instância na mesma região. A Tencent Cloud cria automaticamente três grupos de segurança padrão para os usuários. </td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">Cloud Block Storage</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>Os discos do CBS são específicos de uma zona de disponibilidade.</td>
	  <td>Os usuários só podem criar um disco do Cloud Block Storage em uma zona de disponibilidade específica e montá-lo em instâncias na mesma zona de disponibilidade.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">Snapshots</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>Podem ser usados em várias zonas de disponibilidade em uma região</td>
	  <td>Um snapshot criado a partir de um disco em nuvem pode ser utilizado para outros fins (como criar discos em nuvem) nessa região.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">Cloud Load Balancer</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>Pode ser usado em várias zonas de disponibilidade em uma região</td>
	  <td>O Cloud Load Balancer pode ser associado a CVMs em zonas de disponibilidade diferentes de uma única região para encaminhamento de tráfego.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>Disponível em várias zonas de disponibilidade de uma única região</td>
	  <td>Um VPC em uma região pode ter recursos criados em zonas de disponibilidade diferentes da região.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">Sub-redes</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>As sub-redes são específicas de uma zona de disponibilidade.</td>
	  <td>Os usuários não podem criar sub-redes entre zonas de disponibilidade diferentes.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/31810">Tabelas de rotas</a> </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>Podem ser usadas em várias zonas de disponibilidade em uma região</td>
	  <td>Ao criar uma tabela de rotas, os usuários precisam especificar um VPC. Portanto, as tabelas de rotas também são regionais.</td>
	</tr>
	</tbody>
</table>


## Referências

### Migração de uma instância para outra zona de disponibilidade

Não é possível alterar a zona de disponibilidade de uma instância que já foi iniciada, mas o usuário pode migrá-la para outra zona de disponibilidade por outros meios. O processo de migração envolve a criação de uma imagem personalizada da instância original, o uso da imagem personalizada para iniciar uma instância em uma nova zona de disponibilidade e a atualização da configuração da nova instância.
1. Crie uma imagem personalizada da instância de origem.  [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942)
2. Se o [ambiente de rede](https://intl.cloud.tencent.com/document/product/213/5227) da instância atual for VPC e o endereço IP privado precisar ser retido após a migração, você precisará excluir a sub-rede na zona de disponibilidade atual e criar uma sub-rede na nova zona de disponibilidade com o mesmo intervalo de endereços IP da sub-rede original. Atenção: só é possível excluir uma sub-rede quando não houver instâncias disponíveis nela. Portanto, todas as instâncias da sub-rede atual devem ser migradas para a nova sub-rede.
3. Crie uma nova instância na nova zona de disponibilidade usando a imagem personalizada criada. Você pode escolher o mesmo tipo e configuração da instância original ou escolher novas configurações. Para mais informações, consulte [Criação de instâncias pela página de aquisição da CVM](https://intl.cloud.tencent.com/document/product/213/4855).
4. Se a instância de origem estiver associada a um EIP, desassocie o EIP e associe-o à nova instância. Para mais informações sobre como desligar uma instância, consulte [Desligar instâncias](https://intl.cloud.tencent.com/document/product/213/4929).
5. Para mais informações, consulte [Encerramento de instâncias](https://intl.cloud.tencent.com/document/product/213/4930). 

### Cópia de imagens para outras regiões

O atributo Região é diferenciado para todos os comportamentos, como ativar e exibir instâncias por usuários. Se a imagem da instância que os usuários precisam ativar não existir na região, a imagem precisará ser copiada para a região atual.  [Cópia de imagens](https://intl.cloud.tencent.com/document/product/213/4943)
