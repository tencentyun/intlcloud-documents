### How can I prevent my COS files from hotlinking?

1. If your files are accessed through a browser, you can use the hotlink protection feature to configure an allowlist or blocklist. For detailed directions, please see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319).
2. If your objects are accessed directly via URLs anonymously, you can [add a bucket policy](https://intl.cloud.tencent.com/document/product/436/30927) to set the IP allowlist/blocklist. For more information, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).
3. For signed requests, configuring a blocklist or allowlist is not supported.

### What do I do if the hotlink protection configuration does not take effect when I use a CDN acceleration domain name to access resources?

If you use a CDN acceleration domain name to access resources, factors such as CDN cache may affect the stability of hotlink protection in COS. In this case, you are advised to log in to the [CDN console](https://console.cloud.tencent.com/cdn) to configure hotlink protection. For detailed directions, please see [Hotlink Protection Configuration](https://intl.cloud.tencent.com/document/product/228/6292).

### Can I use an allowlist and also allow accessing the file by opening the URL in a browser?

When setting hotlink protection, you can choose to allow empty referer, so that the file can be accessed by opening its URL in a browser even if an allowlist is configured.

### What do I do if I have allowed `a.com` to access the `test` bucket via an allowlist, but the web player for `a.com` cannot play videos stored in the `test` bucket?

When you play videos on websites using players such as Windows Media Player or Flash Player, if the request referer is empty, the allowlist will not be hit. Therefore, you can allow empty referer when configuring the allowlist.

### How can I allow accessing COS files only via a corporate network?

You can enable hotlink protection for your bucket and configure a blocklist/allowlist to limit visit sources. Currently, domain names, IPs, wildcard addresses, and more are supported. For more information, please see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319).

>?
> - If a CDN acceleration domain name is used for accessing, CDN hotlink protection rules will be executed before COS ones.
> - If a signature is carried in the access URL or headers, hotlink protection−based verification will not be performed.
>


### What do I do if “You are denied by bucket referer rule” is reported when I access objects via a browser?

This error message indicates that your access is denied by the hotlink protection rules set for your bucket. You can check whether your access complies with the hotlink protection rule. If you access with a browser, empty referer should be allowed. Otherwise, accessing via a browser directly will not be available.

### How can I allow only specific IPs to access COS resources?

You can use the hotlink protection feature to configure an IP allowlist. In this case, IPs not included in the allowlist cannot access your COS resources. For detailed directions, please see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319).
