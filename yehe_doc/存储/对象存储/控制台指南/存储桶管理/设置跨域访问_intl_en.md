## Overview

You can set Cross Origin Resource Sharing (CORS) for objects in buckets through the COS console. COS supports configuring multiple rules to respond to OPTIONS requests. CORS is a mechanism that allows resources at one origin to be requested from another origin through HTTP requests. Origins are deemed different from each other as long as their protocols, domain names, or ports are different.

COS supports response to OPTIONS requests for CORS, and returns specific rules set by developers to browsers, but the server does not verify whether subsequent cross-origin requests conform to the rules. For more information, please see [Cross-Origin Resource Sharing](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS) and [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to go to the bucket list page. Then click the bucket of the object for which you want to set CORS.
2. Choose **Security Management** -> **CORS (Cross-Origin Resource Sharing)**. In the **CORS (Cross-Origin Resource Sharing)** area, click **Add a Rule**.
   ![](https://main.qcloudimg.com/raw/1659089c942ec8fadd77c880f1d4f492.png)
3. Configure the rule information (parameters marked with * are required). The parameters are described as follows:

 **Origin**: domain names allowed for cross-origin requests.
 - More than one domain name can be specified, with one domain name per line.
 - Asterisk (*) is supported, meaning that all domain names are allowed. This is not recommended.
 - A single specific domain name is supported, such as `http://www.abc.com`.
 - Second-level wildcard domain names, for example, `http://*.abc.com`, are supported. Note that each line can contain only one asterisk (*).
 - Do not omit the protocol name `http` or `https`. If the port is not the default 80, the port should also be specified.

 **Allow-Methods**: GET, PUT, POST, DELETE, and HEAD are supported. Enumeration of one or more methods is allowed for a cross-origin request.
 **Allow-Headers**: notifies the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent, such as `x-cos-meta-md5`.
 - More than one header can be specified, with one header per line, for example, `Content-type`.
 - Header is easy to omit. Therefore, if there is no special requirement, you are advised to set this field to `*`, meaning that all headers are allowed.
 - Uppercase and lowercase letters [a-z, A-Z] are supported, and no underscores (_) are allowed.
 - Each header specified in `Access-Control-Request-Headers` must correspond to a value in `Allowed-Header`.

 **Expose-Headers**: request headers commonly used in COS. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728). Set this parameter according to the specific application requirements. ETag is recommended. Headers do not allow wildcards and are case insensitive. You can set multiple headers, with one header per line.
 **Max-age**: validity period (in seconds) of the results obtained by OPTIONS. The value must be a positive integer, such as 600.
 ![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)

4. After configuration, click **Confirm** and you will see the CORS rule added. To modify it, click **Edit**.
   ![](https://main.qcloudimg.com/raw/c4399193611b4f81e57a549634ea865a.png)
