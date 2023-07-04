### How do I view the domain validation result of a DV certificate?

After you submit a certificate application, the CA will review your domain and submitted information and issue the certificate after approval. If your certificate has not been issued for a long time, we recommend that you check the domain validation result as follows.

>?
> 
> SSL Certificate Service provides hosts with fully qualified domain names (FQDNs). If your domain management system does not support them, remove the suffix of the root domain.
> 

**DNS validation type**

1. Log in to your domain server and run the `dig` command to query the DNS record.

2. Run the `dig + record type + @119.29.29.29` command to specify to use the DNSPod DNS for validation.
For example, `dig txt cloud.tencent.com @119.29.29.29`![](https://staticintl.cloudcachetci.com/yehe/backend-news/zrr7795_111111111111111111111111.png)

  - If the returned result contains a TXT record similar to that in the figure and the record value is the same as that on the **Certificate Details** page in the SSL Certificate Service console, your DNS configuration is correct and has taken effect.

  - If the returned result does not contain a TXT record, it's possible that the DNS configuration is incorrect or has not taken effect.
If the DNS configuration is incorrect, go to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and click the **Pending validation** tab to enter the **Certificate Details** page. Copy the record value in **Certificate Details** and update the record at your DNS service provider. If the configuration has not taken effect for a long time, contact your domain hosting provider.
    

  >?
  > For detailed directions, see [DNS Validation](https://intl.cloud.tencent.com/document/product/1007/45895).



**File validation type**

1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and click the **Pending validation** tab to enter the **Certificate Details** page.

2. Click to access the validation URL. If the accessed page displays the same content as the validation file content on the **Certificate Details** page, the access is normal; otherwise, check the following:

  - Check whether the validation URL has an address accessible over HTTPS, and if so, use the HTTPS address in the browser for another access. If the browser prompts that the certificate is untrusted or the displayed content is incorrect, disable the HTTPS service of the domain.

  - Check whether the validation URL can be accessed anywhere. As the servers for validating certificates of each brand are located in different regions, you should check whether your site has an image outside the Chinese mainland or whether the smart DNS service is used.

  - File validation requires responding to status code 200 and file content directly and does not support redirects of any kind. Check whether the validation URL has the 301 or 302 redirect, and if so, disable the redirect.
    

      >?
      > 
      > You can run the `wget -S URL` command to check whether the validation URL has a redirect.
      > 
