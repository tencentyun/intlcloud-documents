Set a latency that fits your needs. Note that setting the latency too low may cause playback to stutter.

## Prerequisites
- You have activated CSS and logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).
- You have added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).


## Latency control
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar and click the **playback domain** for which you want to configure RTMP and FLV latency, or click **Manage** on the right to enter the details page.
2. Select the **Advanced Configuration** tab.
3. Select a latency that fits your needs. We recommend you set the GOP for push to 1-2 seconds. Higher GOP means higher latency.
4. When GOP is set to two seconds, the latency is as follows:
<table>
<thead>
<tr>
<th>Setting</th>
<th>High</th>
<th>Medium</th>
<th>Low</th>
</tr>
</thead>
<tbody><tr>
<td>Estimated Latency</td>
<td>7-9s</td>
<td>5-7s</td>
<td>4-5s</td>
</tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/49744a600f2e1101a9261a0205b5e651.png">

