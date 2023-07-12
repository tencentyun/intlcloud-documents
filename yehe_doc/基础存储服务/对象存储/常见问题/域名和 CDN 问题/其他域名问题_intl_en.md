### Does COS support HTTPS access?

Yes. COS allows SSL transport for all access nodes in the [available regions](https://intl.cloud.tencent.com/document/product/436/6224), and HTTPS is enabled by default in the SDK and console. **COS strongly recommends you use HTTPS to protect the data linkage for transport. If you use unencrypted HTTP, the linkage may be monitored or the data may be stolen.**


### When I manage domain names on the console, I am always prompted to "Enable at least one available key". What should I do?

Log in to the [CAM Console](https://console.cloud.tencent.com/cam/capi) to check if the cloud API key is enabled.

- If the cloud API key is not enabled, create and enable a key before managing domain names.
- If the cloud API key is enabled and you are still prompted, check whether the account you are operating with is a sub-account (collaborator's or sub-user's account):
  - If it is a sub-account, log in using the root account and confirm that the cloud API key is enabled.
  - If it is a root account, purge the browser cache and log in to the Tencent Cloud account again.

### What’s the difference between COS default domain name, custom CDN acceleration domain name, and custom origin server domain name?

For more information about domain names, please see [Domain Name Management Overview](https://intl.cloud.tencent.com/document/product/436/18424).
- **Default domain name**: COS origin server's domain name, which is automatically generated based on the bucket name and region when you create a bucket. 
- **Custom CDN acceleration domain name**: you can bind for your bucket a custom domain name to Tencent Cloud Content Delivery Network (CDN), and access objects in your bucket using this domain name. (If you have enabled "Custom domain name" in the legacy COS Console, the new console will continue to display "Custom domain name" instead of “Custom CDN acceleration domain”.)
- **Custom origin server domain name**: You can bind a custom domain name with ICP filing to the current bucket, and access objects in the bucket using this domain name.

### What’s the difference between CDN acceleration and global acceleration in COS?

1. Different use cases: **CDN acceleration** is mainly used for downloading and distributing a great number of objects in a bucket, especially for scenarios where the same data needs to be downloaded repeatedly. For more information, please see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669). **Global acceleration** leverages Tencent’s load balancing system that features global traffic scheduling, to intelligently route and parse user requests and select the optimal network linkage for nearby access. COS’s global acceleration also speeds up uploads and downloads. For more information, please see [Global Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/33409).
2. Different costs. CDN acceleration may involve CDN traffic fees and CDN origin-pull fees, while global acceleration may involve global acceleration traffic fees. For detailed traffic pricing, please see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776).

### Do I need to bind a domain name to use COS?

No. You can access COS with COS’s default domain in the format of `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com` without binding a custom domain name. For more information about COS domain names, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). If you need to bind a custom domain, please see [Enabling Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/31507).

### Why can I access COS via a private IP range 169.254.0.x in a VPC in the same region?

If the client and COS are in the same region, the COS domain name is forcibly resolved to the IP range 169.254.0.x in the private DNS service of Tencent Cloud through hijacking. By default, the IP range 169.254.0.x communicates with your VPC IP range, and the traffic is diverted to the gateway through internal routes to access COS. Therefore, if you access COS via a private network, do not modify the DNS service configuration. Otherwise, private DNS will fail.

