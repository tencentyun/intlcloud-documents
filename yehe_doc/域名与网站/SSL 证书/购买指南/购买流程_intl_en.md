Before purchasing a certificate, it is recommended that you understand the differences between certificate types and domain name types and choose the appropriate certificate based on your actual needs. The following introduces the procedure for purchasing a certificate.

### Step 1: go to the SSL certificate purchase page
1. Log in to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl). On the **Certificate Management** page, click **Purchase Certificate** to go to the SSL certificate purchase page.
2. Read the information on the SSL certificate purchase page.
![](https://main.qcloudimg.com/raw/6e6fe4d37a533f2b81f1f70abf76ef8f.png)


### Step 2: select the certificate type and brand
1. Select a certificate type based on your industry and actual needs. For more information about certificate types, see [Certificate Type Selection Cases](https://intl.cloud.tencent.com/document/product/1007/37811).
2. Select a certificate brand. For more information about certificate brands, see [Certificate Brands](https://intl.cloud.tencent.com/document/product/1007/37810).

### Step 3: select the domain name type and the number of domain names supported
<table>
<tr>
<th>Domain Name Type</th>
<th>Description</th>
<th>Remarks</th>
</tr>
<tr>
<td>Single-domain name</td>
<td>Only 1 domain name can be bound, which can be a first-level domain name such as `tencent.com`, a second-level domain name such as `example.tencent.com`, or a third-level domain name such as `example.example.tencent.com`.</td>
<td><li>However, binding all sub-domain names under a first-level domain name is not supported.</li><li>Up to 100 levels of domain names are supported.</li><li>An SSL certificate bound to the domain name `www.tencent.com` (`www` as the sub-domain name) supports the first-level domain name `tencent.com`.</li></td>
</tr>
<tr>
<td>Multi-domain name</td>
<td>A single certificate can be bound to multiple domain names, subject to the maximum number of supported domain names displayed in the console.</td>
<td><li>The prices of SecureSite multi-domain name certificates are calculated based on the number of domain names.</li><li>For GeoTrust, TrustAsia, and GlobalSign multi-domain name certificates, there are additional charges for domain names exceeding the default quantity.</li></td>
</tr>
<tr>
<td>Wildcard domain name</td>
<td>Only 1 wildcard domain name with only 1 wildcard can be bound.</td>
<td><li>For example, `\*.tencent.com` and `\*.example.tencent.com` support up to 100 levels.</li><li>Multi-wildcard domain names such as `\*.\*.tencent.com` are not supported.</li><li>An SSL certificate bound to the domain name `\*.tencent.com` (which must be a second-level wildcard domain name) supports the first-level domain name `tencent.com`.</li></td>
</tr>
<tr>
<td>Multi-wildcard domain name</td>
<td>Multiple wildcard domain names can be bound.</td>
<td>For example, `\*.tencent.com`, `\*.ssl.tencent.com`, and `\*.another.com` are counted as 3 wildcard domain names in total, including all the sub-domain names at the same level, subject to the maximum number of supported domain names displayed in the console.</td>
</tr>
</table>

### Step 4: select the certificate validity period
OV and EV certificates can be valid for up to 2 years, while DV certificates can be valid for up to 1 year only. The price is discounted 15% for 1-year certificates and 25% for 2-year certificates (see the prices published on the Tencent Cloud official website).

### Step 5: pay for the order
After selecting the brand, model, supported domain name, and certificate validity period, you can submit the order and proceed with the payment process.


### Step 6: submit the application
- **OV and EV certificates**: after purchasing a certificate, you need to submit information for review in the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) for certificate application. The certificate will be issued upon approval by the CA. For more information, see [Material Submission for OV/EV SSL Certificates](https://intl.cloud.tencent.com/document/product/1007/30160).
- **DV certificates**: after purchasing a certificate, you need to submit information for domain name ownership authentication. The certificate will be issued upon approval by the CA.

