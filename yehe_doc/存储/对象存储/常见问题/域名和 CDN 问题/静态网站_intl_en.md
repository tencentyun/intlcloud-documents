### How can I display an object when I access it instead of having to download it?

You can bind it to your own domain (if you need to purchase a domain, you can register one from Tencent Cloud and enable the static website feature). For details, see [Setting up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984).

### What should I do if I failed to set a custom domain in the COS console?

1. Ensure that the domain has obtained an ICP filing.
2. Ensure that the DNS of the domain is correct. If CDN acceleration is disabled, you need to go to the DNS console to map the CNAME of your domain to the [default domain](https://intl.cloud.tencent.com/document/product/436/18424) of the bucket.

### What should I do if the images cannot be displayed even after I enable the static website feature?

1. If you want the objects (images) to be displayed directly when you access COS, you need to enable the static website feature, instead of setting `Content-Disposition:inline` in the object headers. 
2. Check browser or CDN for cached data. You can use the curl and wget commands to avoid browser caching. The cached CDN URL can be purged in the [CDN Console](https://console.cloud.tencent.com/cdn).

### What’s the difference between enabling and disabling CDN acceleration if I have my own domain bound?

- **CDN acceleration enabled**: The domain is managed by CDN. Enabling CDN acceleration in the COS console has the same effect as adding a domain in the [CDN console](https://console.cloud.tencent.com/cdn) (setting COS as the origin server). The CDN-allocated CNAME record is needed for domain resolution. During the configuration, add the domain first and then resolve it.
- **CDN acceleration disabled**: The domain is managed by COS. The domain configuration is delivered to all download devices connected to the region where the bucket resides. The default domain of the bucket is used as the CNAME record for domain resolution.

### Why does the `Content-Disposition` header I set for the object not take effect?

Other custom headers can take effect once set. However, `Content-Disposition` takes effect only if the static website feature is enabled, and you access the object with a custom domain.


### What should I do if the images cannot be displayed even after I enable the static website feature?

Check your browser or CDN for cached data. You can use the curl and wget commands to avoid browser caching. The cached CDN data can be purged in the [CDN Console](https://console.cloud.tencent.com/cdn) if you use a CDN domain name for access.

### What if I can't access the configured static website using a CDN domain name?

Check the configuration of the CDN-accelerated domain name by following the steps below.

1. Select "static website" for the origin server type.
2. Origin-pull authentication and CDN service authorization need to be set based on the bucket permission:
 - If the bucket permission is private-read, authorize the CDN service and enable origin-pull authentication.
 - If the bucket permission is public-read, there is no need to authorize the CDN service or enable origin-pull authentication.
3. CDN authentication needs to be set based on the bucket permission:
 1. If the bucket is set to private-read:
 <table>
	<tr><th>CDN Authentication</th><th>Access with CDN Acceleration Domain </th><th>Access with COS Domain </th><th>Scenario</th></tr>
	<tr><td>Disabled (default)</td><td>No </td><td>COS authentication required </td><td>Allowing direct access to CDN domain names to protect the content on the origin server</td></tr>
	<tr><td>Enabled </td><td>URL authentication required </td><td>COS authentication required </td><td>Securing access comprehensively (hotlink protection for CDN authentication is supported)</td></tr>
</table>
 2. If the bucket is set to public-read:
<table>
	<tr><th>CDN Authentication</th><th>Access with CDN Acceleration Domain </th><th>Access with COS Domain </th><th>Scenario</th></tr>
	<tr><td>Disabled (default) </td><td>Yes </td><td>Yes </td><td>Allowing all public access to the entire website via the CDN or origin server</td></tr>
	<tr><td>Enabled </td><td>URL authentication required </td><td>Yes </td><td>Enabling hotlink protection for access via the CDN but not the origin server (not recommended) </td></tr>
</table>
4. After confirming that the above configurations are correct, check the protocol used to access the CDN-accelerated domain name and the **forced HTTPS** configuration of the static website:
 - If you are using the HTTP protocol to access the CDN-accelerated domain name, **do not enable Forced HTTPS**.
 - If you are using the HTTPS protocol to access the CDN-acceleration domain name, you are recommended to **enable Follow 301/302** in the CDN-acceleration domain name configuration. For more information, see [Follow 301/302 Configuration](https://intl.cloud.tencent.com/zh/document/product/228/7183).
5. If the problem persists after you perform the steps above, you can [contact us](https://intl.cloud.tencent.com/contact-sales).

### What should I do if 404 is returned on refresh if the static website is used together with the frontend Vue framework and the router is set to History mode?

On the static website configuration page of the bucket, set the error document path to the landing page of the web application (mostly index.html) and set the status code of the error document to 200. For the configuration directions of static websites, please see [Setting up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984).
![](https://main.qcloudimg.com/raw/9bf814df9706a8cef39969c12f6fd77a.png)

>! After the configurations above are complete, if you need 404 to respond normally, you can configure it at the most bottom layer of the Vue frontend router configuration (in most cases, asterisks match the custom 404 component).
>


