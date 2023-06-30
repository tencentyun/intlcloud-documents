## Visão geral

Os dispositivos de hardware de instâncias do Tencent Cloud CVM podem ser ajustados de forma rápida e flexível. Este documento descreve os métodos de operação para upgrade, downgrade e ajuste entre modelos da configuração.

## Pré-requisitos

Você pode ajustar a configuração de uma instância quando ela está desligada ou em execução. Se a instância estiver em execução, o ajuste entrará em vigor depois do desligamento forçado e da reinicialização.
> 
> - Se a instância foi **desligada**, você pode ajustar sua configuração diretamente pelo console.
> - Se a instância estiver **em execução**, você pode ajustar sua configuração online e confirmar para forçar o desligamento da instância. O ajuste entra em vigor depois que a instância for reiniciada.
> - Você pode ajustar as configurações de instâncias online **em lotes**. Se uma instância da operação em lote estiver **em execução**, você precisará forçar o desligamento dela. O ajuste entra em vigor depois que a instância for reiniciada.

## Limites e impactos

### Limites de ajuste da configuração

Apenas a instância **cujos discos de sistema e de dados são ambos discos em nuvem do CBS** é compatível com o ajuste da configuração.
- Upgrade da configuração:
Sem limites para a quantidade de upgrades de configuração. O upgrade entra em vigor imediatamente.
- Downgrade da configuração:
 - O downgrade das instâncias com pagamento conforme o uso pode ser feito quantas vezes você desejar e a qualquer momento.
- Ajuste entre famílias de instâncias: as configurações podem ser ajustadas entre famílias de instâncias sem a necessidade de migração de dados.
Durante o ajuste da configuração, as especificações de destino dependem dos tipos de instâncias fornecidos na zona de disponibilidade atual. Observe os seguintes limites:
 - As **Instâncias spot** não são compatíveis com o ajuste da configuração entre modelos.
 - As **Instâncias dedicadas** não são compatíveis com o ajuste da configuração entre modelos. O escopo de ajuste está sujeito aos recursos restantes do host dedicado onde a instância está localizada.
 - As **Instâncias heterogêneas, como instâncias de GPU e FPGA** não podem ser usadas como tipo de instância de origem ou destino para o ajuste da configuração entre famílias de instâncias.
 - As **Instâncias configuradas com uma rede clássica** não podem ser ajustadas para as instâncias que são compatíveis apenas com o VPC.
 - Se o tipo de instância de destino não for compatível com o tipo de disco do CBS configurado para o tipo de instância atual, a configuração não pode ser ajustada.
 - Se o tipo de instância de destino não for compatível com o tipo de imagem configurado para o tipo de instância atual, a configuração não pode ser ajustada.
 - Se o tipo de instância de destino não for compatível com o ENI ou a quantidade de ENIs configurada para o tipo de instância atual, a configuração não pode ser ajustada. Para obter mais informações, consulte os [Limites de uso](https://intl.cloud.tencent.com/document/product/576/18527).
 - Se o tipo de instância de destino não for compatível com o limite da largura de banda da rede pública configurado para o tipo de instância atual, a configuração não pode ser ajustada. Para obter mais informações, consulte [Limite da largura de banda da rede pública](https://intl.cloud.tencent.com/document/product/213/12523).

### Impactos

O IP privado de uma instância pode mudar após o ajuste da configuração. Nesse caso, um aviso aparecerá na página de ajuste da configuração. Caso contrário, o IP privado permanecerá o mesmo.

## Direções

>
> - Se a sua empresa mudar, você pode ajustar a configuração da instância.
> - Durante o upgrade da configuração, faça o upgrade da sua instância do CVM de acordo e pague as taxas que podem incorrer.
> - Durante o downgrade da configuração, realize o desligamento forçado e reinicie sua instância do CVM para que a nova configuração tenha efeito imediato.

### Ajuste da configuração pelo console

#### Ajuste da configuração de uma única instância

1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm) e clique em **Instances (Instâncias)** para visualizar a lista de instâncias do CVM.
2. Localize a instância a ser ajustada e escolha **More (Mais)** > **Resource Adjustment (Ajuste de recursos)** > **Adjust Configuration (Ajustar a configuração)** na coluna **Operation (Operação)** à direita, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/65541031befe2d0144227cf5a616e161.png)
3. Na etapa "Select target configuration (Selecionar a configuração de destino)", confirme o status e a operação da instância, **selecione o modelo e as especificações necessários, confirme os parâmetros de desempenho** e clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/818fbf0dfa791ad5d5a76186eefba019.png)
4. Com base no método de faturamento da instância, confirme as taxas e clique em **Next (Avançar)**.
	- Instâncias com pagamento conforme o uso: confirme o valor a ser congelado para o novo tipo de instância. Após o ajuste da configuração, as instâncias com pagamento conforme o uso são cobradas a partir do preço de nível 1. Confirme as regras de faturamento, conforme mostrado na figura a seguir:
	![](https://main.qcloudimg.com/raw/25f8630836acdfe274357142d8609c5d.png)
5. Na etapa "Shutdown CVM (Desligar o CVM)", leia o aviso cuidadosamente com base no status de execução da instância.
 - Se a instância atual estiver em execução, leia o aviso com atenção e selecione "Agree to a forced shutdown (Concordar com um desligamento forçado)", conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/e016f2cc674938acd0046115f007669b.png)
 - Se a instância atual estiver desligada, o seguinte aviso aparecerá:
![](https://main.qcloudimg.com/raw/8385495393237523d0d71460a7b7009b.png)
6. Clique em **Adjust Now (Ajustar agora)** para ir para a página do pedido e concluir o pagamento. 

### Ajuste da configuração por API 

Você pode usar a API ResetInstancesType para ajustar a configuração da instância. Para obter mais informações, consulte a documentação da API [ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239).





