## Configuration Process for Apache HTTPS Mutual Authentication
>!If your domain certificate has expired, follow the instructions below to reconfigure your domain certificate.

This document uses the third-party developer domain name `www.example.com` as an example. The following two cases may arise:

- **The third-party developer already has a certificate issued by an authoritative third party.**
 - The developer prepares the certificate `www.example.com.crt` issued by and the private key `www.example.com.key` assigned by the authoritative third party for `www.example.com`. Note that the certificate must be issued by an authoritative third party, such as Topway or GlobalSign.
 - Chat provides the developer backend with a CA certificate [TencentQQAuthCA.crt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TencentQQAuthCA.crt.zip), which is used to verify the certificate of the requesting party (Chat).
 - Perform configuration by referring to the **Reference for Apache HTTPS Mutual Authentication Configuration** below.

- **The third-party developer sends an application to Chat, requesting Chat to issue a certificate for its domain name.**
 - The developer [configures the webhook URL](https://intl.cloud.tencent.com/document/product/1047/34520), such as `www.example.com`, in the console.
 <dx-alert infotype="notice" title="">
  When you register a domain, follow the rules below:
- Use English letters (a-z, case-insensitive), digits (0-9), and hyphen `-` only.
- Do not use spaces and special characters such as `!`, `$`, `&`, and `?`.
- Hyphen `-` cannot appear consecutively, be registered independently, or be placed at the beginning or end.
- The length of the domain cannot exceed 63 characters.
</dx-alert>
 - Chat issues the certificate `www.example.com.crt` and assigns the private key `www.example.com.key` to the developer with the domain name `www.example.com`. The developer can [download the certificate](https://intl.cloud.tencent.com/document/product/1047/34520#.E4.B8.8B.E8.BD.BD-https-.E5.8F.8C.E5.90.91.E8.AE.A4.E8.AF.81.E8.AF.81.E4.B9.A6) from the [console](https://console.cloud.tencent.com/im/callback-setting).
 - Chat provides the developer backend with a CA certificate [TencentQQAuthCA.crt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TencentQQAuthCA.crt.zip), which is used to verify the certificate of the requesting party (Chat).
 - Perform configuration by referring to the **Reference for Apache HTTPS Mutual Authentication Configuration** below.

## Reference for Apache HTTPS Mutual Authentication Configuration

1. Copy `www.example.com.crt`, `www.example.com.key`, and `TencentQQAuthCA.crt` to the `conf` folder under the Apache installation directory.
2. Modify the `httpd.conf` file. The reference configuration is as follows:
```
	SSLEngine on # Enables SSL
	SSLCertificateFile "/usr/local/apache2/conf/example.com.crt" # Certificate issued by Tencent to the third party
	SSLCertificateKeyFile "/usr/local/apache2/conf/example.com.key" # Private key paired with the certificate
	SSLCACertificateFile  "/usr/local/apache2/conf/TencentQQAuthCA.crt" # CA certificate authenticated by Tencent
	SSLVerifyClient require # Verify the request source
```
