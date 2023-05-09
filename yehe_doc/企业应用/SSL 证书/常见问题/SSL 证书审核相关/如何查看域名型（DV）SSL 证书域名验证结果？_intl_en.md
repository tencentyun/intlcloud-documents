### How do I view the domain validation result of a DV certificate?

After you submit a certificate application, the CA will review your domain and submitted information and issue the certificate after approval. If your certificate has not been issued for a long time, we recommend that you check the domain validation result as follows.

> **Notes**
> 
> SSL Certificate Service provides hosts with fully qualified domain names (FQDNs). If your domain management system does not support them, remove the suffix of the root domain.
> 

**DNS validation type**

1. Log in to your domain server and run the `dig` command to query the DNS record.

2. Run the `dig + record type + @119.29.29.29` command to specify to use the DNSPod DNS for validation.
For example, `dig txt cloud.tencent.com @119.29.29.29`![](https://write-document-release-1258344699.cos-internal.ap-guangzhou.tencentcos.cn/100023397743/92cc06f3399711edb1de525400c56988.png?q-sign-algorithm=sha1&q-ak=AKIDcmqi7yunGwC4T11ADQ4FPbYG2IVi-mB-bvMbjj4_HA0zp-HFlWlxYApZ61m3LpzV&q-sign-time=1676448793;1676452393&q-key-time=1676448793;1676452393&q-header-list=&q-url-param-list=&q-signature=be798d80ff5926db1a28aab1fc0ed91509d920b3&x-cos-security-token=fHqwGc36xI6d5QUWAmWE4lOfUGuwp6la54ea5f2979a343a3b1645d9e7eab10e9VUlHxW6drilDRAMT1gTp7OLWhq0dK4anP2t6CGFlcByLB9aYxuO9FVMwjKOZVur8ECv9IbZx_-CVSARNO8JlGYVwM9MfzMlTSzToLTjQ1eB5hI9LI9lEXuqti_B3Q-e2QwHqCzBIA_8VHEVfDkJhBjqN1yF8oGJIiJ4u_f2GmxQSxkqdavD0rAlp9M_qtJuRZyZcqqYGca6K_xM32e7l7eS38jzJsjati4VIHNJv85655OLbI8XXwK6eq8I2huEtRMBsm18V9jE-YV9b_Jdx5lbQKLezB4wqg7PQbdb9IB_pH3qPj_q5MoXBh7Fk7pbc7SNzwWGM0qAhBDL5RuW2YBAoPc_TdwfU5aLypiYFUWjjh19fPM8Mba6QiKBzVf4c)

  - If the returned result contains a TXT record similar to that in the figure and the record value is the same as that on the **Certificate Details** page in the SSL Certificate Service console, your DNS configuration is correct and has taken effect.

  - If the returned result does not contain a TXT record, it's possible that the DNS configuration is incorrect or has not taken effect.
If the DNS configuration is incorrect, go to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and click the **Pending validation** tab to enter the **Certificate Details** page. Copy the record value in **Certificate Details** and update the record at your DNS service provider. If the configuration has not taken effect for a long time, contact your domain hosting provider.
    

  > **Notes**
  > For detailed directions, see [DNS Validation](https://intl.cloud.tencent.com/document/product/1007/45895).



**File validation type**

1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and click the **Pending validation** tab to enter the **Certificate Details** page.

2. Click to access the validation URL. If the accessed page displays the same content as the validation file content on the **Certificate Details** page, the access is normal; otherwise, check the following:

  - Check whether the validation URL has an address accessible over HTTPS, and if so, use the HTTPS address in the browser for another access. If the browser prompts that the certificate is untrusted or the displayed content is incorrect, disable the HTTPS service of the domain.

  - Check whether the validation URL can be accessed anywhere. As the servers for validating certificates of each brand are located in different regions, you should check whether your site has an image outside the Chinese mainland or whether the smart DNS service is used.

  - File validation requires responding to status code 200 and file content directly and does not support redirects of any kind. Check whether the validation URL has the 301 or 302 redirect, and if so, disable the redirect.
    

      > **Notes**
      > 
      > You can run the `wget -S URL` command to check whether the validation URL has a redirect.
      > 
