TRTC is one of Tencent Cloud’s LiteAV products. Because all LiteAV products use the same underlying modules, integrating more than one LiteAV SDK into your project will cause a duplicate symbol error. Given this, we have provided multiple SDK editions that come with different capabilities, including **LiteAV_Smart (TRTC)**, **Professional**, and **Enterprise**. You can choose the one that fits your needs.



<h2 id="TRTC">LiteAV_TRTC</h2>  
LiteAV_TRTC integrates only TRTC and stream playback (`TXLivePlayer`) features. It adds the least to the installation package and is suitable for customers who need only TRTC features.

<table>
   <tr>
      <th width="0px" style="text-align:center">Platform</td>
      <th width="0px" style="text-align:center">ZIP File</td>
      <th width="0px"  style="text-align:center">GitHub</td>
      <th width="0px" style="text-align:center">Gitee</td>
      <th width="0px" style="text-align:center">How to Run Demo</td>
      <th width="0px" style="text-align:center">Integration Guide</td>
      <th width="0px" style="text-align:center">Increase Installation Package By</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center">3M（arm64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center">jar：546K<br> so（armeabi）：4.5M<br> so（armv7）：4.5M<br>so（arm64）：5.3M</td>
   </tr>
     <tr>
      <td style="text-align:center">Windows(C++)  </td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35085">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_cpp', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35095">DOC</a></td>
      <td style="text-align:center">12.7M（C++ x86）<br>15.6M（C++ x64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Windows(C#) </td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35085">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_csharp', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35095">DOC</a></td>
      <td style="text-align:center">13.8M（C# x64）<br>13.3M（C# x86）</td>
   </tr>
     <tr>
      <td style="text-align:center">Mac</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'zip'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_mac', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35094">DOC</a></td>
      <td style="text-align:center">2.05M（arm64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Web</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'zip'})" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35607">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_web', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35096">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
   <tr>
      <td style="text-align:center">Electron  </td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'zip'})" href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'github'})" href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'gitee'})" href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/35089">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_electron', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35097">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
	    <tr>
      <td style="text-align:center">Flutter</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_flutter', ext1: 'zip'})" href="https://pub.dev/packages/tencent_trtc_cloud/versions">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_flutter', ext1: 'github'})" href="https://github.com/c1avie/trtc_demo">Github</a></td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_flutter', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/39243">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_flutter', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/35098">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
      <tr>
      <td style="text-align:center">React Native</td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_rn', ext1: 'github'})" href="https://github.com/tencentyun/TRTCReactNative">Github</a></td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_rn', ext1: 'doc_demo'})" href="https://intl.cloud.tencent.com/document/product/647/43297">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_rn', ext1: 'doc_sdk'})" href="https://intl.cloud.tencent.com/document/product/647/43298">DOC</a></td>
      <td style="text-align:center">N/A</td>
</tr>
</table>

>? 
>- To reduce the amount that the SDK adds to the size of your installation package, see [How to Downsize Installation Package](https://intl.cloud.tencent.com/document/product/647/35165).
>- Scan the QR code to follow our WeChat Official Account and stay up to date on updates and new features of the SDK.
> ![](https://main.qcloudimg.com/raw/d8a8c8c130ef7799feff6efbc0260ea2.jpg)


<h2 id="Professional">Professional</h2>

The Professional edition integrates multiple key audio/video features of Tencent Cloud, including TRTC, [superplayer](https://intl.cloud.tencent.com/document/product/266/7836), [MLVB](https://intl.cloud.tencent.com/product/mlvb), and [UGSV](https://intl.cloud.tencent.com/product/ugsv). This integrated edition adds less to the installation package than two independent SDKs do because the SDKs share many of their underlying modules. You can also avoid the duplicate symbol issue by using this edition.

<table>
   <tr>
      <th width="0px" style="text-align:center">Platform</td>
      <th width="0px" style="text-align:center">ZIP File</td>
      <th width="0px"  style="text-align:center">GitHub</td>
      <th width="0px" style="text-align:center">64-bit Support</td>      
      <th width="0px" style="text-align:center">How to Run Demo</td>
      <th width="0px" style="text-align:center">Integration Guide</td>
      <th width="0px" style="text-align:center">Increase Installation Package By</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'zip', ext2:'professional'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'github', ext2:'professional'})" href="https://github.com/tencentyun/LiteAVProfessional_iOS">Github</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_demo', ext2:'professional'})" href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_sdk', ext2:'professional'})" href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center">3.2M（arm64）</td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'zip', ext2:'professional'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'github', ext2:'professional'})" href="https://github.com/tencentyun/LiteAVProfessional_Android">Github</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_demo', ext2:'professional'})" href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_sdk', ext2:'professional'})" href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center">jar：1M<br> so（armeabi）：5.7M<br> so（armv7）：5.7M<br>so（arm64）：6.8M</td>
   </tr>
</table>

>? 
>- Only one edition of the SDK, rather than three, is available for Windows and macOS for the time being.
>- Because all LiteAV SDKs use the same underlying modules, the duplicate symbol issue occurs if you integrate two or more LiteAV SDKs into your project. You are advised to integrate the professional edition only to avoid the problem.
>- To reduce the amount that the SDK adds to the size of your installation package, see [How to Downsize Installation Package](https://intl.cloud.tencent.com/document/product/647/35165).


<h2 id="Enterprise">Enterprise</h2>

In addition to the features of the Professional edition, the Enterprise edition integrates an AI beauty filter component. It supports eye enlarging, face slimming, retouching, as well as animated stickers and widgets. AI beauty effects are a value-added service. [Contact us](https://intl.cloud.tencent.com/contact-us) for their billing details. You need a decompression password and license to use the Enterprise edition. [Contact us](https://intl.cloud.tencent.com/contact-us) to obtain them.

<table>
   <tr>
      <th width="0px" style="text-align:center">Platform</td>
      <th width="0px" style="text-align:center">ZIP File</td>
      <th width="0px" style="text-align:center">64-bit Support</td>
      <th width="0px" style="text-align:center">How to Run Demo</td>
      <th width="0px" style="text-align:center">Integration Guide</td>
      <th width="0px" style="text-align:center">Increase Installation Package By</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'zip', ext2:'enterprise'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Enterprise_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_demo', ext2:'enterprise'})" href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_ios', ext1: 'doc_sdk', ext2:'enterprise'})" href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center"> 5.5M（arm64）</td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'zip', ext2:'enterprise'})" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Enterprise_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center">Yes</td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_demo', ext2:'enterprise'})" href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a onclick="aegis.reportEvent({name: 'intl_download_click_android', ext1: 'doc_sdk', ext2:'enterprise'})" href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center"> jar：2.2M<br>so(armeabi)：9.3M</td>
   </tr>
</table>

>?
>- For Windows and macOS, only one edition of the SDK is available, which does not offer the AI-based beauty filter component.
>- To reduce the amount that the SDK adds to your installation package size, see [How to Downsize Installation Package](https://intl.cloud.tencent.com/document/product/647/35165).


## Comparison Among Editions

![](https://main.qcloudimg.com/raw/d3c876e8d751709e1df52faf4c0bf012.jpg)

<table>
  <tr>
    <th width="100px" style="text-align:center">Module</th>
    <th width="100px" style="text-align:center">Feature</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1071/38150">LiteAV_Smart</a></th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1069/37914">LiteAV_UGC</a></th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/34615">LiteAV_TRTC</a></th>
    <th width="100px" style="text-align:center">LiteAV_Player</th>
    <th width="100px" style="text-align:center"><a href="#Professional">Professional</a></th>
    <th width="100px" style="text-align:center"><a href="#Enterprise">Enterprise</a></th>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Stream publishing</td>
    <td style="text-align:center">Camera</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">Screen</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">Stream playback</td>
    <td style="text-align:center">RTMP</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP-FLV</td>
    <td style="text-align:center">&#10003;</td>
     <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS (M3U8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">VOD playback</td>
    <td style="text-align:center">MP4</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS (M3U8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Beauty filter</td>
    <td style="text-align:center">Retouching</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Basic filters</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Co-anchoring/Mic connect</td>
    <td style="text-align:center">Same-room co-anchoring/mic connect</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Cross-room competition</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">Video call</td>
    <td style="text-align:center">One-to-one call</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Video conferencing</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">UGSV</td>
    <td style="text-align:center">Recording/Shooting</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Clipping/Splicing</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">TikTok-like special effects</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Video upload</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">AI-powered special effects</td>
    <td style="text-align:center">Eye enlarging/Face slimming</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Chin slimming/Nose reshaping</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Animated stickers</td>
   <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">Green screen keying</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
</table>



