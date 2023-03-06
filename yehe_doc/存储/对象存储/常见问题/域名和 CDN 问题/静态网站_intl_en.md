


### What should I do if I failed to set a custom domain name in the COS console?

1. Make sure that the domain name has obtained an ICP filing.
2. Make sure that the DNS resolution of the domain name is correct. If CDN acceleration is disabled, you need to go to the DNS console to map the CNAME record of your domain name to the [default domain name](https://intl.cloud.tencent.com/document/product/436/18424) of the bucket.



### What is the difference between enabling and disabling CDN acceleration if I have my own domain name bound?

- **CDN acceleration enabled**: The domain name is managed by CDN. Enabling CDN acceleration in the COS console has the same effect as adding a domain name in the [CDN console](https://console.cloud.tencent.com/cdn) (setting COS as the origin). The CDN-allocated CNAME record is needed for DNS resolution. During the configuration, add the domain name first and then resolve it.
- **CDN acceleration disabled**: The domain name is managed by COS. The domain name configuration is delivered to all download devices connected to the region where the bucket resides. The default domain name of the bucket is used as the CNAME record for DNS resolution.

### Why does the `Content-Disposition` header I set for objects not take effect?

Other custom headers can take effect once set. However, `Content-Disposition` takes effect only if the static website hosting feature is enabled and you access objects with a custom domain name.




### What should I do if a static website cannot be accessed by using a CDN domain name?

Check the configuration of the CDN-accelerated domain name in the following steps:

1. Select **Static Website Endpoint** as the origin type.
2. Set origin-pull authentication and CDN service authorization based on the bucket permission:
 - If the bucket permission is private read, authorize the CDN service and enable origin-pull authentication.
 - If the bucket permission is public read, there is no need to authorize the CDN service or enable origin-pull authentication.
3. Set CDN authentication based on the bucket permission:
 1. If the bucket permission is private read:
 <table>
	<tr><th>CDN Authentication</th><th>Access at CDN Acceleration Domain Name </th><th>Access at COS Domain Name </th><th>Use Case</th></tr>
	<tr><td>Disabled (default)</td><td>No </td><td>COS authentication required </td><td>Direct access to the CDN domain name to protect the content on the origin</td></tr>
	<tr><td>Enabled </td><td>URL authentication required </td><td>COS authentication required </td><td>Full-linkage protection (with hotlink protection for CDN authentication supported)</td></tr>
</table>
 2. If the bucket permission is public read:
<table>
	<tr><th>CDN Authentication</th><th>Access at CDN Acceleration Domain Name </th><th>Access at COS Domain Name </th><th>Use Case</th></tr>
	<tr><td>Disabled (default) </td><td>Yes </td><td>Yes </td><td>Site-wide public access via CDN or origin</td></tr>
	<tr><td>Enabled </td><td>URL authentication required </td><td>Yes </td><td>Hotlink protection enabled for access via CDN but not origin (not recommended)</td></tr>
</table>
4. After confirming that the above configurations are correct, check the protocol used to access the CDN acceleration domain name and the **forced HTTPS** configuration of the static website:
 - If you are using the HTTP protocol to access the CDN acceleration domain name, **do not enable forced HTTPS**.
 - If you are using the HTTPS protocol to access the CDN acceleration domain name, we recommend you **enable follow 301/302** for the CDN acceleration domain name. For more information, see [Follow 301/302 Configuration](https://intl.cloud.tencent.com/document/product/228/7183).
5. If the problem persists, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.

### What should I do if 404 is returned on refresh when the static website is used together with the frontend Vue framework and the router is set to History mode?

On the static website configuration page of the bucket, set the error document path to the landing page of the web application (generally index.html) and set the status code of the error document to 200. For the configuration directions of static websites, see [Setting Up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984).


>! After the above configurations are completed, if you need 404 to respond normally, you can configure it at the most bottom layer of the Vue frontend router configuration. In most cases, wildcards match the custom 404 component.
>


