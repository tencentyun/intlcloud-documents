O Tencent Cloud fornece uma ampla variedade de dispositivos de armazenamento de dados, flexíveis e acessíveis, para instâncias do CVM. O desempenho e o preço variam de acordo com o tipo de dispositivo de armazenamento que melhor se encaixa para os diferentes cenários.


## Dispositivos de armazenamento
Os dispositivos de armazenamento podem ser divididos por dimensão nas seguintes categorias:
<table>
        <tbody>
		<tr>
            <th style="width: 5%;">Dimensão</th>
            <th style="width: 5%;" >Categoria</th>
            <th style="width: 20%;" >Descrição</th>
        </tr>
        <tr>
            <td rowspan="2">Mídia de armazenamento</td>
            <td>Disco HDD</td>
            <td>Utiliza a unidade de disco rígido (HHD) como mídia de armazenamento. Apresenta um preço baixo e velocidade rápida de leitura/gravação.</td>
        </tr>
				<tr>
				    <td>Disco SSD</td>
					<td>Utiliza a unidade de estado sólido (SSD) como mídia de armazenamento. Apresenta excelentes velocidades de IOPS e leitura/gravação, com uma IOPS e taxa de transferência até 20 vezes e 16 vezes superiores às do disco rígido. Seu custo é maior em comparação com o disco HDD.</td>
			    <tr>
            		<td rowspan="2">Casos de uso</td>
            		<td>Disco do sistema</td>
            		<td>Utilizado para armazenar o conjunto de sistemas que controlam e programam a operação do CVM. Utiliza imagens.</td>
        </tr>
				<tr>
				    <td>Disco de dados</td>
						<td>Usado para armazenar todos os dados do usuário.</td>
						<tr>
						<td rowspan="2">Arquitetura</td>
						<td><a href="https://intl.cloud.tencent.com/document/product/213/4953">Cloud Block Storage</a></td>
            <td>O Cloud Block Storage (CBS) é um dispositivo de bloco de rede elástico, com alta disponibilidade, altamente confiável, de baixo custo e personalizável que pode ser usado como um disco dimensionável autônomo para o CVM. Ele fornece armazenamento de dados em um nível de bloco de dados e emprega um mecanismo distribuído de 3 cópias para garantir a confiabilidade dos dados.<br><font style="font-weight:bold">Você pode ajustar o hardware, o disco e a rede de um CVM com o CBS.</font><br>
						</td>
        </tr>
				<td><a href="https://intl.cloud.tencent.com/document/product/213/4961">Cloud Object Storage</a></td>
						<td>O Cloud Object Storage (COS) é um dispositivo de armazenamento de dados na internet. Permite a recuperação de dados a partir de qualquer local na instância do CVM ou na internet, reduzindo os custos de armazenamento. É inadequado para cenários de baixa latência e alta E/S.
						</td>
				</tbody>
				</table>

## Mapeamento de dispositivos de armazenamento em bloco

Cada instância tem um disco do sistema para garantir as operações básicas de dados, e pode montar mais discos de dados. Uma instância usa o mapeamento de dispositivos de armazenamento em blocos para mapear os dispositivos de armazenamento a locais que ela consegue identificar.
O CBS transforma os dados em blocos, em bytes, e permite o acesso aleatório. O Tencent Cloud é compatível com dois tipos de dispositivos do CBS: disco local e disco em nuvem.
![](https://main.qcloudimg.com/raw/3815bb250f6178d67b8fe2be11a50bf8.svg)
Esta figura mostra como o CBS mapeia o dispositivo de armazenamento em blocos para o CVM: ele mapeia `/dev/vda` para o disco do sistema e mapeia os dois discos de dados para `/dev/vdb` e `/dev/vdc`, respectivamente.
A instância do CVM pode criar automaticamente o mapeamento de dispositivos de armazenamento em bloco para discos locais e discos em nuvem montados nela.

