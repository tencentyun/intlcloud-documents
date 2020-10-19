Before purchasing a certificate, it is important to understand the differences between certificate types and domain name types and choose the appropriate certificate based on your actual needs. The following introduces the procedure for purchasing a certificate.

>? The SSL certificate purchase page is not available to all users currently. If you want to purchase a SSL certificate, please [contact sales](https://intl.cloud.tencent.com/contact-sales) and we will come back to you soon.

### Step 1: go to the SSL certificate purchase page
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl). On the **Certificate Management** page, click **Purchase Certificate** to go to the SSL certificate purchase page.
2. Read the information on the SSL certificate purchase page.
![](https://main.qcloudimg.com/raw/6e6fe4d37a533f2b81f1f70abf76ef8f.png)


### Step 2: select the certificate type and brand
1. Select a certificate type that best fits with your industry and actual needs. For more information on certificate types, see [Certificate Type Selection Cases](https://intl.cloud.tencent.com/document/product/1007/37811).
2. Select a certificate brand. For more information about certificate brands, see [Certificate Brands](https://intl.cloud.tencent.com/document/product/1007/37810).

### Step 3: select the domain name type and the number of domain names supported
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
<td><li>The prices of SecureSite multi-domain name certificates are calculated based on the number of domain names.</li><li>For GeoTrust, TrustAsia, GlobalSign, Wotrus, and DNSPod multi-domain name certificates, there are additional charges for domain names that exceed the default maximum number of domain names supported.</li></td>
</tr>
<tr>
<td>Wildcard domain name</td>
<td>Only 1 wildcard domain name with only 1 wildcard can be bound.</td>
<td><li>For example, `\*.tencent.com` and `\*.example.tencent.com` support up to 100 levels.</li><li>Multi-wildcard domain names such as `\*.\*.tencent.com` are not supported.</li><li>An SSL certificate bound to the domain name `\*.tencent.com` (which must be a second-level wildcard domain name) supports the second-level domain name `tencent.com`.</li></td>
</tr>
<tr>
<td>Multi-wildcard domain name</td>
<td>Multiple wildcard domain names can be bound.</td>
<td>For example, `\*.tencent.com`, `\*.ssl.tencent.com`, and `\*.another.com` are counted as 3 wildcard domain names in total, including all the sub-domain names at the same level, subject to the maximum number of supported domain names displayed in the console.</td>
</tr>
</table>

### Step 4: select the certificate validity period
Due to the changes in Apple and Google root store policies, as of September 1, 2020, newly issued SSL/TLS certificates with a validity period greater than 13 months (397 days) will be prohibited and will not be trusted. Starting from September 1, 2020, global CAs will no longer issue 2-year SSL certificates, and **only 1-year SSL certificates can be purchased by default.** For more information, see [Notice on Stopping the Issuance of 2-Year SSL Certificates by CAs Starting from September 1, 2020](https://intl.cloud.tencent.com/document/product/1007/38090).

### Step 5: pay for the order
After selecting the brand, model, supported domain name, and certificate validity period, you can submit the order and complete the payment process.


### Step 6: submit the application
- **DNSPod OV and EV SSL certificates:**
After purchasing the certificate, submit materials for review on the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) to apply for the certificate and verify the domain name ownership. The application will be reviewed manually. The certificate will be issued after the certificate application is approved and the domain name ownership is successfully verified.
- **Wotrus OV and EV SSL certificates:**
After purchasing the certificate, submit materials for review on the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) to apply for the certificate and verify the domain name ownership. The application will be reviewed manually. The certificate will be issued after the certificate application is approved and the domain name ownership is successfully verified.
- **Other OV and EV SSL certificates:**
After purchasing the certificate, submit materials for review on the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) to apply for the certificate. The certificate will be issued upon approval by the CA. For more information, see [Required Submission Materials for Other OV/EV SSL Certificates](https://intl.cloud.tencent.com/document/product/1007/30160).
- **DV SSL certificates:**
After purchasing the certificate, submit materials for review on the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) to apply for the certificate and verify the domain name ownership. After the application is submitted, the domain name ownership will be verified. The certificate will be issued upon approval by the CA.
- **Free DV SSL certificates:**
After purchasing the certificate, apply for the domain name ownership verification. The certificate will be issued upon approval by the CA.

