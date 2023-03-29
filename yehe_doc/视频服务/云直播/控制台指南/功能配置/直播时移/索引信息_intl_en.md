This document shows you how to view time shifting details and configure time-shifted playback in the CSS console.

## Prerequisites
- You have logged in to the CSS console.
- You have created a [time shifting template](https://cloud.tencent.com/document/product/267/85686), bound it to a push domain, and successfully pushed a stream.

## Directions
1. Click **Feature Configuration** > **Time Shifting** on the left sidebar and select the [Time shifting details](https://console.cloud.tencent.com/live/config/time-shift/meta) tab.
2. Select a domain or enter a stream ID, specify the time period (cannot be longer than 24 hours), and click **Query**.
![](https://qcloudimg.tencent-cloud.cn/raw/98a84c68da571dbe3e8c1fa96e80c47d.png)
3. Click **Details** to enter the details page.
4. View the push URL and stream type in the **Basic Info** area.
5. In the **Index details** area, mouse over the timeline to view the timestamps.
6. Click the timeline to preview the video at a specific time point and mark that point.

>! To preview time-shifted content, the domain used for playback must have an HTTPS certificate. If your playback domain does not have an HTTPS certificate yet, add one in **Domain Management**> [Certificate Management](https://console.cloud.tencent.com/live/domainmanage/certificate). Using the time shifting feature will incur playback traffic/bandwidth fees.

7. Configure time-shifted playback as follows:

<table>
   <thead><tr><th width="20%" colspan=2>Item</th><th>Description</th></tr></thead>
   <tbody><tr>
   <tr>
   <td rowspan=2 width="10%">Time shifting mode</td>
   <td width="30%">Offset</td> 
   <td>In this mode, you configure time-shifted playback by specifying how long to delay the playback by. This is suitable for ongoing live streams.</ul></td>
   </tr><tr>
   <td>Time period</td>
   <td>In this mode, you specify the start and end time for playback (which cannot be more than six hours apart). This is suitable for live streams that have already ended.</td>
   </tr><tr>
   <td colspan=2>Playback domain</td>
   <td>Select a playback domain you added to CSS.</td>
   </tr><tr>
 <td colspan=2>Generate time-shifting playback URL</td>
   <td>Click <b>Generate Address</b> to generate a time-shifting playback URL and copy it.</td>
   </tr><tr>  
</tbody></table>

![](https://qcloudimg.tencent-cloud.cn/raw/55aa01d9fc5c2a8aabf1db3b6dcf92f8.png)
