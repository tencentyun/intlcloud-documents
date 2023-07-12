### How do I access objects with my own domain name?

You can do so by binding a custom domain name. For more information, see [Enabling Custom Origin Domain Name](https://intl.cloud.tencent.com/document/product/436/31507).

### Do I need to obtain an ICP filing from Tencent Cloud if I use a custom domain name?

It depends on the following requirements:

- For content delivery in the Chinese mainland, ICP filing is required. You are not required to do so through Tencent Cloud though.
- If your domain name is connected to a CDN node outside the Chinese mainland, you don't need to obtain an ICP filing for it.

### Does a COS custom domain name support HTTPS?

The feature of configuring HTTPS for custom COS domain names is being upgraded. Currently, certificate hosting is supported in public cloud regions in the Chinese mainland, Singapore, and Silicon Valley, with more regions to come. For unsupported regions, you can configure a reverse proxy for the domain name by referring to [Supporting HTTPS for Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/11142).

### How does COS return the access links of custom domain names after files are uploaded?

COS currently does not support this feature. However, you can implement it by concatenating access links and using custom domain names to replace default domain names. For more information, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

### Do I need to enable CDN if I use custom domain names to access COS?

No. You can log in to the [COS console](https://console.cloud.tencent.com/cos5) to set custom domain names. For detailed directions, see [Enabling Custom Origin Domain Name](https://intl.cloud.tencent.com/document/product/436/31507).

### Why does the original custom domain name disappear from the COS console when the origin is changed in the CDN console?

**If you use the COS v5 console and a JSON domain name is configured, the COS v5 console cannot display the new domain name.** Check whether the domain name configured in your bucket is in JSON format, and if so, change it to an XML domain name.

### Do I need to remove the DNS configuration from the Lighthouse instance before binding a custom domain name to a COS bucket?

Only one CNAME record can be configured for a domain name. Therefore, you need to delete the DNS relationship between the domain name and the Lighthouse instance first and then bind the domain name to the COS bucket.


### What should I do if the system prompts that DNS resolution or CNAME is not in effect?

After being configured, DNS resolution or CNAME may take several minutes to take effect. You can wait a while and try to access your bucket at your custom origin domain name again. If the problem persists, log in to your DNS console to check whether the DNS relationship is configured correctly.

