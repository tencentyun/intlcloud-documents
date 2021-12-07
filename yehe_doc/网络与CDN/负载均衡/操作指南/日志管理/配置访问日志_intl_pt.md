O CLB oferece suporte à configuração de logs de acesso da camada 7 (HTTP/HTTPS) que podem ajudá-lo a entender melhor as solicitações do cliente, solucionar problemas e analisar o comportamento do usuário. Atualmente, os logs de acesso podem ser armazenados no CLS, relatados em uma granularidade de minuto e pesquisados on-line por várias regras.

Os logs de acesso do CLB são usados principalmente para localizar e solucionar problemas rapidamente. O recurso de log de acesso inclui relatórios de log, armazenamento e pesquisa:
- O relatório de log oferece serviço de melhor esforço, ou seja, prioriza o encaminhamento de serviço em detrimento de relatório de log.
- O armazenamento de log e a pesquisa fornecem SLA com base no serviço de armazenamento atualmente em uso.

>?
>- Atualmente, os logs de acesso podem ser armazenados no CLS apenas para protocolos da camada 7 (HTTP/HTTPS), mas não para os protocolos da camada 4 (TCP/UDP/TCP SSL).
- Agora, o armazenamento de logs de acesso do CLB no CLS é gratuito. Você só precisa pagar pelo serviço do CLS.
- Este recurso só é compatível em regiões nas quais o CLS está disponível. Veja [Regiões disponíveis](https://intl.cloud.tencent.com/document/product/614/18940).



## Método 1: Registro de acesso de instância única
### Etapa 1. Habilitar armazenamento de log de acesso no CLS
1. Faça login no [console do CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3) e clique em **Instance Management (Gerenciamento de instâncias)** na barra lateral esquerda.
2. Clique no ID da instância do CLB para abrir a página **Instance Management (Gerenciamento de instâncias)**.
3. Clique no ícone de lápis no módulo **Access Log (Layer-7) (Log de acesso (Camada 7))** na página **Basic Information (Informações básicas)**.
![](https://main.qcloudimg.com/raw/b3f9b4276b4ff2f28ac184478ce7964c.png)
4. Na janela pop-up **Modify CLS Log Storage Location (Modificar local de armazenamento de log do CLS)**, ative o log e selecione o conjunto de logs de destino e o tópico de log para o armazenamento de logs de acesso e clique em **Submit (Enviar)**. Se você ainda não criou um conjunto de logs ou tópico de log, [crie recursos relevantes](https://console.cloud.tencent.com/cls/logset) e selecione-os como o local de armazenamento.
![](https://main.qcloudimg.com/raw/33386c84ae812881548d1b621fbe6a70.png)
>?Recomenda-se usar um tópico de log marcado com "CLB" no conjunto de logs clb_logset. As diferenças entre um tópico de log marcado com "CLB" e um comum são:
>- Os tópicos de log CLB podem criar um índice automaticamente, enquanto um tópico de log comum requer a criação manual de índice.
>- Um painel é fornecido para tópicos de log CLB por padrão, mas precisa ser configurado manualmente para um tópico de log comum.
6. Clique no conjunto de logs ou no tópico de log para redirecionar para a página de pesquisa de log no CLS.
7. (Opcional) Para desativar o log, clique no ícone de lápis para abrir a janela **Modify CLS Lo Storage Location (Modificar local de armazenamento de log do CLS)** e desative-a.

### Etapa 2. Configurar índices de tópico de log
>?Se o log de acesso for configurado para uma única instância, é preciso configurar o índice para o tópico de log; caso contrário, nenhum log pode ser encontrado.
>
Os índices recomendados são os seguintes:

| Índice de valor de chave | Tipo de campo | Delimitador |
| :---------- | :------- | :----- |
| server_addr | text     | Não é necessário delimitador     |
| server_name | text     | Não é necessário delimitador     |
| http_host | text     | Não é necessário delimitador     |
| status      | long     | -     |
| vip_vpcid   | long     | -     |

As etapas são as seguintes:
1. Faça login no [Console do CLS](https://console.cloud.tencent.com/cls) e clique em **Log Topic (Tópico de log)** na barra lateral esquerda.
2. Clique no ID do tópico de log de destino na página "Log Topic (Tópico de log)".
3. Na página de detalhes do tópico de log, selecione a guia **Index Configuration (Configuração de índice)** e clique em **Edit (Editar)** para adicionar índices. Consulte [Configuração de índice](https://intl.cloud.tencent.com/document/product/614/39594) para obter mais informações sobre a configuração do índice.
![](https://main.qcloudimg.com/raw/38b22da412497a25ac9d6d304766d1ac.png)
4. O resultado da configuração de índice é conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/6e2393e34cd06c5d073faba88d34110f.png)

### Etapa 3. Visualizar logs de acesso
1. Faça login no [Console do CLS](https://console.cloud.tencent.com/cls) e clique em **Search and Analysis (Pesquisa e análise)** na barra lateral esquerda.
2. Na página **Search and Analysis (Pesquisa e análise)**, selecione um conjunto de logs, tópico de log e intervalo de tempo e clique em **Search and Analysis (Pesquisa e análise)** para pesquisar os logs de acesso relatados pelo CLB ao CLS. Consulte [Sintaxe de pesquisa de CLS legado](https://intl.cloud.tencent.com/document/product/614/37882) para obter mais informações sobre a sintaxe de pesquisa.
![](https://main.qcloudimg.com/raw/e15271ea2d1ffac0e735eb254224a5e5.png)

## Método 2: Configuração de log de acesso em lote
>?No momento, este recurso está disponível apenas para usuários beta. Para usá-lo, você pode enviar uma requisição.
### Etapa 1. Criar conjuntos de logs e tópicos de log[](id:step2)
Para configurar os logs de acesso no CLS, é preciso primeiro criar um conjunto de logs e um tópico de log.
É possível pular diretamente para a [Etapa 2](#step3) se tiver criado um conjunto de logs e um tópico de log.
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb) e selecione **Access Logs (Logs de acesso)** na barra lateral esquerda.
2. Na página **Access Logs (Logs de acesso)**, selecione uma região para o conjunto de logs e clique em **Create Logset (Criar conjunto de logs)** na seção "Logset Information (Informações do conjunto de logs)".
3. Na caixa de diálogo pop-up **Create Logset (Criar conjunto de log)**, defina o período de retenção e clique em **Save (Salvar)**.
>?É possível criar apenas um único conjunto de logs denominado "clb_logset" em cada região.
4. Clique em **Create Log Topic (Criar tópico de log)** na seção **Log Topic (Tópico de log)** da página "Access Logs (Logs de acesso)".
5. Na janela pop-up, selecione uma instância do CLB para adicionar à lista à direita e clique em **Save (Salvar)**.
>?
>- Ao criar um tópico de log, você pode adicionar uma instância do CLB conforme necessário. Para adicionar uma, selecione um tópico de log na lista e clique em **Manage (Gerenciar)** na coluna de operação. Cada instância do CLB só pode ser adicionada a um tópico de log.
>- Um conjunto de logs pode conter vários tópicos de log. Você pode categorizar os logs do CLB em vários tópicos de log que serão marcados com "CLB".
>
![](https://main.qcloudimg.com/raw/9f19f80439f0044768eac4cc235aae9d.png)
6. (Opcional) Para desabilitar o log, basta clicar em **Disable (Desabilitar)**.

### Etapa 2. Ver logs de acesso [](id:step3)
Sem nenhuma configuração manual, o CLB foi configurado automaticamente com pesquisa de índice por importância de log de acesso. É possível consultar diretamente os logs de acesso por meio de pesquisa e análise.
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb) e selecione **Access Logs (Logs de acesso)** na barra lateral esquerda.
2. Selecione um tópico de log e clique em **Search (Pesquisar)** na coluna de operação para redirecionar para a página **Search and Analysis (Pesquisa e análise)** no [Console do CLS](https://console.cloud.tencent.com/cls/search).
3. Na página **Search and Analysis (Pesquisa e análise)**, insira a sintaxe de pesquisa na caixa de entrada, selecione um intervalo de tempo e clique em **Search and Analysis (Pesquisa e análise)** para pesquisar os logs de acesso relatados pelo CLB ao CLS.
>?Consulte [Sintaxe e regras](https://intl.cloud.tencent.com/document/product/614/30439) para obter mais informações sobre a sintaxe de pesquisa.


## Formato do log e descrição da variável
### Formato de log
```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port]  [$server_name] [$remote_addr:$remote_port] [$status] [$upstream_addr] [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer] [$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$vip_vpcid] [$uri] [$server_protocol]
```

### Tipo de campo
Atualmente, o CLS é compatível com os três tipos de campo a seguir:

| Name   | Descrição do tipo     |
| :----- | :----------------------- |
| text   | Tipo de texto     |
| long   | Tipo inteiro (Int 64) |
| double | Tipo ponto flutuante (64 bit) |

## Descrição de variável de log
<table class="table"><thead><tr><th>Variável</th><th>Descrição</th></tr></thead>Tipo de campo</th></tr></thead>
<tbody><tr><td>stgw_request_id</td><td> Solicitar ID. </td></tr>text</td></tr>
<tr><td>time_local</td><td> Tempo de acesso e fuso horário, como "01/Jul/2019:11:11:00 +0800", em que "+0800" representa UTC+8, ou seja, horário de Pequim.</td><td>text</td></tr>
<tr><td>protocol_type</td><td> Tipo de protocolo (HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>text</td></tr>
<tr><td>server_addr</td><td>VIP do CLB. </td><td>text</td></tr>
<tr><td>server_port</td><td>VPort do CLB, ou seja, a porta de escuta</td><td>long</td></tr>
<tr><td>server_name</td><td> `server_name` de uma regra, ou seja, o nome de domínio configurado em um listener do CLB.</td><td>text</td></tr>
<tr><td>remote_addr</td><td> IP do cliente IP.</td><td>text</td>
<tr><td>remote_port</td><td> Porta do cliente</td><td>long</td></tr>
<tr><td>status</td><td> Código de status retornado para o cliente. </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> Endereço RS.</td><td>text</td>
<tr><td>upstream_status</td><td> Código de status retornado pelo RS ao CLB. </td><td>text</td></tr>
<tr><td>proxy_host</td><td> ID do fluxo. </td><td>text</td>
<tr><td>request</td><td> Linha de solicitação. </td><td>text</td></tr>
<tr><td>request_length</td><td> Número de bytes da solicitação recebida do cliente.</td><td>long</td></tr>
<tr><td>bytes_sent</td><td> Número de bytes enviados para o cliente.<td>long</td></tr>
<tr><td>http_host</td><td> Nome do domínio solicitado, ou seja, o host do cabeçalho HTTP.</td><td>text</td></tr>
<tr><td>http_user_agent</td><td> campo `user_agent` do cabeçalho HTTP.</td><td>text</td></tr>
<tr><td>http_referer</td><td> Origem de solicitação HTTP. </td><td>text</td></tr>
<tr><td>request_time</td><td> Tempo de processamento da solicitação. O tempo começa a contar quando o primeiro byte é recebido do cliente e para quando o último byte é enviado ao cliente; ou seja, o tempo total que todo o processo leva, quando a solicitação do cliente atinge uma instância do CLB, a instância do CLB encaminha a solicitação para um RS, o RS responde e envia dados para a instância do CLB e, finalmente, a instância do CLB encaminha os dados para o cliente.</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td> O tempo que leva todo um processo de solicitação de back-end. O tempo começa a contar quando uma instância do CLB se conecta a um RS e para quando o RS recebe a solicitação e responde.<td>double</td></tr>
<tr><td>upstream_connect_time</td><td> O tempo que leva para estabelecer uma conexão TCP com um RS. O tempo começa a contar quando uma instância do CLB se conecta a um RS e para quando a solicitação HTTP é enviada.</td><td>double</td></tr>
<tr><td>upstream_header_time</td><td> O tempo para receber um cabeçalho HTTP do RS. O tempo começa a contar quando uma instância do CLB se conecta a um RS e para quando o cabeçalho de resposta HTTP é recebido do RS.</td><td>double</td></tr>
<tr><td>tcpinfo_rtt</td><td> RTT de conexão TCP. </td><td>long</td></tr>
<tr><td>connection</td><td> ID de conexão. </td><td>long</td></tr>
<tr><td>connection_requests</td><td> Número de solicitações na conexão. </td><td>long</td></tr>
<tr><td>ssl_handshake_time</td><td> O tempo que leva um handshake SSL. </td><td>double</td></tr>
<tr><td>ssl_cipher</td><td> Pacote de criptografia SSL.</td><td>text</td></tr>
<tr><td>ssl_protocol</td><td> Versão do protocolo SSL</td><td>text</td></tr>
<tr><td>vip_vpcid</td><td>ID VPC de um VIP do CLB; o `vip_vpcid` de uma instância do CLB de rede pública é `-1`.</td><td>long</td></tr>
<tr><td>request</td><td> Método de solicitação. Apenas solicitações POST e GET são compatíveis.</td><td>text</td></tr>
<tr><td>uri</td><td> Identificador de recurso.</td><td>text</td></tr>
<tr><td>server_protocol</td><td>Protocolo usado para CLB.</td><td>text</td></tr>
</tbody></table>

### Pesquisa padrão por importância de log
Os seguintes campos podem ser encontrados em conjuntos de logs com "CLB" por padrão:
<table class="table"><thead><tr><th>Campo de índice</th><th>Descrição</th></tr>Tipo de campo</th></tr></thead>
<tbody>
<tr><td>time_local</td><td> Tempo de acesso e fuso horário, como "01/Jul/2019:11:11:00 +0800", em que "+0800" representa UTC+8, ou seja, horário de Pequim.</td><td>text</td></tr>
<tr><td>protocol_type</td><td> Tipo de protocolo (HTTP/HTTPS/SPDY/HTTP2/WS/WSS).</td><td>text</td></tr>
<tr><td>server_addr</td><td>VIP do CLB. </td><td>text</td></tr>
<tr><td>server_name</td><td> `server_name` de uma regra, ou seja, o nome de domínio configurado em um listener do CLB.</td><td>text</td></tr>
<tr><td>remote_addr</td><td> IP do cliente IP.</td><td>text</td>
<tr><td>status</td><td> Código de status retornado para o cliente. </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> Endereço RS.</td><td>text</td>
<tr><td>upstream_status</td><td> Código de status retornado pelo RS ao CLB. </td><td>text</td></tr>
<tr><td>request_length</td><td> Número de bytes da solicitação recebida do cliente.</td><td>long</td></tr>
<tr><td>bytes_sent</td><td> Número de bytes enviados para o cliente.<td>long</td></tr>
<tr><td>http_host</td><td> Nome do domínio solicitado, ou seja, o host do cabeçalho HTTP.</td><td>text</td></tr>
<tr><td>request_time</td><td> Tempo de processamento da solicitação. O tempo começa a contar quando o primeiro byte é recebido do cliente e para quando o último byte é enviado ao cliente; ou seja, o tempo total que todo o processo leva, quando a solicitação do cliente atinge uma instância do CLB, a instância do CLB encaminha a solicitação para um RS, o RS responde e envia dados para a instância do CLB e, finalmente, a instância do CLB encaminha os dados para o cliente.</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td> O tempo que leva todo um processo de solicitação de back-end. O tempo começa a contar quando uma instância do CLB se conecta a um RS e para quando o RS recebe a solicitação e responde.<td>double</td></tr>
</tbody></table>
