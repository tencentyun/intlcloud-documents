腾讯云视立方播放器 Player 是为用户连接云端服务、打造云端一体能力的重要组成。播放器 Player 可为点播播放场景提供超级播放器和超级播放器 Adapter 两种类型的播放器，支持 Web 端、iOS 端、Android 端、Flutter 端四大终端。播放器 Player 可帮助点播用户在短时间内打造出流畅的观看体验，提供集多功能于一体的高性能解决方案。
本文为您介绍播放器 Player 不同类型播放器的区别和使用方法，帮助用户选择适合自己的播放器类型。



## 基本概念说明[](id:concept)
### 超级播放器
超级播放器支持 URL 播放、FileID 播放这两种播放方式：
<table>
   <tr>
      <th width="178px" style="text-align:center">播放方式</td>
      <th width="0px" style="text-align:center">说明</td>
   </tr>
   <tr>
      <td style="text-align:center">超级播放器 - URL 播放</td>
      <td>用户通过 URL 进行播放的方式，该播放方式不支持基于 FileID 的数据统计和复杂媒资功能。常用于<b>短视频</b>或<b>短中视频</b>短等无需其他媒资辅助信息的场景。</td>
   </tr>
   <tr>
      <td>超级播放器 - FileID 播放</td>
      <td>用户通过云点播的 FileID 进行视频播放的方式，该播放方式提供点播云端资源和播放器 SDK 深度耦合的能力，用户可以基于 FileID 实现数据上报、监控和复杂媒资绑定功能。常用于<b>长视频</b>等需要其他媒资辅助信息一起播放的场景。</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">
超级播放器功能列表请参考 [超级播放器能力清单](https://intl.cloud.tencent.com/document/product/266/38295)。
</dx-alert>


### 超级播放器 Adapter
超级播放器 Adapter 为云点播提供给客户希望使用第三方播放器或自研播放器开放的对接云 PAAS 资源的播放器插件，常用于有**强烈自定义播放器功能**需求的用户，有一定的技术接入门槛，基本功能与超级播放器保持一致。


### 播放器类别对比
<table>
    <tr>
        <th width="120px">播放器类别</td> 
        <th width="250px">功能</td> 
        <th>特点</td>
        <th>自定义程度</td> 
   </tr>
   <tr>
        <td rowspan="2">超级播放器</td>    
        <td >支持播放 URL</td>
        <td > 支持播放点播 URL 和第三方来源的 URL </td> 
        <td > 低 </td> 
   </tr>
   <tr>
        <td> 支持播放点播 FileID </td> 
        <td> 提供点播一体化数据上报、质量监控服务 </td> 
        <td > 低 </td> 
   </tr>
     <tr>
        <td >超级播放器 Adapter</td> 
        <td> 仅支持播放点播 FileID </td> 
        <td> 支持用户使用第三方或者自研播放器集成 </td> 
        <td> 高 </td>
   </tr>

</table>



## 核心优势[](id:core)
<table>
   <tr>
      <th width="120px" style="text-align:center">介绍</td>
      <th width="0px" style="text-align:center">说明</td>
   </tr>
   <tr>
      <td style="text-align:center">云端一体</td>
      <td>用户可以轻松使用云点播 PAAS 资源，构建云端一体能力。</td>
   </tr>
   <tr>
      <td style="text-align:center">视频安全</td>
      <td>提供防盗链、URL 鉴权、HLS 加密、私有协议加密、本地加密等多种加密方案，全方位保证用户媒体安全，满足不同场景安全需求。</td>
   </tr>
   <tr>
      <td style="text-align:center">视频播放</td>
      <td>提供首屏秒开、边播边缓存、倍速播放、视频打点、媒体弹幕和外挂字幕等多种功能。</td>
   </tr>
   <tr>
      <td style="text-align:center">视频加速</td>
      <td>依靠腾讯云海量加速节点，提供完备的视频加速能力，毫秒级的延迟让用户无延迟体验极速视频播放。</td>
   </tr>
</table>

## 特色功能[](id:function)
通过集成腾讯云视立方播放器 Player，我们支持多种功能一键集成，更多功能查看 [功能列表](https://intl.cloud.tencent.com/document/product/266/38295)。
<table>
   <tr>
      <th width="120px" style="text-align:center">功能</td>
      <th width="0px" style="text-align:center">功能描述</td>
      <th width="120px"  style="text-align:center">其他说明</td>
   </tr>
   <tr>
      <td style="text-align:center">视频加密</td>
      <td>支持标准 HlS 加密和腾讯云私有协议加密</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38131">视频加密综述</a></td>
   </tr>
   <tr>
      <td style="text-align:center">视频播放</td>
      <td>支持在不同场景下结合点播下媒体和相关媒资辅助信息，并通过 FileID 输出，完成多样化视频播放能力</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38295">视频播放综述</a></td>
   </tr>
   <tr>
      <td style="text-align:center">安全下载</td>
      <td>支持将下载的视频在本地进行二次加密，确保用户的媒体仅通过唯一的应用播放</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/38295">视频播放综述</a></td>
   </tr>
</table>

## 相关链接[](id:link)
腾讯云视立方播放器 Player 支持 Web 端、iOS 端、Android 端、Flutter 端四大终端, 其中 Flutter 仅支持超级播放器使用，详情请参见表格中的文档。


<table>
   <tr>
      <th width="120px" style="text-align:center">终端类别</td>
      <th width="70px" style="text-align:center">播放器类型</td>
      <th width="0px"  style="text-align:center">SDK & Demo 下载地址</td>
      <th width="0px" style="text-align:center">Demo 展示</td>
      <th width="0px"  style="text-align:center">	使用文档</td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>Web 端</td>
      <td>超级播放器</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33977#transcoding-service-on-vod-platform">SDK</a></td>
      <td><a href="https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html">Demo</a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33977">Web - 超级播放器</a></td>
   </tr>
   <tr>
      <td>超级播放器 Adapter</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42095">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42095">Web - 超级播放器 Adapter</a></td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>iOS 端</td>
      <td>超级播放器</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer_iOS">SDK + Demo</a></td>
      <td><a><button style="width:120px;height: 120px;border:none;background-image:url(https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png);background-size: cover;">
</button></a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33976">iOS - 超级播放器</a></td>
   </tr>
   <tr>
      <td>超级播放器 Adapter</td>
      <td><a href="https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_iOS.zip">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42096">iOS - 超级播放器 Adapter</a></td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>Android 端</td>
      <td>超级播放器</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer_Android">SDK + Demo</a></td>
      <td><a><button style="width:120px;height: 120px;border:none;background-image:url(https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png);background-size: cover;">
</button></a></td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/33975">Android - 超级播放器</a></td>
   </tr>
   <tr>
      <td>超级播放器 Adapter</td>
      <td><a href="https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_Android.zip">SDK</a></td>
      <td>-</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/266/42097">Android- 超级播放器 Adapter</a></td>
   </tr>
   <tr>
      <td  style="text-align:center">Flutter 端</td>
      <td>超级播放器</td>
      <td><a href="https://github.com/tencentyun/SuperPlayer/tree/main/Flutter">SDK + Demo</a></td>
	     <td><a href="https://github.com/tencentyun/SuperPlayer/tree/main/Flutter">Demo</a></td>
	     <td><a href="https://intl.cloud.tencent.com/document/product/266/42099">Flutter - 超级播放器</a></td>
   </tr>
</table>




## 接入指引
为了帮助您快速接入超级播放器，我们为您提供了超级播放器 [接入指引](https://intl.cloud.tencent.com/document/product/266/38098)，以示例的方式为您讲解接入步骤。
- 如遇到播放问题，请参见 [常见问题文档](https://intl.cloud.tencent.com/document/product/266/1303)。
- 如遇到专业词汇，请参见 [词汇表](https://intl.cloud.tencent.com/document/product/266/11732)。
  
