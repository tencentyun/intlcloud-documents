## What should I do if the quick HTTPS plan will expire soon?

If you want to continue your use of the quick HTTPS feature, go to the [SSL Certificate Service console](https://console.cloud.tencent.com/https) to renew and upgrade it.

If you no longer want to use the feature, we recommend that you switch the connected domain to the origin before the quick HTTPS plan expires to avoid affecting normal access after the expiration. The following are directions for DNSPod:
1. Log in to the [DNSPod console](https://console.dnspod.cn/dns/list).

2. Click the target **domain** to enter the **Record Management** page.

3. Search for the CNAME record type of the connected domain and change the **Record Value** to your origin address.
   

   > **Notes**
   > 

   > If your origin address is an IP, change the **Record Type** to **A record** and enter the origin IP in **Record Value**.
   > 



4. Click **OK**.
