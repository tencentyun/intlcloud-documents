## Visão geral da permissão a nível de recurso
A permissão a nível de recurso pode ser usada para especificar quais recursos um usuário pode manipular. O TcaplusDB aceita algumas permissões a nível de recurso, ou seja, permitindo que o usuário execute operações ou use recursos especificados.

No Cloud Access Management (CAM), os tipos de recursos do TcaplusDB que podem ser autorizados são os seguintes:

| Tipo de recurso                         | Método de descrição de recursos na política de autorização                                     |
| :------------------------------- | ------------------------------------------------------------ |
| [Cluster](#tcaplusdbCorrelation)    | ` qcs::tcaplusdb:$region:$account:cluster/$clusterId `       |
| [Grupo de tabelas](#tablegroupCorrelation) | `qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [Tabela](#tableCorrelation)        | `qcs::tcaplusdb:$region:$account:table/$tableId`             |

As seções [APIs do cluster do TcaplusDB](#tcaplusdbCorrelation), [APIs do grupo de tabelas do TcaplusDB](#tablegroupCorrelation) e [APIs da tabela do TcaplusDB](#tableCorrelation) abaixo descrevem as operações das APIs do TcaplusDB que atualmente aceitam o controle de permissões a nível de recurso, assim como os recursos e as chaves de condições aceitos por cada operação. Ao definir o caminho do recurso, você precisa substituir os parâmetros variáveis, como `$region` e `$account`, por suas informações de parâmetro reais. Você também pode usar o curinga `\*` no caminho. Para obter exemplos de operações relacionadas, consulte [Exemplos de controle de acesso do TcaplusDB](https://intl.cloud.tencent.com/document/product/1016/35752).

> Para uma operação de API do TcaplusDB que não aceita a autorização em nível de recurso, você ainda pode autorizar um usuário a executá-la, mas deve especificar `\*` como o elemento de recurso na instrução da política.

## Lista de APIs que não aceitam permissão a nível de recurso

| Operação da API               | Descrição da API                  |
| :--------------------- | :----------------------- |
| CreateBackup           | Cria backup                 |
| CompareIdlFiles        | Carrega e verifica o arquivo de modificação da tabela       |
| VerifyIdlFiles         | Carrega e verifica o arquivo de criação da tabela   |
| DescribeUinInWhitelist | Consulta se o usuário atual está na lista de permissões |
| DescribeRegions        | Consulta a lista de regiões             |
| DeleteIdlFiles         | Exclui o arquivo de descrição IDL          |
|DescribeIdlFileInfos   | Consulta os detalhes do arquivo de descrição da tabela       |
| DescribeIdlFileInfos          | Consulta a lista de tarefas             |

## Lista de APIs que aceitam permissão a nível de recurso

<span id="tcaplusdbCorrelation"></span>
### APIs do cluster do TcaplusDB

| Operação da API                                                     | Caminho do recurso                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateCluster](https://intl.cloud.tencent.com/document/product/1016/35053) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [ModifyClusterName](https://intl.cloud.tencent.com/document/product/1016/35049) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [DeleteCluster](https://intl.cloud.tencent.com/document/product/1016/35052) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [DescribeClusters](https://intl.cloud.tencent.com/document/product/1016/35050) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [ModifyClusterPassword](https://intl.cloud.tencent.com/document/product/1016/35048) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |

<span id="tablegroupCorrelation"></span>
### APIs de grupo de tabelas do TcaplusDB

| Operação da API                                                     | Caminho do recurso                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateTableGroup](https://intl.cloud.tencent.com/document/product/1016/35027) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [DeleteTableGroup](https://intl.cloud.tencent.com/document/product/1016/35026) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [DescribeTableGroups](https://intl.cloud.tencent.com/document/product/1016/35025) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [ModifyTableGroupName](https://intl.cloud.tencent.com/document/product/1016/35024) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |

<span id="tableCorrelation"></span>
### APIs de tabelas do TcaplusDB

| Operação da API                                                     | Caminho do recurso                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateTables](https://intl.cloud.tencent.com/document/product/1016/35039) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ClearTables](https://intl.cloud.tencent.com/document/product/1016/35042) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DeleteTables](https://intl.cloud.tencent.com/document/product/1016/35038) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DescribeTables](https://intl.cloud.tencent.com/document/product/1016/35036) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DescribeTablesInRecycle](https://intl.cloud.tencent.com/document/product/1016/35035) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTableMemos](https://intl.cloud.tencent.com/document/product/1016/35034) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTableQuotas](https://intl.cloud.tencent.com/document/product/1016/35033) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTables](https://intl.cloud.tencent.com/document/product/1016/35032) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [RecoverRecycleTables](https://intl.cloud.tencent.com/document/product/1016/35031) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [RollbackTables](https://intl.cloud.tencent.com/document/product/1016/35030) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
