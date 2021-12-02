Este documento descreve como habilitar ou desabilitar o multicast para os VPCs.

## Informações gerais
O multicast e o broadcast são modos de comunicação um para muitos, que podem ajudar as empresas a reduzir o consumo de largura de banda da rede e a carga da rede por meio da transmissão de dados eficiente ponto a multiponto.
Se o unicast for usado, o servidor de envio precisará enviar separadamente para N servidores por um total de N vezes. Se o multicast for usado, o servidor envia os mesmos dados para N servidores apenas uma vez, reduzindo assim o consumo de recursos do servidor e de largura de banda da rede de backbone.
>?Atualmente, as funcionalidades broadcast e multicast estão em beta. Para testá-las, envie uma solicitação.
>
- Multicast: o Tencent Cloud fornece o multicast em um VPC.
- Broadcast: o Tencent Cloud fornece o broadcast em uma sub-rede.

## Casos de uso
O multicast e o broadcast são usados principalmente nos setores financeiro e de jogos:
- Serviços de broadcast ou dados de mercado do setor financeiro. Por exemplo, após obter os preços das ações e outros dados em tempo real, os corretores podem transmitir dados de ações para vários clientes em tempo real, reduzindo muito a carga da rede.
- Para o setor de jogos, o broadcast e o multicast são usados principalmente para manter a conexão entre vários servidores.

## Instruções
### Habilitação do multicast
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Na lista de VPCs, localize o VPC para o qual deseja habilitar o multicast e clique em **Enable (Habilitar)** na coluna **Multicast**.


### Desabilitação do multicast
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Na lista de VPCs, localize o VPC para o qual deseja desabilitar o multicast e clique em **Disable (Desabilitar)** na coluna **Multicast**.


## Operações relevantes
Para obter instruções detalhadas sobre o broadcast da sub-rede, consulte [Habilitação ou desabilitação do broadcast e do multicast](https://intl.cloud.tencent.com/document/product/215/31809).

