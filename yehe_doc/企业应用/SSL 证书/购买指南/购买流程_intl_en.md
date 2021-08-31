We recommend that you take the time to understand the differences between the different certificate types and domain name types so that you can purchase the appropriate certificate for your actual needs. The following details the process of purchasing a certificate.

### Step 1. Go to the SSL certificate purchase page
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl).
2. On the **Certificate Management** page, click **Purchase Certificate** to go to the SSL certificate purchase page.
3. Read the information on the SSL certificate purchase page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/6e6fe4d37a533f2b81f1f70abf76ef8f.png)


### Step 2. Select the certificate type and brand
1. Select a certificate type that best fits your industry and actual needs. For more information about certificate types, please see [Selecting Certificate Types](https://intl.cloud.tencent.com/document/product/1007/37811).
2. Select a certificate brand. For more information, please see [Certificate Brands](https://intl.cloud.tencent.com/document/product/1007/37810).


### Step 3. Select the domain name type and the number of domain names supported
<table>
<tr>
<th>Domain Name Type</th>
<th>Description</th>
<th>Notes</th>
</tr>
<tr>
<td>Single-domain name</td>
<td>Only 1 domain name can be bound. The domain name can be a second-level domain name such as `tencent.com` or a third-level domain name such as `example.tencent.com`.</td>
<td><li>However, binding all sub-domain names under a second-level domain name is not supported.</li><li>Up to 100 levels of domain names are supported.</li><li>An SSL certificate bound to the domain name `www.tencent.com` (`www` as the sub-domain name) supports the second-level domain name `tencent.com`.</li></td>
</tr>
<tr>
<td>Multi-domain name</td>
<td>A single certificate can be bound to multiple domain names, subject to the maximum number of supported domain names displayed in the console.</td>
<td><li>The prices of SecureSite multi-domain name certificates are calculated based on the number of domain names.</li><li>For the GeoTrust, TrustAsia, GlobalSign, Wotrus, and DNSPod multi-domain name certificates, there are additional charges for the domain names that exceed the default maximum number of domain names supported.</li></td>
</tr>
<tr>
<td>Wildcard domain name</td>
<td>Only 1 wildcard domain name with only 1 wildcard can be bound.</td>
<td><li>For example, `\*.tencent.com` and `\*.example.tencent.com` support up to 100 levels.</li><li>Multi-wildcard domain names such as `\*.\*.tencent.com` are not supported.</li><li>An SSL certificate bound to the domain name `\*.tencent.com` (which must be a second-level wildcard domain name) supports the second-level domain name `tencent.com`.</li></td>
</tr>
<tr>
<td>Multi-wildcard domain name</td>
<td>Multiple wildcard domain names can be bound.</td>
<td>For example, `\*.tencent.com`, `\*.ssl.tencent.com`, and `\*.another.com` are counted as a total of 3 wildcard domain names, including all the sub-domain names at the same level, subject to the maximum number of supported domain names displayed in the console.</td>
</tr>
</table>

### Step 4. Select the certificate validity period
Due to changes in Apple and Google root store policies, as of September 1, 2020, newly issued SSL/TLS certificates with a validity period greater than 13 months (397 days) will be prohibited and will not be trusted. Starting from September 1, 2020, global CAs will no longer issue 2-year SSL certificates, and **only 1-year SSL certificates will be available for purchase by default.** For more information, see the [Notice on Stopping the Issuance of 2-Year SSL Certificates by CAs Starting from September 1, 2020](https://intl.cloud.tencent.com/document/product/1007/38090).

### Step 5. Pay for your order
After selecting the brand, model, supported domain name, and certificate validity period, you can submit your order and complete the payment process.
>?If you need an invoice, please see [Self-Service Invoice Feature](https://intl.cloud.tencent.com/document/product/555/31993).


### Step 6. Submit an application
#### DNSPod (SM2) OV and EV SSL certificates:
1. After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and click **Submit info** to go to the **Certificate Information Submission** page. Then, enter the relevant information, upload the confirmation letter, and complete the domain ownership verification.
2. After your application is submitted, it will be reviewed. After the review is successfully completed, the certificate will be issued.

#### Wotrus OV and EV SSL certificates
1. After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and click **Submit info** to go to the **Certificate Information Submission** page. Then, enter the relevant information to pre-apply for the certificate. After your pre-application is successfully reviewed, the domain ownership will need to be verified.
2. After the domain ownership is verified, it will be reviewed. After the review is successfully completed, the certificate will be issued.

#### Other OV and EV SSL certificates
1. After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and click **Submit info** to go to the **Certificate Information Submission** page. Then, enter the relevant information and upload the confirmation letter to apply for the certificate.
2. After your application is submitted, it will be reviewed. After the review is successfully completed, the certificate will be issued. For more information, please see The Process of Submitting Materials for OV/EV SSL Certificates.

#### DV SSL certificates
After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and click **Submit info** to go to the **Certificate Information Submission** page. Then, enter the relevant information and complete the domain ownership verification, after which the CA will issue the certificate.

#### Free DV SSL certificates
After applying for the certificate, complete the domain ownership verification. The CA will then issue the certificate.
