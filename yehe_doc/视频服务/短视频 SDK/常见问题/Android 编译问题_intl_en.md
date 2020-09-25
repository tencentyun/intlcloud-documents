
 
### How do I fix an integration exception?

![](https://main.qcloudimg.com/raw/b631f468aca6a2d1e83b868874631030.png)
If you use the Enterprise Edition, you can only use the armeabi architecture and must disable other architectures such as armeabi-v7a. If you use another edition, you can use both the armeabi and armeabi-v7a architectures.
![](https://main.qcloudimg.com/raw/9d75515640b65d91ab8730991e4c2602.png)
As shown above, please set `abiFilters` to `armeabi` in `build.gradle` in `app`.

### What should I do if I integrated two or more SDKs of the LiteAV system and conflicts occurred?
If two or more SDKs of the LiteAV system are integrated into your project, symbol conflicts (symbol duplicates) will occur because those SDKs use the same basic modules.

To avoid symbol duplicates, please do not integrate two or more SDKs at the same time. You only need to integrate the Enterprise Edition SDK that has the complete set of features.

<table>
   <tr>
      <th width="0px" style="text-align:center">Platform</td>
      <th width="0px" style="text-align:center">ZIP File</td>
      <th width="0px"  style="text-align:center">GitHub</td>
      <th width="0px" style="text-align:center">64-bit Support</td>
      <th width="0px" style="text-align:center">Installation Package Size Increment</td>
      <th width="0px" style="text-align:center">Installation Package Downsizing</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_ios_professional") href="http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_Professional_iOS_latest.zip">Download</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center">4.08 MB (arm64)</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35165">Document</a></td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_android_professional") href="http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_Professional_Android_latest.zip">Download</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center">.jar file: 1.5 MB <br>.so file (armeabi): 6.5 MB <br>.so file (armv7): 6.1 MB <br>.so file (arm64): 7.3 MB</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35165">Document</a></td>
   </tr>
</table>


### Why can’t the UGSV features be used after the SDK is upgraded?

1. If Android Studio is used, after the new .aar file replaces the legacy one, please modify the .aar reference in `build.gradle` in `app` and check whether it has **the same filename** as the .aar file in the `/libs` directory of the project. Then, clean and build your project again.
2. Check the SDK version. UGSV SDK 4.5 or later requires a license.

Please apply for a license first. The SDK has two editions and two types of authorization licenses.

- The SDK can be classified into the Basic Edition and the Enterprise Edition, whose differences lie in whether the AI-based special effects are provided.
- The license can be classified into the Basic Edition and the Enterprise Edition. For the Basic Edition SDK, you need to apply for the basic feature license. For the Enterprise Edition SDK, in addition to the basic feature license, you also need to apply for the license for the AI-based special effects. You can apply for trial licenses for both SDK editions.
