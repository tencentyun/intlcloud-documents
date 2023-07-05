## Visão geral das configurações

O CDN do Tencent Cloud aceita a adição de cabeçalhos de solicitação de pull de origem:

- Transporta o IP real do cliente para o servidor de origem por meio do cabeçalho `X-Forwarded-For`.
- Transporta a porta real do cliente para o servidor de origem, para análise, por meio do cabeçalho `X-Forwarded-Port`.
- Adiciona cabeçalhos personalizados.

Também é possível definir e excluir cabeçalhos de solicitação de pull de origem personalizados.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Selecione a guia **Origin-pull Configuration (Configuração de pull de origem)** para localizar a seção **Origin-pull Request Header Configuration (Configuração de cabeçalho de solicitação de pull de origem)**. A funcionalidade fica desabilitada e não é pré-configurada por padrão.
![img](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)

### Operação

| Operação | Descrição                                                         |
| -------- | ------------------------------------------------------------ |
| Definir     | Define o valor de um parâmetro de cabeçalho de solicitação especificado.<br/>Se o cabeçalho de destino não existir, um novo será adicionado.<br/>Se o parâmetro de cabeçalho de solicitação de pull de origem já existir, o novo cabeçalho de solicitação substituirá o antigo, pois cabeçalhos duplicados não são permitidos.|
| Adicionar     | Adiciona um parâmetro de cabeçalho de solicitação de pull de origem especificado.<br/>Se o cabeçalho de destino já existir, o novo cabeçalho da solicitação substituirá o antigo, pois cabeçalhos duplicados não são permitidos.|
| Excluir     | Exclui um parâmetro de cabeçalho de solicitação especificado.                                       |

>!
> - As regras são executadas de baixo para cima e a prioridade é significativa apenas para o mesmo tipo de operações, ou seja, as prioridades de várias regras de "Definir", "Adicionar" e "Excluir" são independentes.
> - Se um parâmetro de cabeçalho de solicitação de pull de origem for configurado com várias regras de operações diferentes, as operações serão conduzidas na ordem de "Adicionar", "Excluir" e "Definir". Por exemplo, se o cabeçalho `X-CDN` estiver configurado com regras de "Adicionar", "Excluir" e "Definir", ele será adicionado, excluído e, por último, definido.

### Parâmetro do cabeçalho

| Parâmetro do cabeçalho       | Descrição                                                         |
| -------------- | ------------------------------------------------------------ |
| X-Forward-For  | O cabeçalho usado para transportar o IP real do cliente. Seu valor padrão é a variável `$client_ip`, que não pode ser modificada. |
| X-Forward-Port | O cabeçalho usado para transportar a porta real do cliente. Seu valor padrão é a variável `$remote_port`, que não pode ser modificada. |
| Cabeçalho personalizado     | Chave: 1 a 100 caracteres, incluindo dígitos (0 - 9), letras minúsculas (a - z), letras maiúsculas (A - Z) e hifens (-).<br>Valor: 1 a 1.000 caracteres. Caracteres chineses não são aceitos.<br>Alguns cabeçalhos padrão não podem ser definidos, adicionados ou excluídos pelo usuário. Para a lista detalhada, consulte [Observações](#notice). |

> !
> - Podem ser configuradas até 10 regras de cabeçalho de solicitações de pull de origem.
> - Tipos de regra aceitos: todo o conteúdo, tipo de arquivo especificado, pasta especificada e arquivo especificado. Atualmente, a correspondência de regex não é compatível.



## Exemplos de configuração

A configuração do cabeçalho da solicitação de pull de origem do nome de domínio de aceleração `cloud.tencent.com` é a seguinte:
![img](https://main.qcloudimg.com/raw/397759f6f138183d3f1ba60b33c7effc.png)
Se o recurso acessado for `http://cloud.tencent.com/test/test.mp4`:

1. Ele atinge a regra `*`, então o cabeçalho `X-Forward-For:$client_ip` será adicionado, e `$client_ip` será substituído pelo IP real do cliente durante o pull de origem.
2. Ele atinge a regra de tipo de arquivo `.mp4` e a regra de caminho `/test`. As duas regras são do mesmo tipo, "Adicionar". Como a regra inferior tem a prioridade mais alta, o cabeçalho `x-cdn:Tencent` é adicionado.

<span id="notice"></span>

## Observações
Atualmente, nas regras de cabeçalho de solicitação de pull de origem, os seguintes cabeçalhos padrão não podem ser definidos, adicionados ou excluídos:

| www-authenticate              | authorization                    | proxy-authenticate             | proxy-authorization                 |
| ----------------------------- | -------------------------------- | ------------------------------ | ----------------------------------- |
| age                           | cache-control                    | clear-site-data                | expires                             |
| pragma                        | warning                          | accept-ch                      | accept-ch-lifetime                  |
| early-data                    | content-dpr                      | dpr                            | device-memory                       |
| save-data                     | viewport-width                   | width                          | last-modified                       |
| etag                          | if-match                         | if-none-match                  | if-modified-since                   |
| if-unmodified-since           | vary                             | connection                     | keep-alive                          |
| accept                        | accept-charset                   | expect                         | max-forwards                        |
| access-control-allow-origin   | access-control-max-age           | access-control-allow-headers   | access-control-allow-methods        |
| access-control-expose-headers | access-control-allow-credentials | access-control-request-headers | access-control-request-method       |
| origin                        | timing-allow-origin              | dnt                            | tk                                  |
| content-disposition           | content-length                   | content-type                   | content-encoding                    |
| content-language              | content-location                 | forwarded                      | x-forwarded-host                    |
| x-forwarded-proto             | via                              | from                           | host                                |
| referer-policy                | allow                            | server                         | accept-ranges                       |
| range                         | if-range                         | content-range                  | cross-origin-embedder-policy        |
| cross-origin-opener-policy    | cross-origin-resource-policy     | content-security-policy        | content-security-policy-report-only |
| expect-ct                     | feature-policy                   | strict-transport-security      | upgrade-insecure-requests           |
| x-content-type-options        | x-download-options               | x-frame-options(xfo)           | x-permitted-cross-domain-policies   |
| x-powered-by                  | x-xss-protection                 | public-key-pins                | public-key-pins-report-only         |
| sec-fetch-site                | sec-fetch-mode                   | sec-fetch-user                 | sec-fetch-dest                      |
| last-event-id                 | nel                              | ping-from                      | ping-to                             |
| report-to                     | transfer-encoding                | te                             | trailer                             |
| sec-websocket-key             | sec-websocket-extensions         | sec-websocket-accept           | sec-websocket-protocol              |
| sec-websocket-version         | accept-push-policy               | accept-signature               | alt-svc                             |
| date                          | large-allocation                 | link                           | push-policy                         |
| retry-after                   | signature                        | signed-headers                 | server-timing                       |
| service-worker-allowed        | sourcemap                        | upgrade                        | x-dns-prefetch-control              |
| x-firefox-spdy                | x-pingback                       | x-requested-with               | x-robots-tag                        |
| x-ua-compatible               | max-age                          |                                |                                     |
