The MLVB SDK comes in three editions. To learn about their differences and the licenses required to use them, please see [Feature Description](https://intl.cloud.tencent.com/document/product/1071/38149).


​      
<h2 id="Smart">LiteAV_Smart</h2>

LiteAV_Smart integrates only the stream publishing (`TXLivePusher`) and playback (`TXLivePlayer`) features. It adds the least to the installation package and is suitable for customers who need only MLVB features. 
     
<table>
   <tr>
      <th width="0px" style="text-align:center">Platform</td>
      <th width="0px" style="text-align:center">ZIP File</td>
      <th width="0px"  style="text-align:center">GitHub</td>
      <th width="0px" style="text-align:center">Gitee</td>
      <th width="0px" style="text-align:center">Integration Guide</td>
      <th width="0px" style="text-align:center">64-bit Support</td>
      <th width="0px" style="text-align:center">Increase Installation Package By</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_ios_smart") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Smart_iOS_latest.zip">Download</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/MLVBSDK">GitHub</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/MLVBSDK">Gitee</a></td>
      <td style="text-align:center">Document</td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center">1.27 MB (arm64)</td>
   </tr>
     <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_android_smart") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Smart_Android_latest.zip">Download</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/MLVBSDK">GitHub</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/MLVBSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1071/38156">Document</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center">jar: 1.5 MB <br> so (armeabi): 4.4 MB <br>so (armeabi-v7a): 4.1 MB <br>so (arm64-v8a): 4.9 MB</td>
   </tr>
</table>

>? Scan the QR code to follow our WeChat Official Account and stay up to date on updates and new features of the SDK.
>![](https://main.qcloudimg.com/raw/23242df893a3ecb11779a59ed9a5629c.jpg)


<h2 id="Professional">Professional</h2>

MLVB Professional Edition integrates multiple key video/audio features of Tencent Cloud, including MLVB, [TRTC](https://intl.cloud.tencent.com/product/trtc), Superplayer (Player+), and [UGSV](https://intl.cloud.tencent.com/product/ugsv). This integrated edition adds less to the size of the installation package than two independent SDKs do because many underlying modules are shared among the SDKs. It is also free of the duplicate symbol issue.

<table>
   <tr>
      <th width="0px" style="text-align:center">Platform</td>
      <th width="0px" style="text-align:center">ZIP File</td>
      <th width="0px"  style="text-align:center">GitHub</td>
      <th width="0px" style="text-align:center">64-bit Support</td>
      <th width="0px" style="text-align:center">Increase Installation Package By</td>
      <th width="0px" style="text-align:center">Downsizing Installation Package</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_ios_professional") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">Download</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center">4.08 MB (arm64)</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35165">Document</a></td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_android_professional") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">Download</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center">jar: 1.5 MB<br> so (armeabi): 6.5 MB<br> so (armv7): 6.1 MB<br>so (arm64): 7.3 MB</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35165">Document</a></td>
   </tr>
</table>

>? You need different authorization to use different features of MLVB Professional Edition:

>1. To use MLVB features, you must purchase a [live publishing license (previously LiteAV_Smart license)](https://intl.cloud.tencent.com/document/product/1071/38114).
>2. To use UGSV features, you must purchase a UGC_Smart/UGC license.
>3. To use TRTC features, you must purchase a [TRTC package](https://intl.cloud.tencent.com/document/product/647/34610).

## Comparison Among Editions

![](https://main.qcloudimg.com/raw/d3c876e8d751709e1df52faf4c0bf012.jpg)

<table>
  <tr>
    <th width="100px" style="text-align:center">Module</th>
    <th width="100px" style="text-align:center">Feature</th>
    <th width="100px" style="text-align:center"><a href="#Smart">LiteAV_Smart</a></th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1069/37914">LiteAV_UGC</a></th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/34615">LiteAV_TRTC</a></th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/266/7836">LiteAV_Player</a></th>
    <th width="100px" style="text-align:center"><a href="#Professional">Professional</a></th>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Stream publishing</td>
    <td style="text-align:center">Camera</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
   <tr>
    <td style="text-align:center">Screen</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">Stream playback</td>
    <td style="text-align:center">RTMP</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP-FLV</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS (M3U8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
   <tr>
    <td style="text-align:center">LEB (WebRTC)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">VOD playback</td>
    <td style="text-align:center">MP4</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS (M3U8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">Basic filters</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Co-anchoring/Mic connect</td>
    <td style="text-align:center">Same-room co-anchoring/mic connect</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">Cross-room competition</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Video call</td>
    <td style="text-align:center">One-to-one call</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">Video conferencing</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">UGSV</td>
    <td style="text-align:center">Recording/Shooting</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">Clipping/Splicing</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">TikTok-like special effects</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">Video upload</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  </tr>
</table>


