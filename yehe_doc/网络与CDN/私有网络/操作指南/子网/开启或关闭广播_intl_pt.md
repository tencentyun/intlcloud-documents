## Informações gerais
O multicast e o broadcast são modos de comunicação um para muitos, que podem ajudar as empresas a reduzir o consumo de largura de banda da rede e a carga da rede por meio da transmissão eficiente de dados ponto a multiponto.
No modo unicast, o servidor inicial envia dados para N servidores separadamente. No modo multicast, o servidor envia os mesmos dados para N servidores de uma vez, o que reduz o consumo de recursos do servidor e também o recurso de largura de banda do backbone da rede.
- Multicast: a Tencent Cloud aceita o multicast no âmbito da VPC.
- Broadcast: a Tencent Cloud aceita o broadcast no âmbito da sub-rede.

>?
>- Atualmente, as funcionalidades de broadcast e multicast estão em teste beta. Se você precisar usá-las, [envie uma solicitação](https://console.cloud.tencent.com/workorder/category).
>- No momento, as regiões que aceitam multicast e broadcast são: Pequim, Xangai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong da China, Singapura, Seul, Tóquio, Bangkok, Toronto, Vale do Silício, Virgínia, Frankfurt e Moscou.
>

## Visão geral
O multicast e o broadcast são usados principalmente nos setores financeiro e de jogos:
- Serviços de broadcast ou dados de mercado do setor financeiro. Por exemplo, depois de obter os preços das ações e outros dados em tempo real, os corretores podem transmitir dados de ações para vários clientes em tempo real, reduzindo muito a carga da rede.
- Para o setor de jogos, o broadcast e o multicast são usados principalmente para manter a conexão entre vários servidores.

Este documento descreve como ativar ou desativar o broadcast para sub-redes.

## Instruções
### Ativação do broadcast
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Subnet (Sub-rede)** na barra lateral esquerda, para acessar a página de admin.
3. Na lista de VPCs, localize a VPC em questão e alterne para **Enable (Ativar)** na coluna **Subnet broadcast (Broadcast da sub-rede)**.
![]()

### Desativação do broadcast
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Subnet (Sub-rede)** na barra lateral esquerda, para acessar a página de admin.
3. Na lista de VPCs, localize a VPC em questão e alterne para **Disable (Desativar)** na coluna **Subnet broadcast (Broadcast da sub-rede)**.
![]()

## Referências
Para mais informações sobre o multicast no nível da VPC, consulte [Ativação ou desativação do multicast](https://intl.cloud.tencent.com/document/product/215/40072).

