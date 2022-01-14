Anti-DDoS Pro provides Tencent Cloud public IPs with higher anti-DDoS capability. It supports Tencent Cloud services such as CVM, CLB, NAT, and WAF. It is easy to access and requires no IP changes.

## Prerequisites
You have [purchased an Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/36115) before you can bind it to the IP addresses you want to protect.

## Directions
1. Log in to the [Anti-DDoS Pro (New) Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Service Packs** on the left sidebar.
2. Select a region of the target Anti-DDoS Pro instance and click **Protected Resource** on the right of the instance.
![](https://main.qcloudimg.com/raw/f172262c384263d02239ec2243059198.png)
3. On the **Protected Resource** page, select a resource type and a resource instance as needed.
>? Anti-DDoS Pro supports Tencent Cloud managed IPs, which is currently available for beta users. If you want to use this feature, please call 4009100100 ext. 1 (Monday–Sunday, 9:00–18:00), or [submit a ticket](https://console.cloud .tencent.com/workorder/category?level1_id=141&level2_id=630&source=0&data_title=DDOS%E9%98%B2%E6%8A%A4(%E5%A4%A7%E7%A6%B9)&level3_id=861&radio_title=%E5 %8A%9F%E8%83%BD%E5%92%A8%E8%AF%A2&queue=15&scene_code=20597&step=2).

  - Resource type: supports public cloud resources with public IPs such as CVM, CLB, and WAF.
  - Select resource: supports one or more resources. The maximum resources selected cannot exceed the number of bound IPs.

![](https://main.qcloudimg.com/raw/934ccebda9aebc6647cd4a98a07348f1.png)
4. Click **OK**.
>?After you have accessed the service, you can customize your protection settings on the [Configurations](https://console.cloud.tencent.com/ddos/antiddos-native/config/port) page. For more details, see [Protection Configuration](https://intl.cloud.tencent.com/document/product/1029/36132).

