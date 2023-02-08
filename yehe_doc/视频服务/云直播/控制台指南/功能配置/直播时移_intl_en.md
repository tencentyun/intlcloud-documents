Time shifting is powered by the recording capability of CSS. It allows users to rewind and play earlier parts of a live stream. This is commonly used to play back highlights of live streamed sports events.

## Notes
- After creating a time shifting template, you need to bind it to a push domain. The configuration takes effect 5-10 minutes after binding.
- Time shifting is billed based on the traffic of live streams for which time shifting is enabled. Using this feature will also incur [playback traffic/bandwidth costs](https://intl.cloud.tencent.com/document/product/267/2819).
- To timeshift a transcoded live stream, you need to configure a transcoding task for the stream in advance. This will incur transcoding fees. Please make sure the transcoding template used is not deleted.

## Prerequisites
- You have activated CSS and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).

## Creating a Time Shifting Template
1. Log in to the CSS console and select **Feature Configuration** > [Time Shifting](https://console.cloud.tencent.com/live/config/time-shift/template) on the left sidebar.
2. Click **Create template**.
![](https://qcloudimg.tencent-cloud.cn/raw/ffae437b96aada6754ad374093088218.png)

<table>
   <thead><tr><th width="20%" colspan=2>Item</th><th>Description</th></tr></thead>
   <tbody><tr>
   <tr>
   <td colspan=2>Template Name</td>
   <td>The time shifting template name, which can be 1-10 characters long and can contain Chinese characters, letters, numbers, and _-</td>
   </tr><tr>
   <td colspan=2>Template Description</td>
   <td>The description of the template, which can contain Chinese characters, letters, numbers, and _-</td>
   </tr><tr>
   <td colspan=2>Region</td>
   <td>The Chinese mainland is selected by default. You can change to “Outside Chinese mainland”. Make sure you select the correct region. Cross-region time shifting may lead to stuttering or playback failure. </td>
   </tr><tr>
   <td rowspan=3 width="10%">Stream type</td>
   <td width="30%">Original stream</td> 
   <td>The original stream (not transcoded, watermarked, or mixed) is timeshifted. For WebRTC streams, please select other stream types, as audio will be missing from the timeshifted content.</ul></td>
   </tr><tr>
   <td>Watermarked stream</td>
   <td>The watermarked stream (watermarked as specified in the selected watermark template) is timeshifted.</td>
   </tr><tr>
   <td>Transcoded stream</td>
       <td>The transcoded stream (transcoded as specified in the selected transcoding templates) is timeshifted. If a transcoding template is deleted, time shifting will not work for that template.
</td>
   </tr><tr>
   <td colspan=2>Time-shift days</td>
   <td>1 day is selected by default. You can choose 3 days, 7 days, 15 days, or 30 days.</td>
   </tr><tr>
   <td colspan=2>TS segment length</td>
   <td>The default length is five seconds. You can set it to a value between 3 and 10.</td>
   </tr><tr>
   </tbody></table>

3. Click **Save**.

## Binding a Domain Name

1. Log in to the CSS console, and select **Feature Configuration** > [Time Shifting](https://console.cloud.tencent.com/live/config/time-shift/template) on the left sidebar.
   - **Bind a domain to an existing template**: Click **Bind Domain Name** in the top left.
     ![](https://qcloudimg.tencent-cloud.cn/raw/121c2a1f6a42f56c537efdcf9f9d2837.png)
   - **Bind a domain after creating a template**: After [creating a template](#C_record), click **Bind Domain Name** in the dialog box that pops up.
     ![](https://qcloudimg.tencent-cloud.cn/raw/4e2eb59f230a83a8ee739d35992ceab0.png)
2. In the pop-up window, select a **time shifting template** and a **push domain** and then click **Confirm**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/36611d57b671961122f9690ed202a998.png)
>? You can click **Add** to bind multiple push domains to a template.

## Unbinding a Domain Name

1. Log in to the CSS console, and select **Feature Configuration** > [Time Shifting](https://console.cloud.tencent.com/live/config/time-shift/template) on the left sidebar.
2. Select a time shifting template bound with domain names, find the target domain name, and click **Unbind**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8a04377777c3eb3bee46be2b0ed38785.png)
3. In the pop-up window, click **Confirm**.
   ![](https://main.qcloudimg.com/raw/690daf43f9b1d5f57b6033720c19860a.png)

>? Unbinding a time shifting template will not affect ongoing live streams.

[](id:change)

## Modifying a Template

1. Go to **Feature Configuration** > [Time Shifting](https://console.cloud.tencent.com/live/config/time-shift/template).
2. Select the target time shifting template, click **Edit** on the right, modify the settings, and click **Save**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/6e283a7e7a541da14bd58806b502f785.png)

[](id:delete)
## Deleting a Template

1. Log in to the CSS console, and select **Feature Configuration** > [Time Shifting](https://console.cloud.tencent.com/live/config/time-shift/template) on the left sidebar.
2. Select the target time shifting template, and click **Delete** in the upper right.
3. In the pop-up window, click **Confirm**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/1ca10b189eaf82a772dc3c460df2c1bd.png)

>! 
>- If domain names are bound to a template, you need to [unbind](#unite) them before you can delete the template.
>- In the console, time shifting templates are managed at the domain level. You cannot unbind time shifting rules bound to streams by APIs.

## More

You can also **unbind** and **bind** domains and time shifting templates on the **Domain Management** page. For details, see “Time Shifting Configuration”.