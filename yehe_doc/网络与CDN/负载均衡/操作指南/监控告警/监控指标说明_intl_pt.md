O Cloud Monitor coleta dados brutos das instâncias do CLB em execução e exibe as entradas de dados em gráficos intuitivos. As estatísticas serão mantidas por um mês por padrão. Você pode observar o funcionamento das instâncias no mês para se manter informado sobre o status dos serviços do aplicativo.

É possível acessar o [Console do Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) para exibir os dados de monitoramento do CLB. Clique em **Cloud Product Monitoring (Monitoramento de produto em nuvem)** -> [**Cloud Load Balancer**](https://console.cloud.tencent.com/monitor/clb) e, em seguida, clique no ID da instância do CLB para acessar a página de detalhes de monitoramento. É possível exibir os dados de monitoramento da instância do CLB e expandi-los para exibir o listener e as informações de monitoramento do servidor de back-end.

## Nível da instância do CLB
>?A utilização da largura de banda de entrada e a utilização da largura de banda de saída são aplicáveis a todas as regiões de serviço, exceto Tóquio e Bangkok. Essas duas métricas são apenas para contas de faturamento por IP. Para verificar o seu tipo de conta, consulte [Verificação do tipo de conta](https://intl.cloud.tencent.com/document/product/684/15246).

| Métrica | Unidade | Descrição |
|----|------|----|
| Largura de banda de entrada | Mbps | A largura de banda usada pelo cliente para acessar o CLB na rede pública dentro do período de referência. |
| Largura de banda de saída | Mbps | A largura de banda usada pelo CLB para acessar a rede pública dentro do período de referência. |
| Pacotes de entrada | Pacotes/s | A quantidade de pacotes de dados de solicitações recebidos pelo CLB por segundo dentro do período de referência. |
| Pacotes de saída | Pacotes/s | A quantidade de pacotes de dados enviados por CLB por segundo dentro do período de referência. |
|Conexões perdidas | Conexões/s  | A quantidade de conexões perdidas pelo CLB por segundo dentro do período de referência.|
|Largura de banda de entrada perdida | bps  | A largura de banda de entrada perdida pelo CLB por segundo dentro do período de referência.|
|Largura de banda de saída perdida | bps  | A largura de banda de saída perdida pelo CLB por segundo dentro do período de referência.|
|Pacotes de dados de entrada perdidos | Pacotes/s  |A quantidade de pacotes de dados de entrada perdidos pelo CLB por segundo dentro do período de referência. |
|Pacotes de dados de saída perdidos | Pacotes/s  |A quantidade de pacotes de dados de saída perdidos pelo CLB por segundo dentro do período de referência. |
|Utilização de largura de banda de entrada | %  | A utilização da largura de banda de entrada do CLB dentro do período de referência.|
|Utilização de largura de banda de saída | %  | A utilização da largura de banda de saída do CLB dentro do período de referência.|


## Nível do listener (TCP/UDP) da camada 4
Os listeners da camada 4 permitem que você exiba as métricas de monitoramento em três níveis:
- Nível do listener
- Nível do servidor de back-end
- Nível da porta do servidor de back-end

| Métrica | Unidade | Descrição |
|----|------|----|
| Conexões | Contagem | A quantidade de conexões no listener dentro do período de referência. |
| Novas conexões | Contagem | A quantidade de conexões novas no listener dentro do período de referência. |
| Largura de banda de entrada | Mbps | A largura de banda usada pelo cliente para acessar o CLB na rede pública dentro do período de referência. |
| Largura de banda de saída | Mbps | A largura de banda usada pelo CLB para acessar a rede pública dentro do período de referência. |
| Pacotes de entrada | Pacotes/s | A quantidade de pacotes de dados de solicitações recebidos pelo CLB por segundo dentro do período de referência. |
| Pacotes de saída | Pacotes/s | A quantidade de pacotes de dados enviados por CLB por segundo dentro do período de referência. |

## Nível do listener (HTTP/HTTPS) da camada 7
Os listeners da camada 7 permitem que você exiba as métricas de monitoramento em cinco níveis:
- Nível do listener
- Nível do nome de domínio
- Nível do caminho de encaminhamento de URL
- Nível do servidor de back-end
- Nível da porta do servidor de back-end

| Métrica | Unidade | Descrição |
|----|------|----|
| Conexões | - | A quantidade de conexões no listener dentro do período de referência. |
| Novas conexões | - | A quantidade de conexões novas no listener dentro do período de referência. |
| Largura de banda de entrada | Mbps | A largura de banda usada pelo cliente para acessar o CLB na rede pública dentro do período de referência. |
| Largura de banda de saída | Mbps | A largura de banda usada pelo CLB para acessar a rede pública dentro do período de referência. |
| Pacotes de entrada | Pacotes/s | A quantidade de pacotes de dados de solicitações recebidos pelo CLB por segundo dentro do período de referência. |
| Pacotes de saída | Pacotes/s | A quantidade de pacotes de dados enviados por CLB por segundo dentro do período de referência. |
| Duração média da solicitação | ms | A duração média da solicitação do CLB dentro do período de referência. A duração começa no ponto em que a instância do CLB recebe o primeiro byte do cliente e termina quando ela envia o último byte ao cliente. |
| Duração máxima da solicitação | ms | A duração máxima da solicitação do CLB dentro do período de referência. A duração começa no ponto em que a instância do CLB recebe o primeiro byte do cliente e termina quando ela envia o último byte ao cliente. |
| Duração média da resposta | ms | A duração média da resposta do servidor de back-end dentro do período de referência. A duração se refere a toda a duração da solicitação, começando do ponto em que a instância do CLB se conecta ao servidor de back-end e terminando quando o servidor de back-end recebe o último byte da resposta. |
| Duração máxima da resposta | ms | A duração máxima da resposta do servidor de back-end dentro do período de referência. A duração se refere a toda a duração da solicitação, começando do ponto em que a instância do CLB se conecta ao servidor de back-end e terminando quando o servidor de back-end recebe o último byte da resposta. |
| Solicitações expiradas | Solicitações/minuto |  A quantidade de solicitações expiradas dentro do período de referência.  |
| Solicitações bem-sucedidas por minuto | Solicitações/minuto |  A quantidade de solicitações bem-sucedidas do CLB por minuto dentro do período de referência.|
| Solicitações por segundo | - | A quantidade de solicitações do CLB por segundo no período de referência, ou seja, QPS. |
| Código de status 2xx | - | A quantidade de códigos de status 2xx retornados pelo servidor de back-end dentro do período de referência. |
| Código de status 3xx | - | A quantidade de códigos de status 3xx retornados pelo servidor de back-end dentro do período de referência. |
| Código de status 4xx | - | A quantidade de códigos de status 4xx retornados pelo servidor de back-end dentro do período de referência. |
| Código de status 5xx | - | A quantidade de códigos de status 5xx retornados pelo servidor de back-end dentro do período de referência. |
| Código de status 404 | - | A quantidade de códigos de status 404 retornados pelo servidor de back-end dentro do período de referência. |
| Código de status 502 | - | A quantidade de códigos de status 502 retornados pelo servidor de back-end dentro do período de referência. |
| Códigos de status 3xx retornados pelo CLB | - | A quantidade de códigos de status 3xx retornados pelo CLB dentro do período de referência (soma dos códigos de retorno do CLB e do servidor de back-end).|
| Códigos de status 4xx retornados pelo CLB | - | A quantidade de códigos de status 4xx retornados pelo CLB dentro do período de referência (soma dos códigos de retorno do CLB e do servidor de back-end).|
| Códigos de status 5xx retornados pelo CLB | - | A quantidade de códigos de status 5xx retornados pelo CLB dentro do período de referência (soma dos códigos de retorno do CLB e do servidor de back-end).|
| Códigos de status 404 retornados pelo CLB | - | A quantidade de códigos de status 404 retornados pelo CLB dentro do período de referência (soma dos códigos de retorno do CLB e do servidor de back-end).|
| Códigos de status 502 retornados pelo CLB | - | A quantidade de códigos de status 502 retornados pelo CLB dentro do período de referência (soma dos códigos de retorno do CLB e do servidor de back-end).|

>!Se você deseja exibir os dados de monitoramento de uma instância do CVM em um listener, faça login no [Console do CLB](https://console.cloud.tencent.com/clb), clique no ícone da barra de monitoramento próximo ao ID da instância do CLB e, em seguida, navegue pelos dados de desempenho de cada instância na janela flutuante.

