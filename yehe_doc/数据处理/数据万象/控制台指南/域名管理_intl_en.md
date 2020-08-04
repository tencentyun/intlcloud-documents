## Concepts
You can recognize and process images in your bucket using CI when downloading them through Cloud Infinite (CI) domain names.
Images in buckets can be accessed through the following addresses:
- System-assigned domain name
- CDN acceleration domain name
- Custom domain name

## System-Assigned Domain Name
This domain name is defined by Tencent Cloud and cannot be changed. When you access an image through this domain name from services in Tencent Cloud, the request is sent and received in a private network environment. If you access resources through this domain name from a public network, the request is sent from the public network to CI. After a bucket is created, Tencent Cloud automatically generates a system-assigned domain name in the following format:
```plaintext
[BucketName-APPID].pic[area].myqcloud.com
For example, test-1250000000.picgz.myqcloud.com
```

>This domain name is unchangeable.


Get the URL of a resource in a bucket by appending the relative path to the bucket’s domain name, for example:
```plaintext
http://testbucket-1250000000.picgz.myqcloud.com/test.txt
```

>If the permission to the resource is private, append the signature suffix to the preceding URL.


### Viewing the system-assigned domain name

1. In the [CI console](https://console.cloud.tencent.com/ci), click **Bucket Management** to go to the bucket list.
2. Select the bucket you want to open the bucket management page.
3. Click **Domain Management**, and you will see the system-assigned domain at the very top.
![](https://main.qcloudimg.com/raw/99549145e0099e20ef282103d1ecd346.png)

**System-assigned domain name - cross-origin access over private network:** System-assigned domain names can be used to access different Tencent Cloud products in the same region. However, if you want to access resources cross regions over a private network (for example, a CVM in Guangzhou needs to access CI data in Singapore), a dedicated network connection deployed with VPC must be established to enable high-speed access. For more information, see [VPC](https://intl.cloud.tencent.com/product/vpc).


## CDN Acceleration Domain Name
The CDN acceleration domain name is initialized by Tencent Cloud and can be changed (where CNAME is required) to achieve larger bandwidth and lower latency. After a bucket is created, Tencent Cloud generates a CDN acceleration domain name in the format of:
```plaintext
[BucketName-APPID].image.myqcloud.com
```

You can choose to enable CDN acceleration either when [creating a bucket](https://intl.cloud.tencent.com/document/product/1045/33436) or  using **Domain Management** after creating a bucket. For more information, see [Configuring CDN Acceleration Domain Names](#.E9.85.8D.E7.BD.AE-cdn-.E5.8A.A0.E9.80.9F.E5.9F.9F.E5.90.8D). Once enabled, a CDN acceleration domain can be accessed over public network. Example:
```plaintext
http:// testbucket-1250000000.image.myqcloud.com/testdir/test.jpg
```
At the same time, a new domain name, which is the CDN acceleration domain name, will be added in CDN Console.

>You can create a maximum of 100 CDN acceleration domain names for each APPID.


### Configuring the CDN acceleration domain name
1. Log in to [CI Console](https://console.cloud.tencent.com/ci). In the left sidebar, click **Bucket Management**, and then click the bucket for which you want to configure the domain name (for example, imagetest).
2. Click **Domain Management** to go to the domain management page, and click the **Edit** button for CDN acceleration to configure the domain name.
![](https://main.qcloudimg.com/raw/87a938bb960473a4dd51418145d08f5f.png)
3. Toggle **Status** on, and click **Save**.
![](https://main.qcloudimg.com/raw/a04eaadfc0129cac9f325ca45cec8814.png)

## Custom Domain Name
You may not want domain names like `qcloud.com` to appear on your website or in your services. For example, you may prefer `http://myblog.net/` over `http://myblog-1250000000.image.myqcloud.com` for a website hosted on Tencent Cloud. In this case, you can use a custom domain name. To do this, create a CNAME record in CDN Console to map `http://myblog.net/` to `http://myblog-1250000000.image.myqcloud.com`.

You can create a custom domain name that points to a bucket, and access content in the bucket after binding. After that, you can enable CDN acceleration for faster access. To avoid security issues related to businesses, we recommend that you use custom domain names to access images in CI.

>
- To ensure the normal access to CI by using the custom domain name, you need to change the CNAME DNS record to the specified address to make the domain name effective.
- The bound custom domain name must have an MIIT ICP filing, otherwise the access from the domain name will not work.
- Custom domain names do not support the configuration of HTTPS certificates. To use this feature, enable CDN acceleration and bind CDN domain names.

## Setting Hotlink Protection

To protect developers’ images against hotlinking and traffic theft, Tencent Cloud CI provides the hotlink protection feature, which identifies and manages access sources with the referer mechanism supported by the HTTP protocol.
1. Log in to [CI Console](https://console.cloud.tencent.com/ci). In the left sidebar, click **Bucket Management**, and then click the bucket for which you want to configure the domain name (for example, imagetest).
2. Click **Domain Management** and scroll down to the **Hotlink Protection Setting** section to make a configuration.

>
>- You can allowlist or blocklist websites. The referer list supports the wildcard and multiple domain names separated by line breaks (one entry per line).
>- After hotlink protection is enabled, you can limit service sources based on policies.
