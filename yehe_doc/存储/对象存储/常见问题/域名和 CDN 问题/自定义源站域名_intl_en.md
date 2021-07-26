### How do I access objects with my own domain name?

This can be achieved by binding a custom domain name. For more information, see [Enabling Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/31507).

### Must the custom domain name be ICP filed by Tencent Cloud if I use it?

It depends:

- For domain names connected to a CDN node in the Chinese mainland, you need to obtain ICP filing (not necessarily through Tencent Cloud).
- If your domain name is connected to a CDN node outside the Chinese mainland, you don't need to obtain an ICP filing for it.

### Do custom domain names in COS support HTTPS?

The feature of configuring HTTPS for custom domain names of COS is being upgraded. Currently, certificate hosting is supported in Hong Kong, Shanghai, Chengdu, Beijing, and Nanjing, and will be supported in other regions in the future. For regions that do not support certificate hosting yet, you can configure a reverse proxy for the domain name by referring to [Supporting HTTPS for Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/11142).

### How does COS return the access links of custom domain names after files are uploaded?

COS currently does not support returning the access links of custom domain names after files are uploaded. However, you can implement the feature by splicing access links and using custom domain names to replace [default domain names](https://intl.cloud.tencent.com/document/product/436/6224).

### Do I have to enable CDN if I use custom domain names to access COS?

You do not have to enable CDN to access COS with custom domain names. You can log in to the [COS console](https://console.cloud.tencent.com/cos5) to set custom endpoints. For operation details, see [Enabling Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/31507).

### When the origin server is changed in the CDN console, why does the original custom domain name disappear in the COS console?

**If you use the COS V5 console and a JSON domain name is configured, the COS V5 console cannot display the new domain name.** Check whether the JSON domain name is configured for your bucket. If so, change the JSON domain name to an XML domain name.

### Do I need to remove the resolution configuration from the lightweight server before binding a custom domain name to a COS bucket?

Only one CNAME record can be configured for a domain name. Therefore, you need to delete the resolution relationship between the domain name and the lightweight server first and then bind the domain name resolution relationship to the COS bucket.


## What should I do if the system indicates that domain name resolution or CNAME is not in effect?

After being configured, domain name resolution or CNAME may take several minutes to take effect. You can wait a while and try to access your bucket using your custom endpoint again. If the problem persists, you can log in to your DNS console to check whether the resolution relationship is configured correctly.

