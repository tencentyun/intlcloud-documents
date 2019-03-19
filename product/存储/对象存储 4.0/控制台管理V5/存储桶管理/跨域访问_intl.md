## Overview
You can set Cross Origin Resource Sharing(CORS) for objects in buckets through the COS Console. COS supports configuring multiple rules to respond to OPTIONS requests. CORS is a mechanism that allows resources at one origin to be requested from another origin through HTTP requests. Origins are deemed different from each other as long as their protocols, domain names or ports are different.

COS supports response to OPTIONS requests for CORS, and returns specific rules set by developers to browsers, but the server does not verify whether subsequent cross-origin requests conform to the rules. For more information, see [Cross-Origin Resource Sharing](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS).

## Procedure

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), and then select the **Bucket List** in the left pane to go to the Bucket List page. Click the bucket of the object for which you want to set CORS to enter the bucket.
![](https://main.qcloudimg.com/raw/b90ad17947a0ec530db87210f4b9027d.png)
2. Click **Basic Configuration** to go to the Basic Configuration page of the bucket, find **CORS Settings**, and click **Add Rule**.
![](https://main.qcloudimg.com/raw/6f3d6f81cb550bac4076d54861efdc60.png)
3. Add rule information (Fields with * are required). Configuration items are as follows:

 **Source Origin**: The domain names allowed for cross-origin requests.
 - More than one domain name can be specified, with one domain name per line.
 - Wildcard `*` is supported, which means all domain names are allowed. Not recommended.
 - A single specific domain name is supported, such as `http://www.abc.com`.
 - Second-level wildcard domain names are supported, such as `http://*.abc.com`. Only one second-level wildcard domain name with only one `*` in it is allowed per line.
 - Do not omit protocol name HTTP or HTTPS, and specify the port if the port is not default 80.

 **Operating Methods**: GET, PUT, POST, DELETE, and HEAD are supported. Enumeration of one or more methods is allowed for a cross-domain request.

 **Allow-Headers**: Allow-Header is used to notify the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent, such as x-cos-meta-md5.
 - More than one header can be specified, with one header per line.
 - Header is easy to be omitted, so it is recommended to set this field to `*` to indicate that all headers are allowed if there is no special requirement.
 - Uppercase and lowercase letters [a-z, A-Z] are supported, and no underscores (`_`) are allowed.
 - Each header specified in Access-Control-Request-Headers must also be provided in Allowed-Header.

 **Expose-Headers**: Expose-Header returns a common header for COS. For more information, see the [Common Request Headers](https://cloud.tencent.com/document/product/436/7728). The configuration should be specific to the requirements of application. Etag is recommended. Wildcard is not allowed. Headers are case insensitive, with one header per line.

 **Timeout Max-Age**: Sets the validity period (in seconds) of the results obtained by OPTIONS. The value must be a positive integer, such as 600.

 ![](https://main.qcloudimg.com/raw/7ca1c22c33129a0602c2a83573c31fef.png)

4. After configuration, click **Submit** and you will see the CORS rules added. To modify it, click the **Modify** button.
![](https://main.qcloudimg.com/raw/e42826a0832f1b4283952a1e7af6c826.png)

