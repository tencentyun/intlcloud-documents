This document describes how to check whether the SaaS WAF is running.

## Directions
1. Bind a WAF instance via a domain name and origin server to protect traffic. To verify whether the SaaS WAF is effective, make sure that your local computer can normally access to the domain names on your SaaS WAF instances.
2. Open `http:// saas.technicalsupport.cn/?test=alert(123)` in a browser. If a block page is displayed, WAF protection works properly.
>! Please replace `saas.technicalsupport.cn` with your actual domain name.

![](https://qcloudimg.tencent-cloud.cn/raw/9761b764f9523d92540f1034aaf6820f.png)



