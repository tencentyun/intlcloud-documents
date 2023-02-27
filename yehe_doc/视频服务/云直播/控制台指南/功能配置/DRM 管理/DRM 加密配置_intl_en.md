CSS offers DRM encryption capabilities based on Widevine, FariPlay, and NormalAES to help you protect your content and prevent piracy and hotlinking. This document shows you how to configure DRM encryption in the CSS console.

## Must-Knows
Tencent Cloud only encrypts your content. DRM licenses are offered by third party licensing services SDMC and DRMtoday, which charge a licensing fee. To learn more details, please contact the companies.

## Prerequisites
- You have activated CSS and added a [playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created an account at [SDMC DRM](https://console.multidrm.tv/setting/drm/index) or [DRMtoday](https://castlabs.com/free-trials/drmtoday/) and configured an access key.

## Console Settings
[](id:step1)

### Configuring DRM key information
1. Log in to the CSS console and select **Feature Configuration** > [DRM management](https://console.cloud.tencent.com/live/config/drm) on the left sidebar.
2. Click **Edit**, select a licensing provider (SDMC or DRMtoday), and fill in the key information.
- If your licensing service provider is **SDMC**:
   - Enter your SDMC UID, secret ID, and secret key (you need to obtain the information from SDMC).
![](https://qcloudimg.tencent-cloud.cn/raw/09a9b34d85b87b89c43e5c5831530ee9.png)
- If your licensing service provider is **DRMtoday**:
   - Enter your DRMtoday merchant name, merchant UUID, merchant API name, merchant API password, key seed ID, and IV seed ID (you need to obtain the information from DRMtoday).
![](https://qcloudimg.tencent-cloud.cn/raw/292500dccf57d708dca961985020cbc6.png)

[](id:step2)
### Creating a transcoding template and binding a domain
1. Select **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode) on the left sidebar.
2. Click **Create Transcoding Template** and toggle **DRM encryption** on.
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
<td>Widevine, FairPlay, or NomalAES. For FairPlay encryption, you need to upload the certificate you obtain from Apple to your player. For details, see <a href="https://www.tencentcloud.com/document/product/267/48069">Obtaining a FairPlay certificate</a>.</td>
</tr>
<td>Track (resolution)</td>
<td>Yes</td>
<td>SD, HD, UHD1, or UHD2.</a></td>
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
- On iOS, you need to apply for a certificate and upload it to the [SDMC console](https://console.multidrm.tv/licenses/drm/index).

>? You need to create an account first before you can visit the SDMC console. For detailed directions on how to create an SDMC account, see [Obtaining the UID and Key Information](https://www.tencentcloud.com/document/product/267/48070). If you encounter any problems, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). We will help you navigate the process.
