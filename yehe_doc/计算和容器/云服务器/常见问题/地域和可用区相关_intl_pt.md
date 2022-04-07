### Como posso exibir as regiões e as zonas de disponibilidade?

Para exibir as regiões e as zonas de disponibilidade, tente o seguinte:
- Consulte o documento [Regiões e zonas de disponibilidade](https://intl.cloud.tencent.com/document/product/213/6091).
- Use APIs para consultar as regiões e as zonas de disponibilidade.
 - Para exibir as regiões, use a API [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708).
 - Para exibir as zonas de disponibilidade, use a API [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071).


### Quais regiões e zonas de disponibilidade da CVM estão disponíveis e como escolher?

Para mais informações sobre as regiões e as zonas de disponibilidade disponíveis da CVM, consulte [Regiões e zonas de disponibilidade](http://intl.cloud.tencent.com/document/product/213/6091).
Para mais informações sobre como escolher as regiões e as zonas de disponibilidade, consulte [Como escolher as regiões e as zonas de disponibilidade](https://intl.cloud.tencent.com/document/product/213/6091#.E5.A6.82.E4.BD.95.E9.80.89.E6.8B.A9.E5.9C.B0.E5.9F.9F.E5.92.8C.E5.8F.AF.E7.94.A8.E5.8C.BA).


### Posso alterar a região de uma CVM adquirido?

Não. Você não pode alterar as regiões das CVMs adquiridos. Se você precisar implantar uma CVM existente em outra região ou zona de disponibilidade, tente o seguinte:
- [Encerre a instância](https://intl.cloud.tencent.com/document/product/213/4930) e adquira uma nova.

- Crie uma imagem personalizada da instância original. Depois, use a imagem personalizada para criar uma instância, iniciá-la e atualizar sua configuração em uma nova zona de disponibilidade.
  1. Crie uma imagem personalizada da instância atual. Para mais informações, consulte [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942).
  2. Se o [ambiente de rede](https://intl.cloud.tencent.com/document/product/213/5227) da instância atual for o VPC e você precisar manter o endereço IP privado após a migração, exclua a sub-rede na zona de disponibilidade atual e crie uma sub-rede na nova zona de disponibilidade com o mesmo intervalo de endereço IP da sub-rede original.
  > Se a sub-rede a ser excluída contiver instâncias disponíveis, primeiro migre todas as instâncias dela para a nova sub-rede.
  >
  3. Use a imagem personalizada recém-criada para criar uma nova instância na nova zona de disponibilidade.
  Você pode escolher o mesmo tipo e configuração de instância da instância original ou configurar novos para a nova instância. Para mais informações, consulte [Criação de uma instância](https://intl.cloud.tencent.com/document/product/213/4855).
  4. Se um endereço IP público elástico estiver associado à instância original, desassocie-o da instância original e associe-o à nova instância. Para mais informações, consulte [Endereços IP elásticos (EIPs)](https://intl.cloud.tencent.com/document/product/213/5733).
  5. (Opcional) Se os [modos de preços](https://intl.cloud.tencent.com/document/product/213/2180) da instância original forem com pagamento conforme o uso, você poderá encerrá-la. Para mais informações, consulte [Encerramento de instâncias](https://intl.cloud.tencent.com/document/product/213/4930).

### Os usuários da Tencent Cloud na China podem desfrutar da mesma qualidade de produtos e serviços dos recursos adquiridos na China e em outras regiões ou países?
Sim. O console da Tencent Cloud da China oferece a todos os usuários a mesma qualidade de produtos e serviços. A região de compra não afetará seus direitos de usuário no console.

### Posso usar a funcionalidade de replicação de uma imagem personalizada para migrar uma CVM na China Continental para outro país ou região?
- Não. As imagens só podem ser replicadas dentro do mesmo país ou região. Para replicar imagens entre países, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) para solicitar.

### Quais são as diferenças entre as instâncias dentro e fora da China Continental, e como determino qual região é a melhor para mim?
As instâncias em outros países ou regiões são implantadas fora da China Continental, oferecendo vantagens geográficas e de mercado para usuários globais. A rede local rápida também pode atender às necessidades dos clientes internacionais, o que é adequado para os usuários que administram negócios em outros países ou regiões.

- Para mais informações sobre as regiões compatíveis, consulte [Regiões e zonas de disponibilidade](https://intl.cloud.tencent.com/document/product/213/6091).

### Posso alternar entre os sistemas operacionais Linux e Windows em uma instância da CVM adquirida em uma região fora da China Continental?
Não. A alternância de SO entre Windows e Linux está disponível apenas para as instâncias da CVM na China Continental.

### Como posso solicitar serviços pós-venda para produtos adquiridos em regiões fora da China Continental?
Se você adquiriu um produto no site oficial da Tencent Cloud, ligue para a linha direta de serviços ininterrupta da Tencent Cloud (4009100100) ou [envie um tíquete](https://console.cloud.tencent.com/workorder/category).

### Como implantar instâncias da CVM em regiões fora da China?
As instâncias da CVM em regiões fora da China têm o mesmo método de implantação se tiverem o mesmo tipo de sistema operacional.

### Posso migrar instâncias para regiões fora da China Continental?
A região e a zona de disponibilidade de uma instância não podem ser alteradas. Para usar uma instância em outros países ou regiões, você precisa adquirir outra instância.

### Por que alguns tipos de instância só podem ser adquiridos nas regiões da China?
Algumas regiões podem não prover suporte a determinados tipos de instância. Para mais informações sobre os tipos de instância com suporte, acesse a [página de aquisição da CVM](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.78908498.770173325.1571651505) para exibir as informações de aquisição de instâncias.

### Se eu criar um site usando uma instância da CVM de uma região fora da China Continental e meus usuários acessarem o site por meio de um nome de domínio, esse nome de domínio precisa da declaração ICP?
Para sites em regiões da China Continental, a declaração ICP é obrigatória para os nomes de domínio. Para sites em outros países ou regiões, a declaração ICP não é necessária. 

### As instâncias em regiões diferentes têm o mesmo preço?
O preço de uma instância da CVM inclui suas especificações, armazenamento, largura de banda da rede etc. Os preços desses componentes variam de acordo com a região, portanto, o preço da instância será diferente.
Para mais informações sobre preços, consulte [Preços](https://buy.cloud.tencent.com/price/cvm/calculator).
