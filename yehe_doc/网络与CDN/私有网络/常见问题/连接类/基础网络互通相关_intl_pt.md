### O que é o Classiclink?
O Classiclink é usado para associar os CVMs na rede clássica ao VPC específico, permitindo que os CVMs se comuniquem com serviços da Tencent Cloud, incluindo os CVMs e os bancos de dados no VPC. Para mais informações, consulte [Gerenciamento de redes clássicas](https://intl.cloud.tencent.com/document/product/215/31807).

### Como posso estabelecer a comunicação entre uma CVM em uma rede clássica e uma CVM em um VPC?
Você pode usar o [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) para estabelecer a comunicação entre as redes clássicas e os VPCs.
Ao usar o Classiclink, atenção os seguintes limites:
1. A rede clássica e o VPC que precisam se comunicar devem estar na mesma região (mas podem estar em zonas de disponibilidade diferentes, como Zona 1 de Guangzhou e Zona 2 de Guangzhou).
2. O CIDR (intervalo de IP) do VPC deve ser `10.0.0.0/16 - 10.47.0.0/16` (incluindo subconjuntos), caso contrário ocorrerá um conflito.

Se a rede clássica e o VPC atenderem a essas condições, você poderá configurar a guia **Classiclink** na página de detalhes do VPC no console, a fim de associar o VPC aos CVMs na rede clássica para interconexão.

### Os recursos como Cloud Load Balancers e bancos de dados na rede clássica podem se comunicar com o VPC?
- Uma conexão de terminal ajuda a estabelecer a comunicação entre as instâncias em um VPC e outras instâncias em uma rede clássica por meio da rede privada. O princípio é mapear os endereços IP de instâncias na rede clássica para endereços IP do VPC, a fim de que você possa acessar uma instância da rede clássica acessando o endereço IP do VPC correspondente. Os serviços que aceitam a rede clássica incluem o CLB clássico, o TencentDB, o CMEM, o REDIS e o MongoDB. A comunicação entre regiões e entre contas diferentes não é aceita.
- Direção: unidirecional (o VPC acessa a rede clássica).
- Se precisar de mais direções, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para solicitar.

### As instâncias da rede clássica e do VPC em contas diferentes podem se comunicar?
Não. Atualmente, os recursos (CVMs e bancos de dados) em instâncias da rede clássica e do VPC em contas diferentes não podem se comunicar entre si. Um VPC fornece mais funcionalidades com maior flexibilidade, por isso recomendamos a migração da rede clássica para o VPC.
