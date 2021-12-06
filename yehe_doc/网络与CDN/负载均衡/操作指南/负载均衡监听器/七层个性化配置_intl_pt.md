O CLB aceita configurações personalizadas, permitindo que você defina os parâmetros de configuração para uma única instância do CLB, como `client_max_body_size` e` ssl_protocols`, de modo a atender às suas necessidades exclusivas.
>?
>- Cada região pode ter até 200 entradas de configurações personalizadas.
>- As configurações personalizadas são limitadas a 64 KB.
>- Atualmente, cada instância pode ser vinculada a apenas uma entrada de configuração personalizada.
>- As configurações personalizadas são válidas apenas para listeners HTTP/HTTPS da camada 7 do CLB (anteriormente conhecido como CLB do aplicativo).

## Parâmetros de configuração personalizada do CLB
Atualmente, a configuração personalizada do CLB aceita os seguintes campos:

| Campo de configuração |   Valor padrão/Valor recomendado  |    Intervalo dos parâmetros  | Descrição  |
| :-------- | :-------- | :------ |:------ |
|ssl_protocols | TLSv1 TLSv1.1 TLSv1.2 |TLSv1 TLSv1.1 TLSv1.2 TLSv1.3 | Versão do protocolo TLS usado |
|  ssl_ciphers  | Veja mais abaixo. | Veja mais abaixo. | Pacote de criptografia |
|  client_header_timeout  | 60 s |  [30 a 120] s | O tempo limite de obtenção de um cabeçalho de solicitação do cliente. Caso ele seja atingido, um erro 408 será retornado.|
|  client_header_buffer_size | 4k |[1 a 256]k | Tamanho do buffer padrão em que um cabeçalho de solicitação do cliente é armazenado. |
|  client_body_timeout | 60 s |  [30 a 120] s | O tempo limite de obtenção de um corpo de solicitação do cliente, que não é o tempo de obtenção de todo o corpo, mas se refere ao período de inatividade sem transmissão de dados. Caso o tempo limite seja atingido, um erro 408 será retornado. |
|  client_max_body_size | 60 M |[1 a 10.240] M| <ul><li>Intervalo de configuração padrão: 1 MB a 256 MB; ele pode ser configurado diretamente.</li><li>Tamanho máximo: 2.048 MB; se `client_max_body_size` for mais do que 256 MB, o valor de <a href="#buffer">proxy_request_buffering</a> deve ser "off".</li></ul> |
|  keepalive_timeout | 75 s | [0 a 900] s| O tempo de espera de conexão persistente do `Client-server`; se for definido como 0, a conexão persistente é proibida. Se você quiser definir para mais de 900, envie uma solicitação(https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1). O valor máximo que você pode definir é 3.600. |
|  add_header |Personalizado| - | O campo de cabeçalho específico retornado ao cliente no formato de `add_header xxx yyy`. |
|  more_set_headers |Personalizado| - | O campo de cabeçalho específico retornado ao cliente no formato de `more_set_headers "A:B"`. |
|  proxy_connect_timeout | 4 s | [4 a 120] s |O tempo limite de conexão de back-end upstream.|
|  proxy_read_timeout |60 s |[30 a 3.600] s|O tempo limite de leitura da resposta de back-end upstream.|
|  proxy_send_timeout |60 s |[30 a 3.600] s|O tempo limite de envio de uma solicitação para o back-end upstream.|
|  server_tokens | on | on, off | <ul><li>`on`: exibe as informações de versão;</li><li>`off`: oculta as informações de versão.</li></ul>|
|  keepalive_requests | 100 | [1 a 10.000] |Quantidade máxima de solicitações que podem ser enviadas pela conexão persistente `client-server`.|
|  proxy_buffer_size | 4k |[1 a 64]k| Tamanho do cabeçalho de resposta do servidor, que é o tamanho de um único buffer definido em `proxy_buffer` por padrão; para usar `proxy_buffer_size`, `proxy_buffers` deve ser definido ao mesmo tempo.|
|  proxy_buffers | 8 4k |[3 a 8] [4 a 8]k|Quantidade e tamanho do buffer.|
|  <span id="buffer">proxy_request_buffering</span> | on |on, off|<ul><li>`on`: armazena em cache o corpo da solicitação do cliente; a instância do CLB armazena em cache a solicitação e a encaminha para a instância do CVM de back-end em várias partes depois que a solicitação é completamente recebida.</li><li>`off`: não armazena em cache o corpo da solicitação do cliente; após receber uma solicitação, a instância do CLB a encaminha diretamente para a instância do CVM de back-end, o que aumenta a pressão no desempenho do CVM de back-end.</li></ul>|
|  proxy_set_header   |X-Real-Port $remote_port|<ul><li>X-Real-Port $remote_port</li><li>X-clb-stgw-vip $server_addr</li><li>Stgw-request-id $stgw_request_id</li><li>X-Forwarded-Port $vport</li><li>X-Method $request_method</li><li>X-Uri $uri</li><li>X-Forwarded-Proto </li></ul>|<ul><li>`X-Real-Port $remote_port`: client port.</li><li>`X-clb-stgw-vip $server_addr`: VIP do CLB.</li><li>`Stgw-request-id $stgw_request_id`: ID da solicitação (usado apenas no CLB).</li><li>`X-Forwarded-Port`: porta do listener do CLB.</li><li>`X-Method`: método de solicitação do cliente.</li><li>`X-Uri`: URI de solicitação do cliente.</li><li>`X-Forwarded-Proto`: protocolo para a porta do listener do CLB (compatível por padrão).</li></ul> |
|  send_timeout | 60 s |[1 a 3.600] s|O tempo limite de transferência de dados do servidor para o cliente, que é o intervalo de tempo entre duas ações consecutivas de transferência de dados, e não todo o período de transferência da solicitação.|
|  ssl_verify_depth |  1 |[1, 10]|Profundidade da verificação da cadeia de certificados do cliente.|
|proxy_redirect | http:// https:// | http:// https://  | Se o servidor upstream retornar uma solicitação para redirecionar ou atualizar, por exemplo, o código de resposta HTTP 301 ou 302, o `proxy_redirect` vai redefinir http para https no campo "Location (Local)" ou "Refresh (Atualizar)" no cabeçalho HTTP, para um redirecionamento seguro.  |
| ssl_early_data  |  off |on, off| Ativa ou desativa o TLS 1.3 0-RTT. Somente quando o valor do campo de `ssl_protocols` contiver `TLSv1.3`, o `ssl_early_data` poderá ter efeito. **Você deve considerar o risco de ataques de reprodução antes de ativar `ssl_early_data`.**|
|http2_max_field_size|4k|[1 a 256]k|Restringe o tamanho máximo do cabeçalho da solicitação compactado em HPACK.|
|error_page|-|error_page code [ = [ response]] uri|Um URL predefinido será exibido para o código de erro específico. O código de resposta padrão é 302. O URI deve começar com `/`.|


>?Requisitos sobre o valor de `proxy_buffer_size` e `proxy_buffers`: 2 * max (proxy_buffer_size, proxy_buffers.size) ≤ (proxy_buffers.num - 1)\* proxy_buffers.size; Por exemplo, se `proxy_buffer_size` for "24k", `proxy_buffers` será "8 8k"; então 2 * 24k = 48k, (8 - 1)\* 8k = 56k; e 48k ≤ 56k; portanto, não haverá nenhum erro de configuração.
>
## Instruções de configuração do ssl_ciphers
O conjunto de criptografia ssl_ciphers que está sendo configurado deve estar no mesmo formato que o usado pelo OpenSSL. A lista de algoritmos é um ou mais `<cipher strings>`; vários algoritmos devem ser separados por ":"; ALL representa todos os algoritmos, "!" indica não ativar um algoritmo e "+" indica mover um algoritmo para o último lugar.
O algoritmo de criptografia para desativação forçada padrão é: `!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE`.

** Valor padrão:**
```plaintext
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE:3DES;
```

**Intervalo de parâmetros:**
```plaintext
ECDH-ECDSA-AES128-SHA256:ECDH-RSA-AES256-SHA:ECDH-ECDSA-AES256-SHA:SRP-DSS-AES-256-CBC-SHA:SRP-AES-128-CBC-SHA:ECDH-RSA-AES128-SHA256:DH-RSA-AES128-SHA256:DH-RSA-CAMELLIA128-SHA:DH-DSS-AES256-GCM-SHA384:DH-RSA-AES256-SHA256:AES256-SHA256:SEED-SHA:CAMELLIA256-SHA:ECDH-RSA-AES256-SHA384:ECDH-ECDSA-AES128-GCM-SHA256:DH-RSA-AES128-SHA:DH-RSA-AES128-GCM-SHA256:DH-DSS-AES128-SHA:ECDH-RSA-AES128-SHA:DH-DSS-CAMELLIA256-SHA:SRP-AES-256-CBC-SHA:DH-DSS-AES128-SHA256:SRP-RSA-AES-256-CBC-SHA:ECDH-ECDSA-AES256-GCM-SHA384:ECDH-RSA-AES256-GCM-SHA384:DH-DSS-AES256-SHA256:ECDH-ECDSA-AES256-SHA384:AES128-SHA:DH-DSS-AES128-GCM-SHA256:AES128-SHA256:DH-RSA-SEED-SHA:ECDH-ECDSA-AES128-SHA:IDEA-CBC-SHA:AES128-GCM-SHA256:DH-RSA-CAMELLIA256-SHA:CAMELLIA128-SHA:DH-RSA-AES256-GCM-SHA384:SRP-RSA-AES-128-CBC-SHA:SRP-DSS-AES-128-CBC-SHA:ECDH-RSA-AES128-GCM-SHA256:DH-DSS-CAMELLIA128-SHA:DH-DSS-SEED-SHA:AES256-SHA:DH-RSA-AES256-SHA:kEDH+AESGCM:AES256-GCM-SHA384:DH-DSS-AES256-SHA:HIGH:AES128:AES256:AES:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE
```

## Exemplos de configuração personalizada do CLB
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance/index?rid=8) e clique em **Custom Configuration (Configuração personalizada)** na barra lateral esquerda.
2. Clique em **Create (Criar)**, preencha os itens de configuração e termine com ";".
![](https://main.qcloudimg.com/raw/7ef70a06f9509ba8759e5a923515a471.png)
3. Clique em **Completed (Concluído)**.
4. Clique em **Bind to Instance (Vincular à instância)**.
5. Na janela pop-up, selecione uma instância do CLB da mesma região e clique em **Submit (Enviar)**.
![](https://main.qcloudimg.com/raw/ad8fb7874b9ce1fe7bf5c9366c7e64e7.png)
6. Agora, você pode exibir as informações de configuração personalizada correspondentes na página da lista de instâncias.
![](https://main.qcloudimg.com/raw/d07bdbc134480fa89f732c93c3861243.png)
Exemplo de código de configuração padrão:
```plaintext
ssl_protocols   TLSv1 TLSv1.1 TLSv1.2;
client_header_timeout   60s;
client_header_buffer_size   4k;
client_body_timeout    60s;
client_max_body_size   60M;
keepalive_timeout    75s;
add_header     xxx yyy;
more_set_headers      "A:B";
proxy_connect_timeout    4s;
proxy_read_timeout    60s;
proxy_send_timeout    60s;
```

