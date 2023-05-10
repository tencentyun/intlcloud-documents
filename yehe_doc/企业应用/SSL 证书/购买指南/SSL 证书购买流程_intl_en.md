We recommend that you take the time to understand the differences between the different certificate types and domain name types so that you can purchase the appropriate certificate for your actual needs. The following details the process of purchasing a certificate.

### Step 1. Go to the SSL certificate purchase page
1. Log in at the [SSL certificate purchase page](https://intl.cloud.tencent.com/pricing/ssl).

2. Click **Purchase Certificate** to view the detailed certificate configuration and pricing information, as shown in the following image:
![](https://main.qcloudimg.com/raw/6e6fe4d37a533f2b81f1f70abf76ef8f.png)
   

   > **Notes**
   >   - If you are not familiar with certificate types and brands, click **Quick Configuration** to quickly purchase a certificate recommended by the system.
   >   - Click **Advanced Settings** and set **Project** and **Tag** to better manage existing Tencent Cloud resources by category. For detailed directions on how to add a tag, see [Querying Resources by Tag](https://intl.cloud.tencent.com/document/product/651/32582).



### Step 2. Select the certificate type and brand
1. Select a certificate type that best fits your industry and actual needs. For more information, see [Certificate Type Selection Cases](https://www.tencentcloud.com/document/product/1007/37811).

2. Select a certificate brand. For more information, please see [Certificate Brands](https://intl.cloud.tencent.com/document/product/1007/37810).


### Step 3. Select the domain name type and the number of domain names supported
<table>
<tr>
<td rowspan="1" colSpan="1" >Domain Type</td>
<td rowspan="1" colSpan="1" >Description</td>
<td rowspan="1" colSpan="1" >Notes</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Single-domain</td>
<td rowspan="1" colSpan="1" >Only one domain can be bound. The domain can be a second-level domain such as `tencent.com` or a third-level domain such as `example.tencent.com`.</td>
<td rowspan="1" colSpan="1" >Binding all subdomains under a second-level domain is not supported.<br>Up to 100 levels of domains are supported.<br>An SSL certificate bound to the domain `www.tencent.com` (`www` as the subdomain) supports the second-level domain `tencent.com`.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Multi-domain</td>
<td rowspan="1" colSpan="1" >A certificate can be bound to multiple domains, subject to the maximum number of domains displayed in the console.</td>
<td rowspan="1" colSpan="1" >The prices of SecureSite multi-domain certificates are calculated based on the number of domains.<br>For the GeoTrust, TrustAsia, GlobalSign, WoTrus, and DNSPod multi-domain certificates, there are additional charges for the domains that exceed the default maximum number of domains supported.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Wildcard domain</td>
<td rowspan="1" colSpan="1" >One and only one wildcard domain can be bound, and only one wildcard can be added.</td>
<td rowspan="1" colSpan="1" >For example, `\*.tencent.com` and `\*.example.tencent.com` support up to 100 levels.<br>Multi-wildcard domains such as `\*.\*.tencent.com` are not supported.<br>An SSL certificate bound to the domain `\*.tencent.com` (which must be a second-level wildcard domain) supports the second-level domain `tencent.com`.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Multiple wildcard domains</td>
<td rowspan="1" colSpan="1" >Multiple wildcard domains can be bound.</td>
<td rowspan="1" colSpan="1" >For example, `\*.tencent.com`, `\*.ssl.tencent.com`, and `\*.another.com` are counted as a total of three wildcard domains, including all the subdomains at the same level, subject to the maximum number of domains displayed in the console.</td>
</tr>
</table>




### Step 4. Select the certificate validity period

Due to changes in Apple and Google root store policies, newly issued SSL/TLS certificates with a validity period greater than 13 months (397 days) have been prohibited by policy since September 1, 2020. Therefore, global CAs have ceased issuing such certificates since September 1, 2020.
**Currently, only certain multi-year SSL certificates are available from Tencent Cloud (others available are all SSL certificates with a validity period of 13 months). Within 30 days before expiration of your current multi-year certificate, Tencent Cloud will automatically apply for a new one for you, which will be automatically issued upon CA approval.**

> **Notes**
> 
> - Available multi-year SSL certificate brands and types are as displayed on the purchase page.
> - If the original certificate is installed at the server website, you need to replace it with a newly issued one as instructed in [Selecting an Installation Type for an SSL Certificate](https://intl.cloud.tencent.com/document/product/1007/30173).


### Step 5. Pay for your order

After selecting the brand, model, supported domain name, and certificate validity period, you can submit your order and complete the payment process.



### Step 6. Submit an application

#### DNSPod (SM2) OV and EV SSL certificates:
1. After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and select **Pending Submission** to enter the management page. Then, submit the information, upload the confirmation letter, and complete the domain ownership verification.

2. After your application is submitted, it will be reviewed. After the review is successfully completed, the certificate will be issued.

#### WoTrus OV and EV SSL certificates
1. After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and select **Pending Submission** to enter the management page. Then, submit the information to pre-apply for the certificate. After your pre-application is approved, the domain ownership needs to be verified.

2. After your domain is validated, manual approval is needed, upon which the certificate will be issued. For more information, see [Information Submission Process for Wotrus OV and EV SSL Certificates](https://intl.cloud.tencent.com/document/product/1007/40206).


#### Other OV and EV SSL certificates
1. After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and select **Pending Submission** to enter the management page. Then, submit the information and upload the confirmation letter to apply for the certificate.

2. After your application is submitted, it will be reviewed. After the review is successfully completed, the certificate will be issued. For more information, please see [The Process of Submitting Materials for OV/EV SSL Certificates](https://intl.cloud.tencent.com/document/product/1007/30160).
   

   > **Notes**
   > 
   >   - If you use the approved organization and administrator information in [**My Profile**](https://console.cloud.tencent.com/ssl/info), the confirmation letter is not required.
   >   - For GlobalSign certificates, the confirmation letter still needs to be uploaded when you submit the information.


#### DV SSL certificates

After purchasing the certificate, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and select **Pending Submission** to enter the management page. Then, submit the information and complete the domain ownership verification, after which the CA will issue the certificate. For more information, see [Information Submission Process for DV SSL Certificates](https://www.tencentcloud.com/document/product/1007/53628).

#### Free DV SSL certificates

After applying for the certificate, complete the domain ownership verification. The CA will then issue the certificate.