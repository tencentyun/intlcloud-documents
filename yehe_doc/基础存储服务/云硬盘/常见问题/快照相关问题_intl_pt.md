### Um disco em nuvem adotou um mecanismo de redundância de três cópias para a segurança de dados. Por que ainda precisamos usar snapshots?
Em situações em que ocorre um erro de dados de nível lógico, por exemplo, suponha que o usuário tenha excluído os dados sem querer ou que os dados tenham sido danificados por um vírus ou exceções de sistema de arquivos, todas as três cópias de dados armazenadas serão afetadas e os dados históricos não poderão ser restaurados. Se você criou um snapshot anteriormente, será possível usá-lo para restaurar os dados de volta ao ponto temporal em que o snapshot foi criado.
![](https://main.qcloudimg.com/raw/824b34d077d2e58114e08de86edae2b8.png)
Suponha que um administrador tenha criado o snapshot A para um disco em nuvem às 11h, e o disco em nuvem tenha sido infectado por vírus às 12h, o que tornou esses dados inutilizáveis. Nesse caso, as três cópias de dados teriam sido atualizadas para o status 2 e os dados não poderiam ser restaurados. Para restaurar os dados de volta ao status 1 não infectado, você precisa usar o snapshot A criado às 11h.

### Por que o armazenamento em disco usado exibido no sistema de arquivos é diferente do tamanho do snapshot?
Um snapshot de disco em nuvem é um backup ou clone de nível de bloco. Em geral, o tamanho do snapshot será maior do que o tamanho dos dados exibidos no sistema de arquivos, porque:
- O respectivo bloco de dados armazena os metadados do sistema de arquivos.
- Alguns dados são excluídos. A exclusão dos dados modifica o bloco de dados gravados, o qual terá uma cópia nos snapshots.


### Quais são as diferenças entre snapshots e imagens?
Se nenhum disco de dados estiver montado em uma instância e todos os dados estiverem gravados no disco do sistema, os dados do disco do sistema não poderão ser protegidos pela criação de uma imagem. Não é possível programar imagens para backup contínuo. Após os dados do disco do sistema serem danificados, você só poderá recuperar os dados de volta ao estado em que a imagem foi criada inicialmente. Portanto, as imagens não são adequadas para proteção dos dados. As diferenças específicas são:

<table>
		<tr>
		<th width="10%">Nome</th>
		<td width="45%">Snapshots</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">Imagens</a></td>
		</tr>
		<tr>
		<th>Características</th>
			<td>Dados de backup de um disco em nuvem em um determinado ponto temporal</td>
	   	<td>Modelo de configuração do software do CVM, que contém informações sobre o sistema operacional e os programas pré-instalados</td>
		</tr>
		<tr>
		<th>Casos de uso</th>
		<td>
			<ul>
				<li>Faz backup regularmente dos dados empresariais importantes</li>
				<li>Faz backup de dados antes de grandes operações</li>
				<li>Gera várias cópias dos dados</li>
			</ul>
		</td>
		<td>
			<ul>
				<li>Faz backup de sistemas que permanecerão inalterados no curto prazo</li>
				<li>Implanta aplicativos em lotes</li>
				<li>Migra o sistema</li>
			</ul>
		</td>
		</tr>
</table>


### Por que não é possível usar alguns dos snapshots para criar imagens?
Você pode criar snapshots para discos do sistema e discos de dados. Entretanto, apenas o snapshot de um disco do sistema pode ser usado para criar uma imagem personalizada.

### Por que eu não posso excluir um snapshot?
Para excluir um snapshot, confira se o snapshot que você pretende excluir não está associado a nenhuma imagem. Para consultar snapshots associados a uma imagem, acesse a página [Imagem](https://console.cloud.tencent.com/cvm/image) e clique no ID/Nome da imagem.

### Como os snapshots são criados a partir de uma imagem faturada?
As imagens usam o serviço de snapshot do CBS para o armazenamento de dados. Os snapshots associados a uma imagem personalizada serão faturados por tamanho de armazenamento. Para ver o tamanho dos seus snapshots, acesse [Visão geral de snapshots](https://console.cloud.tencent.com/cvm/snapshot/overview).

### Como as imagens compartilhadas são faturadas?
Nós cobramos uma taxa do proprietário de imagens compartilhadas. Já a conta de destino não é cobrada. Para obter mais informações sobre o faturamento de snapshots, consulte [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/362/32415).



### O que é um snapshot programado?
Um snapshot programado é criado automaticamente para o disco em nuvem de acordo com a respectiva política do snapshot programado. Para usar essa funcionalidade, primeiramente você deve criar uma política de snapshot programado e associá-la ao disco em nuvem. Para obter mais informações, consulte [Snapshots programados](https://intl.cloud.tencent.com/document/product/362/35238).


### Quais são os limites de snapshots programados?
É possível criar, no máximo, 30 políticas de snapshots programados em uma determinada região. Cada política de snapshot programado pode ser associada a até 200 discos em nuvem. Além disso, os snapshots criados de acordo com as políticas de snapshots programados devem estar em conformidade com a cota de snapshots. Para obter mais informações, consulte os [Limites de uso](https://intl.cloud.tencent.com/document/product/362/32406).

### Como os snapshots são criados?
Você pode criar um snapshot com os seguintes métodos:
- Snapshot personalizado: você pode criar manualmente um snapshot para salvar dados do disco em nuvem rapidamente em um ponto temporal especificado. Para obter mais informações, consulte a [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Snapshot programado: você pode associar uma política de snapshot programado ao disco em nuvem para criar e excluir snapshots periodicamente.

### O snapshot fica disponível em todas as zonas de disponibilidade?
Sim.

## Como os snapshots são faturados?
Os snapshots são faturados de acordo com o tamanho total do seu armazenamento de snapshots de cada região com **pagamento conforme o uso**; e a taxa é calculada e deduzida a cada hora exata. Para obter mais informações sobre o faturamento, consulte [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/362/32415) e [Visão geral de preços](https://intl.cloud.tencent.com/document/product/362/2413).

### Eu preciso desmontar um disco ou interromper todas as leituras e gravações antes de criar um snapshot?
Não. Você pode criar um snapshot em tempo real enquanto o disco está conectado e em uso, sem afetar a operação normal da sua empresa. Entretanto, o snapshot só pode registrar dados gravados, mas não dados em cache no disco em nuvem. Para garantir que todos os dados de aplicativos sejam registrados, nós recomendados que você suspenda todas as operações de E/S do disco antes de criar um snapshot. Para um disco em nuvem utilizado como um disco do sistema, nós recomendamos que você encerre o CVM para criar um snapshot mais completo.

### A criação de um snapshot afetará o desempenho do disco?
A criação de um snapshot ocupará uma pequena parte das operações de E/S do disco em nuvem. Nós recomendamos criar snapshots fora de horários de pico dos seus negócios.

### Quanto tempo leva para criar um snapshot?
O tempo necessário para criar um snapshot é influenciado por fatores como a quantidade de gravações em disco e as operações de leitura-gravação simultâneas. A criação de um snapshot não afetará o uso do disco.

### Como eu crio um disco em nuvem usando um snapshot?
Para obter mais informações, consulte a [Criação de discos em nuvem usando snapshots](https://intl.cloud.tencent.com/document/product/362/5757).

### Como eu reverto snapshots?
Para obter mais informações, consulte [Reversão de snapshots](https://intl.cloud.tencent.com/document/product/362/5756).

### Eu preciso encerrar o CVM para reverter um snapshot?
- Para um disco em nuvem que foi montado em um CVM, você precisa encerrar o CVM para reverter um snapshot.
- Para um disco em nuvem que não foi montado, você pode reverter um snapshot diretamente.

### Eu posso ler um snapshot anterior para restaurar um disco em nuvem?
Sim. Você pode usar um snapshot existente criado em qualquer ponto temporal para restaurar dados, independentemente do ponto temporal do snapshot.

### Eu posso excluir o snapshot de origem quando ele for replicado?
Não. Ele só pode ser excluído após a replicação ser concluída.

### O novo snapshot criado por replicação continuará associado ao disco de origem do snapshot de origem?
O snapshot criado por replicação entre regiões não estará mais associado ao disco de origem do snapshot de origem. A funcionalidade de reversão não está disponível para snapshots replicados.

### Os snapshots associados serão excluídos quando o CVM for encerrado?
Não, os snapshots associados não serão excluídos automaticamente. Você pode excluí-los pelo console ou por uma API. Para obter mais informações, consulte [Exclusão de snapshots](https://intl.cloud.tencent.com/document/product/362/5758).

### Como eu excluo um snapshot?
- Para snapshots de disco em nuvem, você pode excluí-los diretamente pelo console ou via API. Para obter mais informações, consulte [Exclusão de snapshots](https://intl.cloud.tencent.com/document/product/362/5758).
- Para snapshots associados a imagens personalizadas, primeiramente você deve excluir as imagens personalizadas e depois [excluir os snapshots](https://intl.cloud.tencent.com/document/product/362/5758).

### Eu posso usar um snapshot criado a partir do disco do sistema para criar um disco em nuvem?
Não. Você só pode usar o snapshot do disco do sistema para criar uma imagem personalizada.

### O snapshot é compatível com a funcionalidade de replicação entre regiões?
Sim. Você pode usar essa funcionalidade para migrar os dados e os serviços facilmente para outras regiões ou criar seu sistema de recuperação de desastres entre regiões. Para obter mais informações, consulte [Replicação de snapshots entre regiões](https://intl.cloud.tencent.com/document/product/362/31623).

