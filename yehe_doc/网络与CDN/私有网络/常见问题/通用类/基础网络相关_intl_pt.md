### Qual é a diferença entre uma rede clássica e um VPC?
- Um Virtual Private Cloud (VPC) é um espaço de rede logicamente isolado na Tencent Cloud.
- Os VPCs fornecem mais funcionalidades do que a rede clássica. Para mais informações sobre suas diferenças e como escolher entre eles, consulte [Gerenciamento de redes clássicas](https://intl.cloud.tencent.com/document/product/215/31807).

### Posso mudar uma CVM de uma rede clássica para um VPC? 
Sim. A Tencent Cloud permite migrar uma CVM ou um lote de CVMs de uma rede clássica para um VPC. Para mais etapas e instruções detalhadas, consulte [Alteração para VPC](https://intl.cloud.tencent.com/document/product/213/20278).
>!Essa operação não pode ser desfeita. Leia atentamente o documento antes de realizá-la.

### Posso mudar uma CVM de um VPC para uma rede clássica?
Não. Um VPC fornece mais funcionalidades com maior flexibilidade e, portanto, recomendamos que você migre os CVMs da rede clássica para o VPC.

### Como posso estabelecer comunicação entre uma CVM da rede clássica e uma CVM baseado no VPC?
Você pode usar o [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) para estabelecer a comunicação entre a rede clássica e o VPC.
O uso do Classiclink está sujeito às seguintes limitações:
1. A rede clássica e o VPC que precisam se comunicar estão localizados na mesma região (podem estar em zonas de disponibilidade diferentes, como Zona 1 de Guangzhou e Zona 2 de Guangzhou).
2. O bloco CIDR do VPC (intervalo de IP) deve estar dentro de `10.[0-47].0.0/16` (incluindo subconjuntos). Caso contrário, haverá conflitos.

Se a rede clássica e o VPC atenderem a essas condições, você poderá configurar o Classiclink na página de detalhes do VPC no console, a fim de associar o VPC aos CVMs da rede clássica para interconexão.

### Os recursos como Cloud Load Balancers e bancos de dados na rede clássica podem se comunicar com o VPC?
- Uma conexão de terminal ajuda a estabelecer a comunicação entre as instâncias em um VPC e outras instâncias em uma rede clássica por meio da rede privada. Ela mapeia os endereços IP de instâncias da rede clássica para endereços IP do VPC, permitindo que você acesse as instâncias da rede clássica por meio de um endereço IP do VPC. Os produtos da rede clássica, incluindo o CLB clássico, o TencentDB, o CMEM, o REDIS e o MongoDB, podem se comunicar com o VPC dessa maneira. A comunicação entre regiões e entre contas diferentes não é aceita.
- Direção: unidirecional (o VPC acessa a rede clássica).
- Se necessário, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para solicitar.

### As instâncias da rede clássica e do VPC em contas diferentes podem se comunicar?
Não. Um VPC fornece mais funcionalidades com maior flexibilidade e, portanto, recomendamos que você migre os recursos da rede clássica para o VPC.

### Como posso desassociar uma CVM de um VPC ou de uma rede clássica?
Realize as etapas a seguir para desassociar uma CVM.
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc/vpc).
2. Clique no ID do VPC que está interconectado com a rede clássica para acessar a página de detalhes do VPC.
3. Clique em **Classiclink**. Na lista de CVMs da rede clássica, selecione a CVM a ser desassociada e clique em **Disassociate (Desassociar)**.
4. Clique em **OK**.

Para mais instruções detalhadas, consulte a seção “Desassociação de uma CVM do VPC e da rede clássica” em [Gerenciamento de redes clássicas](https://intl.cloud.tencent.com/document/product/215/31807).
