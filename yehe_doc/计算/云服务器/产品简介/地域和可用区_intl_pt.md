## Regiões

### Visão geral

Uma região é a localização física de um IDC. No Tencent Cloud, as regiões são totalmente isoladas umas das outras, garantindo a estabilidade entre regiões e a tolerância a falhas. Recomendamos que você opte pela região mais próxima aos seus usuários para minimizar a latência e melhorar a velocidade de acesso.

Você pode consultar a tabela a seguir ou usar a API [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708) para obter uma lista completa das regiões.

### Características

- As redes de regiões diferentes são totalmente isoladas. Os serviços do Tencent Cloud em regiões diferentes **não podem se comunicar por meio de uma rede privada por padrão**.
- Os serviços do Tencent Cloud entre regiões podem se comunicar uns com os outros por meio de [IPs públicos](https://intl.cloud.tencent.com/document/product/213/5224) pela internet, já os serviços em diferentes VPCs comunicam-se por meio de [CCN](https://intl.cloud.tencent.com/document/product/1003), que é mais rápido e estável.
- O [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214) agora é compatível com encaminhamento de tráfego intra-região por padrão. Se você habilitar a funcionalidade [vinculação entre regiões](https://intl.cloud.tencent.com/document/product/214/38441), a vinculação entre regiões do CLB e das instâncias do CVM será permitida.

## Zonas de disponibilidade

### Visão geral

Uma zona de disponibilidade (AZ) é um IDC físico do Tencent Cloud com fonte de alimentação independente e rede na mesma região. Pode garantir a estabilidade da empresa, já que as falhas (exceto as causadas por grandes desastres ou falhas de energia) em uma AZ são isoladas sem afetar outras AZs na mesma região. Ao iniciar uma instância em uma zona de disponibilidade independente, os usuários podem proteger seus aplicativos de serem afetados por um ponto único de falha.
Você pode consultar a tabela a seguir ou usar a API [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) para obter uma lista completa de AZs.

### Características

Os serviços do Tencent Cloud no mesmo VPC estão interconectados por meio da rede privada, o que significa que podem se comunicar utilizando [IPs privados](https://intl.cloud.tencent.com/document/product/213/5225), mesmo que estejam em AZs diferentes da mesma região.
>?Interconexão de rede privada refere-se à interconexão de recursos da mesma conta. Os recursos de contas diferentes estão totalmente isolados na rede privada.
>

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
		<td>Zona 3 de Guangzhou<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Zona 4 de Guangzhou<br>ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>Zona 6 de Guangzhou<br>ap-guangzhou-6</td>
	</tr>
	<tr>
               <td>Zona 7 de Guangzhou<br>ap-guangzhou-7</td>
	</tr>
	<tr>
		<td rowspan="5">Leste da China (Xangai)<br>ap-xangai</td>
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
			<td>Zona 1 de Pequim(esgotada)<br>ap-beijing-1</td>
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
			<td>Zona 2 de Chengdu<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >Sudoeste da China (Chongqing)<br>ap-chongqing</td>
			<td>Zona 1 de Chongqing<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="3">Hong Kong, Macao e Taiwan, China (Hong Kong)<br>ap-hongkong</td>
			<td>Zona 1 de Hong Kong (Os nós em Hong Kong, na China, podem abranger as regiões de Hong Kong/Macao/Taiwan)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Zona 2 de Hong Kong (Os nós em Hong Kong, na China, podem abranger as regiões de Hong Kong/Macao/Taiwan)<br>ap-hongkong-2</td>
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
			<td  rowspan="4">Sudeste da Ásia (Singapura)<br>ap-singapore</td>
			<td>Zona 1 de Singapura (Os nós em Singapura podem abranger o Sudeste da Ásia)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Singapura (Os nós em Singapura podem abranger o Sudeste da Ásia)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>Zona 3 de Singapura (Os nós em Singapura podem abranger os serviços no Sudeste da Ásia)<br>ap-singapore-3</td>
		</tr>
		<tr>
                        <td>Zona 4 de Singapura (Os nós em Singapura podem abranger os serviços no Sudeste da Ásia)<br>ap-singapore-4</td>
		</tr>
		<tr>
			<td  rowspan="2">Sudeste da Ásia (Jacarta)<br>ap-jakarta</td>
			<td>Zona 1 de Jacarta (Os nós em Jacarta podem abranger o Sudeste da Ásia)<br>ap-jakarta-1</td>
		</tr>
		<tr>
                        <td>Zona 2 de Jacarta (Os nós em Jacarta podem abranger o Sudeste da Ásia)<br>ap-jakarta-2</td>
		</tr>
		<tr>
			<td  rowspan="2">Nordeste da Ásia (Seul)<br>ap-seoul</td>
			<td>Zona 1 de Seul (Os nós em Seul podem abranger o Nordeste da Ásia)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Zona 2 de Seul (Os nós em Seul podem abranger o Nordeste da Ásia)<br>ap-seoul-2</td>
		</tr>
		<tr>
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
		  	<td rowspan="2" >Sudeste da Ásia (Bangkok)<br>ap-bangkok </td>
				 <td >Zona 1 de Bangkok (Os nós em Bangkok podem abranger o Sudeste da Ásia-Pacífico)<br>ap-bangkok-1</td>
		</tr>
		<tr>
                                  <td >Zona 2 de Bangkok (Os nós em Bangkok podem abranger o Sudeste da Ásia-Pacífico)<br>ap-bangkok-2</td>
		</tr>
		<tr>
			<td>América do Norte (Toronto)<br>na-toronto</td>
			<td>Zona 1 de Toronto (Os nós em Toronto podem abranger a América do Norte)<br>na-toronto-1</td>
		</tr>
		<tr>
                        <td>América do  Sul (Saopaulo)<br>sa-saopaulo</td>
			<td>Zona 1 de Saopaulo (Os nós em Saopaulo podem abranger a América do Sul)<br>sa-saopaulo-1</td>
		</tr>
		<tr>
			<td rowspan="2">Oeste dos EUA (Vale do Silício)<br>na-siliconvalley</td>
			<td>Zona 1 do Vale do Silício (Os nós no Vale do Silício podem abranger o Oeste dos EUA)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Zona 2 do Vale do Silício (Os nós no Vale do Silício podem abranger o Oeste dos EUA)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">Leste dos EUA (Virgínia) <br>na-ashburn</td>
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
                <tr>
	</tbody>
</table>

## Como escolher as regiões e as zonas de disponibilidade

Ao escolher uma região e zona de disponibilidade, leve em consideração o seguinte:
- Sua localização, a localização dos seus usuários e a região das instâncias do CVM.
Recomendamos que opte pela região mais próxima aos seus usuários ao adquirir as instâncias do CVM, para minimizar a latência e melhorar a velocidade de acesso.
- Outros serviços do Tencent Cloud que você usa.
Ao escolher outros serviços do Tencent Cloud, recomendamos que você tente locar todos na mesma região e zona de disponibilidade para permitir que se comuniquem entre si por meio da rede privada, reduzindo a latência e aumentando a velocidade de acesso.
- Alta disponibilidade e recuperação de desastres.
Mesmo que você tenha apenas um VPC, ainda recomendamos que você mobilize seus negócios em diferentes zonas de disponibilidade, para evitar um ponto único de falha e habilitar a recuperação de desastres entre AZ.
- Pode haver latência de rede entre diferentes zonas de disponibilidade. Recomendamos que você avalie as necessidades da sua empresa e encontre o equilíbrio ideal entre a alta disponibilidade e a baixa latência.
- Se precisar de acesso a instâncias do CVM em outros países ou regiões, recomendamos que escolha um CVM nesses países ou regiões. Se você usar uma instância do CVM na [China](#MainlandChina) para acessar os [servidores em outros países e regiões](#InternationalArea), você pode encontrar uma latência de rede muito maior.

## Disponibilidade de recursos
A tabela a seguir descreve quais recursos do Tencent Cloud são globais, regionais e específicos às zonas de disponibilidade.

<table>
	<tr><th>Recurso</th><th>ID do recurso com string<br><Resource Abbreviation> no formato de 8 dígitos com números e letras</th><th>Tipo</th><th>Descrição</th></tr>
	<tbody>
	<tr>
	  <td>Conta do usuário</td>
	  <td>Sem limite</td>
	  <td>Globalmente exclusivo</td>
	  <td>Os usuários podem utilizar a mesma conta para acessar os recursos do Tencent Cloud no mundo todo.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">Chaves SSH</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>Global</td>
	  <td>Os usuários podem usar uma chave SSH para vincular um CVM em qualquer região sob a conta.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">Instâncias do CVM</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>As instâncias do CVM são específicas de uma zona de disponibilidade</td>
	  <td>Uma instância do CVM criada em uma zona de disponibilidade não fica disponível para outras zonas de disponibilidade.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941?from_cn_redirect=1">Imagens personalizadas</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>As imagens personalizadas criadas para a instância ficam disponíveis para todas as zonas de disponibilidade da mesma região. Use <b>Copy Image (Copiar imagem)</b> para copiar uma imagem personalizada se precisar usá-la em outras regiões.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIPs</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>Os EIPs só podem ser associados a instâncias na mesma região.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452?from_cn_redirect=1">Grupos de segurança</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>O grupo de segurança só pode ser associado a instâncias na mesma região. O Tencent Cloud cria automaticamente três grupos de segurança por padrão para os usuários.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">Cloud Block Storage</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>Os discos do CBS são específicos de uma zona de disponibilidade.</td>
	  <td>Os usuários só podem criar um disco do Cloud Block Storage em uma AZ específica e montá-lo em instâncias na mesma zona de disponibilidade.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">Snapshots</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>Um snapshot criado a partir de um disco em nuvem pode ser utilizado para outros fins (como criar discos na nuvem) nesta região.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524?from_cn_redirect=1">Cloud Load Balancer</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>O Cloud Load Balancer pode ser associado a CVMs em diferentes zonas de disponibilidade de uma única região para encaminhamento de tráfego.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>Um VPC em uma região pode ter recursos criados em diferentes zonas de disponibilidade.</td>
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
	  <td>Regional</td>
	  <td>Ao criar uma tabela de rotas, os usuários precisam especificar um VPC. Portanto, as tabelas de rotas também são regionais.</td>
	</tr>
	</tbody>
</table>


## Operações relevantes

### Migração de uma instância para outra zona de disponibilidade

Depois de iniciada, uma instância não pode ser migrada. No entanto, é possível criar uma imagem personalizada da sua instância do CVM e usá-la para iniciar ou atualizar uma instância em uma zona de disponibilidade diferente.
1. Crie uma imagem personalizada a partir da instância atual. Para obter mais informações, consulte [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942).
2. Se a instância estiver em um [VPC](https://intl.cloud.tencent.com/document/product/213/5227) e você quiser manter seu endereço IP privado atual após a migração, exclua primeiro a sub-rede na zona de disponibilidade atual e, em seguida, crie uma sub-rede na nova zona de disponibilidade com o mesmo intervalo de endereços IP. Observe que uma sub-rede pode ser excluída apenas quando não houver instâncias disponíveis. Portanto, todas as instâncias da sub-rede atual devem ser migradas para a nova sub-rede.
3. Crie outra instância na nova zona de disponibilidade usando a imagem personalizada que você acabou de criar. Você pode escolher o mesmo tipo e configuração da instância original ou escolher novas configurações. Para obter mais informações, consulte [Criação de instâncias pela página de aquisição do CVM](https://intl.cloud.tencent.com/document/product/213/4855).
4. Se um IP elástico estiver associado à instância original, desvincule-o da instância antiga e associe-o à nova instância. Para obter mais informações, consulte [IP elástico (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).
5. (Opcional) Se a instância original for [pagamento conforme o uso](https://intl.cloud.tencent.com/document/product/213/2180), você pode optar por encerrá-la. Para obter mais informações, consulte [Encerramento de instâncias](https://intl.cloud.tencent.com/document/product/213/4930).

### Cópia de imagens para outras regiões

Operações como iniciar e visualizar instâncias são específicas da região. Se a imagem da instância que você precisa iniciar não existir na região, copie a imagem para a região desejada. Para obter mais informações, consulte [Cópia de imagens](https://intl.cloud.tencent.com/document/product/213/4943).
