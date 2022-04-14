## Cenário
Este documento fornece orientação sobre o gerenciamento e a aquisição de instâncias spot. Atualmente, as instâncias spot estão disponíveis por meio dos seguintes canais:
- **Console do CVM**: as **Instâncias spot** foram adicionadas como uma opção para o **Modo de faturamento** na página de aquisição do CVM.
- **Console do BatchCompute**: as instâncias spot podem ser selecionadas quando os usuários enviam trabalhos e criam ambientes de computação no console do BatchCompute.
- **API do TencentCloud**: os parâmetros relacionados a instâncias spot foram adicionados à [API RunInstances](https://intl.cloud.tencent.com/document/product/213/33237).


## Direções
### Console do CVM

1. Faça login na [Página de aquisição do CVM](https://buy.cloud.tencent.com/cvm).
2. Na página da guia **Select a model (Selecionar um modelo)**, defina **Billing Mode (Modo de faturamento)** como **Spot Instances (Instâncias spot)**.
3. Especifique a **Region (Região)**, a **Availability Zone (Zona de disponibilidade)**, a **Network (Rede)**, a **Instance (Instância)** e outras configurações conforme necessário e solicitado.
4. Verifique as informações da instância spot a ser adquirida e os detalhes de custo de cada item de configuração.
5. Clique em **Purchase (Adquirir)** e conclua o pagamento.
Após concluir o pagamento, você pode fazer login no [console do CVM](https://console.cloud.tencent.com/cvm) para verificar sua instância spot.

### Console do BatchCompute
- **API Async**: ao enviar um trabalho, criar um ambiente de computação ou modificar a quantidade esperada de instâncias em um ambiente de computação, a instância do BatchCompute processa suas solicitações de forma assíncrona. Quando não pode atender à solicitação atual devido a motivos de estoque ou de preço, a instância do BatchCompute solicita continuamente recursos de instância spot até que a solicitação atual seja atendida.
Se for necessário liberar uma instância, você precisará ajustar a quantidade esperada de instâncias no ambiente de computação pelo console do BatchCompute. Se você liberar instâncias pelo console do CVM, o console do BatchCompute criará instâncias automaticamente até que a quantidade esperada de instâncias seja atingida.
- **Modo de cluster**: o ambiente de computação de uma instância do BatchCompute pode manter um lote de instâncias spot como um cluster. Basta enviar a quantidade esperada, as configurações e o preço máximo das instâncias spot. O ambiente de computação solicitará continuamente as instâncias spot até que a quantidade esperada seja atingida. Mesmo se as instâncias spot ficarem offline, o ambiente de computação solicitará automaticamente as instâncias spot novamente para atender à quantidade esperada.
- **Peço fixo**: atualmente, as instâncias spot são fornecidas com descontos fixos. Você deve definir um valor maior ou igual ao preço de mercado atual. Para obter os preços de mercado, consulte [Instâncias spot – Regiões compatíveis e tipos de instâncias](https://intl.cloud.tencent.com/document/product/213/17817).

#### Direções

1. Faça login no [Console do BatchCompute](https://console.cloud.tencent.com/batch/env).
2. Na página **Computing environment (Ambiente de computação)**, selecione aleatoriamente uma região, como Guangzhou, e clique em **New (Novo)**.
A página **New computing environment (Novo ambiente de computação)** é exibida.
3. Na página **New computing environment (Novo ambiente de computação)**, defina o **Billing Type (Tipo de faturamento)** para **Spot Instance (Instância spot)** e, em seguida, especifique as configurações, como **Model Type (Tipo de modelo)**, **Image (Imagem)**, **Name (Nome)** e **Expected quantity (Quantidade esperada)** conforme necessário, assim como mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/afb048292803098eeddd7c9ae6ede96a.png)
4. Clique em **OK** para concluir a criação.
Em seguida, você pode verificar o novo ambiente de computação no [console do BatchCompute](https://console.cloud.tencent.com/batch/env). Para visualizar o progresso da criação de instâncias do CVM que estão sendo criadas no ambiente de computação, clique em **Activity Logs (Logs de atividades)** e **Instance List (Lista de instâncias)** para o ambiente de computação.


### API do TencentCloud
Na API RunInstances, você pode especificar o parâmetro [InstanceMarketOptionsRequest](https://intl.cloud.tencent.com/document/api/213/15753#InstanceMarketOptionsRequest) para ativar ou desativar o modo de instância spot e configurar as informações sobre as instâncias spot.
* **API Sync**: atualmente, RunInstances fornece uma API de solicitação de sincronização única. Isso significa que se o aplicativo falhar porque o estoque é insuficiente ou o preço solicitado é inferior ao preço de mercado, a API RunInstances retorna imediatamente um código de falha e não solicita a instância spot novamente.
* **Peço fixo**: atualmente, as instâncias spot são fornecidas com descontos fixos. Você deve definir um valor maior ou igual ao preço de mercado atual. Para obter os preços de mercado, consulte [Instâncias spot – Regiões compatíveis e tipos de instâncias](https://intl.cloud.tencent.com/document/product/213/17817).

## Exemplo
Você tem uma instância na Zona 3 de Guangzhou e o modo de faturamento da instância é com pagamento conforme o uso por hora e no modo spot. As configurações específicas do modo de faturamento são as seguintes:
- MaxPrice: 0,0923 USD/hora
- SpotInstanceType: única
- ImageId: img-pmqg1cw7
- InstanceType: S2.MEDIUM4 (Padrão 2, 2 núcleos, 4 GB)
- InstanceCount: 1

#### Parâmetros de solicitação
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Placement.Zone=ap-guangzhou-3
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.0923
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&ImageId=img-pmqg1cw7
&InstanceType=S2.MEDIUM4
&InstanceCount=1
&<common request parameters>
```

#### Parâmetros de resposta
```
{
  "Response": {
    "InstanceIdSet": [
      "ins-1vogaxgk"
    ],
    "RequestID": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```
