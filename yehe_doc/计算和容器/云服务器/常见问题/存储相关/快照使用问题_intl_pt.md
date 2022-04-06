### O snapshot está disponível em todas as zonas de disponibilidade?
Sim.

### A criação de um snapshot afetará o desempenho do disco?
A criação de um snapshot ocupará uma pequena quantidade de E/S do disco em nuvem. Recomendamos criar snapshots quando tiverem poucas atividades.

### Quanto tempo leva para criar um snapshot?
O tempo necessário para criar um snapshot é influenciado por fatores como a quantidade de gravações em disco e as operações de leitura e gravação subjacentes. A criação de um snapshot não afetará o uso do disco.

### Preciso desligar a CVM para reverter snapshots?
- Para um disco em nuvem que foi montado em uma CVM, você deve desligar a CVM para reverter os snapshots.
- Para um disco em nuvem que não foi montado, você pode reverter os snapshots diretamente.

### Como é calculado o tamanho do primeiro snapshot completo de um disco em nuvem?
O primeiro snapshot criado em um disco em nuvem é um snapshot completo que copia todos os dados do disco em nuvem em um determinado momento. O tamanho do snapshot é igual à capacidade usada do disco em nuvem. Por exemplo, se a capacidade total de um disco em nuvem for 200 GB e 122 GB tiverem sido usados, o tamanho do primeiro snapshot completo será 122 GB.

### Posso baixar ou exportar snapshots de instâncias da CVM para um dispositivo local?
Não. Os snapshots não podem ser baixados ou exportados para dispositivos locais. Você precisa criar uma imagem personalizada a partir de um snapshot e depois exportar a imagem.

### Os snapshots automáticos diferem ou entram em conflito com os snapshots manuais?
Não. Você pode usar os dois ao mesmo tempo. No entanto, você não pode criar snapshots manuais enquanto os automáticos estão sendo criados.
- Você não pode criar um snapshot de disco personalizado até que o de disco automático termine de ser criado e vice-versa.
- Se um snapshot criado a partir de um disco grande durar mais do que o intervalo entre dois snapshots automáticos, o próximo snapshot automático será ignorado. Por exemplo, se você configurar os snapshots automáticos para serem criados às 9h, 10h e 11h e o snapshot automático criado às 9h durar 70 minutos e terminar às 10h10, o próximo snapshot automático será ser criado às 11h e não às 10h.

### Posso criar snapshots para discos locais?
Não. Recomendamos que você use a redundância de dados na camada de aplicativos ou crie conjuntos de implantação para clusters para melhorar a disponibilidade dos aplicativos.

### Após liberar o disco em nuvem, os snapshots locais serão excluídos?
Não. Você precisa excluir os snapshots por meio do console ou das APIs. Para mais informações, consulte [Exclusão de snapshots](https://intl.cloud.tencent.com/document/product/362/5758).

### Por que a capacidade de disco usada exibida no sistema de arquivos difere do tamanho do snapshot?
Um snapshot de disco em nuvem é um clone ou backup em nível de bloco. Em geral, a capacidade do snapshot será maior que a capacidade de dados exibida no sistema de arquivos porque:
- O bloco de dados subjacente armazena os metadados do sistema de arquivos.
- Alguns dados foram excluídos. A exclusão de dados modifica o bloco de dados gravado, do qual será feito backup em snapshots.

### Como evitar que os snapshots sejam excluídos pela Tencent Cloud?
- Snapshots manuais: a Tencent Cloud nunca os excluirá, independentemente de o disco ou a instância correspondente terem sido liberados.
- Snapshots programados: você pode definir o período de retenção de snapshots programados para retenção de longo prazo, a fim de evitar que sejam excluídos. Dessa forma, apenas o snapshot criado mais cedo será excluído quando a cota de snapshots for atingida. Para mais detalhes, consulte [Snapshot programado](https://intl.cloud.tencent.com/document/product/362/35238) e [Limites de uso](https://intl.cloud.tencent.com/document/product/362/32406).

### Como excluir snapshots para reduzir os custos de backup?
- Para os snapshots de disco em nuvem, você pode excluí-los diretamente por meio do console ou das APIs. Para mais informações, consulte [Exclusão de snapshots](https://intl.cloud.tencent.com/document/product/362/5758).
- Para os snapshots associados a imagens personalizadas, você deve primeiro excluir as imagens personalizadas e depois [excluir os snapshots](https://intl.cloud.tencent.com/document/product/362/5758).

### Os snapshots automáticos serão excluídos após a expiração da instância ou a liberação do disco em nuvem?
Não. Os snapshots automáticos não serão excluídos após a expiração da instância ou a liberação do disco em nuvem, pois são retidos com base nas políticas do período de retenção dos snapshots programados. Para modificar as políticas de snapshots programados, consulte [Snapshot programado](https://intl.cloud.tencent.com/document/product/362/35238).

### Como excluir snapshots dos quais uma imagem ou disco em nuvem foi criado?
- Snapshots dos quais um disco em nuvem foi criado: você pode excluir os snapshots separadamente. Após excluir um snapshot, você não poderá operar uma atividade que dependa dos dados do snapshot original.
- Snapshots dos quais uma imagem personalizada foi criada: primeiro você deve excluir a imagem e depois excluir os snapshots.
- Snapshots dos quais uma instância foi criada: você pode excluir os snapshots separadamente. Após excluir um snapshot, você não poderá operar uma atividade que dependa dos dados do snapshot original.

### A política de snapshots não será executada se eu criar uma imagem personalizada ou um disco em nuvem com base no snapshot programado?
Não.


### Um disco em nuvem pode ter várias políticas de snapshots automáticos?
Não.

### Como evitar a perda de dados causada por operações incorretas?
Você pode criar snapshots para fazer backup de dados antes de realizar operações arriscadas. Por exemplo, você pode criar um snapshot antes de modificar arquivos críticos do sistema, migrar instâncias de uma rede clássica para um VPC, fazer backup de dados, restaurar uma instância que foi liberada acidentalmente, evitar ataques à rede, alterar sistemas operacionais ou fornecer suporte de dados para um ambiente de produção. Para mais informações, consulte a [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755). Se ocorrer um erro, você pode [reverter os snapshots](https://intl.cloud.tencent.com/document/product/362/5756) para reduzir os riscos.

### Criei uma instância na região de Guangzhou e criei snapshots para os discos de dados da instância. Depois que a instância expirou e foi liberada, comprei outra instância na região de Guangzhou. Posso reverter os snapshots na nova instância para restaurar a instância original?
Não. Os snapshots só podem ser revertidos para o disco em nuvem em que foram criados. Você pode usar os snapshots do disco de dados anterior para criar um disco em nuvem e montar o disco em nuvem na nova instância. Para mais informações, consulte [Criação de discos em nuvem usando snapshots](https://intl.cloud.tencent.com/document/product/362/5757) e [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32401).

### Quais são as diferenças entre os snapshots e as imagens?
Se nenhum disco de dados estiver montado em uma instância e todos os dados forem gravados no disco do sistema, os dados no disco do sistema não poderão ser protegidos com a criação de uma imagem. As imagens não podem ser programadas para backup contínuo. Depois que os dados do disco do sistema estiverem danificados, você só poderá recuperar os dados para o estado em que a imagem foi criada inicialmente. Portanto, as imagens não são adequadas para proteção de dados. Veja abaixo as diferenças específicas:
<table>
		<tr>
		<th width="10%">Nome</th>
		<td width="45%">Snapshots</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">Imagens</a></td>
		</tr>
		<tr>
		<th>Características</th>
			<td>Dados de backup de um disco em nuvem em um determinado momento</td>
	   	<td>Modelo de configuração do software da CVM, que contém informações sobre o sistema operacional e os programas pré-instalados</td>
		</tr>
		<tr>
		<th>Casos de uso</th>
		<td>
			<ul>
				<li>Backups regulares de dados de atividades importantes</li>
				<li>Backup dos dados antes de operações principais</li>
				<li>Produção de várias cópias de dados</li>
			</ul>
		</td>
		<td>
			<ul>
				<li>Backup de sistemas que permanecerão inalterados no curto prazo</li>
				<li>Implantação de aplicativos em lotes</li>
				<li>Migração do sistema</li>
			</ul>
		</td>
		</tr>
</table>

### Como migrar dados de snapshots da conta A para a conta B?
Os snapshots não podem ser migrados. Em vez disso, você pode criar uma imagem do snapshot que deseja migrar e compartilhar a imagem com outra conta.

### Posso criar uma imagem personalizada a partir de snapshots de disco de dados?
Não. Você só pode criar uma imagem personalizada a partir de snapshots de disco do sistema.



