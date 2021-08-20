移动直播 SDK 提供了3种版本的 SDK，了解3个版本 SDK 的关系和对应的 License 使用可参见 [功能说明](https://intl.cloud.tencent.com/document/product/1071/38149)。


​      
<h2 id="Smart">直播基础版（Smart）</h2>

基础版仅包含直播推流（TXLivePusher）和直播播放（TXLivePlayer）两项功能，对 App 的安装包体积增量最小，适合仅使用移动直播相关功能的客户。 
     
<table>
   <tr>
      <th width="0px" style="text-align:center">所属平台</td>
      <th width="0px" style="text-align:center">ZIP 包</td>
      <th width="0px"  style="text-align:center">Github</td>
      <th width="0px" style="text-align:center">Gitee</td>
      <th width="0px" style="text-align:center">SDK 集成指引</td>
      <th width="0px" style="text-align:center">64位支持</td>
      <th width="0px" style="text-align:center">安装包增量</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_ios_smart") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Smart_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/MLVBSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/MLVBSDK">Gitee</a></td>
      <td style="text-align:center">DOC</td>
      <td style="text-align:center">支持</td>
      <td style="text-align:center">1.27M（arm64）</td>
   </tr>
     <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_android_smart") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Smart_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/MLVBSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/MLVBSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://cloud.tencent.com/document/product/454/7877">DOC</a></td>
      <td style="text-align:center">支持</td>
      <td style="text-align:center">jar：1.5M <br> so(armeabi)：4.4M <br>so(armeabi-v7a)：4.1M <br>so(arm64-v8a)：4.9M</td>
   </tr>
</table>

>? 扫码关注公众号，了解 SDK 的版本更新以及最新的技术动态。
>![](https://main.qcloudimg.com/raw/23242df893a3ecb11779a59ed9a5629c.jpg)


<h2 id="Professional">专业版（Professional）</h2>

专业版集合了包含移动直播在内的多个音视频相关的核心功能，这包括 [实时音视频 SDK](https://intl.cloud.tencent.com/product/trtc)、超级播放器（Player+）和 [短视频（UGSV）](https://intl.cloud.tencent.com/product/ugsv) 等，由于底层模块的高度复用，集成专业版的体积增量要小于同时集成两个独立的 SDK，并且可以避免符号冲突（symbol duplicate）的困恼。

<table>
   <tr>
      <th width="0px" style="text-align:center">所属平台</td>
      <th width="0px" style="text-align:center">ZIP 包</td>
      <th width="0px"  style="text-align:center">Github</td>
      <th width="0px" style="text-align:center">64位支持</td>
      <th width="0px" style="text-align:center">安装包增量</td>
      <th width="0px" style="text-align:center">安装包瘦身</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_ios_professional") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_iOS">Github</a></td>
      <td style="text-align:center">支持</td>
      <td style="text-align:center">4.08M（arm64）</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35165">DOC</a></td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("mlvb_sdk_download_android_professional") href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_Android">Github</a></td>
      <td style="text-align:center">支持</td>
      <td style="text-align:center">jar：1.5M<br> so(armeabi)：6.5M<br> so(armv7)：6.1M<br>so(arm64)：7.3M</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35165">DOC</a></td>
   </tr>
</table>

>? 根据您具体使用的服务，使用专业版需先购买对应产品授权，您可按需选购：

>1. 使用其中的移动直播请购买  [直播推流 License（原移动直播基础版 License）](https://intl.cloud.tencent.com/document/product/1071/38114)。
>1. 使用其中的短视频请购买 短视频精简版/基础版 License。
>1. 使用其中的实时音视频请购买 [实时音视频套餐包](https://intl.cloud.tencent.com/document/product/647/34610)。

## 各版本差异对照表

![](https://main.qcloudimg.com/raw/d3c876e8d751709e1df52faf4c0bf012.jpg)

<table>
  <tr>
    <th width="100px" style="text-align:center">功能模块</th>
    <th width="100px" style="text-align:center">功能项</th>
    <th width="100px" style="text-align:center"><a href="#Smart">直播基础版</a><br>LiteAV_Smart</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1069/37914">短视频版</a><br>LiteAV_UGC</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/34615">TRTC版</a><br>LiteAV_TRTC</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/266/7836">播放器版</a><br>LiteAV_Player</th>
    <th width="100px" style="text-align:center"><a href="#Professional">专业版</a><br>Professional</th>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">直播推流</td>
    <td style="text-align:center">摄像头推流</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
   <tr>
    <td style="text-align:center">录屏推流</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">直播播放</td>
    <td style="text-align:center">RTMP 协议</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP - FLV</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
   <tr>
    <td style="text-align:center">快直播（WebRTC 协议）</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">点播播放</td>
    <td style="text-align:center">MP4 格式</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM 加密</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">基础滤镜</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">直播连麦</td>
    <td style="text-align:center">连麦互动</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">跨房 PK</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">视频通话</td>
    <td style="text-align:center">双人通话</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">视频会议</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">短视频</td>
    <td style="text-align:center">录制和拍摄</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">裁剪拼接</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">“抖音”特效</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  <tr>
    <td style="text-align:center">视频上传</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003</td>
  </tr>
  </tr>
</table>



<script>
  var _mtac = {"senseHash":0};
  (function() {
    var mta = document.createElement("script");
    mta.src = "//pingjs.qq.com/h5/stats.js?v2.0.4";
    mta.setAttribute("name", "MTAH5");
    mta.setAttribute("sid", "500695331");
    mta.setAttribute("cid", "500695332");
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(mta, s);
  })();
</script>
   


