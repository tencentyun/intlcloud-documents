COS will release a new domain name `tencentcos.cn` on July 25, 2022. The current domain name `myqcloud.com` will remain available, but will not support new features of COS. We recommend you switch to the new domain name, which is more secure and reliable.


>! The current domain name `myqcloud.com` will remain available, and its existing features will not be affected. However, it will not support new COS features provided later.
>

Specifically, there will be the following changes:

**1. The suffix `tencentcos.cn` will be used for domain names.**

Taking the default bucket domain name as an example, the new domain name will be in the format of &lt;bucket-appid&gt;.cos.&lt;region&gt;.tencentcos.cn.

**2. Private network domain names will be provided.**

Independent private network domain names will be provided, which can be accessed only over the private network and thus avoid using public network traffic.

Taking the default bucket domain name as an example, the new private network domain name will be in the format of &lt;bucket-appid&gt;.cos-internal.&lt;region&gt;.tencentcos.cn.

**3. The `tencentcos.cn` domain name will be supported.**
Except private network domain names, all new domain names support smart DNS, so the system will switch between the private and public networks automatically based on the access environment.

| Domain Name | Example |
| -------------- | ---------------- |
| Default bucket domain name | &lt;bucket-appid&gt;.cos.&lt;region&gt;.tencentcos.cn  |
| Default bucket domain name (private network) | &lt;bucket-appid&gt;.cos-internal.&lt;region&gt;.tencentcos.cn  |
| Global acceleration domain name | &lt;bucket-appid&gt;.cos.&lt;accelerate&gt;.tencentcos.cn  |
| Global acceleration domain name (private network) | &lt;bucket-appid&gt;.cos-internal.&lt;accelerate&gt;.tencentcos.cn  |
| Static website domain name | &lt;bucket-appid&gt;.cos-website.&lt;region&gt;.tencentcos.cn  |
| Static website domain name (private network) | &lt;bucket-appid&gt;.cos-website-internal.&lt;region&gt;.tencentcos.cn  |   
