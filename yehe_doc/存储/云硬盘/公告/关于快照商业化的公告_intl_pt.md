O snapshot do CBS foi submetido a um teste beta em 2016 e lançou a **comercialização formal** no Tencent Cloud China a partir de 0h de 22 de janeiro de 2019 e no Tencent Cloud International a partir de 1º de março de 2019. Após a comercialização, todos os snapshots novos e existentes serão cobrados por capacidade usada.
> As [Imagens](https://intl.cloud.tencent.com/document/product/213/4940) usam o serviço de snapshot do CBS para armazenamento de dados. Por isso, a retenção de imagens personalizadas ocupa capacidade do seu snapshot e gera custos.

## Detalhes de comercialização
### Data e escopo da comercialização de snapshots
A comercialização de snapshots se aplica a todos os usuários do Tencent Cloud China e do Tencent Cloud International.
O snapshot foi comercializado no Tencent Cloud China no ponto temporal especificado abaixo:
- 0h de 22 de janeiro de 2019, comercializado formalmente no nordeste da Ásia-Pacífico (Tóquio).
- 0h de 23 de janeiro de 2019, comercializado formalmente em Hong Kong, Macau e Taiwan, China (Hong Kong) e outras regiões fora da China Continental.
- 0h de 24 de janeiro de 2019, comercializado formalmente no Sul da China (Shenzhen Finance), Sul da China (Guangzhou Open) e Leste da China (Shanghai Finance).
- 0h de 25 de janeiro de 2019, comercializado formalmente no Norte da China (Pequim), Leste da China (Xangai), Sul da China (Guangzhou) e Sudoeste da China (Chengdu e Chongqing).

O snapshot foi comercializado no Tencent Cloud International a partir de 1º de março de 2019.

### Upgrades do serviço após a comercialização
Após a comercialização do snapshot, o Tencent Cloud será fornecido aos usuários com um serviço melhor.
>Abaixo estão indicados os valores máximos permitidos na mesma região em uma única conta do Tencent Cloud.

| Upgrade | Antes da comercialização | Após a comercialização|
|---------|---------|---------|
| Quantidade de snapshots | 7 vezes maior do que a quantidade de discos do CBS na região | Cada disco do CBS pode salvar até 64 snapshots. Confira a quantidade de snapshots e exclua os snapshots desnecessários para liberar espaço |
| Capacidade total de snapshots | 20 TB | Sem limites |
| Quantidade de políticas de snapshots programados | 20 | 30 |
| Quantidade de discos em nuvem que podem ser vinculados a uma política de snapshot programado | 100 | 200 |
| Capacidade máxima de disco em nuvem permitida por snapshot programado | 1.000 GB | 16 TB |

### Snapshots e imagens
- As imagens usam o serviço de snapshot do CBS para o armazenamento de dados. Quando uma imagem é criada, um snapshot é automaticamente gerado e vinculado à imagem. Para excluir o snapshot, primeiramente você deve [excluir a imagem](https://intl.cloud.tencent.com/document/product/213/6036). Você pode conferir os detalhes da imagem para obter mais informações sobre o snapshot associado à imagem personalizada.
- Ao usar imagens compartilhadas, apenas a conta do Tencent Cloud que criou a imagem compartilhada precisa pagar as taxas de snapshot associado. O usuário do compartilhamento não precisa pagar nada.
- Os snapshots associados que foram gerados por imagens personalizadas são faturados pela capacidade real, que pode ser conferida na visão geral de snapshots.
- Após o pagamento da sua conta do Tencent Cloud estar em atraso, você não poderá criar imagens personalizadas, então confira se você tem saldo suficiente na sua conta antes de criar uma imagem personalizada.

### Faturamento de snapshots
#### Regras de faturamento
- Modo de faturamento: você é cobrado de acordo com a capacidade total de armazenamento dos seus snapshots. Cada região é cobrada separadamente. No momento, o CBS é **pago conforme o uso** em um ciclo de faturamento por hora.
- Padrão de faturamento: a cobrança dos snapshots varia dependendo da região. Para obter mais informações, consulte [Lista de preços](https://intl.cloud.tencent.com/document/product/362/2413).
- Política de congelamento: após o pagamento da conta do Tencent Cloud estar em atraso, os serviços de snapshot são imediatamente suspensos, inclusive a criação, a reversão, a replicação entre regiões e as políticas de snapshots programados. Após o pagamento da conta estar em atraso por 30 dias, todos os snapshots são excluídos.

#### Nível gratuito
O Tencent Cloud oferece 50 GB de espaço de armazenamento gratuito a usuários da China. Os detalhes da política são os seguintes:
- O nível gratuito se aplica a Pequim, Xangai, Guangzhou, Chengdu, Chongqing e Hong Kong (China). No momento, as regiões exteriores não são compatíveis.
- Os discos em nuvem nas regiões mencionadas anteriormente com um status que não seja `to be repossessed (a ser reavido)` ou `terminated (encerrado)` recebem 50 GB de armazenamento de snapshots gratuito.
- Esse nível gratuito será desativado em julho de 2020.

#### Exemplo de faturamento
A tabela a seguir descreve como o armazenamento de snapshots é cobrado em diferentes circunstâncias:

<table>
     <tr>
         <th>Região</th>  
         <th nowrap="nowrap">Capacidade total de snapshots</th>  
				 <th nowrap="nowrap">Quantidade e status de discos em nuvem</th>
				 <th>Detalhes</th>
     </tr>
	 <tr>
         <td nowrap="nowrap">Norte da China (Pequim)</td>
         <td>100 GB</td>
				 <td nowrap="nowrap">1 disco em nuvem<br/><b>To be repossessed (a ser reavido)</b></td>
				 <td><li>Não elegível ao nível gratuito no momento. A capacidade total de snapshots é de 100 GB faturados com pagamento conforme o uso por hora.</li><li>Após o disco em nuvem ser renovado ou um novo disco em nuvem ser adquirido, o nível gratuito é aplicável. A capacidade total de snapshots é de 100 GB - 50 GB = 50 GB faturados por pagamento conforme o uso por hora.</li></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Hong Kong, Macau e Taiwan, China (Hong Kong)</td>
         <td>60GB</td>
				 <td>1 disco em nuvem<br/><b>Mounted (Montado)</b></td>
				 <td>Elegível ao nível gratuito. A capacidade total de snapshots é de 60 GB - 50 GB = 10 GB faturados por pagamento conforme o uso por hora.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Sudeste da Ásia-Pacífico (Singapura)</td>
         <td>40GB</td>
				 <td>1 disco em nuvem<br/><b>Mounted (Montado)</b></td>
				 <td>Não elegível ao nível gratuito. A capacidade total de snapshots é de 40 GB faturados por pagamento conforme o uso por hora.</td>
     </tr>
</table>

## Snapshots manuais e snapshots programados
O Tencent Cloud disponibiliza a você os dois métodos de criação de snapshots a seguir:
- Snapshots manuais: é possível criar um snapshot manualmente dos dados de disco em nuvem em um determinado ponto temporal. Esse snapshot pode ser utilizado para criar outros discos em nuvem com dados idênticos ou para restaurá-lo de volta ao status desse ponto temporal posteriormente. Para obter mais informações, consulte a [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Snapshots programados: para atualizar seus negócios continuamente, você pode usar snapshots programados para criar backups de dados contínuos. Para obter backups contínuos dos dados do disco em nuvem durante um determinado período, você só precisa configurar uma política de backup e associá-la aos discos em nuvem, o que melhora significativamente a segurança dos dados. Para obter mais informações, consulte [Snapshots programados](https://intl.cloud.tencent.com/document/product/362/35238).

<a id="reduceoverhead"></a>
## Como reduzir de forma efetiva os custos dos snapshots após a comercialização
### Se você quiser continuar a usar snapshots
- Exclua snapshots que não estão mais em uso.
- Exclua imagens personalizadas que não estão mais em uso e seus snapshots associados.
- Reduza a frequência de criação de snapshots para negócios não centrais.
- Reduza o tempo de armazenamento de snapshots para negócios não centrais.

| Cenário de negócios | Snapshot recomendado | Período de retenção |
|---------|---------|---------|
| Negócios centrais | Snapshots programados, com política definida para uma vez por dia. | 7 a 30 dias |
| Negócios não centrais e sem dados | Snapshots programados, com política definida para uma vez por semana | 7 dias |
| Negócios de arquivamento | Snapshots manuais criados às vezes com base nas necessidades empresariais | Um mês ou mais |
| Negócios de testes | Snapshots manuais criados às vezes com base nas necessidades empresariais | Exclusão imediata após o uso |

### Se você quiser parar de usar snapshots
- Verificar e excluir snapshots existentes: verifique e exclua snapshots armazenados em cada região.
- Verificar e excluir imagens personalizadas existentes e os snapshots associados: verifique e exclua as imagens personalizadas armazenadas em cada região e depois exclua os snapshots associados.
- Verificar e modificar as políticas de snapshots programados: verifique a política de programação de cada região e exclua ou desative a política para evitar a geração contínua de novos snapshots programados.
