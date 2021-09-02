O Tencent Cloud oferece duas maneiras de adquirir uma instância do CVM: pagamento conforme o uso e instância spot. Cada uma é adequada para atender às diferentes necessidades dos clientes.
A tabela a seguir compara os dois planos de faturamento:

| Plano de faturamento da instância  | Pagamento conforme o uso | Instância spot |
|---------|:---------:|:---------:|
| Método de pagamento  | [Depósito](https://intl.cloud.tencent.com/document/product/555/12039) na aquisição, faturada por hora | [Depósito](https://intl.cloud.tencent.com/document/product/555/12039) na aquisição, faturada por hora |
| Unidade de pagamento  | USD/s | USD/s |
| Unidade de preço | Preço | O preço flutua. Na maioria dos casos, o preço é cerca de 10 a 20% do preço de uma instância com pagamento conforme o uso com as mesmas especificações. |
| Tempo mínimo de uso | Cobrada por segundo e faturada por hora. Adquira e libere a qualquer momento. | Cobrada por segundo e faturada por hora. Adquira e libere a qualquer momento. Pode ser reavida pelo sistema. |
| Alteração das configurações da instância | Sem limite. Altere a qualquer momento. | Não é aceito. |
| Casos de uso | Melhor para casos de uso em que a demanda da empresa flutua muito, como ofertas relâmpago de comércio eletrônico. | Melhor para casos de uso, como serviços online e de site que usam computação de big data e balanceamento de carga. |


## Pagamento conforme o uso

O pagamento conforme o uso é um plano de faturamento flexível para as instâncias do CVM. Você pode ativar e encerrar uma instância do CVM a qualquer momento. Você só precisa pagar o que usar com uma precisão de **segundos**, sem a necessidade de pagamento adiantado. Os recursos com pagamento conforme o uso serão faturados por hora. Esse plano de faturamento é adequado para casos de uso em que a demanda da empresa flutua muito, como ofertas relâmpago de comércio eletrônico.

Quando você ativa uma instância do CVM com pagamento conforme o uso, a cobrança de uma hora (incluindo encargos para a CPU, a memória e os discos de dados) será congelada no saldo da sua conta como um depósito. Você será faturado por hora (horário de Pequim) pelo uso na última hora. Quando você adquire uma instância do CVM, o preço é listado como uma taxa por hora. No entanto, você será **faturado por segundo** e a cobrança será arredondada para as duas casas decimais mais próximas. O faturamento começa no segundo em que a instância é criada e para no segundo em que a instância é encerrada.

Quando uma instância do CVM com pagamento conforme o uso é criada, a cobrança de uma hora é congelada no saldo da sua conta como um depósito. Ao alterar as configurações do CVM, o depósito atual será liberado e um novo depósito será congelado com base no preço unitário da nova configuração. Seu depósito será liberado de volta para sua conta quando a instância do CVM for encerrada.

Você pode habilitar a funcionalidade Sem Cobranças Quando Desligada para as instâncias com pagamento conforme o uso, para interromper o faturamento de taxas de CPU e de memória após o desligamento da instância. Para saber as limitações dessa funcionalidade, consulte a [Funcionalidade Sem Cobranças Quando Desligada para as instâncias com pagamento conforme o uso](https://intl.cloud.tencent.com/document/product/213/19918). 

## Instância spot

A instância spot é uma nova forma de usar e pagar por instâncias do CVM. Semelhante às com pagamento conforme o uso, ela permite que você seja cobrado por segundo e faturado por hora. Os preços das instâncias spot flutuam de acordo com a demanda do mercado, o que oferece um desconto substancial (cerca de 80 a 90% de desconto sobre os preços das instâncias com pagamento conforme o uso com as mesmas especificações). No entanto, as instâncias spot podem ser reavidas automaticamente pelo sistema como resultado de escassez de estoque ou ofertas mais altas de outros usuários.
- Para obter mais informações sobre as políticas, os casos de uso e as limitações da instância spot, consulte a [Instância spot](https://intl.cloud.tencent.com/document/product/213/17816).

