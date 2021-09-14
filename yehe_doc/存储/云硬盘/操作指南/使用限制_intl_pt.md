## Limites de uso de disco em nuvem
<table>
<tr>
		<th width="22%">Tipo de limite</th>
		<th>Descrição</th>
	</tr>
	<tr>
	  <td>Uso do Enhanced SSD</td>
		<td> 1. Atualmente, o Enhanced SSD está disponível apenas na Zona 3 de Guangzhou, Zona 4 de Guangzhou, Zona 2 de Xangai, Zona 3 de Xangai, Zona 5 de Xangai, Zona 3 de Pequim, Zona 4 de Pequim, Zona 1 de Chengdu, Zona 1 de Chongqing, Zona 1 de Nanquim e na Zona 2 de Nanquim. Haverá suporte em mais zonas de disponibilidade.<br>2. O desempenho do Enhanced SSD só é garantido quando ele é montado nos modelos S5, M5, SA2, IT3 e D3 criados após 1º de agosto de 2020 e todos os modelos de geração posterior.<br>3. Não é possível usar o Enhanced SSD como disco do sistema.<br>4. Não é possível criptografar o Enhanced SSD.<br>5. Não é possível fazer o upgrade do Enhanced SSD a partir de outros tipos de discos.</td>
	</tr>
	<tr>
		<td>Capacidade do disco em nuvem elástico</td>
		<td>A partir de maio de 2018, todos os discos de dados adquiridos com CVMs são discos em nuvem elásticos, que são compatíveis com a desmontagem e a remontagem de CVMs. Essa funcionalidade é compatível com todas as zonas de disponibilidade.</a></td>
	</tr>
	<tr>
		<td>Desempenhos de discos em nuvem</td>
		<td>A especificação de E/S se aplica ao desempenho de entrada e saída ao mesmo tempo.<br/>Por exemplo, se um SSD de 1 TB tiver um IOPS aleatório máximo de 26.000, isso significa que seu desempenho de leitura e gravação pode atingir esse valor. Devido aos limites de desempenho, se o tamanho do bloco nesse exemplo for 4 KB ou 8 KB, o IOPS máximo pode ser atingido. Se o tamanho do bloco for 16 KB, o IOPS máximo não pode ser atingido (a taxa de transferência já atingiu o limite de 260 MB/s.).</td>
	</tr>
		<tr>
	<td>Máximo de discos em nuvem elásticos montáveis por CVM</td>
	<td>Um CVM pode ter no máximo 20 discos em nuvem montados.</td>
	</tr>
		<tr>
	<td>Montagem</td>
	<td>Só é possível montar um disco em nuvem em um CVM na mesma zona de disponibilidade.</td>
	</tr>
	<tr>
		<td>Retomada de posse de discos em nuvem em atraso</td>
		<td>Quando um disco em nuvem com assinatura mensal expira e você não o renova dentro de 7 dias após a expiração, ele será desmontado de forma forçada do CVM (se houver) e movido para a lixeira. Para obter detalhes sobre o mecanismo de retomada de posse, consulte <a href="https://intl.cloud.tencent.com/document/product/362/31625">Pagamento em atraso</a>.<br>Atualmente, quando você <a href="https://intl.cloud.tencent.com/document/product/362/32401">monta</a> um disco em nuvem com assinatura mensal para o CVM também com assinatura mensal, os seguintes métodos de renovação estão disponíveis:
			<ul style="margin-bottom:0;">
			<li>Renove o disco em nuvem quando o CVM associado expirar</li>
			<li>Renove o disco em nuvem todo o mês e de forma automática após a expiração.</li>
			<li>Monte diretamente sem uma política de renovação.</li>
			</ul>
		</td>
	</tr>
</table>

## Limites de uso de snapshots
<table>
<tr>
		<th width="22%">Tipo de limite</th>
		<th>Descrição</th>
	</tr>
		<tr>
		<td>Tipo de disco compatível</td>
		<td>Só é possível usar o snapshot do disco de dados para criar discos em nuvem elásticos enquanto o snapshot do disco do sistema é usado para criar uma imagem personalizada.</td>
	</tr>
		<tr>
	<td>Capacidade do disco em nuvem criado</td>
	<td>A capacidade do disco em nuvem criado usando um snapshot deve ser maior ou igual à do snapshot.</td>
	</tr>
			<tr>
			<td>Reversão do snapshot</td>
			<td>Os dados do snapshot só podem ser revertidos para o disco em nuvem de origem em que o snapshot foi criado. Se desejar criar um disco em nuvem com dados em um snapshot existente, consulte <a href="https://intl.cloud.tencent.com/document/product/362/5757">Criação de discos em nuvem usando snapshots<a>.
		</td>
	</tr>
	<tr>
		<td>Tamanho total do snapshot</td>
		<td>Sem limite.</td>
	</tr>
	<tr>
		<td>Cota do snapshot em uma região</td>
		<td>64 + a quantidade de discos em nuvem na região * 64.</td>
	</tr>
</table>

## Limites de uso na política de snapshots programados
<table>
<tr>
		<th width="40%">Tipo de limite</th>
		<th>Descrição</th>
	</tr>
	<tr>
		<td>Cota da política de snapshots programados em uma região</td>
		<td>Uma única conta do Tencent Cloud pode definir no máximo 30 políticas de snapshots programados em cada região.</td>
	</tr>
	<tr>
		<td>Quantidade de políticas de snapshots programados associadas a um disco em nuvem</td>
		<td>Um disco em nuvem pode ser associado a um máximo de 10 políticas de snapshots programados na mesma região.</td>
	</tr>
	<tr>
		<td>Quantidade de discos em nuvem associados a uma política de snapshots programados</td>
		<td>Uma política de snapshots programados pode ser associada a no máximo 200 discos em nuvem na mesma região.</td>
	</tr>
</table>
