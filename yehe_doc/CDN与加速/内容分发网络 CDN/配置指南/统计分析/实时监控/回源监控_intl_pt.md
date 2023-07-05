

>!  Atualmente, a consulta de dados de pull de origem não está disponível para nomes de domínio do ECDN.

## Descrição das métricas
### Métricas na página de visão geral
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e selecione **Statistics (Estatísticas)** > **Realtime Monitoring (Monitoramento em tempo real)** na barra lateral esquerda para acessar a página de gerenciamento. A guia **Access Monitoring (Monitoramento de acesso)** é exibida por padrão. Você pode clicar em **Origin-Pull Monitoring (Monitoramento de pull de origem)** à direita para acessar a página de métricas de monitoramento de pull de origem. As curvas de monitoramento de todos os nomes de domínio com granularidade de 1 minuto nas últimas 6 horas serão retornadas, incluindo as seguintes métricas:
+ Largura de banda de pull de origem: calculada dividindo o tráfego total de pull de origem em um minuto por 60 segundos.
+ Tráfego de pull de origem: o tráfego total de pull de origem no nó de cache na última camada.
+ Solicitações de pull de origem: a quantidade total de solicitações de pull de origem no nó de cache na última camada.
+ Taxa de falha de pull de origem: a porcentagem de solicitações de pull de origem com falha de todas as solicitações de pull de origem.
+ Porcentagem do código de status de pull de origem: Gráficos de porcentagem dos códigos de status (2XX/3XX/4XX/5XX) retornados para solicitações de pull de origem no período selecionado.
+ Códigos de status 2XX de pull de origem: os códigos de status gerados pelo monitoramento de código de status 2XX de pull de origem serão contabilizados.
+ Códigos de status 3XX de pull de origem: os códigos de status gerados pelo monitoramento de código de status 3XX de pull de origem serão contabilizados.
+ Códigos de status 4XX de pull de origem: os códigos de status gerados pelo monitoramento de código de status 4XX de pull de origem serão contabilizados.
+ Códigos de status 5XX de pull de origem: os códigos de status gerados pelo monitoramento de código de status 5XX de pull de origem serão contabilizados.

**As seguintes condições serão contabilizadas como solicitações de pull de origem com falha:**
+ Tempo limite no recebimento de dados de pull de origem.
+ Tempo limite no envio de solicitação de pull de origem.
+ Tempo limite no estabelecimento de uma conexão TCP para pull de origem.
+ O servidor de origem fecha ativamente a conexão.
+ Erro de compatibilidade do protocolo HTTP do servidor de origem.

### Dados na página de detalhes
Clique em **Learn More (Mais informações)** em cada métrica para acessar a página de detalhes da métrica.
![](https://main.qcloudimg.com/raw/f63c60b1e8d89db0302c9e102548fe70.png)
Também é possível alternar para outra métrica selecionando-a na lista suspensa no canto superior esquerdo da página de detalhes.
![](https://main.qcloudimg.com/raw/795eeb398f3f73663f5168f3b41612c4.png)

## Descrição da granularidade
### Granularidade na página de visão geral
A página de monitoramento oferece opções para exibir curvas de dados em granularidade de 1 minuto, 5 minutos, 1 hora ou 1 dia. A granularidade de tempo mínima que pode ser exibida varia de acordo com o período selecionado.
+ Período ≤ 6 horas: a granularidade de tempo mínima é de 1 minuto. A latência para exibir a curva de 1 minuto é de cerca de 3 minutos.
+ 6 horas < período ≤ 24 horas: a granularidade de tempo mínima é de 5 minutos. A latência para exibir a curva de 5 minutos é de cerca de 5 a 10 minutos.
+ 24 horas < período ≤ 31 dias: a granularidade de tempo mínima é de 1 hora.
+ Período > 31 dias: a granularidade de tempo mínima é de 1 dia.


### Granularidade na página de detalhes
As opções de granularidade de tempo na página de detalhes de métricas são as seguintes:
+ Período ≤ 24 horas: a granularidade de tempo mínima é de 1 minuto. A latência para exibir a curva de 1 minuto é de cerca de 3 minutos.
+ 24 horas < período ≤ 31 dias: A granularidade de tempo mínima pode ser 5 minutos, 1 hora ou 1 dia.
+ Período > 31 dias: a granularidade de tempo mínima é de 1 dia.

>!
>- Os dados coletados em uma granularidade de 1 minuto podem ser consultados apenas na nova versão do console. Para dados históricos, a granularidade mínima para consulta é 5 minutos.
>- O período máximo de consulta é de 90 dias.

### Descrição da agregação
O método para agregar dados de 1 minuto em dados de 5 minutos, 1 hora ou 1 dia varia de acordo com a métrica de dados.
+ Largura de banda de pull de origem: a menor granularidade fornecida pelo CDN para monitorar dados de largura de banda é de 1 minuto. Com base no padrão do setor, as taxas costumam ser cobradas por granularidade de 5 minutos, que é calculada considerando a média dos valores de dados de 1 minuto. Portanto, os dados de largura de banda em uma granularidade de 1 hora ou 1 dia podem ser calculados com base no valor máximo de largura de banda de 5 minutos.
+ Tráfego de pull de origem: os dados de tráfego em uma granularidade de 5 minutos, 1 hora ou 1 dia são obtidos pela agregação de dados de tráfego de 1 minuto.
+ Solicitações de pull de origem: as contagens de solicitações em uma granularidade de 5 minutos, 1 hora ou 1 dia são obtidas pela agregação de contagens de solicitações de 1 minuto.
+ Taxa de falha de pull de origem: calculado dividindo a quantidade total de falhas de pull de origem pela quantidade total de solicitações de pull de origem com base na granularidade de tempo selecionada.
+ Códigos de status de pull de origem: os dados de códigos de status em uma granularidade de 5 minutos, 1 hora ou 1 dia são obtidos pela agregação de dados de códigos de status de 1 minuto.



