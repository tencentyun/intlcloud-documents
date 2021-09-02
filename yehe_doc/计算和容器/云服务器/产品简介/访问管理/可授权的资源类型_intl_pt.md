A permissão no nível do recurso refere-se à capacidade de especificar quais recursos os usuários podem operar. O Cloud Virtual Machine (CVM) tem suporte parcial para a permissão no nível de recursos. Isso significa que para determinados CVMs, você pode controlar quando os usuários têm permissão para operar neles e quais recursos específicos eles têm permissão para usar. Por exemplo, você [autoriza os usuários a executar operações em CVMs específicos em Guangzhou](https://intl.cloud.tencent.com/document/product/213/10312).
Os tipos de recursos que podem ser autorizados no Cloud Access Management (CAM) são os seguintes:

| Tipo de recurso | Método de descrição de recursos na política de autorização |
| :-------- | -------------- |
| [Instância do CVM](#CVMCorrelation) |  ` qcs::cvm:$region::instance/* `|
| [Chave do CVM](#KeyCorrelation) |   `qcs::cvm:$region::keypair/*`  |
| [Imagem do CVM](#ImageCorrelation) |   `qcs::cvm:$region:$account:image/*` |

A [Instância do CVM](#CVMCorrelation), a [Chave do CVM](#KeyCorrelation) e a [Imagem do CVM](#ImageCorrelation) introduzem operações de API do CVM compatíveis com as permissões no nível do recurso, bem como com as chaves de recursos e condições aceitas pelas operações de API do CVM. **Ao configurar o caminho do recurso,** é necessário alterar os parâmetros variáveis tais como `$ region`, `$ account` dentro das informações do seu parâmetro atual. Você também pode usar um curinga \* no caminho. Para obter mais informações, consulte [Exemplos de operações](https://intl.cloud.tencent.com/document/product/213/10312).
> As operações de API do CVM não listadas na tabela não aceitam a permissão no nível de recursos. Você ainda pode autorizar o usuário a executar essas operações, mas deve especificar \* como o elemento de recurso na instrução da política.
>

<span id="CVMCorrelation"></span>
#### Instância do CVM

| Operação da API | Caminho do recurso | Chave de condição |
| :-------- | :--------| :------ |
|DescribeInstanceInternetBandwidthConfigs	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstanceInternetChargeType	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesAttribute](https://intl.cloud.tencent.com/document/product/213/33246)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`  | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesProject](https://intl.cloud.tencent.com/document/product/213/33245)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstancesRenewFlag	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RebootInstances](https://intl.cloud.tencent.com/document/product/213/33243)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|RenewInstances	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:systemdisk/*` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesInternetMaxBandwidth](https://intl.cloud.tencent.com/document/product/213/33241)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesPassword](https://intl.cloud.tencent.com/document/product/213/33240)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239)	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResizeInstanceDisks](https://intl.cloud.tencent.com/document/product/213/33238)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RunInstances](https://intl.cloud.tencent.com/document/product/213/33237)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`<br>`qcs::vpc:$region:$account:subnet/* `<br>`qcs::vpc:$region:$account:subnet/$subnetId`<br>`qcs::cvm:$region:$account:systemdisk/*`<br>`qcs::cvm:$region:$account:datadisk/*`<br>`qcs::vpc:$region:$account:vpc/* `<br>`qcs::vpc:$region:$account:vpc/$vpcId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StartInstances](https://intl.cloud.tencent.com/document/product/213/33236)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StopInstances](https://intl.cloud.tencent.com/document/product/213/33235)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[TerminateInstances](https://intl.cloud.tencent.com/document/product/213/33234)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|


<span id="KeyCorrelation"></span>
#### Chave do CVM

| Operação da API | Caminho do recurso | Chave de condição |
| :-------- | :--------| :------ |
|[AssociateInstancesKeyPairs](https://intl.cloud.tencent.com/document/product/213/33232)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`  | -|
|[CreateKeyPair](https://intl.cloud.tencent.com/document/product/213/33231)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[DeleteKeyPairs](https://intl.cloud.tencent.com/document/product/213/33230)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[DescribeKeyPairs](https://intl.cloud.tencent.com/document/product/213/33229)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|DescribeKeyPairsAttribute	|  `qcs::cvm:$region:$account:keypair/*`<br>` qcs::cvm:$region:$account:keypair/$keyId` | -|
| [DisassociateInstancesKeyPairs](https://intl.cloud.tencent.com/document/product/213/33228)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[ImportKeyPair](https://intl.cloud.tencent.com/document/product/213/33227)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[ModifyKeyPairAttribute](https://intl.cloud.tencent.com/document/product/213/33226)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|

<span id="ImageCorrelation"></span>
#### Imagem do CVM

| Operação da API | Caminho do recurso | Chave de condição |
| :-------- | :--------| :------ |
| [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br> `qcs::cvm:$region:$account:image/*` | cvm:region |
| [DeleteImages](https://intl.cloud.tencent.com/document/product/213/33275)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
|[DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272)| `qcs::cvm:$region:$account:image/*`|cvm:region|
| DescribeImagesAttribute|  `qcs::cvm:$region:$account:image/*`<br>` qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [DescribeImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33273)	|  `qcs::cvm:$region:$account:image/*` | cvm:region |
| [ModifyImageAttribute](https://intl.cloud.tencent.com/document/product/213/33269)|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [ModifyImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33268)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [SyncImages](https://intl.cloud.tencent.com/document/product/213/33267)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |







