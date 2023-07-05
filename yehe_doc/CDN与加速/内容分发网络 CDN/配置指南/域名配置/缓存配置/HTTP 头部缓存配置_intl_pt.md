

## Visão geral das configurações
Além dos recursos, o CDN do Tencent Cloud também armazenará em cache os seguintes cabeçalhos do servidor de origem e os retornará aos usuários por padrão:
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

Se o servidor de origem tiver cabeçalhos especiais que precisem ser armazenados em cache e devolvidos aos usuários pelo CDN, você pode ativar o cache de cabeçalhos.

## Guia de configuração
### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Cache Configuration (Configuração de cache)** para localizar a seção **HTTP Header Cache Configuration (Configuração de cache do cabeçalho HTTP)**. A configuração fica ativada por padrão e você pode desativá-la conforme necessário.
![](https://main.qcloudimg.com/raw/0fb4739f743b6242c463672a2f059098.png)





