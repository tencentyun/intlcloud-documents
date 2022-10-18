
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site Acceleration** > **HTTPS configuration** on the left sidebar.

2. On the HTTPS configuration page, select the target site and configure the following HTTPS items for site acceleration:

### Forced HTTPS[](id:QZ)
In the forced HTTPS module, click ![](https://qcloudimg.tencent-cloud.cn/raw/4f521701c30f8f3f7ca4b577e00b62b9.png) to forcibly redirect all edge HTTP requests to HTTPS through 301/302. It is disabled by default.
>?After this feature is enabled, all requests will be transferred over HTTPS. Make sure that certificates of service-providing subdomains have been deployed in EdgeOne.


### Origin-Pull HTTPS[](id:HY)
In the origin-pull HTTPS module, click **Edit**, select the origin-pull encryption mode (i.e., protocol used for origin-pull), and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/3cfaf7c4204ac3e337ef7e66e2a3c558.png)
**Parameter description:**

- Follow protocol (default): The origin-pull protocol follows the request protocol. For example, if the request uses HTTP, origin-pull will also use HTTP.
- HTTP: All origin-pull requests use the HTTP protocol.
- HTTPS: All origin-pull requests use the HTTPS protocol.

### HTTP Strict Transport Security (HSTS)
1. In the HSTS module, click **Enable HSTS**, configure relevant parameters, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/0972beacae2fef98b98559ea1a0758ea.png)
**Parameter description:**
 - Default status: It is disabled by default. To use the HSTS feature, you need to enable it.
 - Cache time: Set the HSTS header validity period in seconds, during which browsers always initiate requests over HTTPS. The value range is 1–31536000.
 - Include subdomain: If it is enabled, HSTS will take effect for the current domain and its subdomains.
 - Preload: If it is enabled, browsers will automatically load the HSTS configuration in advance to avoid the attack risks of the first HTTP request. This feature can take effect only if you add the domain to the HSTS preload list in browsers first.
2. After HSTS is configured, the `Strict-Transport-Security` header will be added to the EdgeOne cache node responses to force clients such as browsers to establish connections to edge nodes over HTTPS for global website encryption.
 - HTTPS header format
```
Strict-Transport-Security: max-age=expireTime [; includeSubDomains] [; preload]
```
 - Field description
    - max-age: HSTS header validity period in seconds, during which browsers always initiate requests over HTTPS.
    - includeSubDomains: It is an optional field. If it is enabled, HSTS will take effect for the current domain and its subdomains.
    - preload: It is an optional field. If it is enabled, browsers will automatically load the HSTS configuration in advance to avoid the attack risks of the first HTTP request. This feature can take effect only if you add the domain to the HSTS preload list in browsers first.
>?
>- Before enabling HSTS, make sure that domain certificates have been deployed to respond to HTTPS requests normally.
>- We recommend you also enable [forced HTTPS](#QZ) when enabling HSTS; otherwise, if requests use HTTP, browsers won't execute the HSTS configuration.
>- The value range of `max-age` is 1–31536000 seconds.

### TLS version
In the TLS version module, click **Edit**, select the target version, and click **Save**.
>?Only HTTPS links on enabled TLS versions are allowed. Available TLS versions are 1.0–1.3. You can enable a single version or a series of consecutive versions.

![](https://qcloudimg.tencent-cloud.cn/raw/437014896fde7f6b8bcab2c001bf7547.png)


### OCSP stapling
In the OCSP stapling module, the cached OCSP response will be sent during TLS handshake to improve the handshake efficiency. After you click ![](https://qcloudimg.tencent-cloud.cn/raw/0ce2f7ccf282e1b1bda8dd2e7032cd8a.png) to enable OCSP stapling, cache nodes will cache the OCSP response for clients to verify it, and clients won't need to send query requests to certificate authorities (CAs), which accelerates TLS handshakes.
