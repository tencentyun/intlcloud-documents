Anti-DDoS Pro provides Tencent Cloud public IPs with higher anti-DDoS capability. It supports Tencent Cloud services such as CVM, CLB, NAT, and WAF and is easy to access with no IP changes required.
## Prerequisites
You need to [purchase an Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/36115) before you can bind a protected IP.

## Directions
1. Log in to the [new Anti-DDoS Pro Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Anti-DDoS Pro Instance** on the left sidebar.
2. Select the region of the target Anti-DDoS Pro instance and click **Manage Protected Object** in the "Operation" column on the right of the instance.
![](https://main.qcloudimg.com/raw/f172262c384263d02239ec2243059198.png)
3. On the protected object management page, select "Resource Type" and "Resource Instance" as needed.
 >Anti-DDoS Pro supports hosted IPs. This feature is currently available to allowed users . If you are using an IP hosted by Tencent Cloud and want to connect it to Anti-DDoS Pro, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=630&source=0&data_title=DDOS%E9%98%B2%E6%8A%A4(%E5%A4%A7%E7%A6%B9)&level3_id=861&radio_title=%E5%8A%9F%E8%83%BD%E5%92%A8%E8%AF%A2&queue=15&scene_code=20597&step=2) for application.

  - Resource Type: resources with public IPs in the public cloud are supported, such as CVM, CLB, and WAF.
  - Resource Instance: you can select multiple instances (no more than the number of **bindable IPs**).
![](https://main.qcloudimg.com/raw/934ccebda9aebc6647cd4a98a07348f1.png)
4. After completing the selection, click **OK**.
