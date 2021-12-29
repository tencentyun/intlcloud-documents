## Criação de listener HTTP/HTTPS

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Access Management (Gerenciamento de acesso)** e clique em **ID/Connection Name (ID/Nome da conexão)** da conexão especificada.
2. Na página exibida, selecione **HTTP/HTTPS Listener Management (Gerenciamento de listener HTTP/HTTPS)** > **Create (Criar)**. É possível selecionar o protocolo HTTP ou HTTPS. (Observação: atualmente, a configuração do listener HTTP/HTTPS não é aceita em conexões IPv6.)
3. A configuração específica é mostrada abaixo:
   1. Se HTTP for selecionado, apenas o número da porta será necessário e o listener encaminhará pacotes pelo protocolo HTTP, por padrão.
![](https://main.qcloudimg.com/raw/0096d45b44fbd916012317a49a97a884.png)
   2. Se HTTPS for selecionado, os certificados e informações adicionais precisam ser configurados conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/941665ba354633d345929e3fbd02fa8c.png)
      - **Listeners communicate with the origin server using HTTP protocol (Os listeners se comunicam com o servidor de origem usando o protocolo HTTP)** significa que o protocolo HTTPS é usado entre o cliente e o VIP de conexão de aceleração, já o protocolo HTTP é usado entre o VIP e o servidor de origem, que requer uma porta HTTP para ser aberto no servidor de origem.
        **Listeners communicate with the origin server using HTTPS protocol (Os listeners se comunicam com o servidor de origem usando o protocolo HTTPS)** significa que o protocolo HTTPS é usado entre o cliente e o servidor de origem, que requer uma porta HTTPS para ser aberto no servidor de origem.
      - SSL Parsing (Análise SSL): são aceitas a autenticação unilateral e bidirecional.
      - Server/Client Certificate (Certificado do servidor/cliente): é necessário fazer o upload de um certificado ou atualizá-lo em **Certificate Management (Gerenciamento de certificados)** no console do GAAP e, em seguida, selecioná-lo ao criar/modificar um listener HTTPS. Para obter mais informações, consulte [Gerenciamento de certificados](https://intl.cloud.tencent.com/document/product/608/42343).

## Configuração de listener HTTP/HTTPS

Abra a guia **HTTP/HTTPS Listener Management (Gerenciamento de listener HTTP/HTTPS)** e clique em **Set Rule (Definir regra)** na coluna **Operation (Operação)** para inserir o nome de domínio e a página de gerenciamento de URL.

### Adição de nome de domínio

Para adicionar um nome de domínio para um listener HTTP, basta inseri-lo no formato especificado. Apenas a correspondência exata é aceita. Um nome de domínio pode conter de 3 a 80 caracteres dos seguintes tipos: `a–z`, `0–9`, `_` e `–`.
 ![](https://qcloudimg.tencent-cloud.cn/raw/fed0aa02e83804a36799763b0f88cf33.png)
Para adicionar um nome de domínio para um listener HTTPS, basta inseri-lo e selecionar o certificado do servidor correspondente. O certificado selecionado durante a criação do listener é usado no console por padrão. Se você carregar um novo certificado, o nome de domínio será autenticado com ele.
 ![](https://qcloudimg.tencent-cloud.cn/raw/27131602718160d5f4c096db488dccf6.png)

### Adição de regra

Após adicionar um nome de domínio, você pode clicar em **Add Rule (Adicionar regra)** para adicionar o URL correspondente e selecionar o tipo de servidor de origem. É possível adicionar até 20 regras de URL para um nome de domínio conforme mostrado abaixo:

1. Configurações básicas:
   ![](https://main.qcloudimg.com/raw/fcf56bdf702b67b81990cc4dedd89f0d.png)
   - URL: pode conter de 1 a 80 caracteres dos seguintes tipos: `a–z`, `A–Z`, `0–9`, `_`, `.`, `-` e `/`.
   - Origin Server Type (Tipo de servidor de origem): pode ser um IP ou nome de domínio, mas apenas um tipo pode ser selecionado para um listener. 
2. Política de processamento do servidor de origem:
   Defina a regra de encaminhamento do servidor de origem; ou seja, se um listener estiver vinculado a vários servidores de origem, será necessário selecionar uma política de programação para os servidores de origem.
    ![](https://main.qcloudimg.com/raw/bb6f7d4cf05d2fb6e623c5ed28904dbc.png)
   - RR: vários servidores de origem efetuam o pull de origem, de acordo com a política de RR.
   - Weighted RR (RR ponderado): vários servidores de origem efetuam o pull de origem, de acordo com a relação de peso (esta configuração não é aceita se o tipo de servidor de origem for nome de domínio).
   - Least Connections (Conexões mínimas): significa programar primeiro o servidor de origem com a menor quantidade de conexões.
3. Mecanismo de verificação de integridade do servidor de origem:
   Você pode optar por ativar o mecanismo de verificação de integridade para o nome de domínio atual e definir um URL de verificação independente. Os métodos de solicitação HEAD e GET são aceitos. Os códigos de status de verificação incluem http_1xx, http_2xx, http_3xx, http_4xx e http_5xx, e você pode selecionar um ou mais deles. Quando um código de status especificado for detectado, o listener considerará que o servidor de origem de back-end está normal. Se nenhum código de status for detectado, o listener considerará que o servidor de origem de back-end está excepcional.
![](https://main.qcloudimg.com/raw/20d08ec6efd43a94734b6a408afc2d10.png)

### Modificação de nome de domínio

Após adicionar um nome de domínio, você pode clicar em **Modify Domain Name (Modificar nome de domínio)** para modificá-lo.
 ![](https://main.qcloudimg.com/raw/c61efa495d61009bc93ebff1a8891de5.png)

### Exclusão de nome de domínio

Após adicionar um nome de domínio, você pode clicar em **Delete (Excluir)** para exclui-lo. Se uma regra sob o nome de domínio tiver sido vinculada a um servidor de origem, será necessário selecionar **Force deletion of listeners bound with origin server (Forçar exclusão de listeners vinculados ao servidor de origem)**.
 ![](https://main.qcloudimg.com/raw/3a7a088320acb13f1c822b1ec34c9ba1.png)

### Modificação de regra

Siga as etapas detalhadas em "Adding rule (Adição de regra)" acima. A principal diferença é que o nome de domínio e o tipo de servidor de origem não podem ser modificados.

### Vinculação do servidor de origem

Para obter mais informações, consulte "Vinculação do servidor de origem". É possível vincular portas diferentes a servidores de origem diferentes. Para obter mais informações sobre as funcionalidades **Cover Port (Porta de cobertura)** e **Complement Port (Porta de complemento)**, consulte "Vinculação de listener TCP/UDP ao servidor de origem".

> ! Uma regra pode ser vinculada a até 100 servidores de origem.

### Exclusão de regra

Após adicionar uma regra, você pode clicar em **Delete (Excluir)** para exclui-la. Se uma regra tiver sido vinculada um servidor de origem, primeiro será necessário selecionar **Force deletion of listeners bound with origin server (Forçar exclusão de listeners vinculados ao servidor de origem)**.
 ![](https://main.qcloudimg.com/raw/2fd560217ca2f53847033d501eb90e1a.png)

### Configuração do cabeçalho da solicitação de pull de origem

1. Após adicionar uma regra, você pode selecionar **More (Mais)** na coluna **Operation (Operação)** da regra e clicar em **Set Origin-Pull Request Header (Definir cabeçalho da solicitação de pull de origem)**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9dc95f9ef0c564ec6435c4b7f0635cdd.png)
2. Clique em **Add Parameter (Adicionar parâmetro)** para adicionar o parâmetro de nome e o valor do cabeçalho da solicitação. O valor da variável do cabeçalho que carrega o IP real do usuário é `$remote_addr` (por padrão, o cabeçalho `X-Forwarded-For` carrega o IP do cliente para o pull de origem). Atualmente, com exceção da variável `$remote_addr`, outras variáveis com `$` não são aceitas.

> !
> 1. O valor `Key` do nome do cabeçalho HTTP pode conter de 1 a 100 dígitos (0 a 9), letras (a–z, A–Z) e símbolos especiais (-, _, : e espaço). O `Value` pode conter de 1 a 100 caracteres. Com exceção de `$remote_addr`, os outros itens de configuração não podem conter o caractere `$`.
> 2. Até 10 cabeçalhos de solicitação HTTP de pull de origem podem ser configurados para cada regra.
> 3. Os cabeçalhos padrões listados abaixo não podem ser definidos/adicionados/excluídos de maneira automática.

<table>
    <tr>
        <td>www-authenticate</td>
        <td>authorization</td>
        <td>proxy-authenticate</td>
        <td>proxy-authorization</td>
    </tr>
    <tr>
        <td>age</td>
        <td>cache-control</td>
        <td>clear-site-data</td>
        <td>expires</td>
    </tr>
    <tr>
        <td>pragma</td>
        <td>warning</td>
        <td>accept-ch</td>
        <td>accept-ch-lifetime</td>
    </tr>
    <tr>
        <td>early-data</td>
        <td>content-dpr</td>
        <td>dpr</td>
        <td>device-memory</td>
    </tr>
    <tr>
        <td>save-data</td>
        <td>viewport-width</td>
        <td>width</td>
        <td>last-modified</td>
    </tr>
    <tr>
        <td>etag</td>
        <td>if-match</td>
        <td>if-none-match</td>
        <td>if-modified-since</td>
    </tr>
    <tr>
        <td>if-unmodified-since</td>
        <td>vary</td>
        <td>connection</td>
        <td>keep-alive</td>
    </tr>
    <tr>
        <td>accept</td>
        <td>accept-charset</td>
        <td>expect</td>
        <td>max-forwards</td>
    </tr>
    <tr>
        <td>access-control-allow-origin</td>
        <td>access-control-max-age</td>
        <td>access-control-allow-headers</td>
        <td>access-control-allow-methods</td>
    </tr>
    <tr>
        <td>access-control-expose-headers</td>
        <td>access-control-allow-credentials</td>
        <td>access-control-request-headers</td>
        <td>access-control-request-method</td>
    </tr>
    <tr>
        <td>origin</td>
        <td>timing-allow-origin</td>
        <td>dnt</td>
        <td>tk</td>
    </tr>
    <tr>
        <td>content-disposition</td>
        <td>content-length</td>
        <td>content-type</td>
        <td>content-encoding</td>
    </tr>
    <tr>
        <td>content-language</td>
        <td>content-location</td>
        <td>forwarded</td>
        <td>x-forwarded-host</td>
    </tr>
    <tr>
        <td>x-forwarded-proto</td>
        <td>via</td>
        <td>from</td>
        <td>host</td>
    </tr>
    <tr>
        <td>referer-policy</td>
        <td>allow</td>
        <td>server</td>
        <td>accept-ranges</td>
    </tr>
    <tr>
        <td>range</td>
        <td>if-range</td>
        <td>content-range</td>
        <td>cross-origin-embedder-policy</td>
    </tr>
    <tr>
        <td>cross-origin-opener-policy</td>
        <td>cross-origin-resource-policy</td>
        <td>content-security-policy</td>
        <td>content-security-policy-report-only</td>
    </tr>
    <tr>
        <td>expect-ct</td>
        <td>feature-policy</td>
        <td>strict-transport-security</td>
        <td>upgrade-insecure-requests</td>
    </tr>
    <tr>
        <td>x-content-type-options</td>
        <td>x-download-options</td>
        <td>x-frame-options(xfo)</td>
        <td>x-permitted-cross-domain-policies</td>
    </tr>
    <tr>
        <td>x-powered-by</td>
        <td>x-xss-protection</td>
        <td>public-key-pins</td>
        <td>public-key-pins-report-only</td>
    </tr>
    <tr>
        <td>sec-fetch-site</td>
        <td>sec-fetch-mode</td>
        <td>sec-fetch-user</td>
        <td>sec-fetch-dest</td>
    </tr>
    <tr>
        <td>last-event-id</td>
        <td>nel</td>
        <td>ping-from</td>
        <td>ping-to</td>
    </tr>
    <tr>
        <td>report-to</td>
        <td>transfer-encoding</td>
        <td>te</td>
        <td>trailer</td>
    </tr>
    <tr>
        <td>sec-websocket-key</td>
        <td>sec-websocket-extensions</td>
        <td>sec-websocket-accept</td>
        <td>sec-websocket-protocol</td>
    </tr>
    <tr>
        <td>sec-websocket-version</td>
        <td>accept-push-policy</td>
        <td>accept-signature</td>
        <td>alt-svc</td>
    </tr>
    <tr>
        <td>date</td>
        <td>large-allocation</td>
        <td>link</td>
        <td>push-policy</td>
    </tr>
    <tr>
        <td>retry-after</td>
        <td>signature</td>
        <td>signed-headers</td>
        <td>server-timing</td>
    </tr>
    <tr>
        <td>service-worker-allowed</td>
        <td>sourcemap</td>
        <td>upgrade</td>
        <td>x-dns-prefetch-control</td>
    </tr>
    <tr>
        <td>x-firefox-spdy</td>
        <td>x-pingback</td>
        <td>x-requested-with</td>
        <td>x-robots-tag</td>
    </tr>
    <tr>
        <td>x-ua-compatible</td>
        <td>max-age</td>
        <td></td>
        <td></td>
    </tr>
</table>

## Exclusão do listener HTTP/HTTPS

Abra a guia **HTTP/HTTPS Listener Management (Gerenciamento de listener HTTP/HTTPS)** e clique em **Delete (Excluir)** na coluna **Operation (Operação)** do listener especificado a ser excluído. Se o listener estiver vinculado a um servidor de origem, primeiro será necessário marcar **Allow force deletion of listeners with bound origin servers (Permitir exclusão forçada de listeners com servidores de origem vinculados)**. Após a exclusão, o serviço de aceleração da porta do listener será interrompido.
 ![](https://main.qcloudimg.com/raw/5df2bff2fb4f07ce2631824792429147.png)