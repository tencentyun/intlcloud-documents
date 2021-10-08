This document describes how to check whether the SaaS WAF is running.

## Directions
1. Bind a WAF instance via a domain name and real server to protect traffic. To verify whether the SaaS WAF is effective, make sure that your local computer can normally access to the domain names on your SaaS WAF instances.
2. Open `http://wow.qcloudwaf.com/?test=alert(123)` in a browser. If a blocking page is displayed, WAF protection works properly.
>! `wow.qcloudwaf.com` is a sample domain name. Please replace it with the actual domain name that has been added.

![](https://main.qcloudimg.com/raw/253fdfbae2d6529f2b1e64c1f599c8cc.png)



