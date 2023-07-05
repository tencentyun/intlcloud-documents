## Descrição do problema
O usuário se depara com alta latência ao realizar login em CVMs localizados na América do Norte.

## Análise do problema
Devido à quantidade limitada de roteadores de saída internacional no país, a alta simultaneidade pode causar congestionamento de ligação e acesso instável. A Tencent Cloud relatou esse problema aos ISPs.
Caso necessite gerenciar dentro do país um CVM localizado na América do Norte, poderá adquirir um CVM localizado em Hong Kong (China) e usá-lo como ponto de transferência para fazer login no CVM localizado na América do Norte.

## Solução
1. Compre um CVM do Windows localizado em Hong Kong (China) como um **jump server (servidor trampolim)**.
> 
> - Na seção “1. Select a model (1. Selecione um modelo)” da página “Custom Configuration (Configuração personalizada)”, selecione **Hong Kong, China**.
> [Clique aqui para comprar >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1®ionId=5&zoneId=0&instanceType=S2ne.SMALL2&platform=CentOS&systemDiskType=CLOUD_PREMIUM&systemDiskSize=50&bandwidthType=BANDWIDTH_PREPAID&loginSet=SET_PASSWORD)
> - O sistema operacional Windows aceita o login em CVMs do Windows e do Linux localizados na América do Norte (mais indicada).
> - **Ao adquirir o CVM do Windows localizado em Hong Kong (China), você precisa comprar no mínimo 1 Mbps de largura de banda. Do contrário, você não conseguirá fazer login no servidor trampolim.**
>
2. Finalizada a compra, faça login no CVM do Windows localizado em Hong Kong (China) de acordo com suas necessidades:
 - [Login em uma instância do Windows usando o arquivo RDP](https://intl.cloud.tencent.com/document/product/213/5435)
 - [Login em uma instância do Windows via Área de Trabalho Remota](https://intl.cloud.tencent.com/document/product/213/32498)
 - [Login em uma instância do Windows via VNC](https://intl.cloud.tencent.com/document/product/213/32496)
3. Faça login em seu CVM localizado na América do Norte a partir do CVM do Windows localizado em Hong Kong (China) de acordo com suas necessidades:
 - Login em um CVM do Linux localizado na América do Norte
    - [Login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436)
    - [Login em uma instância do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
    - [Login em uma instância do Linux via chave SSH](https://intl.cloud.tencent.com/document/product/213/32501).
 - Login em um CVM do Windows localizado na América do Norte 
    - [Login em uma instância do Windows usando o arquivo RDP](https://intl.cloud.tencent.com/document/product/213/5435)
    - [Login em uma instância do Windows via Área de Trabalho Remota](https://intl.cloud.tencent.com/document/product/213/32498)
    - [Login em uma instância do Windows via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
