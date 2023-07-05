## Liberação da instância
### Por que uma instância spot é liberada automaticamente?
Uma característica importante das instâncias spot é que o sistema reaverá as instâncias atribuídas com base nos preços ou na relação oferta-demanda. Se o preço de mercado for superior à sua oferta ou se o pool de recursos da CVM correspondente às suas instâncias spot estiver em falta, o processo será interrompido pelo sistema.

### É possível evitar que a instância seja reavida pelo sistema por meio de ofertas?
Não. Porque a retomada de posse provocada por estoque insuficiente é inevitável. Você precisa aceitar que a retomada de posse da instância pode ocorrer quando implanta negócios na instância spot.

### Como sei que uma instância está prestes a ser interrompida?
Dois minutos antes da interrupção, notificaremos você na forma de metadados de que a instância está prestes a ser interrompida e reavida.
Para mais informações, consulte [Consulta do status de retomada de posse de uma instância spot](https://intl.cloud.tencent.com/document/product/213/32487).

### Como solicitar automaticamente instâncias spot após a recuperação do inventário?
Você pode usar produtos de nuvem que podem manter automaticamente o cluster da CVM, como o [BatchCompute](http://console.cloud.tencent.com/batch/env) e o [Auto Scaling](http://console.cloud.tencent.com/autoscaling). Com seus recursos entre modelos e entre zonas de disponibilidade, você pode manter uma quantidade especificada de clusters da CVM com mais eficiência.

## Preço e faturamento
### Quais são as semelhanças e as diferenças entre as instâncias spot e as instâncias com pagamento conforme o uso?
<table>
	<tr><th style="width: 14%">Método de faturamento</th><th style="width: 43%">Semelhanças</th><th style="width: 43%">Diferenças</th></tr>
	<tr><td>Instâncias spot</td><td rowspan=2>Ambas são com pagamento conforme o uso. Não há necessidade de pagar antecipadamente, mas alguns custos devem ser congelados. Você pode habilitar/encerrar a CVM a qualquer momento e pagar de acordo com o uso real. A granularidade do tempo de faturamento tem precisão de segundos, e a conta será liquidada a cada hora. </td><td rowspan=2><ul  style="margin: 0;"><li><b>Preço</b>: na maioria dos casos, o preço da instância spot é de 10% a 20% do preço da instância com pagamento conforme o uso com as mesmas especificações. </li><li><b>Mecanismo de liberação</b>: o ciclo de vida de uma instância com pagamento conforme o uso é controlado pelo usuário, já a instância spot pode ser reavida ativamente pelo sistema. </li><li><b>Limitações das funcionalidades</b>：não são permitidos ajustes de configuração. </li></ul></td></tr>
	<tr><td>Instâncias com pagamento conforme o uso</td></tr>
</table>

### Qual preço, o preço de mercado ou a oferta mais alta especificada pelo usuário, será usado para o faturamento?
O preço de mercado será usado para o faturamento. Você pode especificar uma oferta alta para evitar que as instâncias sejam reavidas devido ao preço. No entanto, o sistema cobrará apenas o preço de mercado atual (o preço de mercado atual será fixo).

### Como os períodos de faturamento são calculados para as instâncias spot?
Você será faturado pelo período desde o momento em que solicitar uma instância spot até o momento em que a instância spot for liberada manualmente ou interrompida pelo sistema. O período de faturamento tem precisão de segundos.

### Onde posso encontrar os preços atuais de mercado de todas as instâncias spot?
Durante o período de teste beta, não podemos fornecer uma página na qual você possa consultar os preços de mercado de todas as instâncias, mas ela estará disponível no futuro. Atualmente, a maioria das instâncias spot terá um preço de 20% das instâncias regulares com pagamento conforme o uso do mesmo modelo e especificação.

### Onde posso exibir os detalhes de consumo das instâncias spot?
Assim como nas instâncias com pagamento conforme o uso, você pode encontrar as informações detalhadas de uso e faturamento das instâncias spot em **Billing Center (Centro de faturamento)** > **Bills (Faturas)** na parte superior do console. As instâncias spot são serviços com pagamento conforme o uso.

## Cotas e limitações
### Em quais regiões as instâncias spot estão disponíveis? Quais modelos de instância e especificações são compatíveis com as instâncias spot?
<table>
<tr><th>Região</th><th>Modelos compatíveis com as instâncias spot</th><th>Descontos</th></tr>
<tr><td>Pequim, Xangai, Chengdu, Chongqing, Guangzhou aberta</td><td rowspan="4">Todos os modelos compatíveis com as instâncias com pagamento conforme o uso</td><td rowspan="4">80% de desconto nos preços publicados das instâncias com pagamento conforme o uso com as mesmas especificações</td></tr>
<tr><td>Guangzhou (exceto a Zona 1 de Guangzhou)</td></tr>
<tr><td>Hong Kong (China), Singapura, Bangkok, Seul, Tóquio, Mumbai, Toronto, Vale do Silício, Virgínia, Frankfurt</td></tr>
</table>

### Os limites de cota das instâncias spot são compartilhados com as instâncias com pagamento conforme o uso?
Não. Cada usuário pode ter até 50 núcleos de vCPU de instâncias spot em cada zona de disponibilidade. Para aumentar os limites de cota, envie um tíquete.

### Posso fazer upgrade ou downgrade das especificações das instâncias spot?
Não é permitido o upgrade ou o downgrade das especificações das instâncias spot.

### As instâncias spot possibilitam o interrompimento das cobranças quando desligadas?
As instâncias spot não possibilitam o interrompimento das cobranças quando desligadas.

### As instâncias spot são compatíveis com a reinstalação de sistema?
As instâncias spot não são compatíveis com a reinstalação de sistema.
