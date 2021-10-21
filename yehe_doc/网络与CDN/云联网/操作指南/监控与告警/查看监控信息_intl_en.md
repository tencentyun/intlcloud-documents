You can view network monitoring data of CCN instances in the console to facilitate your troubleshooting.

## Directions
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) and access the CCN management page.
2. On the CCN instance list page, click the **ID/Name** of the target monthly-subscribed CCN instance to enter its details page. Click the **Monitoring** tab.
3. View the following monitoring data of the current bandwidth limit type:
  - Region outbound bandwidth limit
  Select regions where network instances are associated with the CCN instance, and view **Region Bandwidth Out**, **Region Bandwidth In**, **Region Packets Out** and **Region Packets In**. You can filter to display the monitoring data for the last 24 hours, last 7 days or a custom time range.
    - Region Bandwidth Out: the average outbound traffic per second for network instances in the region
    - Region Bandwidth In: the average inbound traffic per second for network instances in the region
    - Region Packet Out: the total outbound traffic per second for network instances in the region
    - Region Packet In: the total inbound traffic per second for network instances in the region
 >?Click the ![](https://main.qcloudimg.com/raw/58861f008a814f64adb91130767f684d.png) icon to show more information of the monitoring data. Click the ![](https://main.qcloudimg.com/raw/592e164589b53ed1205fbc9e5844e487.png) icon to download it.
  - Inter-region bandwidth limit
  Select regions where network instances are associated with the CCN instance, and view **Inter-region outbound bandwidth**, **Inter-region inbound bandwidth**, **Packets out** and **Packets In**. You can filter to display the monitoring data for the last 24 hours, last 7 days or a custom time range.
    - Inter-region outbound bandwidth: the average outbound traffic per second for the two regions
    - Inter-region inbound bandwidth: the average inbound traffic per second for the two regions
    - Packets out: the total outbound traffic for the two regions
    - Packets in: the total inbound traffic for the two regions
 >?Click the ![](https://main.qcloudimg.com/raw/58861f008a814f64adb91130767f684d.png) icon to show more information of the monitoring data. Click the ![](https://main.qcloudimg.com/raw/592e164589b53ed1205fbc9e5844e487.png) icon to download it.
4. To export monitoring data, click the top-right **Export Data**. You can also specify the time range, time granularity and export metric in the pop-up window and click **Export**.
