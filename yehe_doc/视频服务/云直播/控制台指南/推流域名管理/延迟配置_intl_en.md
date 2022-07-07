It is possible to control the latency of HLS playback by adjusting the size and number of HLS segments. Note that setting the latency too low may cause playback to stutter.

## Prerequisites
- You have activated CSS and logged in to the [CSS console](https://console.cloud.tencent.com/live/livestat).
- You have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).


## Latency control
1. Select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar and click the target **push domain** or click **Manage** on the right to enter the details page.
2. Select the **Advanced Configuration** tab.
3. Select a latency that fits your needs. GOP affects the size of HLS segments. We recommend you set the GOP for push to 1-2 seconds.
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
<td>20-25s</td>
<td>10-15s</td>
<td>6-8s</td>
</tr>
</tbody></table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/3032e36b30c1a966f5db814f19635612.png">
