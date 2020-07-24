### 1. Select certificate brand and model

Tencent Cloud provides 4 brands of SSL certificates for sale:

#### SecureSite
SecureSite is the world's largest information security service provider and most reputable digital certificate issuer. It provides a wide spectrum of content and network security solutions to individuals, businesses, and service providers. Ninety three percent of Fortune Global 500 companies choose VeriSign SSL digital certificates. SecureSite acquired VeriSign in August 2010, changed VeriSign's product name and brand logo in April 2012, and since then has been providing the VeriSign verification service.

#### GeoTrust
GeoTrust, the world's second-largest digital certificate authority (CA) and a leader in identity verification and trust certification, provides state-of-the-art technologies that enable organizations and companies of all sizes to deploy SSL digital certificates securely and cost-effectively and achieve a wide range of identity verification. GeoTrust was founded in 2001, and by 2006, it accounted for 25% of the global market share. VeriSign acquired GeoTrust for 125 million USD in May-September 2006, and is now another **cost-effective** SecureSite SSL certificate brand.

From a technical point of view, the differences between SecureSite (formerly VeriSign) and GeoTrust are as follows:
- Algorithm support: SecureSite (supporting RSA, DSA and ECC) outperforms GeoTrust (supporting RSA and DSA).
- Compatibility: SecureSite outperforms GeoTrust. SecureSite is compatible with all browsers on the market as well as many mobile devices.
- OCSP response speed: SecureSite outperforms GeoTrust.
- CA security: SecureSite outperforms GeoTrust. As an internationally renowned security vendor, SecureSite provides the best CA security in the world.
- Data security: in addition to encrypted data transfer, SecureSite certificates provide malware scanning and vulnerability assessment features.
- Certificate commercial insurance compensation: SecureSite (up to 1.75 million USD) outperforms GeoTrust (up to 1.5 million USD).

#### TrustAsia
TrustAsia, a brand under Yashu Information Technology (Shanghai) Co., Ltd in the field of information security, is a SecureSite platinum partner. TrustAsia specializes in providing businesses with complete network security services including digital certificates. TrustAsia SSL certificates are also issued by SecureSite root certificates.

#### GlobalSign
Founded in 1996, GlobalSign is a reputable and trusted CA and provider of SSL certificates with more than 20 million SSL certificates issued worldwide. A great number of server providers, domain name registrars, and system service providers in the Chinese market favor GlobalSign and partner with it in digital certification service.

#### Brand Differences
Certificates of different brands vary depending on browser address bar, encryption level, and guaranteed compensation. The most important difference lies in root certificates. For example, a GeoTrust wildcard certificate is issued using a GeoTrust root certificate, while a SecureSite wildcard certificate is issued using a SecureSite root certificate, which is compatible with all browsers on the market and also best supports mobile devices. A TrustAsia wildcard certificate is issued using a SecureSite root certificate, and a GlobalSign wildcard certificate is issued using a GlobalSign root certificate.

For more information, see the parameters comparison provided on the [SSL Certificates Service Console](https://console.cloud.tencent.com/ssl).
![](https://main.qcloudimg.com/raw/f33d982ede59c72696add01f28c84c5c.jpg)

### 2. Select the number of supported domain names

#### Single-domain name
Only 1 domain name can be bound, which can be a second-level domain name such as example.domain.com, a third-level domain name such as example.example.domain.com, or a first-level domain name such as domain.com. **However, all sub-domains under the first-level domain name are not supported**. Up to 100 levels of domain name can be supported.
> An SSL certificate bound to the domain name www.domain.com (subdomain is www) supports the first-level domain name domain.com.

#### Multi-domain name
A single certificate can be bound to multiple domain names, subject to the maximum number of supported domain names displayed in the console.
> 
> - The prices of SecureSite multi-domain name certificates are calculated based on the number of domain names.
> - For GeoTrust, TrustAsia, and GlobalSign multi-domain name certificates, there are additional charges for domain names exceeding the default quantity.

![](https://main.qcloudimg.com/raw/f58e72c57294735d23a21b2815710822.jpg)

#### Wildcard domain name
Only 1 wildcard domain name with only 1 wildcard can be bound, such as, \*.domain.com and \*.example.domain.com (up to 100 levels). Multi-wildcard domain names such as \*.\*.domain.com are not supported.
> An SSL certificate bound to the domain name \*.domain.com (which must be a second-level wildcard domain name) supports the first-level domain name domain.com.

![](https://main.qcloudimg.com/raw/2d984c38bd2ee35ddd04b86009ada117.jpg)

#### Multi-wildcard domain name
Multiple wildcard domain names can be bound. For example, \*.domain.com, \*.ssl.domain.com, and \*.another.com are counted as 3 wildcard domain names in total, including all the sub-domain names at the same level, subject to the maximum number of supported domain names displayed in the console.
![](https://main.qcloudimg.com/raw/a458616c337d4dc1dc083019679f793a.png)

### 3. Select certificate validity
OV and EV certificates can be valid for up to 2 years, while DV certificates can be valid for up to 1 year only. The price discounted 15% for 1-year certificates and 25% for 2-year certificates (see the prices published on the Tencent Cloud official website).

### 4. Payment
After selecting the brand, model, supported domain name, and certificate validity period, you can submit the order and proceed with the payment process.


### 5. Submit the application
After purchasing a certificate, you need to submit information for review in the [SSL Certificate Services Console](https://console.cloud.tencent.com/ssl) for certificate application. The certificate will be issued upon approval by the CA. For more information, see [Material Submission for OV/EV SSL Certificates](https://intl.cloud.tencent.com/document/product/1007/30160).


