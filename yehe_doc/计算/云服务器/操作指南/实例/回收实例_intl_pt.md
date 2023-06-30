Este documento descreve como recuperar uma instância do Cloud Virtual Machine (CVM) da Lixeira. Para obter mais informações, consulte [Pagamento em atraso](https://intl.cloud.tencent.com/document/product/213/2181). 

## Lixeira
A Lixeira do Tencent Cloud fornece um mecanismo de retomada de posse da instância do CVM da seguinte maneira:
- **Instâncias com pagamento conforme o uso**: a instância com pagamento conforme o uso entrará na Lixeira depois de ser encerrada pelo usuário ou no horário programado. Se a conta estiver em atraso, a instância com pagamento conforme o uso não entrará na Lixeira. Ela será liberada depois que a conta estiver em atraso por 2 horas e 15 dias.

### Instâncias com pagamento conforme o uso na Lixeira

 - **Período de retenção**: a instância encerrada pelo usuário ficará retida na Lixeira por 2 horas.
 - **Processamento de expiração**: se as instâncias não forem renovadas antes do término do período de retenção, o sistema vai liberar os recursos da instância e automaticamente [encerrar as instâncias](https://intl.cloud.tencent.com/document/product/213/4930), que não poderão ser recuperadas. Os IPs elásticos vinculados a essas instâncias também serão liberados.
 - **Relacionamento de montagem**: depois que a instância entra na Lixeira, seu relacionamento de montagem com o Cloud Load Balancer, o Cloud Block Storage e o Classiclink **não será encerrado automaticamente**.
 - **Restrição de operação**: as instâncias na Lixeira só podem ser [restauradas depois da renovação](https://intl.cloud.tencent.com/document/product/213/6143) ou [encerradas](https://intl.cloud.tencent.com/document/product/213/4930). Alguns tipos de instâncias aceitam a [criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942)
 
>! 
> - Não é possível restaurar instâncias com pagamento conforme o uso da Lixeira se sua conta estiver em atraso. Primeiro, renove o pagamento.
> - As instâncias com pagamento conforme o uso são mantidas na Lixeira por no máximo 2 horas. Observe a hora de liberação e renove o pagamento a tempo para restaurar as instâncias.
> - As Instâncias com pagamento conforme o uso não podem entrar na Lixeira se sua conta estiver em atraso. É possível visualizá-las na página da lista de instâncias do CVM. As instâncias serão liberadas depois que a sua conta estiver em atraso por 2 horas e 15 dias.

## Recuperação de instâncias
 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Na barra lateral esquerda, clique em **Recycle Bin (Lixeira)** -> **Instance Recycle Bin (Lixeira de instâncias)** para entrar na lista de lixeira do CVM.
 3. Recuperar uma única instância: localize a instância a ser recuperada na lista, clique em **Recover (Recuperar)** na coluna **Operation (Operação)** e conclua o pagamento da renovação.
 4. Recuperar instâncias em lotes: selecione todas as instâncias a serem recuperadas, clique em **Recover Selected (Recuperar selecionadas)** na parte superior e conclua o pagamento da renovação.

