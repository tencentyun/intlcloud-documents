## Creating HTTP/HTTPS Listener

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page, and click the **ID/Connection Name** of the specified connection.
2. On the page that appears, select **HTTP/HTTPS Listener Management** > **Create**. You can select either the HTTP or HTTPS protocol. (Note: currently, HTTP/HTTPS listener configuration is not supported for IPv6 connections.)
3. The specific configuration is as follows:
   1. If HTTP is selected, only the port number is required, and the listener will forward packets over the HTTP protocol by default.
![](https://main.qcloudimg.com/raw/0096d45b44fbd916012317a49a97a884.png)
   2. If HTTPS is selected, certificates and additional information need to be configured as shown below:
![](https://main.qcloudimg.com/raw/941665ba354633d345929e3fbd02fa8c.png)
      - **Listeners communicate with the origin server using HTTP protocol** means that the HTTPS protocol is used between the client and the acceleration connection VIP, while the HTTP protocol is used between the VIP and the origin server, which requires an HTTP port to be opened on the origin server;
        **Listeners communicate with the origin server using HTTPS protocol** means that the HTTPS protocol is used between the client and the origin server, which requires an HTTPS port to be opened on the origin server.
      - SSL Parsing: both one-way and two-way authentication are supported.
      - Server/Client Certificate: you need to upload a certificate or update it in **Certificate Management** in the GAAP console and then select it when creating/modifying an HTTPS listener. For more information, see Certificate Management.

## Configuring HTTP/HTTPS Listener

Open the **HTTP/HTTPS Listener Management** tab and click **Set Rule** in the **Operation** column to enter the domain name and URL management page.

### Adding domain name

To add a domain name for an HTTP listener, you only need to enter it in the specified format, and only exact match is supported. A domain name can contain 3–80 characters in the following types: `a–z`, `0–9`, `_`, and `–`.
 ![](https://qcloudimg.tencent-cloud.cn/raw/fed0aa02e83804a36799763b0f88cf33.png)
To add a domain name for an HTTPS listener, you need to enter it and select the corresponding server certificate. The certificate selected during listener creation is used in the console by default. If you upload a new certificate, the domain name will be authenticated with the new certificate.
 ![](https://qcloudimg.tencent-cloud.cn/raw/27131602718160d5f4c096db488dccf6.png)

### Adding rule

After adding a domain name, you can click **Add Rule** to add the corresponding URL and select the origin server type. You can add up to 20 URL rules for one domain name as shown below:

1. Basic configuration:
   ![](https://main.qcloudimg.com/raw/fcf56bdf702b67b81990cc4dedd89f0d.png)
   - URL: it can contain 1–80 characters in the following types: `a–z`, `A–Z`, `0–9`, `_`, `.`, `-`, and `/`.
   - Origin Server Type: this can be an IP or a domain name, but only one type can be selected for one listener. 
2. Origin server processing policy:
   Set the origin server forwarding rule; that is, if a listener is bound to multiple origin servers, you need to select a scheduling policy for origin servers.
    ![](https://main.qcloudimg.com/raw/bb6f7d4cf05d2fb6e623c5ed28904dbc.png)
   - RR: multiple origin servers perform origin-pull according to the RR policy.
   - Weighted RR: multiple origin servers perform origin-pull according to the weight ratio (this configuration is not supported if the origin server type is domain name).
   - Least Connections: this means scheduling the origin server with the least number of connections first.
3. Origin server health check mechanism:
   You can choose to enable the health check mechanism for the current domain name and set an independent check URL. HEAD and GET request methods are supported. Check status codes include http_1xx, http_2xx, http_3xx, http_4xx, and http_5xx, and one or more of them can be selected. When a specified status code is detected, the listener considers that the backend origin server is normal. If no status code is detected, the listener considers that the backend origin server is exceptional.
![](https://main.qcloudimg.com/raw/20d08ec6efd43a94734b6a408afc2d10.png)

### Modifying domain name

After adding a domain name, you can click **Modify Domain Name** to modify the domain name.
 ![](https://main.qcloudimg.com/raw/c61efa495d61009bc93ebff1a8891de5.png)

### Deleting domain name

Click **Delete** to delete a domain name. If a rule under the domain name has been bound to an origin server, you need to select **Force deletion of listeners bound to the origin server**.
 ![](https://main.qcloudimg.com/raw/3a7a088320acb13f1c822b1ec34c9ba1.png)

### Modifying rule

Follow the steps detailed in "Adding rule" above. The main difference is that the domain name and origin server type cannot be modified.

### Binding origin server

For more information, see Binding Origin Server. You can bind different ports to different origin servers. For more information on the **Cover Port** and **Complement Port** features, see Binding TCP/UDP Listener to Origin Server.

> ! A rule can be bound to up to 100 origin servers.

### Deleting rule

Click **Delete** to delete a rule. If the rule has been bound to an origin server, you need to select **Force deletion of listeners bound to the origin server** first.
 ![](https://main.qcloudimg.com/raw/2fd560217ca2f53847033d501eb90e1a.png)

### Configuring origin-pull request header

1. After adding a rule, you can select **More** in the **Operation** column of the rule and click **Set Origin-Pull Request Header**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9dc95f9ef0c564ec6435c4b7f0635cdd.png)
2. Click **Add Parameter** to add the name parameter and value of the request header. The variable value of the header that carries the user's real IP is `$remote_addr` (by default, the `X-Forwarded-For` header carries the client IP for origin-pull). Currently, except the `$remote_addr` variable, other variables with `$` are not supported.

> !
> 1. The `Key` value of the HTTP header name can contain 1–100 digits (0–9), letters (a–z, A–Z), and special symbols (-, _, :, and space). The `Value` can contain 1–100 characters. Except for `$remote_addr`, other configuration items cannot contain the `$` character;
> 2. Up to 10 origin-pull HTTP request headers can be configured for each rule;
> 3. The standard headers listed below cannot be set/added/deleted in a self-service manner.

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

## Deleting HTTP/HTTPS Listener

Open the **HTTP/HTTPS Listener Management** tab and click **Delete** in the **Operation** column of the specified listener to be deleted. If the listener is bound to an origin server, you need to check **Allow force deletion of listeners bound to the origin servers** first. After deletion, the acceleration service for the listener's port will stop.
 ![](https://main.qcloudimg.com/raw/5df2bff2fb4f07ce2631824792429147.png)
