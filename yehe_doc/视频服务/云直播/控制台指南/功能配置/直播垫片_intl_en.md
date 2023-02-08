This document shows you how to create, bind, unbind, modify, and delete a standby stream template. A standby stream shows a video or image that becomes active automatically when your live stream is interrupted, helping you improve viewing experience. Once the original stream is recovered, CSS will switch back.

## Notes
- After creating a template, you need to bind it to a push domain. The configuration takes effect 5-10 minutes after binding.
- Binding, unbinding, or modifying a template affects only new live streams and not ongoing ones. To make the change apply to ongoing live streams, you need to stop them and push them again.
- You can create up to **50** standby stream templates.

## Prerequisites

You have activated CSS and added a [push domain](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:Watermark)
## Creating a Standby Stream Template
1. Log in to the CSS console. Select **Feature Configuration > Standby Streams** on the left sidebar.
2. Click **Create template**.
3. Enter a template name, which can be up to 30 characters long and can contain Chinese characters, letters, numbers, underscores (_), and hyphens (-).
4. Describe the template using Chinese characters, letters, numbers, and _- in not more than 1,024 characters.
5. Select the stream type, which can be image or video.
   - If you select image, upload a JPG or PNG image not larger than 5 MB.
   - If you select video, enter the VOD URL of a video (FLV or MP4) or audio (AAC) file.
6. Configure the wait time, which can be 0-6 seconds.
7. Configure the max playback time. There isn’t an upper limit on the value of this parameter.
8. Click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/b6803bb5cc4cfca3670308aba99f8a8c.png)

[](id:conect)
## Binding a Domain Name
1. Log in to the CSS console and select **Feature Configuration** > [Standby Streams](https://console.cloud.tencent.com/live/config/pad) on the left sidebar.
2. You can bind a domain to a template in one of two ways:
  - **Bind a domain to an existing template**: Click **Bind Domain Name** in the top left.
![](https://qcloudimg.tencent-cloud.cn/raw/a530d49b2391588bb4014d42fa3e4b71.png)
  - **Bind a domain after creating a template**: After creating a standby stream template, click **Bind Domain Name** in the dialog box that pops up.
![](https://qcloudimg.tencent-cloud.cn/raw/90cace3aeed0bae1117f89f4fb161a59.png)
3. In the pop-up window, select a **standby stream template** and a **push domain** and then click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/bee76d1bfcbbc697838cb383d0a74f55.png)
>? You can click **Add** to bind multiple push domains to a template.

[](id:untie)
## Unbinding a Domain Name
1. Log in to the CSS console and select **Feature Configuration** > [Standby Streams](https://console.cloud.tencent.com/live/config/pad) on the left sidebar.
2. Select the target template and click **Unbind**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/7783a32f702d370d41eb2591da5cc820.png)
3. In the pop-up window, click **Confirm**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/a611aff7af82504fdeebed75624a4d5d.png)

[](id:change)

## Modifying a Template

1. Go to **Feature Configuration** > [Standby Streams](https://console.cloud.tencent.com/live/config/pad).
2. Select the target template and click **Edit** on the right to modify the template information.
3. After modification, click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/bdd5c4ba74916133db6763e3c7e9822f.png)


[](id:delete)
## Deleting a Template
If a template is bound to domains, you need to unbind them first before you can delete the template. For how to unbind domains, see [Unbinding a Domain Name](#untie).
1. Go to **Feature Configuration** > [Standby Streams](https://console.cloud.tencent.com/live/config/pad).
2. Select the template you want to delete and click **Delete** in the top right.
3. In the pop-up window, click **Confirm**.

![](https://qcloudimg.tencent-cloud.cn/raw/f5b91fe4eb75e001f796400cc96775af.png)

## More
You can also **unbind** and **bind** domains and standby stream templates on the **Domain Management** page. For details, see [Standby Stream Configuration](https://intl.cloud.tencent.com/document/product/267/31064).