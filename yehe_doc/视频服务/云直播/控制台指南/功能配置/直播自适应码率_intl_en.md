With the adaptive bitrate feature, the playback bitrate of a live stream can change smoothly based on network conditions. This ensures a smooth playback experience under changing network conditions.

## Notes
1. After creating a template, you can bind it with a playback domain. The template will take effect after 5-10 minutes.
2. A playback domain can be bound with **multiple adaptive bitrate templates**, and an adaptive bitrate template can be bound to **multiple playback domains**.
3. Each adaptive bitrate template can have up to 15 streams.
4. For the adaptive bitrate feature to work, the player needs to support adaptive bitrate.
5. The GOP for the streams of an adaptive bitrate template must be identical.
6. The codec for the streams of an adaptive bitrate template must be the same.



## Creating an Adaptive Bitrate Template
1. Log in to the CSS console. Select **Feature Configuration > Adaptive Bitrate** on the left sidebar.

2. Click **Create template** and complete the following settings:

  - Basic information: The template name and description. For details, see [Basic Information](#C_trans_normal).
  - Stream information: See [Stream Information](#C_trans_high).

3. Click **Add stream** to add a new stream to the template. You can add up to 15 streams for each template.

4. Click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/afadb4460bc1e5e275b38785f003158a.png)

<table id="C_trans_normal">
<tr><th width="20%">Basic Information</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Template name</td>
<td>Yes</td>
<td>The name of the adaptive bitrate template, which can be 1-10 characters long and supports letters and numbers (cannot contain only numbers).</td>
</tr><tr>
<td>Template description</td>
<td>No</td>
<td>The description of the template, which can contain letters, numbers, underscores (_), and hyphens (-).</td>
</tr></table>
<table id="C_trans_high">
<tr><th width="20%">Stream Information</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Stream name</td>
<td>Yes</td>
<td>The name of a stream, which can be 1-10 characters long, supports letters and numbers (cannot contain only numbers), and cannot be identical to the name of an existing transcoding template or stream.</td>
</tr><tr>
<td>Video quality</td>
<td>No</td>
<td>You can choose <b>Smooth, SD, or HD</b>. After you select a value, the system will automatically enter the recommended video bitrate and height, which can be modified.</td>
</tr><tr>
<td>Video bitrate (Kbps)</td>
<td>Yes</td>
<td>The output video bitrate. Value range: 100-8000.<ul style="margin:0">
  <li>If you enter a value not larger than 1,000, it must be a multiple of 100.</li>
  <li>If you enter a value larger than 1,000, it must be a multiple of 500.</li></ul>
</td>
</tr><tr>
<td>Video resolution (px)</td>
<td>Yes</td>
<td><li>You can set either the <b>height</b> (default) or <b>short side</b> of the output video.</li><li>Value range: 2-3000. The value must be a multiple of 2. The other side will be auto-scaled.</li></td>
</tr><tr>
<td>Codec</td>
<td>No</td>
<td>The original codec is selected by default. You can change it to H.264, H.265, or AV1. The codec for all the streams in the same adaptive bitrate template must be the same.</td>
</tr><tr>
<td>Video frame rate (fps)</td>
<td>No</td>
<td>Value range: 0-60. If this parameter is left empty, `0` (the original frame rate) will be used.</td>
</tr><tr>
<td>GOP<br>(seconds)</td>
<td>No</td>
<td>The GOP is not specified by default. Value range: 2-6. The higher the GOP, the higher the latency. The GOP for all the streams in the same adaptive bitrate template must be the same.</td>
</tr><tr>
<td>Parameter limit</td>
<td>No</td>
<td>Parameter limits are disabled by default.<br>After a limit is enabled, if you enter a value higher than the original, the original will be used. This can avoid video quality issues caused by using high video quality settings to transcode videos of low quality.</td>
</tr></table>




![](https://qcloudimg.tencent-cloud.cn/raw/9756cb539071adaad4a918ab2e01c551.png)


[](id:related)
## Binding a Domain Name
1. Log in to the CSS console. Select **Feature Configuration > Adaptive Bitrate** on the left sidebar.
2. Bind a domain name in either of two ways:
  - **Bind a domain to an existing template**: Click **Bind Domain Name** in the top left.
    ![](https://qcloudimg.tencent-cloud.cn/raw/7b99a75c0b09c75c4f8a226dc23e9080.png)
  - **Bind a domain after creating a template**: After [creating an adaptive bitrate template](#create), click **Bind Domain Name** in the pop-up window.
    ![](https://qcloudimg.tencent-cloud.cn/raw/9e6816d793fdbeea9adfe939d28cd95c.png)
3. Select an **adaptive bitrate template** and a **playback domain** and then click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/1db512981db33ae4c7c8454005d29e99.png)
>? You can click **Add** to bind a template to multiple playback domains.



[](id:untie)
## Unbinding a Domain Name
1. Log in to the CSS console. Select **Feature Configuration > Adaptive Bitrate** on the left sidebar.
2. Select the target template and click **Unbind**.
![](https://qcloudimg.tencent-cloud.cn/raw/cc40b63592a7ffb550709359f79691d0.png)
3. In the pop-up window, click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/7ce4c285ca40ab72dd62d75e855ea78e.png)



[](id:modify)
## Modifying a Template
1. Log in to the CSS console. Select **Feature Configuration > Adaptive Bitrate** on the left sidebar.
2. Select the target template and click **Edit** on the right to modify it.
3. After modification, click **Save**.

![](https://qcloudimg.tencent-cloud.cn/raw/05ca4a09ac9b73bcaaecdd504c8b4e7e.png)



[](id:delect)
## Deleting a Template
>! If a template has been bound with a domain name, you need to [unbind](#untie) it before deleting the template. 

1. Log in to the CSS console. Select **Feature Configuration > Adaptive Bitrate** on the left sidebar.
2. Select the target template (make sure it’s not bound with a domain), and click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/ed74cfb664fd83e67d567a933e848f2f.png)
3. In the pop-up window, click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/f1b8df196cb97c8787bfd4598dffce5a.png)



