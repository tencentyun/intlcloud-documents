
## Visão geral das configurações
Normalmente, quando um nó do CDN efetua pull de um recurso solicitado do servidor de origem (com um código de status 2XX retornado), o nó processará o recurso com base nas regras na configuração de validade do cache do nó.
Se o servidor de origem não conseguir processar rapidamente as solicitações que não tiverem o código de status 2XX e você não quiser que todas as solicitações sejam enviadas para o servidor de origem, é possível configurar o período de validade do cache do código de status. Nesse caso, o nó do CDN responderá diretamente às solicitações que não tiverem o código de status 2XX, ajudando a reduzir a pressão no servidor de origem.
Atualmente, os códigos de status aceitos são os seguintes:
- 4XX: 400, 401, 403, 404, 405, 407, 414
- 5XX: 500, 501, 502, 503, 504, 509, 514

>! 
>- Por enquanto, algumas plataformas aceitam apenas os códigos 404 e 403. Concluiremos a atualização do servidor o mais breve possível.
>- Atualmente, apenas os códigos de status 404 e 403 são aceitos em regiões fora da China Continental. Se a região de aceleração de um nome de domínio for "Global", as regras de cache do código de status, exceto 404 e 403, só terão efeito na China Continental.


## Guia de configuração

### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Mude para a guia ***Cache Configuration (Configuração de cache)** para localizar a seção **Status Code Cache (Cache de códigos de status)**.
Existe uma regra padrão, que armazenará em cache as solicitações 404 por dez segundos.
![](https://main.qcloudimg.com/raw/508f716869f48fad3424fe6eeb77a67c.png)

### Adição de regras
Você pode clicar em **Add Rule (Adicionar regra)** para adicionar regras de cache de códigos de status, conforme necessário.
<img src="https://main.qcloudimg.com/raw/3f01868799d0ddeda302e52e634bbde1.png" style="height:185px"/>

Limitações de configuração
- Cada código de status pode ter apenas uma regra exclusiva.
- O tempo de cache `0` significa não armazenar o conteúdo em cache.
