## Visão geral

O Tencent Cloud fornece a funcionalidade Cloud Monitor para todos os usuários por padrão. Essa funcionalidade ajuda a monitorar e coletar dados dos produtos do Tencent Cloud que você estiver usando. Este documento descreve como obter os dados de monitoramento.

## Direções
### Obtenção dos dados de monitoramento do console do CVM
>? O console do CVM fornece uma página de monitoramento, na qual você pode visualizar os dados de monitoramento de CPU, memória, largura de banda de rede e discos no período especificado.
>
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm).
2. Na página de gerenciamento da instância, clique no ID/Nome do CVM para acessar sua página de detalhes e visualizar os dados de monitoramento.
3. Clique na guia **Monitoring (Monitoramento)** para obter os dados de monitoramento da instância.

### Obtenção dos dados de monitoramento do console do Cloud Monitor
>? O console do Cloud Monitor fornece os dados de monitoramento de todos os produtos do Tencent Cloud. No console, você pode visualizar os dados de monitoramento de CPU, memória, largura de banda de rede e discos no período especificado.
>
1. Faça login no [Console do Cloud Monitor](https://console.cloud.tencent.com/monitor/overview).
2. Selecione **Cloud Product Monitoring (Monitoramento de produto em nuvem)** > **Cloud Virtual Machine** na barra lateral esquerda.
3. Clique no ID/Nome da instância do CVM para acessar sua página de detalhes e visualizar os dados de monitoramento.

### Obtenção dos dados de monitoramento do painel do Cloud Monitor
Especifique as métricas do CVM necessárias e crie um painel, no qual é possível visualizar os dados de monitoramento em gráficos intuitivos, ajudando você a analisar as métricas por meio de tendências e valores excepcionais.
1. Faça login no console do Cloud Monitor e selecione **Dashboard (Painel)** > [**Default Dashboard (Painel padrão)**](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=8).
2. Crie um painel conforme as instruções em [Criar painel](https://intl.cloud.tencent.com/document/product/248/35282) e obtenha os dados de monitoramento.


### Obtenção dos dados de monitoramento por API
Você pode usar a API `GetMonitorData` para obter os dados de monitoramento de todos os produtos do Tencent Cloud. Para obter mais informações, consulte [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881).
