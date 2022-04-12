Este documento descreve como ativar ou desativar o multicast para os VPCs.

## Informações gerais
O broadcast e o multicast são modos de comunicação um para muitos, que podem economizar a largura de banda da rede dos negócios e reduzir a carga da rede por meio da transmissão eficiente de dados ponto a multiponto.
No modo unicast, o servidor inicial envia dados para N servidores separadamente. No modo multicast, o servidor envia os mesmos dados para N servidores de uma vez, o que reduz o consumo de recursos do servidor e também o recurso de largura de banda do backbone da rede.
>?
>- Atualmente, as funcionalidades de broadcast e multicast estão em teste beta. Se você precisar usá-las, [envie uma solicitação](https://console.cloud.tencent.com/workorder/category).
>- No momento, as regiões que aceitam multicast e broadcast são: Pequim, Xangai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong da China, Singapura, Seul, Tóquio, Bangkok, Toronto, Vale do Silício, Virgínia, Frankfurt e Moscou.
>

- Multicast: a Tencent Cloud aceita o multicast no âmbito da VPC.
- Broadcast: a Tencent Cloud aceita o broadcast no âmbito da sub-rede.

## Visão geral
O multicast e o broadcast são usados principalmente nos setores financeiro e de jogos:
- Serviços de broadcast ou dados de mercado do setor financeiro. Por exemplo, depois de obter os preços das ações e outros dados em tempo real, os corretores podem transmitir dados de ações para vários clientes em tempo real, reduzindo muito a carga da rede.
- Para o setor de jogos, o broadcast e o multicast são usados principalmente para manter a conexão entre vários servidores.

## Instruções
### Ativação do multicast
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Na lista de VPCs, localize a VPC desejada e ative o **Multicast**.
![]()


### Desativação do multicast
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Na lista de VPCs, localize a VPC desejada e desative o **Multicast**.
![]()

## Referências
Para mais informações sobre o broadcast no nível de sub-redes, consulte [Ativação ou desativação do broadcast](https://intl.cloud.tencent.com/document/product/215/31809).

