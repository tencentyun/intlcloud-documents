[](id:que1)
### What should I do if the following error occurs when I integrate the SDK?
![](https://main.qcloudimg.com/raw/b631f468aca6a2d1e83b868874631030.png)
You can use the armeabi and armeabi-v7a architectures.
![](https://main.qcloudimg.com/raw/9d75515640b65d91ab8730991e4c2602.png)
As shown above, set `abiFilters` to `armeabi` in `build.gradle` in `app`.

[](id:que2)
### What should I do if a conflict occurs when I try to integrate two or more LiteAV SDKs?
Because all LiteAV SDKs use the same underlying modules, the duplicate symbol error occurs if you integrate two or more LiteAV SDKs into your project.

To avoid the problem, instead of integrating two SDKs, we recommend you use the full-featured SDK.

<table>
   <tr>
      <th width="0px" style="text-align:center">Platform</td>
      <th width="0px" style="text-align:center">ZIP File</td>
      <th width="0px"  style="text-align:center">GitHub</td>
      <th width="0px" style="text-align:center">64-bit Support</td>
      <th width="0px" style="text-align:center">Size</td>
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

[](id:que3)
### Why can I no longer use UGSV features after updating the SDK?
1. If you use Android Studio, after replacing the AAR file, **change the filename** in the AAR reference in `build.gradle` of `app` to that of the AAR file in `/libs` of your project. Then, clean your project and build it again.
2. Check the SDK version. You need a license to use v4.5 and later versions of the SDK.

If you don’t have a license, please apply for one. The UGSV SDK comes in **Lite** edition and **Basic** edition.

[](id:que5)
### How do I implement playback pause and progress bar in my Android project?
In the UGSV SDK, playback is based on the UGSV player. You need to implement the progress bar **by yourself**.

