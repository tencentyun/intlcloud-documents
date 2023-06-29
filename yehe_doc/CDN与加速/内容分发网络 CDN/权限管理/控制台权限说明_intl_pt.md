
Depois de especificar `Action` e `Resource` para criar uma política personalizada, é possível chamar APIs para realizar operações para os recursos desejados. Este documento descreve os mapeamentos entre as funcionalidades do console e `Action`.

>!
> - O CDN do Tencent Cloud pode autorizar recursos por nome de domínio. A autorização não distingue entre regiões de serviço dentro e fora da China Continental com o mesmo nome de domínio.
> - Quando você migra os serviços do ECDN para o console do CDN, as políticas de permissão de API do ECDN serão mapeadas automaticamente para as políticas de permissão de API do CDN correspondentes. No entanto, para políticas de permissão em nível de recursos, você precisa defini-las novamente no CDN após a migração.

## Visão geral do serviço

A visão geral do serviço pode ser categorizada da seguinte forma com base no conteúdo exibido:

| Funcionalidade     | Ação autorizada                             | Observações                                            |
| ------------ | --------------------------------------- | ---------------------------------------------------- |
| Uso do serviço | DescribeCdnData<br/>DescribeBillingData | Se nem todos os nomes de domínio forem autorizados, o uso de cada nome de domínio terá que ser consultado separadamente |
| Estatísticas de nomes de domínio | DescribeDomains                         | A quantidade total de nomes de domínio autorizados será retornada                                 |
| Status de faturamento     | DescribePayType                         | Atualmente, a permissão para alterar o modo de faturamento não pode ser concedida a subcontas                        |
| Estatísticas do pacote de tráfego | DescribeTrafficPackages                 | O status do pacote de tráfego são dados no nível da conta e todos os recursos associados podem ser consultados       |

## Gerenciamento de nomes de domínio

| Funcionalidade         | Ação autorizada                                  | Observações                                                     |
| ---------------- | -------------------------------------------- | ------------------------------------------------------------ |
| Lista e consulta de nomes de domínio   | DescribeDomains                              | Os itens de configuração básica de um nome de domínio podem ser consultados, exibidos e baixados<br/>Para obter todos os itens de configuração detalhados, `DescribeDomainsConfig` deve ser autorizado |
| Adição de nomes de domínio         | DescribeDomains                              | Os nomes de domínio podem ser adicionados em qualquer região de serviço de aceleração                                  |
| Desativação de nomes de domínio         | StopCdnDomain                                | -                                                            |
| Ativação de nomes de domínio         | StartCdnDomain                               | -                                                            |
| Exclusão de nomes de domínio         | DeleteCdnDomain                              | -                                                            |
| Modificação do projeto de nomes de domínio | UpdateDomainConfig                           | O projeto de nomes de domínio está na configuração de nomes de domínio<br/>Todos os itens de configuração de um nome de domínio podem ser modificados depois da autorização |
| Gerenciamento da configuração de nomes de domínio     | UpdateDomainConfig<br/>DescribeDomainsConfig | Todos os itens de configuração de um nome de domínio podem ser exibidos/modificados depois da autorização                               |

## Gerenciamento de certificados

| Funcionalidade         | Ação autorizada                                  | Observações                                                     |
| ------------ | --------------------- | ------------------------ |
| Consulta da lista de certificados | DescribeDomainsConfig | Todos os itens de configuração de um nome de domínio podem ser exibidos depois da autorização |
| Configuração de certificados     | UpdateDomainConfig    | Todos os itens de configuração de um nome de domínio podem ser modificados depois da autorização |
| Configuração em lote de certificados | UpdateDomainsHttps    | É usada para configurar certificados em lotes         |

## Análise estatística

| Funcionalidade                                                     | Ação autorizada        | Observações                         |
| ------------------------------------------------------------ | ------------------ | -------------------------------- |
| Consulta de dados de acesso detalhados                                              | DescribeCdnData    | Todas as métricas de dados de acesso em um nome de domínio podem ser consultadas depois da autorização |
| Consulta de dados detalhados de pull de origem                                              | DescribeOriginData | Todas as métricas de dados de pull de origem em um nome de domínio podem ser consultadas depois da autorização |
| Consulta de tráfego/solicitações principais<br/>Consulta dos nomes de domínio principais<br/>Consulta de classificações de códigos de status de nomes de domínio<br/>Consulta de classificações de uso por província na China Continental<br/>Consulta de classificações de uso por ISP na China Continental<br/>Consulta de classificações de uso fora da China Continental | ListTopData        | As classificações de métricas e dimensões de dados diferentes podem ser consultadas depois da autorização  |
| Consulta do número de IPs exclusivos                                               | DescribeIpVisit    | -                                |

## Limpeza e pré-busca

| Funcionalidade     | Ação autorizada        |
| ------------ | ------------------ |
| Envio de URLs para limpeza | PurgeUrlsCache     |
| Envio de diretórios para limpeza | PurgePathCache     |
| Consulta de registros de limpeza | DescribePurgeTasks |
| Envio de tarefas de pré-busca | PushUrlsCache      |
| Consulta de registros de pré-busca | DescribePurgeTasks |

## Serviço de registro em log

| Funcionalidade       | Ação autorizada           |
| ---------------- | --------------------- |
| Consulta do link de download do log | DescribeCdnDomainLogs |

## Visão geral do status da rede

A página de monitoramento de status de toda a rede no console pode ser visualizada por todas as subcontas sem a necessidade de autorização.

## Relatório operacional

| Funcionalidades                                                     | Ação autorizada        | Observações                         |
| ------------------------------------------------------------ | ------------------ | -------------------------------- |
| Consulta de dados de acesso detalhados                                              | DescribeCdnData    | Todas as métricas de dados de acesso em um nome de domínio podem ser consultadas depois da autorização |
| Consulta de dados detalhados de pull de origem                                              | DescribeOriginData | Todas as métricas de dados de pull de origem em um nome de domínio podem ser consultadas depois da autorização |
| Consulta de tráfego/solicitações principais<br/>Consulta dos nomes de domínio principais<br/>Consulta de classificações de códigos de status de nomes de domínio<br/>Consulta de classificações de uso por província na China Continental<br/>Consulta de classificações de uso por ISP na China Continental<br/>Consulta de classificações de uso fora da China Continental | ListTopData        | As classificações de métricas e dimensões de dados diferentes podem ser consultadas depois da autorização  |
| Consulta do número de IPs exclusivos                                               | DescribeIpVisit    | -                                |

## Gerenciamento de pacotes de tráfego

| Funcionalidade       | Ação autorizada             | Observações                                           |
| -------------- | ----------------------- | -------------------------------------------------- |
| Consulta da lista de pacotes de tráfego | DescribeTrafficPackages | O conteúdo retornado pela API é irrelevante para o `Resource`. A lista pode ser consultada com qualquer recurso autorizado |

> !Atualmente, a renovação do pacote de tráfego e as lógicas de cancelamento de renovação não podem ser autorizadas.

## Consulta de propriedade de IP

| Funcionalidade                     | Ação autorizada   | Observações                                           |
| ---------------------------- | ------------- | -------------------------------------------------- |
| Consulta se o IP pertence ao CDN do Tencent Cloud | DescribeCdnIp | O conteúdo retornado pela API é irrelevante para o `Resource`. A lista pode ser consultada com qualquer recurso autorizado |

## Ferramenta de autodiagnóstico

Atualmente, a ferramenta de autodiagnóstico não pode ser autorizada para subcontas.
