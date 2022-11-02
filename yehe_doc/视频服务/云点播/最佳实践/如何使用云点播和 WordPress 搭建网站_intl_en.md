## Overview

WordPress is a popular open-source blog framework and content management system. It can significantly reduce the difficulty and increase the efficiency of website building. Using WordPress plans, you can get a small website up and running in just a few minutes. However, as you add images, audios, and videos to your WordPress website, it will become more and more demanding on bandwidth and storage, which may start to affect your website’s performance. The management of media files is crucial to the long-term success of a website.

### Why VOD

We do not recommend using WordPress’ default features to upload videos directly to a WordPress website that you intend to run long term. This is mainly because the media files are stored in a web server, which has the following disadvantages:
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:10px">No.</td>
<td>Disadvantages</td>
</tr>
<tr  ><td>1</td>
<td>When users access media files hosted in a web server, videos may stutter and images may be slow to load.</td>
</tr>
<tr  ><td>2</td>
<td>Accessing media files hosted in a web server consumes bandwidth resources and may take up all your bandwidth.</td>
</tr>
<tr  ><td>3</td>
<td>As your website grows, media files may take up all the server’s storage space.</td>
</tr>
<tr  ><td>4</td>
<td>When you migrate to a different server, the transfer of media files can be cumbersome.</td>
</tr>
</tbody>
</table>

VOD offers media storage, transcoding, and distribution/playback acceleration services. Using it to build your website has the following advantages:
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:10px">No.</td>
<td>Advantages</td>
</tr>
<tr  ><td>1</td>
<td>Using our WordPress plugin or SDK, you can upload and store your website’s media files to VOD. This can free up storage space in the server and facilitate easier server migration. It also avoids the problem of deleting files by mistake.</td>
</tr>
<tr  ><td>2</td>
<td>VOD offers CDN addresses for your media files, which makes accessing images, audios, and videos faster and does not consume your server’s bandwidth.</td>
</tr>
</tbody>
</table>


VOD also offers access control, media processing, and content moderation capabilities. For details, see [Feature Overview](https://intl.cloud.tencent.com/document/product/266/49084).

### VOD plugin

VOD offers a [WordPress plugin](https://wordpress.org/plugins/tencentcloud-vod/). Using this plugin, you can bind a [VOD subapplication](https://intl.cloud.tencent.com/document/product/266/33987) to host your WordPress media files in VOD. Visitors of your website can access the files via the CDN addresses provided by VOD. Currently, the plugin can achieve the following:

- You can bind a VOD subapplication to WordPress.
- The video files you upload to WordPress can be automatically saved to the VOD subapplication.
- If you embed a video on a webpage, the video will be played via the address offered by VOD.

## Prerequisites
### 1. Create a VOD subapplication

VOD supplications help you achieve resource isolation. You can bind different websites to different VOD subapplications so that you can manage their media files separately. To learn about how to create a subapplication, see [Subapplication System](https://intl.cloud.tencent.com/document/product/266/33987#.E5.BC.80.E9.80.9A.E5.AD.90.E5.BA.94.E7.94.A8).

### 2. Use WordPress to build a website
You can build a WordPress website in one of the following two ways:
<dx-tabs>
::: Method 1 (recommended)
Use the WordPress image of TencentCloud Lighthouse or Cloud Virtual Machine to build a website.
:::
::: Method 2
[Download](https://cn.wordpress.org/download/) and install the latest version of WordPress. For detailed directions, see [How to install WordPress](https://wordpress.org/support/article/how-to-install-wordpress/).
:::
</dx-tabs>


## Directions

### Step 1. Install the plugin

<dx-tabs>
::: Install online
Type **tencentcloud-vod** in the search box, click **Install**, and then click **Activate**.

![Install online](https://qcloudimg.tencent-cloud.cn/raw/1dea0a047d5df7dc67eedb907dbaf586.png)
:::
::: Download and install
[Download](https://github.com/Tencent-Cloud-Plugins/tencentcloud-wordpress-plugin-vod/releases/latest/download/tencentcloud-wordpress-plugin-vod.zip) a ZIP file of the latest version of the plugin. In WordPress, click **Upload Plugin > Choose File > Install Now**. After the installation, click **Activate**.

![Download and install](https://qcloudimg.tencent-cloud.cn/raw/3e16ee19f1dcf3a5734e67e293e72f2f.png)
:::
</dx-tabs>


### Step 2. Configure the plugin

In WordPress, select **Tencent Cloud Settings > [VOD](https://intl.cloud.tencent.com/document/product/266/33897)** on the left sidebar.


Complete the following settings:

| **Item**           | **Description**                                                     |
| -------------------- | ------------------------------------------------------------ |
| Custom key           | If you toggle this off, the key configured for **Tencent Cloud Settings** will be used, which means the VOD plugin will use the same key as other Tencent Cloud plugins. If you toggle this on, the key configured below will be used. |
| SecretId, SecretKey | The access key. You can go to the [API Keys](https://console.cloud.tencent.com/cam/capi) page of the console to create and view access keys. |
| SubAppID             | The ID of the VOD subapplication you want to bind. You can view your VOD subapplications in [Application Management](https://console.cloud.tencent.com/vod/app-manage). |
| Adaptive bitrate | If you toggle this on, videos uploaded will be encoded at multiple bitrates. For details, see [Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/49258). |

Click **Save**.

### 3. Upload videos and use VOD videos in your webpage
1. After you finish configuring the plugin, the videos in the media library of WordPress as well as the videos you upload while editing a post or webpage will be automatically saved to VOD.
2. For example, when you edit a post in WordPress, click the plus icon, select **Video**, and click **Upload** to upload a video. After the video is uploaded, click **Preview** in the top right corner. You will see that the video is played via VOD’s URL.
![](https://qcloudimg.tencent-cloud.cn/raw/0d5cd195f0d9db5c0e4cb9161601823f.png)
3. As you can see below, the video on the left is stored in a web server, which stutters due to limited bandwidth. This is not a problem if you use VOD, which uses its CDN to accelerate video distribution.
![](https://qcloudimg.tencent-cloud.cn/raw/c336d83417e255868fe58338413a9325.gif)

## Others
### Using HTTPS

VOD uses HTTP by default. If you want to use HTTPS, select your subapplication in the VOD console, go to **System Settings > Distribution and Playback > Default Distribution Domain**, click **Edit**, and select **HTTPS** for **Default Distribution Protocol**.
