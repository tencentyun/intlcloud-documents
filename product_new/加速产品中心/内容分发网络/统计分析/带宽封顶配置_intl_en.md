You can configure a bandwidth cap for a domain name. When the bandwidth consumed by the domain name exceeds the max bandwidth configured within a statistical cycle (5 minutes), all access requests will be forwarded to the origin server or the CDN service will be disabled, and a 404 error will be returned for all access requests.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click "Manage" on the right of the domain name to be edited.
![](https://main.qcloudimg.com/raw/51af095ddcf92672ea290ce96c511b95.jpg)
2. Click the **Advanced Configuration** tab to see the **Bandwidth Cap Configuration** module. This feature is disabled by default.
![](https://main.qcloudimg.com/raw/5fbfd42e5dd7a0e8dcf4453e488ee373.png)
3. Toggle the switch on to enable it. When enabled, the bandwidth cap is **10 Gbps** by default. If the cap is reached, requests will be **forwarded to the origin server**. You can click the **Edit** icon to set the bandwidth cap and how user requests will be handled if the cap is exceeded.
- If your purpose is to prevent DDoS attacks, we recommend selecting "Return 404" to protect your origin server.
- If your purpose is to control CDN service fees, we recommend selecting "Forward to origin server" to prevent your service from being affected.
![](https://main.qcloudimg.com/raw/d0d18e7f971358cee9fc8e30f279d972.jpg)
4. If the cap is exceeded, you will be notified by email, SMS or through the Message Center. You can check the domain status in the CDN Console. No matter if you select "Forward to origin server" or "Return 404", the domain will be changed to **Disabled** status. It takes about **5 to 15 minutes** for the settings to take effect.
![](https://main.qcloudimg.com/raw/55d11b507196c42184ce19fcc699ca0c/limit2.png)
> The domain will be closed once the bandwidth cap is reached. To continue using the CDN service, you can activate domain name acceleration again in the [CDN Console](https://console.cloud.tencent.com/cdn). For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/doc/product/228/5736).

## Sample Case
If the domain name `www.test.com` is configured as follows:
![](https://main.qcloudimg.com/raw/0bcccaa37b05aa14a3eb47f290fe84fa.png)
CDN will periodically detect the latest bandwidth statistics of the domain name. If it finds at 12:15:00 that the bandwidth value of the domain name at the time point of 12:05:00 (representing the data generated between 12:05:00 and 12:10:00) is above 1 Kbps which exceeds the set cap, it will immediately start to deliver the configuration to forward requests to the origin server. As the configuration is delivered to all CDN nodes in batches and takes effect node by node, the bandwidth will drop gradually and the configuration will take full effect on all nodes at around 12:20:00.
