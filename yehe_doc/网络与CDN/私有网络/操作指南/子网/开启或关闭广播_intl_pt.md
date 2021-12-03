## Informações gerais
O multicast e o broadcast são modos de comunicação um para muitos, que podem ajudar as empresas a reduzir o consumo de largura de banda da rede e a carga da rede por meio da transmissão de dados eficiente ponto a multiponto.
Se o unicast for usado, o servidor de envio precisará enviar separadamente para N servidores por um total de N vezes. Se o multicast for usado, o servidor envia os mesmos dados para N servidores apenas uma vez, reduzindo assim o consumo de recursos do servidor e de largura de banda da rede de backbone.
- Multicast: o Tencent Cloud é compatível com o multicast no âmbito do VPC.
- Broadcast: o Tencent Cloud é compatível com o broadcast no âmbito da sub-rede.

>? Atualmente, as funcionalidades broadcast e multicast estão em beta. Se você precisar usá-las, envie uma solicitação.

## Visão geral
O multicast e o broadcast são usados principalmente nos setores financeiro e de jogos:
- Serviços de broadcast ou dados de mercado do setor financeiro. Por exemplo, após obter os preços das ações e outros dados em tempo real, os corretores podem transmitir dados de ações para vários clientes em tempo real, reduzindo muito a carga da rede.
- Para o setor de jogos, o broadcast e o multicast são usados principalmente para manter a conexão entre vários servidores.

Este documento descreve como habilitar ou desabilitar o broadcast para sub-redes.

## Instruções
### Habilitação do broadcast
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Subnet (Sub-rede)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Na lista de VPCs, localize o VPC para o qual deseja habilitar o broadcast e deslize para **Enable (Habilitar)** na coluna **Subnet broadcast (Broadcast da sub-rede)**.

### Desabilitação do broadcast
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Subnet (Sub-rede)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Na lista de VPCs, localize o VPC para o qual deseja desabilitar o broadcast e deslize para **Disable (Desabilitar)** na coluna **Subnet broadcast (Broadcast da sub-rede)**.

## Operações
Para obter instruções detalhadas sobre o multicast do VPC, consulte [Habilitação ou desabilitação do broadcast e do multicast](https://intl.cloud.tencent.com/document/product/215/31809).

