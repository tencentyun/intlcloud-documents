### Como fazer upgrade/downgrade das configurações dos CVMs?

Você só pode ajustar as configurações de instâncias **cujos discos de sistema e discos de dados são discos em nuvem**. 
- Para  mais informações sobre como fazer upgrade/downgrade de configurações da instância, consulte [Alteração da configuração da instância](https://intl.cloud.tencent.com/document/product/213/2178).
- Para mais informações sobre como ajustar as configurações de largura de banda/rede, consulte [Ajuste da configuração da rede](https://intl.cloud.tencent.com/document/product/213/15517).

Se os ajustes de configuração não entrarem em vigor, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para entrar em contato conosco.

### Como verifico os registros de ajustes de configuração?

1. Faça login no [Console do CloudAudit](https://console.cloud.tencent.com/cloudaudit).
2. Na página **Event history (Histórico de eventos)**, defina filtros como o nome de usuário, o tipo de recurso e o nome do recurso conforme necessário para exibir a lista de registros.
Para mais informações, consulte [Introdução](https://intl.cloud.tencent.com/document/product/1021/30338).

### Posso ajustar as configurações das instâncias da CVM?
Sim. Você pode ajustar as configurações de instâncias cujos discos de sistema e discos de dados são discos em nuvem. Para as instâncias com pagamento conforme o uso, é possível fazer upgrade ou downgrade das configurações delas quantas vezes quiser.

### Qual é a quantidade máxima de vezes que posso fazer downgrade das configurações das CVMs?
- Você pode fazer upgrade e downgrade das configurações de instâncias com pagamento conforme o uso quantas vezes quiser.

### Posso fazer upgrade das especificações e das configurações de instâncias com pagamento conforme o uso?

Sim. Você pode fazer upgrade das configurações de instâncias da CVM com pagamento conforme o uso seguindo as instruções apresentadas em [Alteração da configuração da instância](https://intl.cloud.tencent.com/document/product/213/2178) ou pela API [ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239).

### Quanto tempo leva para fazer upgrade de uma instância da CVM?

Cerca de 1 a 2 minutos.

### Como é calculado o custo incorrido de um upgrade de instância da CVM?

Você pode exibir os detalhes de custo no [Centro de faturamento](https://console.cloud.tencent.com/expense) após atualizar as especificações ou as configurações da instância da CVM.

### O upgrade de instâncias da CVM afetará as configurações de negócios na instância?

Finalizado o upgrade de uma instância da CVM, você deve reiniciá-la para validar as novas configurações. A operação de upgrade interromperá seus negócios por um curto período de tempo. Recomendamos que você faça upgrade das instâncias quando tiverem poucos negócios. Após o upgrade, as instâncias retomarão os negócios normalmente e não exigirão a reconfiguração do ambiente.

### Por que a estimativa de reembolso de um downgrade da CVM é 0?

Um motivo possível é que você adquiriu a instância com desconto, mas a configuração do downgrade é calculada de acordo com o preço original da instância. Quando o preço da instância adquirida com desconto for menor ou igual ao preço original da instância, o reembolso estimado será exibido como 0.

### Por que o upgrade da instância não entrou em vigor?

Finalizado o upgrade de uma instância, você deve reiniciá-la no console ou por meio de uma API.


