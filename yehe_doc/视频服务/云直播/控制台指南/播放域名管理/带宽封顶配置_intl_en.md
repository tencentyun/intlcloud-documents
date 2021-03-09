Tencent Cloud provides the bandwidth cap feature for playback domain name, which is disabled by default. You can set a cap threshold for the downstream bandwidth in the domain name acceleration region. If the peak bandwidth reaches the threshold within a statistical cycle, a 403 error will be returned for all CSS requests. You can enable/disable the bandwidth cap based on the actual usage of the domain name.


## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).


<h2 id="limit">Use Limits</h2>

| Playback Domain Name Acceleration Region | Default Restricted Region | Notes |
|---------|---------|---------|
| Chinese mainland | Chinese mainland | The restricted region cannot be changed |
| Hong Kong/Macao/Taiwan (China Region) and other regions | Hong Kong/Macao/Taiwan (China Region) and other regions | The restricted region cannot be changed |
| Global acceleration | Global acceleration | The restricted regions can be configured to: <ul style="margin-bottom:0px;"><li> Chinese Mainland and/or Hong Kong/Macao/Taiwan (China Region) and other regions</li><li>Global acceleration region</li></ul> |


## Configuring Bandwidth Cap
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **playback domain name** to be configured or **Manage** on the right to enter the domain details page.
2. Select **Advanced Configuration** > **Bandwidth Cap Configuration**.
3. Click **Edit** in the top-right corner to enter the bandwidth cap configuration page.
4. Toggle **Bandwidth Cap** on ![](https://main.qcloudimg.com/raw/96d86bb811611dbc89c4757fb64af536.png).
5. Click **+Add limits** to configure as follows:
	1. 	The available restricted regions are based on the type of playback domain name acceleration region you have selected. For more information on restricted region configuration rules, please see [Use Limits](#limit).
	2. Enter the bandwidth threshold.
	3. Select a bandwidth unit (Mbps, Gbps, or Tbps).
6. Click **Save**.

![](https://main.qcloudimg.com/raw/88017c4326a9392dba00163476887a97.png)
>! 
>- The conversion scale for bandwidth is 1,000; for example, 1 Tbps = 1,000 Gbps, and 1 Gbps = 1,000 Mbps.
>- Switching the region will invalidate the bandwidth cap configuration, so you will need to configure it again.


## Disabling Bandwidth Cap
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **playback domain name** to be configured or **Manage** on the right to enter the domain details page.
2. Select **Advanced Configuration** > **Bandwidth Cap Configuration**.
3. Click **Edit** in the top-right corner to enter the bandwidth cap configuration page.
![](https://main.qcloudimg.com/raw/4dad76e233af788367fd5753a97a01bf.png)
4. Toggle **Bandwidth Cap** off ![](https://main.qcloudimg.com/raw/a02cf62f7cf3e9c072047690a6818ac2.png).
5. Click **Save**.
