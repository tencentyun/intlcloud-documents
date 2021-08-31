CLB supports custom configuration, which allows you to set the configuration parameters such as `client_max_body_size` and `ssl_protocols` of a single CLB instance, meeting your requirements for personalized configuration.
>?
>- Each region can have up to 200 custom configurations.
>- Currently, only one custom configuration can be bound to an instance.
>- Custom configuration takes effect only for layer-7 HTTP/HTTPS listeners of CLB (former "Application Load Balancer").

## Custom CLB Configuration Parameter Description
Currently, custom CLB configuration supports the following fields:

| Configuration Field | Default Value/Recommended Value | Valid Values/Value Range | Description |
| :-------- | :-------- | :------ |:------ |
|  ssl_protocols  | TLSv1 TLSv1.1 TLSv1.2 |  TLSv1 TLSv1.1 TLSv1.2 | Version of used TLS protocol. TLSv1.3 will be added in the future. |
|  ssl_ciphers  | See below | See below | Cipher suite. |
|  client_header_timeout  | 60s |  [30-120]s (s for second) | Timeout period for getting a client request header. In case of timeout, a 408 error will be returned. |
|  client_header_buffer_size | 4k |[1-256]k (k for KB) | Size of default buffer where a client request header is stored. |
|  client_body_timeout | 60s |  [30-120]s (s for second) | Timeout period for getting a client request body, which is not the time for obtaining the entire body but refers to the idle period without data transfer. In case of timeout, a 408 error will be returned. |
|  client_max_body_size | 60M |[1-2048]M (M for MB)| <ul><li>The default value range is 1–256 MB. If the value you want to set is within the default range, directly set it.</li><li>The maximum size is 2,048 MB. If the value of `client_max_body_size` you want to set is greater than 256 MB, <a href="#buffer">proxy_request_buffering</a> should be set to `off`.</li></ul> |
|  keepalive_timeout | 75s | [0-3600]s (s for second)| Client-Server persistent connection hold time. If it is set to 0, persistent connection will be disabled. |
| add_header | Custom | - | Specific header field returned to the client in the format of `add_header xxx yyy`. |
| more_set_headers | Custom | - | Specific header field returned to the client in the format of `more_set_headers "A:B"`. |
|  proxy_connect_timeout | 4s | [4-120]s (s for second) |Timeout period for upstream backend connection. |
|  proxy_read_timeout |60s |[30-3600]s (s for second) | Timeout period for reading upstream backend response. |
|  proxy_send_timeout |60s |[30-3600]s (s for second) | Timeout period for sending a request to the upstream backend. |
|  server_tokens | on | on, off | <ul><li>`on` indicates to display the version information.</li><li>`off` indicates to hide the version information.</li></ul>|
|  keepalive_requests | 100 | [1–10000] |Maximum number of requests that can be sent over the client-server persistent connection. |
|  proxy_buffer_size | 4k |[1-64]k (k for KB) | Size of server response header, which is the size of a single buffer set in `proxy_buffer` by default. To use `proxy_buffer_size`, `proxy_buffers` must be set at the same time. |
|  proxy_buffers | 8 4k |[3-8] [4-8]k (k for KB) | Buffer quantity and size. |
|  <span id="buffer">proxy_request_buffering</span> | on |on, off|<ul><li>`on` indicates that the client request body will be cached: CLB will cache a request and then forward it to a backend CVM instance in multiple parts after receiving the entire request.</li><li>`off` indicates that the client request body will not be cached: after receiving a request, CLB will immediately forward it to a backend CVM instance, which will cause a certain performance pressure on the backend CVM instance.</li></ul>|
|  proxy_set_header   |X-Real-Port $remote_port|<ul><li>X-Real-Port $remote_port</li><li>X-clb-stgw-vip $server_addr</li><li>Stgw-request-id $stgw_request_id</li></ul>|<ul><li>`X-Real-Port $remote_port` indicates the client port. </li><li>`X-clb-stgw-vip $server_addr` indicates the CLB VIP. </li><li>`Stgw-request-id $stgw_request_id` indicates the request ID (for internal use by CLB).</li></ul> |
|  send_timeout | 60s |[1-3600]s (s for second) | Timeout period for the server to transfer data to the client. It refers to the interval between two consecutive data transfers rather than the entire request transfer duration. |
|  ssl_verify_depth |  1 |[1,10]| Verification depth of the client certificate chain. |


## ssl_ciphers Configuration Description
The `ssl_ciphers` cipher suite being configured must be in the same format as that used by OpenSSL. The algorithm list is one or more `<cipher strings>`; two algorithms should be separated with ":"; "ALL" represents all algorithms, "!" indicates not to enable an algorithm, and "+" indicates to move an algorithm to the last place.
The encryption algorithm for default forced disablement is: `!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE`.

**Default value:**
```
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE:3DES;
```

**Valid values:**
```
ECDH-ECDSA-AES128-SHA256:ECDH-RSA-AES256-SHA:ECDH-ECDSA-AES256-SHA:SRP-DSS-AES-256-CBC-SHA:SRP-AES-128-CBC-SHA:ECDH-RSA-AES128-SHA256:DH-RSA-AES128-SHA256:DH-RSA-CAMELLIA128-SHA:DH-DSS-AES256-GCM-SHA384:DH-RSA-AES256-SHA256:AES256-SHA256:SEED-SHA:CAMELLIA256-SHA:ECDH-RSA-AES256-SHA384:ECDH-ECDSA-AES128-GCM-SHA256:DH-RSA-AES128-SHA:DH-RSA-AES128-GCM-SHA256:DH-DSS-AES128-SHA:ECDH-RSA-AES128-SHA:DH-DSS-CAMELLIA256-SHA:SRP-AES-256-CBC-SHA:DH-DSS-AES128-SHA256:SRP-RSA-AES-256-CBC-SHA:ECDH-ECDSA-AES256-GCM-SHA384:ECDH-RSA-AES256-GCM-SHA384:DH-DSS-AES256-SHA256:ECDH-ECDSA-AES256-SHA384:AES128-SHA:DH-DSS-AES128-GCM-SHA256:AES128-SHA256:DH-RSA-SEED-SHA:ECDH-ECDSA-AES128-SHA:IDEA-CBC-SHA:AES128-GCM-SHA256:DH-RSA-CAMELLIA256-SHA:CAMELLIA128-SHA:DH-RSA-AES256-GCM-SHA384:SRP-RSA-AES-128-CBC-SHA:SRP-DSS-AES-128-CBC-SHA:ECDH-RSA-AES128-GCM-SHA256:DH-DSS-CAMELLIA128-SHA:DH-DSS-SEED-SHA:AES256-SHA:DH-RSA-AES256-SHA:kEDH+AESGCM:AES256-GCM-SHA384:DH-DSS-AES256-SHA:HIGH:AES128:AES256:AES:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE
```

## Custom CLB Configuration Sample
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance/index?rid=8) and click **Custom Configuration** on the left sidebar to enter the management page.
2. Click **Create**, enter the corresponding configuration items, and end them with `;`.
![](https://main.qcloudimg.com/raw/7ef70a06f9509ba8759e5a923515a471.png)
3. Click **Complete** to create the custom configuration.
4. In the "Operation" column on the management page, click **Bind to Instance**.
5. Select the CLB instance in the same region to be bound to in the pop-up window and click **Submit**.
![](https://main.qcloudimg.com/raw/ad8fb7874b9ce1fe7bf5c9366c7e64e7.png)
6. After binding the instance, you can find the corresponding custom configuration information on the instance list page.
![](https://main.qcloudimg.com/raw/d07bdbc134480fa89f732c93c3861243.png)
Sample code of the default configuration:
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

