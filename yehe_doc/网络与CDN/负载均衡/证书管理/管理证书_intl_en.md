When configuring an HTTPS listener of a CLB instance, you can directly use a certificate in SSL Certificate Service or upload a server certificate and an [SSL certificate](https://intl.cloud.tencent.com/document/product/1007/30152) issued by a third-party CA to CLB.

## Certificate Requirements
CLB supports only certificates in PEM format. Before uploading a certificate, make sure that your certificate, certificate chain, and private key meet the format requirement. For the certificate requirements, please see [SSL Certificate Format](https://intl.cloud.tencent.com/document/product/214/5369).

## Configuring Certificate
Certificate configuration for an HTTPS listener divides into the following two types:
- If SNI is not enabled, a certificate can be configured at the listener level, under which all domain names use the same certificate. For more information, please see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
- If SNI is enabled, a certificate can be configured at the domain name level, and different certificates can be configured for different domain names under the listener. For more information, please see [SNI Support for Binding Multiple Certificates to a CLB Instance](https://intl.cloud.tencent.com/document/product/214/19048).

## Updating Certificates in Batches
To prevent certificate expiration from affecting your service, please update the certificate before it expires.
>?After a certificate is updated, the system will not delete the legacy certificate; instead, it will generate a new one. The certificate will be automatically updated for all CLB instances using it.

1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb).
2. Click **Certificate Management** on the left sidebar.
3. In the certificate list on the **Certificate Management** page, click **Update** in the "Operation" column on the right of the target certificate.
4. In the "Create Certificate" dialog box that pops up, enter the certificate content and key content of the new certificate and click **Submit**.
![](https://main.qcloudimg.com/raw/d6534b57f4a33fab69b98fca4d1023f3.png)

## Viewing CLB Instance Associated with Certificate
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb).
2. Click **Certificate Management** on the left sidebar.
3. In the certificate list on the **Certificate Management** page, click the ID of the target certificate.
4. On the "Basic Info" page, view the CLB instances associated with the certificate.
![](https://main.qcloudimg.com/raw/b3670e111ec8b9e1a43b9c7d2e870be3.png)
