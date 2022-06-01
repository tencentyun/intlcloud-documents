## Overview

You can set cross-origin resource sharing (CORS) for objects in buckets in the COS console. COS supports configuring multiple rules to respond to OPTIONS requests. CORS is a mechanism that allows resources at one origin to be requested from another origin through HTTP requests. Origins will be deemed to be different from each other as long as their protocols, domain names, or ports are different.

COS supports response to OPTIONS requests for CORS and returns specific rules set by you to the browser, but the server does not verify whether subsequent CORS requests conform to the rules. For more information, see [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS) and [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket for which to set CORS.
4. Select **Security Management** > **CORS (Cross-Origin Resource Sharing)** on the left sidebar and click **Add a Rule**.
![](https://main.qcloudimg.com/raw/1659089c942ec8fadd77c880f1d4f492.png)
5. Configure the rule information (fields marked with * are required). The configuration items are as described below:
 ![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)
 - **Origin**: The sources from which CORS requests are allowed. You can add domain names and IP addresses.
    - The domain name does not need to end with a slash (`/`).
    - Multiple domain names can be specified at a time, with only one per line.
    - `*` is supported, indicating that all domain names and IP addresses are allowed, which is not recommended.
    - A single specific domain name in the format of `http://www.abc.com` is supported.
    - Second-level wildcard domain names in the format of `http://*.abc.com` are supported, but each line can contain only one asterisk (*).
    - Be careful not to omit the protocol name `http` or `https`. If the port is not the default port 80, you also need to include the port. A sample IP address is `http://10.10.10.10`.
 - **Allow-Methods**: GET, PUT, POST, DELETE, and HEAD are supported. You can enumerate one or more allowed CORS request methods.
 - **Allow-Headers**: Informs the server what custom HTTP headers (such as x-cos-meta-md5) are allowed in subsequent requests through an OPTIONS request.
    - Multiple headers can be specified at a time, with only one per line, such as `Content-type`.
    - `Header` tends to be omitted and is recommended to be set to `*` if not otherwise required, indicating all headers are allowed.
    - Uppercase and lowercase letters [a-z, A-Z] are supported, but no underscores (_) are allowed.
    - Each header specified in `Access-Control-Request-Headers` must correspond to a value in `Allowed-Header`.
 - **Expose-Headers**: Headers commonly used by COS. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728). This parameter needs to be configured according to the application requirements, and `ETag` is recommended. Headers cannot be wildcards and are case insensitive. Multiple headers can be set, with only one per line.
 - **Max-age**: Validity period of the result obtained by an OPTIONS request. The value must be a positive integer, such as 600.
6. After completing the configuration, click **Submit**, and you will see that the CORS rule has been added. To modify it, click **Modify**.
![](https://main.qcloudimg.com/raw/c4399193611b4f81e57a549634ea865a.png)
