## TrustAsia Root Certificate Update
As notified by TrustAsia, TrustAsia root certificates have changed from DigiCert root certificates to Sectigo root certificates since **March 3, 2022 22:00:00**. That is, the root certificates of TrustAsia SSL certificates applied before **March 3, 2022 22:00:00** were issued by DigiCert, and those applied after **March 3, 2022 22:00:00** are issued by Sectigo.

Sectigo root certificates support Online Certificate Status Protocol (OCSP) nodes in the Chinese mainland. Therefore, the TrustAsia root certificate update greatly improves the HTTPS access speed of websites in the Chinese mainland.

若需使用 Digcert 颁发证书，请于**2022年03月03日22:00:00**前，前往 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 进行 [证书申请](https://intl.cloud.tencent.com/document/product/1007/40205) 操作。申请成功并颁发后，您可将您的证书部署至云服务。详情参见：[如何选择 SSL 证书安装部署类型？](https://intl.cloud.tencent.com/document/product/1007/30173)


>!
>- This update has no effect on the SSL certificates already issued for use.
>- After the update, the original product features and services remain unchanged.



