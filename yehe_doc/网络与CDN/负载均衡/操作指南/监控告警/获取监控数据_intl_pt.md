O Tencent Cloud Monitor coleta e exibe dados para a instância do CLB e o servidor de back-end, ajudando você a obter estatísticas do CLB, verificar se o sistema está funcionando normalmente e criar alarmes. Para obter mais informações sobre o Tencent Cloud Monitor, consulte a documentação do [Basic Cloud Monitor](https://intl.cloud.tencent.com/doc/product/248).

O Tencent Cloud fornece a funcionalidade Cloud Monitor para todos os usuários por padrão e não requer ativação manual. Você pode usar o Cloud Monitor para coletar os dados de monitoramento de suas instâncias do CLB e exibir os dados usando os seguintes métodos.

## Método do console do CLB
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb), clique no ícone de monitoramento ao lado do ID da instância do CLB e navegue pelos dados de desempenho da instância na janela flutuante.
![](https://main.qcloudimg.com/raw/6580c81d6fd1eee2234fcb5262a976bb.png)
2. Clique no ID/Nome da instância do CLB para acessar sua página de detalhes. Clique em **Monitoring (Monitoramento)** para exibir seus dados de monitoramento.
![](https://main.qcloudimg.com/raw/3eb231b336c9325ae16bfe2937e41b39.png)

## Método do console do Cloud Monitor
Faça login no [Console do Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) para exibir os dados de monitoramento do CLB. Clique em **Cloud Load Balancer**(https://console.cloud.tencent.com/monitor/clb) na barra lateral esquerda e, em seguida, clique no ID/nome da instância do CLB para acessar sua página de detalhes de monitoramento. É possível exibir os dados de monitoramento da instância do CLB e expandir sua lista suspensa para exibir o listener e as informações de monitoramento do servidor de back-end.

## Método de API
Use a API `GetMonitorData` para obter os dados de monitoramento de todos os produtos. Para obter mais informações, consulte [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881), [Métricas de monitoramento do CLB da rede pública](https://intl.cloud.tencent.com/document/product/248/10997), [Protocolo do CLB da rede privada da camada 4](https://intl.cloud.tencent.com/document/product/248/39529) e [Protocolo da camada 7](https://intl.cloud.tencent.com/document/product/248/39530).
