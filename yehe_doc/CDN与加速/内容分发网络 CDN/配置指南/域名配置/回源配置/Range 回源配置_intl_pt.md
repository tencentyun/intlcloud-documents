## Visão geral das configurações
O CDN do Tencent Cloud divide um arquivo em vários fragmentos para melhorar a eficiência de armazenamento dos recursos em cache. Ele também aceita solicitações de intervalo. Por exemplo, se uma solicitação transporta o cabeçalho HTTP `Range: bytes = 0-999`, os primeiros 1.000 bytes do arquivo serão retornados ao usuário.

Após a ativação do GETs de intervalo, se um arquivo parcial solicitado por um usuário tiver expirado, o CDN executará GETs de intervalo para efetuar pull do arquivo parcial necessário, armazená-lo em cache e retorná-lo ao usuário. Depois que GETs de intervalo for desativado, mesmo se um usuário solicitar apenas um arquivo parcial, o CDN efetuará pull do arquivo inteiro e o armazenará em cache antes de retornar o arquivo parcial solicitado ao usuário.

Ativar os GETs de intervalo pode aumentar muito a eficiência de entrega de arquivos grandes, além de reduzir o tempo de resposta e a pressão no servidor de origem.

> ?
> - Depois que GETs de intervalo for ativado, os recursos serão armazenados em cache em fragmentos nos nós. Esses fragmentos têm o mesmo período de validade do cache e seguem a regra de validade do cache definida pelo usuário.
> - Para ativar a configuração de GETs de intervalo, certifique-se de que o servidor de origem aceita solicitações de intervalo, ou o pull de origem pode falhar.

## Guia de configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Origin-pull Configuration (Configuração de pull de origem)** para exibir a seção **Range GETs Configuration (Configuração de GETs de intervalo)**.

Por padrão, ela fica desativada. Se o nome de domínio tiver o COS como servidor de origem, a configuração fica ativa por padrão. É possível ativá-la e desativá-la conforme necessário.
![](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)



## Exemplos de configuração
Se a configuração de GETs de intervalo do nome de domínio `cloud.tencent.com` for a seguinte:
![](https://main.qcloudimg.com/raw/04b9ec63d365b60ba2c3a8c16bc61c36.png)
O usuário A faz uma solicitação para o recurso `http://cloud.tencent.com/test.apk`. Depois que o nó receber a solicitação e perceber que o arquivo em cache `test.apk` já expirou, ele iniciará uma solicitação de GETs de intervalo para obter e armazenar em cache o recurso por fragmentos. Se o usuário B também fizer uma solicitação de intervalo neste momento e os fragmentos armazenados no nó corresponderem aos segmentos de bytes especificados na solicitação de intervalo, o recurso será retornado diretamente ao usuário B, embora os fragmentos não sejam completamente obtidos.

