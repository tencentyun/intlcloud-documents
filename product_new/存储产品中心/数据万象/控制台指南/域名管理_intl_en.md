## Concepts
You need to download images stored in buckets through Cloud Infinite (CI) domain names before you can use CI to process and recognize them.
Images in buckets can be accessed through the following addresses:
- System-assigned domain name
- CDN acceleration domain name
- Custom domain name

## System-Assigned Domain Name
This domain name is defined by Tencent Cloud and cannot be changed. When you access an image through this domain name from services in Tencent Cloud, the request is sent and received in a private network environment. If you access resources through this domain name from a public network, the request is sent from the public network to CI. After a bucket is created, Tencent Cloud automatically generates a system-assigned domain name in the following format:
```
[BucketName-APPID].pic[area].myqcloud.com
For example, test-1250000000.picsgp.myqcloud.com
```

>This domain name is unchangeable.


Get the URL of a resource in a bucket by appending the relative path to the bucket’s domain name, for example:
```
http://testbucket-1250000000.picsgp.myqcloud.com/test.txt
```

>If the permission to the resource is private, append the signature suffix to the preceding URL.


### Viewing the system-assigned domain name
Log in to [CI Console](https://console.cloud.tencent.com/ci) and click **Bucket Management** to go to the management page. On the page that appears, click the **Domain Name Management** tab to view the domain name assigned by the system.
![Domain name management](https://main.qcloudimg.com/raw/18c0384e4cc5a0c72c550f7dded138f1.png)

**System-assigned domain name - cross-region access over private network:** System-assigned domain names can be used to access different Tencent Cloud products in the same region. However, if you want to access resources cross regions over a private network (for example, a CVM in Hong Kong (China) needs to access CI data in Singapore), a dedicated network connection deployed with VPC must be established to enable high-speed access. For more information, see [VPC](https://intl.cloud.tencent.com/product/vpc).


## CDN Acceleration Domain Name
The CDN acceleration domain name is initialized by Tencent Cloud and can be changed (where CNAME is required) to achieve larger bandwidth and lower latency. After a bucket is created, Tencent Cloud generates a CDN acceleration domain name in the format of:
```
[BucketName-APPID].image.myqcloud.com
```

You can enable CDN acceleration either when creating the bucket or in CI Console later as needed. CDN acceleration domain names can be accessed directly from public networks, for example:
```
http://testbucket-1250000000.image.myqcloud.com/testdir/test.jpg
```
At the same time, a new domain name, which is the CDN acceleration domain name, will be added in CDN Console.

>You can create a maximum of 100 CDN acceleration domain names for each APPID.


### Configuring the CDN acceleration domain name
1. Log in to [CI Console](https://console.cloud.tencent.com/ci). In the left sidebar, click **Bucket Management**, and then click the bucket for which you want to configure the domain name (for example, imagetest1).
![CDN1](https://main.qcloudimg.com/raw/c3eaf22d2ae3782401d86adea3d07303.png)
2. Click **Domain Management** to go to the domain management page, and click the **Edit** button for CDN acceleration to configure the domain name.
![CDN2](https://main.qcloudimg.com/raw/cecb03ee36e772faa07c07ba14a09ba3.png)
3. Change the status and click **Save**.
![CDN3](https://main.qcloudimg.com/raw/b4d2b07d4475c738f064825fd089c33f.png)

## Custom Domain Name
You may not want domain names like **qcloud.com** to appear on your website or in your services. For example, you may prefer `http://myblog.net/` over `http://myblog-1250000000.image.myqcloud.com` for a website hosted on Tencent Cloud. In this case, you can use a custom domain name. To do this, create a CNAME record in CDN Console to map `http://myblog.net/` to `http://myblog-1250000000.image.myqcloud.com`.

You can create a custom domain name that points to a bucket, and access content in the bucket after binding. After that, you can enable CDN acceleration for faster access. To avoid security issues related to businesses, we recommend that you use custom domain names to access images in CI.
>
- To ensure the normal access to CI by using the custom domain name, you need to change the CNAME DNS record to the specified address to make the domain name effective.
- The bound custom domain name must have an MIIT ICP filing, otherwise the access from the domain name will not work.
- Custom domain names do not support the configuration of HTTPS certificates. To use this feature, enable CDN acceleration and bind CDN domain names.

### Configuring the custom domain name
#### Binding steps
1. Go to the **Domain Management** page, select **Custom Domain**, and click **Add Domain** to add an existing domain name.
![Example 1](https://main.qcloudimg.com/raw/aa49f743b5c671f5dd7e26622560eb82.png)
2. Copy the CNAME address
![Example 2](https://mc.qcloudimg.com/static/img/86d0429283502cc3f13593ea77a2330f/image.png)
3. Go to Tencent Cloud DNS Console, and click the bound custom domain name.
![Example 3](https://main.qcloudimg.com/raw/56e43e68a65383896809c10802e5542f.png)
>Tencent Cloud DNS is used as an example here. For configuration, contact your DNS provider.

4. Click **Add** to add a CNAME record.
![Example 4](https://main.qcloudimg.com/raw/ad59496dd74d261e84da91ed8a2b2462.png)
>The record value is the CNAME address that you just copied. It takes about 15 minutes for the added record to take effect. 


#### Verifying the result
After the custom domain name is successfully bound, you can download files stored in the bucket through the custom domain name. The following example assumes that the **testnew** bucket contains a file named **index.htm**, and the bound custom domain name is `www.srcostest.com`.
**Before binding:**
You can access the file from the public network through testnew-1250000000.image.myqcloud.com/index.htm, which comprises the system-assigned domain name and the file path.
![Verifying the result](//mc.qcloudimg.com/static/img/9f9abfe04c8c6d43fa677c82eb8cfb8d/image.png)
**After binding:**
![Verifying the result](//mc.qcloudimg.com/static/img/ddb68254d81f45fa27d4cef7d533c1c0/image.png)
You can access the file through `www.srcostest.com/index.htm`, which comprises the custom domain name and the file path.

>If the static website feature is enabled, you can directly open and view the file through the custom domain name. For more information on how to enable the static website feature, see [Static Website Hosting](https://intl.cloud.tencent.com/document/product/436/14984).


## Setting Hotlink Protection

To protect developers’ images against hotlinking and traffic theft, Tencent Cloud CI provides the hotlink protection feature, which identifies and manages access sources with the referer mechanism supported by the HTTP protocol.
Log in to [CI Console](https://console.cloud.tencent.com/ci). In the left sidebar, click **Bucket Management**. Click the bucket for which you want to configure the domain name (for example, imagetest1), and then click **Domain Management** to configure hotlink protection.

>
- You can whitelist or blacklist websites. The referer list supports the wildcard and multiple domain names separated by line breaks (one entry per line).
- After hotlink protection is enabled, you can limit service sources based on policies.