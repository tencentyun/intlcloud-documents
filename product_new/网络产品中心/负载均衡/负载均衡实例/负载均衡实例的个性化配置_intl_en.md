CLB supports custom configuration, allowing you to set the configuration parameters for a single CLB instance, such as `client_max_body_size` and `ssl_protocols`, so as to meet your unique needs.
> The CLB custom configuration feature is currently in beta test. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

## CLB Custom Configuration Parameter Descriptions
Currently, CLB custom configuration supports the following fields:

| Configuration Field | Default Value/Recommended Value | Parameter Range | Description |
| :-------- | :-------- | :------ |:------ |
| ssl_protocols | TLSv1 TLSv1.1 TLSv1.2 | TLSv1 TLSv1.1 TLSv1.2 | Version of TLS protocol used; TLSv1.3 will be added later. |
| ssl_ciphers | See further below | See further below | Encryption suite. |
| client_header_timeout | 60s | [30-120]s | Timeout period of obtaining a client request header; in case of timeout, a 408 error will be returned. |
| client_header_buffer_size | 4 KB | [1-64] KB | Size of default buffer where a client request header is stored. |
| client_body_timeout | 60s | [30-120]s | Timeout period of obtaining a client request body, which is not the time for obtaining the entire body but refers to the idle period without data transmission; in case of timeout, a 408 error will be returned. |
| client_max_body_size | 60 MB |[1-256] MB | Maximum size of client request body, which may need to be modified for uploads; if the maximum size is exceeded, a 413 error will be returned. |
| keepalive_timeout | 75s | [0-3,600]s | Client-server persistent connection hold time; if it is set to 0, persistent connection is prohibited. |
| add_header | Custom | - | Specific header field returned to the client in the format of add_header xxx yyy. |
| more_set_headers | Custom | - | Specific header field returned to the client in the format of more_set_headers "A:B". |
| proxy_connect_timeout | 4s | [4-120]s | Timeout period of upstream backend connection. |
| proxy_read_timeout |60s |[30-3,600]s | Timeout period of reading upstream backend response. |
| proxy_send_timeout |60s |[30-3,600]s| Timeout period of sending a request to the upstream backend. |
| server_tokens | on | on; off | on means displaying version information, while off means hiding version information. |
| keepalive_requests | 100 | [0-10,000] | Maximum number of requests that can be sent over the client-server persistent connection. |
| proxy_buffer_size | 4 KB | [4-16] KB | Size of server response header, which is the size of a single buffer set in `proxy_buffer` by default; to use `proxy_buffer_size`, `proxy_buffers` must be set at the same time. |
| proxy_buffers | 1; 4 KB | [1-8] [4-8] KB | Buffer quantity and size. |
|  proxy_set_header   |X-Real-Port $remote_port|-| proxy_set_header only supports `X-Real-Port $remote_port` but not other custom fields. |

## ssl_ciphers Configuration Instructions
The ssl_ciphers encryption suite being configured must be in the same format as that used by OpenSSL. The algorithm list is one or more `<cipher strings>`; multiple algorithms should be separated with ":"; ALL represents all algorithms, "!" indicates not to enable an algorithm, and "+" indicates to move an algorithm to the last place.
The encryption algorithm for default forced disabling is: `!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE`.

**Default value:**
```
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE:3DES;
```

**Parameter range:**
```
ECDH-ECDSA-AES128-SHA256:ECDH-RSA-AES256-SHA:ECDH-ECDSA-AES256-SHA:SRP-DSS-AES-256-CBC-SHA:SRP-AES-128-CBC-SHA:ECDH-RSA-AES128-SHA256:DH-RSA-AES128-SHA256:DH-RSA-CAMELLIA128-SHA:DH-DSS-AES256-GCM-SHA384:DH-RSA-AES256-SHA256:AES256-SHA256:SEED-SHA:CAMELLIA256-SHA:ECDH-RSA-AES256-SHA384:ECDH-ECDSA-AES128-GCM-SHA256:DH-RSA-AES128-SHA:DH-RSA-AES128-GCM-SHA256:DH-DSS-AES128-SHA:ECDH-RSA-AES128-SHA:DH-DSS-CAMELLIA256-SHA:SRP-AES-256-CBC-SHA:DH-DSS-AES128-SHA256:SRP-RSA-AES-256-CBC-SHA:ECDH-ECDSA-AES256-GCM-SHA384:ECDH-RSA-AES256-GCM-SHA384:DH-DSS-AES256-SHA256:ECDH-ECDSA-AES256-SHA384:AES128-SHA:DH-DSS-AES128-GCM-SHA256:AES128-SHA256:DH-RSA-SEED-SHA:ECDH-ECDSA-AES128-SHA:IDEA-CBC-SHA:AES128-GCM-SHA256:DH-RSA-CAMELLIA256-SHA:CAMELLIA128-SHA:DH-RSA-AES256-GCM-SHA384:SRP-RSA-AES-128-CBC-SHA:SRP-DSS-AES-128-CBC-SHA:ECDH-RSA-AES128-GCM-SHA256:DH-DSS-CAMELLIA128-SHA:DH-DSS-SEED-SHA:AES256-SHA:DH-RSA-AES256-SHA:kEDH+AESGCM:AES256-GCM-SHA384:DH-DSS-AES256-SHA:HIGH:AES128:AES256:AES:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE
```

## CLB Custom Configuration Examples
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance/index?rid=8), click the custom configuration page on the left sidebar, and click **Create** to create a custom configuration file where configuration items should end with `;`.

2. Click **Bind to Instance** and select the CLB instance that you need to bind to in the same region.

3. You can view the corresponding custom configuration information on the instance list page.

Default configuration sample code:
```
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

>
> - Each region can have up to 200 custom configurations.
> - Currently, one instance can be bound to only one custom configuration.
> - Custom configurations are valid only for HTTP/HTTPS **CLB (former Application CLB)** listeners.
