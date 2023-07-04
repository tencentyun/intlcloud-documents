### Are DV certificates permanently free?
Regardless of whether the SSL certificates are free DV certificates or paid OV certificates, CAs set a validity period for security reasons. It is possible that a website becomes a phishing website, so CAs conduct a regular review instead of issuing permanently valid certificates. 

Additionally, you can apply for certificate revocation if you lose your private key. The CA then adds the revoked certificate to a certificate revocation list (CRL). Whenever an HTTPS website is accessed, the browser retrieves the CRL from the CA to determine whether to trust the certificate. Because issuing permanently valid certificates leads to an increasing CRL, it will increase the request traffic for browsers. Therefore, CAs specify validity periods for certificates.

At present, Tencent Cloud provides a free DV certificate with the model of **TrustAsia DV SSL CA - G5** and a valid period of **1 year**. You can apply a new certificate **1 months** before the certificate expires. DV certificates can be issued within 1 business day, so you have sufficient time to switch the certificates for the website.

