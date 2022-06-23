You can view network monitoring data of CCN instances in the console to facilitate your troubleshooting.

## Directions
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) and enter the CCN management page.
2. On the CCN instance list page, click the ID/Name of the target CCN instance to enter its details page. Select the **Monitoring** tab.
3. View the following monitoring data of the current bandwidth limit mode:
  - Single-region monitoring
    Select a region where network instances are associated with the CCN instance, and view **Region bandwidth out**, **Region bandwidth in**, **Region packets out** and **Region packets in** metrics. You can click **last 24 hours**, **last 7 days** or specify a custom time range to view the monitoring data.
    - Region bandwidth out: The outbound bandwidth used by the network instances in this region.
    - Region bandwidth in: The inbound bandwidth used by the network instances in this region.
    - Region packets out: Number of data packets sent from the network instances in this region.
    - Region packets in: Number of data packets received by the network instances in this region.
![](https://qcloudimg.tencent-cloud.cn/raw/8b81a4604b69053dafb9757f0c91e4ca.png)
>?Click the ![](https://main.qcloudimg.com/raw/58861f008a814f64adb91130767f684d.png) icon to show more data of the selected metric. Click the ![](https://main.qcloudimg.com/raw/592e164589b53ed1205fbc9e5844e487.png) icon to download it.
  - Inter-region monitoring
  Select two regions where network instances are associated with the CCN instance, and view **Inter-region outbound bandwidth**, **Inter-region inbound bandwidth**, **Packets out** and **Packets in** metrics. You can click **last 24 hours**, **last 7 days** or specify a custom time range to view the monitoring data.
    - Inter-region outbound bandwidth: The outbound bandwidth used in the source region between the source and destination regions.
    - Inter-region inbound bandwidth: The inbound bandwidth used in the source region between the source and destination regions.
    - Packets out: Number of data packets sent from the source region to the destination region.
    - Packets in: Number of data packets received by the source region from the destination region.
![](https://qcloudimg.tencent-cloud.cn/raw/4038cd43e1874815e036bcf13c84982a.png)
>?Click the ![](https://main.qcloudimg.com/raw/58861f008a814f64adb91130767f684d.png) icon to show more data of the selected metric. Click the ![](https://main.qcloudimg.com/raw/592e164589b53ed1205fbc9e5844e487.png) icon to download it.
4. To export the monitoring data, click the top-right **Export data**. Specify the time range, time granularity and the metrics to export in the pop-up window, and click **Export**.
![](https://qcloudimg.tencent-cloud.cn/raw/d4e20b3fd4f02b2e823a1611625001bf.png)
