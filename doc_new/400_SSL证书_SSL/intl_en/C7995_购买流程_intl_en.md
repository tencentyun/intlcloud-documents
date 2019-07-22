### 1. Select a certificate brand and model

Tencent Cloud provides four brands of SSL certificates for sale, as shown below:

#### Symantec

Symantec, the world's largest information security service producer and provider and the most authoritative digital certification authority, offers a wide range of content and network security solutions to businesses, individual users and service providers. 93% of the Global 500 choose VeriSign SSL digital certificates. Symantec acquired VeriSign in August 2010, and since then has provided the verification services of VeriSign. In April 2012, Symantec changed VeriSign's product name and brand logo.

#### GeoTrust

GeoTrust, the world's second-largest digital certification authority (CA) and a leader in authentication and trust certification, provides state-of-the-art technologies that enable organizations and companies of all sizes to deploy SSL digital certificates securely and cost-effectively and achieve a wide range of authentications. GeoTrust was founded in 2001, and to 2006, it has accounted for 25% of the global market share. VeriSign acquired GeoTrust with USD 125 million in May-September 2006, which is now also a **cost-effective** SSL certificate brand of Symantec.

From a technical point of view, the differences between Symantec (formerly VeriSign) and GeoTrust are as shown below:
1. Symantec (supporting RSA, DSA and ECC) is superior to Geotrust (supporting RSA and DSA) on algorithm.
2. Symantec is superior to Geotrust on compatibility. Symantec is compatible with all browsers on the market, and also shows very good compatibility for mobile devices.
3. Symantec is superior to Geotrust on OCSP response.
4. Symantec is superior to Geotrust on CA security. As an internationally renowned security vendor, Symantec provides the number one CA security in the world.
5. In addition to encrypted data transfer, Symantec certificates provide malware scanning and vulnerability assessment features.
6. A maximum of USD 1.75 million in certificate commercial insurance compensation is provided by Symantec, while the number of GeoTrust is USD 1.5 million.

#### TrustAsia

TrustAsia, the brand of Yashu Information Technology (Shanghai) Co., Ltd in the field of information security, is a platinum partner of Symantec™. TrustAsia specializes in providing businesses with all network security services including digital certificates. And the TrustAsia SSL certificates are issued by the Symantec root certificates.

#### GlobalSign

Founded in 1996, GlobalSign is a reputable and trusted CA and provider of SSL and digital certificates with more than 20 million digital certificates issued worldwide. It has won the favor of a great number of server providers, domain name registrars, and system service providers in the Chinese market thanks to its professional strengths as their digital certificate service partner.

#### Brand Differences

Certificates of different brands vary on browser address bar, encryption level, and guaranteed compensation. The most important difference lies in root certificates. For example, a Geotrust wildcard certificate is issued by Geotrust root certificate, while a Symantec wildcard certificate is issued by Symantec root certificate which is compatible with all browsers on the market and also supports mobile devices best. TrustAsia's wildcard certificates are issued by Symantec root certificates, and GlobalSign's wildcard certificates are issued by its own root certificates.

For more information, see parameters comparison provided on the official website.
![](https://main.qcloudimg.com/raw/f33d982ede59c72696add01f28c84c5c.jpg)

### 2. Select the number of supported domain names

#### Single-domain name

It only allows to bind one domain name, which can be a second-level domain name like example.domain.com, a third-level domain name like example.example.domain.com, or a first-level domain name like domain.com. **But all sub-domains under the first-level domain name are not supported**. Up to 100 levels of domain name can be supported.
> An SSL certificate bound to the domain name www.domain.com (subdomain is www) supports the first-level domain name domain.com.

#### Multi-domain name

One single certificate can be bound to multiple domain names, subject to the maximum number of supported domain names displayed in the console.
> 
> - The price of Symantec multi-domain name certificates are calculated based on the number of domain names.
> - GeoTrust, TrustAsia, and GlobalSign multi-domain name certificates in excess of the default number of supported domain names are charged additionally.
> 
![](https://main.qcloudimg.com/raw/f58e72c57294735d23a21b2815710822.jpg)

#### Wildcard domain name

Only one wildcard domain name with only one wildcard can be bound, such as \*.domain.com and \*.example.domain.com (up to 100 levels). Multi-wildcard domain names like \*.\*.domain.com are not supported.
> An SSL certificate bound to the domain name \*.domain.com (which must be a second-level wildcard domain name) supports the first-level domain name domain.com.
>
![](https://main.qcloudimg.com/raw/2d984c38bd2ee35ddd04b86009ada117.jpg)

#### Multi-wildcard domain name

Multiple wildcard domain names can be bound. For example, \*.domain.com, \*.ssl.domain.com, and \*.another.com are counted as three wildcard domain names in total, including all the sub-domain names at the same level, subject to the maximum number of supported domain names displayed in the console.
![](https://main.qcloudimg.com/raw/a458616c337d4dc1dc083019679f793a.png)

### 3. Select certificate validity

OV and EV certificates can be valid for up to 2 years, while DV certificates can be valid for up to 1 year. 

### 4. Payment

After selecting the brand, model, supported domain name, and certificate validity, you can submit the order and proceed with the payment process.


### 5. Submit the application

After purchasing a certificate, you need to submit approval materials in [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) for certificate application. The certificate will be issued upon approval by the CA. For more information, see [Paid Certificate Application Process](https://intl.cloud.tencent.com/document/product/1007/30160).
