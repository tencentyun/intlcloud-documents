CSS offers DRM encryption capabilities based on Widevine, FariPlay, and NormalAES, as well as hotlink protection to help you protect your content and prevent piracy. This document shows you how to configure DRM encryption in the CSS console.

## Notes
Tencent Cloud only encrypts videos. DRM licenses are offered by the third party licensing service SDMC, which charges a licensing fee. To learn more details, please contact the company.

## Prerequisites
- You have activated CSS and added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created an account with [SDMC](https://www.xmediacloud.com/contact-us/) and configured a DRM key.

## Console Settings
[](id:step1)

### Configuring DRM key information
1. Log in to the CSS console and select **Feature Configuration** > [DRM management](https://console.cloud.tencent.com/live/config/drm) on the left sidebar.
2. Click **Edit** and enter the UID, SecretID, and SecretKey (the information is provided by SDMC).
![](https://qcloudimg.tencent-cloud.cn/raw/4a88319f757d161c4b86cbeef27cbf84.png)

[](id:step2)
### Creating a transcoding template and binding a domain
1. Select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode) on the left sidebar.
2. Click **Create Transcoding Template** and enable DRM encryption for the template.
![](https://qcloudimg.tencent-cloud.cn/raw/048b9d46b1b5305605b2cd41a0a85b75.png)

<table>
<thead><tr><th width=18%>Configuration Item</th><th>Required</th><th>Description</th></tr></thead>
<tbody><tr>
<td>DRM encryption</td>
<td>No</td>
<td>Whether to enable DRM encryption. It’s disabled by default. Before enabling this feature, you need to configure DRM key information in “DRM management”.</td>
</tr><tr>
<td>Type</td>
<td>Yes</td>
<td>Widevine, Fairplay, or NomalAES. For FairPlay encryption, you need to upload the certificate you obtain from Apple to your player. For details, see <a href="https://intl.cloud.tencent.com/document/product/267/48069">Obtaining a FairPlay certificate</a>.</td>
</tr>
</tbody></table>

3. Click **Bind Domain Name** to bind the template to your playback domain.
![](https://qcloudimg.tencent-cloud.cn/raw/96151a6cb6428abceca9e85a66728f99.png)

[](id:step3)
### Obtaining the DRM-encrypted playback URL
Only HLS playback supports DRM encryption. Use the [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) to generate playback URLs (select the template you created). The HLS URL generated is DRM-encrypted.

![](https://qcloudimg.tencent-cloud.cn/raw/823cbe64c7fb7fdcbd88f5b3742eacf5.png) 

[](id:step4)
### Configuring your player
For the DRM encryption feature to work, your player must meet the following requirements:
- It must have been equipped by [SDMC](https://www.xmediacloud.com/contact-us/) with the ability to obtain and decrypt license information from video data.
- Use FairPlay encryption for iOS players and Widevine or NormalAES for Android players.
- For iOS players, you need to obtain a certificate from Apple and upload it to [SDMC](https://www.xmediacloud.com/contact-us/)’s platform.
