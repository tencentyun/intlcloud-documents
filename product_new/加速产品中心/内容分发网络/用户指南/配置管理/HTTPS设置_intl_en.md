HTTPS refers to Hypertext Transfer Protocol Secure, which is a security protocol that encrypts and transfers data based on the HTTP protocol to ensure the security of data transfer. When configuring HTTPS, you need to provide a certificate for the domain name and deploy it on all CDN nodes to implement encrypted data transfer across the network.

>
> - After CDN acceleration is enabled for **COS** or **Cloud Image**, default domain names `.file.myqcloud.com` and `.image.myqcloud.com` directly support HTTPS with no need to configure the certificate.
> - Tencent Cloud CDN's support for HTTP 2.0 protocol is in beta test and can be used directly once enabled.

## Configuration Guide
Tencent Cloud CDN supports two certificate deployment methods:
- Self-owned certificate: Upload your own certificate and private key to CDN for deployment. Transfer is encrypted throughout the process to ensure the security of your certificate.
- Tencent Cloud-hosted certificate: You can go to [Certificate Management](https://console.cloud.tencent.com/ssl) to host your existing certificate in Tencent Cloud for use by multiple Tencent Cloud products. You can also apply for a third-party certificate provided by TrustAsia free of charge through this platform and deploy it directly to CDN.


1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the desired domain name and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/47ca7b8ed8414f624262aa8b65bf06dd.png)
2. Click **Advanced Configuration** and find **HTTPS Configuration**. Click **Configure Now** to enter the **Certificate Management** page where you can configure a certificate. For the configuration process, please see [Certificate Management](https://intl.cloud.tencent.com/document/product/228/6303).
![img](https://main.qcloudimg.com/raw/2d0c2762eda5f17aeeaed6bfce5417a8.png)
3. After the certificate is **successfully configured**, the **Forced HTTPS Redirect** switch will appear, which is disabled by default.
![img](https://main.qcloudimg.com/raw/c0133b1cae3c9b429f4cb265b8746349.png)
4. After enabling **Forced HTTPS Redirect**, even if the user initiates an HTTP request, it will be redirected to HTTPS for access. The redirect method is 302 redirect by default.
![image](https://main.qcloudimg.com/raw/c731097643f44dc960dfdc03f5f400bd.png)
You can click **Edit** to modify the redirect mehod:
![image](https://main.qcloudimg.com/raw/fae0b873ff49de6ce7c20dd8d03cfbc3.png)

## HTTP2.0 Configuration

After successfully configuring the HTTPS certificate for the domain name, you can enable HTTP 2.0.
![img](https://main.qcloudimg.com/raw/b78e5bc45ca42a1c4fbeb9db059fa6fa.png)
<!--For more information on HTTP 2.0 features, please see [New Features of HTTP 2.0]().-->

> Currently, acceleration domain names suffixed with `.myqcloud.com` do not support HTTP 2.0.

## OCSP stapling configuration
**Feature Description**
OCSP stapling is a TLS certificate status query extension. An OCSP stapling server can send the cached OCSP query result to the client during TLS handshake for verification by the user without having the client send the request to the CA. OCSP stapling greatly improves the efficiency of TLS handshake and reduces user verification time.

After successfully configuring the HTTPS certificate for the domain name, you can enable OCSP stapling.
![image](https://main.qcloudimg.com/raw/536f6bd66f8013a67026a2be579916da.png)


## Algorithms supported by HTTPS origin-pull

HTTPS origin-pull currently supports the following algorithms (in no particular order):

| ECDHE-RSA-AES256-SHA   | ECDHE-RSA-AES256-SHA384   | ECDHE-RSA-AES256-GCM-SHA384   |
| ---------------------- | ------------------------- | ----------------------------- |
| ECDHE-ECDSA-AES256-SHA | ECDHE-ECDSA-AES256-SHA384 | ECDHE-ECDSA-AES256-GCM-SHA384 |
| SRP-AES-256-CBC-SHA    | SRP-RSA-AES-256-CBC-SHA   | SRP-DSS-AES-256-CBC-SHA       |
| DH-RSA-AES256-SHA      | DH-RSA-AES256-SHA256      | DH-RSA-AES256-GCM-SHA384      |
| DH-DSS-AES256-SHA      | DH-DSS-AES256-SHA256      | DH-DSS-AES256-GCM-SHA384      |
| DHE-RSA-AES256-SHA     | DHE-RSA-AES256-SHA256     | DHE-RSA-AES256-GCM-SHA384     |
| DHE-DSS-AES256-SHA     | DHE-DSS-AES256-SHA256     | DHE-DSS-AES256-GCM-SHA384     |
| CAMELLIA256-SHA        | DH-RSA-CAMELLIA256-SHA    | DHE-RSA-CAMELLIA256-SHA       |
| PSK-3DES-EDE-CBC-SHA   | DH-DSS-CAMELLIA256-SHA    | DHE-DSS-CAMELLIA256-SHA       |
| ECDH-RSA-AES256-SHA    | ECDH-RSA-AES256-SHA384    | ECDH-RSA-AES256-GCM-SHA384    |
| ECDH-ECDSA-AES256-SHA  | ECDH-ECDSA-AES256-SHA384  | ECDH-ECDSA-AES256-GCM-SHA384  |
| AES256-SHA             | AES256-SHA256             | AES256-GCM-SHA384             |
| ECDHE-RSA-AES128-SHA   | ECDHE-RSA-AES128-SHA256   | ECDHE-RSA-AES128-GCM-SHA256   |
| ECDHE-ECDSA-AES128-SHA | ECDHE-ECDSA-AES128-SHA256 | ECDHE-ECDSA-AES128-GCM-SHA256 |
| SRP-AES-128-CBC-SHA    | SRP-RSA-AES-128-CBC-SHA   | SRP-DSS-AES-128-CBC-SHA       |
| DH-RSA-AES128-SHA      | DH-RSA-AES128-SHA256      | DH-RSA-AES128-GCM-SHA256      |
| DH-DSS-AES128-SHA      | DH-DSS-AES128-SHA256      | DH-DSS-AES128-GCM-SHA256      |
| DHE-RSA-AES128-SHA     | DHE-RSA-AES128-SHA256     | DHE-RSA-AES128-GCM-SHA256     |
| DHE-DSS-AES128-SHA     | DHE-DSS-AES128-SHA256     | DHE-DSS-AES128-GCM-SHA256     |
| ECDH-RSA-AES128-SHA    | ECDH-RSA-AES128-SHA256    | ECDH-RSA-AES128-GCM-SHA256    |
| ECDH-ECDSA-AES128-SHA  | ECDH-ECDSA-AES128-SHA256  | ECDH-ECDSA-AES128-GCM-SHA256  |
| CAMELLIA128-SHA        | DH-RSA-CAMELLIA128-SHA    | DHE-RSA-CAMELLIA128-SHA       |
| PSK-RC4-SHA            | DH-DSS-CAMELLIA128-SHA    | DHE-DSS-CAMELLIA128-SHA       |
| AES128-SHA             | AES128-SHA256             | AES128-GCM-SHA256             |
| SEED-SHA               | DH-RSA-SEED-SHA           | DH-DSS-SEED-SHA               |
| DES-CBC3-SHA           | DHE-RSA-SEED-SHA          | DHE-DSS-SEED-SHA              |
| IDEA-CBC-SHA           | PSK-AES256-CBC-SHA        | PSK-AES128-CBC-SHA            |
| EDH-RSA-DES-CBC3-SHA   | ECDH-RSA-DES-CBC3-SHA     | ECDHE-RSA-DES-CBC3-SHA        |
| EDH-DSS-DES-CBC3-SHA   | ECDH-ECDSA-DES-CBC3-SHA   | ECDHE-ECDSA-DES-CBC3-SHA      |
| RC4-SHA                | ECDH-RSA-RC4-SHA          | ECDHE-RSA-RC4-SHA             |
| RC4-MD5                | ECDH-ECDSA-RC4-SHA        | ECDHE-ECDSA-RC4-SHA           |
| SRP-3DES-EDE-CBC-SHA   | SRP-RSA-3DES-EDE-CBC-SHA  | SRP-DSS-3DES-EDE-CBC-SHA      |
| DH-DSS-DES-CBC3-SHA    | DH-RSA-DES-CBC3-SHA       | -                             |
