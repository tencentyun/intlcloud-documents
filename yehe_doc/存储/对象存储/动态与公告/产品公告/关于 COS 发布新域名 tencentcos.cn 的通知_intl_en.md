COS will release a new domain – tencentcos.cn – on March 15, 2022. The current domain myqcloud.com will remain available, but will not support new features of COS. We recommend you switch to the new domain, which is more secure and reliable.


>! The current domain myqcloud.com will remain available, and its existing features (e.g., intelligent resolution for public and private access) will not be affected. However, it will not support new features provided later.
>

Specifically, there will be two changes:

**1. The suffix tencentcos.cn will be used for domain names.**

Take default bucket domains for example:

- Current domain names are in the format of &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com.
- New domain names will be in the format of &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.tencentcos.cn.

**2. Different domain names will be used for private and public access.**

Currently, domain names for private and public access have the same format. For example, all default bucket domains are in the format of &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com.

In the future, domain names for public and private access will use different formats. Take default bucket domains for example:

- A domain name for public access will be in the format of &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.tencentcos.cn.
- A domain name for private access will be in the format of &lt;BucketName-APPID&gt;.cos-internal.&lt;Region&gt;.tencentcos.cn.


The table below compares current and new domains.

| Type   | Current                    | New                |
| -------------- | ---------------------------------- | ---------------- |
| Default bucket domain | &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com, the same for domains for private and public access | <ul  style="margin: 0;"><li>Domain for public access: &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.tencentcos.cn </li><li>Domain for private access: &lt;BucketName-APPID&gt;.cos-internal.&lt;Region&gt;.tencentcos.cn  </li></ul>     |   
| Global acceleration domain | &lt;BucketName-APPID&gt;.cos.accelerate.myqcloud.com, the same for domains for private and public access   |  <ul  style="margin: 0;"><li>Domain for public access: &lt;BucketName-APPID&gt;.cos.accelerate.tencentcos.cn </li><li>Domain for private access: &lt;BucketName-APPID&gt;.cos-internal.accelerate.tencentcos.cn </li></ul>              |   
| Domain for static website |&lt;BucketName-APPID&gt;.cos-website.&lt;Region&gt;.myqcloud.com, the same for domains for private and public access | <ul  style="margin: 0;"><li>Domain for public access: &lt;BucketName-APPID&gt;.cos-website.&lt;Region&gt;.tencentcos.cn </li><li>Domain for private access: &lt;BucketName-APPID&gt;.cos-website-internal.&lt;Region&gt;.tencentcos.cn</li></ul> |       


