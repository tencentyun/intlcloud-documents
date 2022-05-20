CSS allows you to set a bandwidth cap for your playback domain. In the acceleration region of your domain, if the peak downstream bandwidth in a reference period hits the cap you set, a 403 error will be returned to playback requests. This feature is disabled by default.


## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:limit)
## Limits
| Acceleration Region | Default Bandwidth Capping Region | Remarks |
|---------|---------|---------|
| Chinese mainland | Chinese mainland | You can only set a cap for the Chinese mainland. |
| Outside the Chinese mainland | Outside the Chinese mainland | You can only set a cap for outside the Chinese mainland. |
| Global acceleration | Global acceleration | <ul style="margin-bottom:0px;"><li> You can set different caps for inside and outside the Chinese mainland.</li><li>You can also set a global cap.</li></ul> |


## Configuring Bandwidth Cap
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage). Click the name of your playback domain or **Manage** on the right.
2. Select the **Advanced Configuration** tab.
3. In the **Bandwidth cap configuration** area, click **Edit**.
4. Toggle on **Bandwidth Cap** ![](https://main.qcloudimg.com/raw/96d86bb811611dbc89c4757fb64af536.png), and complete the following settings:
	- The **valid region** is determined by the acceleration region of your playback domain. For details, see [Limits](#limit).
	- Enter a bandwidth cap.
	- Select a bandwidth unit (Mbps, Gbps, or Tbps).
5. Toggle on **Alert threshold** ![](https://main.qcloudimg.com/raw/96d86bb811611dbc89c4757fb64af536.png). 
     Set an alert threshold as a percentage of the bandwidth cap. When the threshold is reached, the system will send you alerts via the Message Center or other channels. 
6. Click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/b0cb7574efca181f31062e272211f103.png)

>! 
>- The conversion factor between the bandwidth units is 1,000: 1 Tbps = 1,000 Gbps; 1 Gbps = 1,000 Mbps
>- If you change the acceleration region for your domain, you need to configure the bandwidth cap again.
>- The default alert threshold is 80% of the bandwidth cap. Value range: 0-100.


## Disabling Bandwidth Cap
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage). Click the name of your playback domain or **Manage** on the right.
2. Select the **Advanced Configuration** tab.
3. In the **Bandwidth cap configuration** area, click **Edit**.
4. Toggle off **Bandwidth Cap** ![](https://main.qcloudimg.com/raw/a02cf62f7cf3e9c072047690a6818ac2.png).
5. Click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/490bd4983649a535f888a91a11446521.png)
