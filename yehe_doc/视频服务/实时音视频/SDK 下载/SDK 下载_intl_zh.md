<link rel="stylesheet"
   href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/portal/css/global-20209142343.css?max_age=31536000&amp;t=20191128" />
<link rel="stylesheet"
   href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/portal/css/global-components.css?max_age=31536000&amp;t=20180817" />
<link rel="stylesheet"
   href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/documentation/documentation-v4/css/pandect-20219091610.css" />
<link rel="stylesheet"
   href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/documentation/documentation-v4/css/import-2-markdown-20219091610.css" />
<link rel="stylesheet"
   href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/platform/documents/css/documents-202205161915.css" />
<link rel="stylesheet"
   href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/documentation/documentation-v4/css/pandect-202012171130.css" />
<link rel="stylesheet" href="//qcloudimg.tencent-cloud.cn/static/document/qcloud-document-sdk.v0.0.17.css" />
<link rel="stylesheet"
   href="//cloudcache.tencentcs.com/qcloud/main/components/document-feedback/document-feedback.944df9c907.css" />

<style>
   * {
      font-family: 'pingfang SC', 'helvetica neue', arial, 'hiragino sans gb', 'microsoft yahei ui', 'microsoft yahei', simsun, sans-serif;
   }

   .card-box {
      background: #F2F6F9;
      border-radius: 10px;
      padding: 20px 30px;
      height: 264px;
      box-sizing: border-box;
      white-space: nowrap;
      border: 0;
      height: 100%;
   }

   .card-box .left-section {
      display: inline-block;
      height: 193px;
   }

   .card-box .left-section img {
      background-color: #F2F6F9;
      box-shadow: none;
      max-width: 100%;
      max-height: 100%;
      display: block;
      margin: auto;
   }

   .card-box .right-content {
      display: inline-block;
      vertical-align: top;
      margin-left: 25px;
      width: 63%;
   }

   .rno-markdown ul>li {
      position: relative;
      margin-bottom: 0px;
      padding-left: 18px;
      list-style: none;
   }

   .card-box .section-content {
      display: block;
   }

   .card-box .doc-section .section-content {
      width: 100%;
      overflow: hidden;
   }

   .card-box .right-content img {
      background-color: #F2F6F9;
      box-shadow: none;
   }

   .card-box .section-header {
      font-weight: 500;
      font-size: 14px;
      line-height: 26px;
   }

   .card-box .section-header img {
      display: inline-block;
      vertical-align: middle;
   }

   .card-box .header-text {
      display: inline-block;
      vertical-align: middle;
      margin-left: 9px;
      color: #3D3D3D;
   }

   .card-box .doc-section {
      margin-top: 18px;
      width: 100%;
   }

   .card-box .doc-section .doc-link:nth-child(3n+1) {
      margin-left: 0;
   }

   .card-box .doc-section .doc-link {
      float: left;
      background: #FFFFFF;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.02);
      border-radius: 24px;
      padding: 5px 10px;
      text-align: center;
      margin-left: 8px;
      margin-top: 10px;
      width: 148px;
   }

   .card-box .doc-section .doc-title {
      margin-bottom: 0px;
      margin-right: 7px;
      display: inline-block;
   }

   .card-box .doc-section .doc-icon {
      display: inline-block;
   }

   .card-box .doc-section .doc-icon img {
      width: 5px;
   }

   .card-container {
      width: 50%;
      display: block;
      float: left;
      /* padding-left: 15px; */
      padding-right: 15px;
      box-sizing: border-box;
   }

   .card {
      border-radius: 4px;
      padding: 17px 16px;
      margin-top: 30px;
      border: 1px solid #ebeef5;
      background-color: #fff;
      overflow: hidden;
      box-shadow: 0px 1px 8px rgb(156 175 204 / 25%);
      text-align: center;
      height: 93px;
   }

   .card-header {
      text-align: left;
      height: 20px;
   }

   .card-header .titlename {
      display: inline-block;
      margin-bottom: 0px;
      font-size: 14px;
      vertical-align: top;
      color: #191919;
      font-weight: 600;
      padding-left: 9px;
      line-height: 20px;
   }

   .card-header .icon {
      width: 20px;
      height: 20px;
      float: left;
      box-shadow: none;
   }

   .card-content {
      text-align: left;
      margin-top: 16px;
   }

   .card-content a {
      font-weight: 500;
      font-size: 12px;
      line-height: 18px;
   }

   .card-content a.with-box {
      border: 1px solid #2DA9F9;
      border-radius: 20px;
      padding: 2px 15px;
   }

   .card-box img {
      box-shadow: none;
   }

   .rno-tabs-operation-wrap {
      border: none;
   }

   .rno-tabs-operation-item {
      padding-bottom: 20px;
   }

   .rno-tabs-operation-item>a {
      padding-bottom: 20px;
   }

   .markdown-text-box h4 {
      margin: 0 0 20px 20px
   }

   @media (max-width: 768px){

      .card-container,
      .scene-card-container {
         width: 100%;
      }
    
      .scene-card>div {
         width: 100% !important;
         margin-left: 0 !important;
      }
    
      img {
         box-shadow: none;
      }
   }

</style>

<dx-tabs>
   ::: 音视频通话SDK
   <div class="card-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/2dab7b72bfab9b3d38f471b89294e7c6.svg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  应用场景
               </div>
            </div>
            <div class="section-content">
               语音通话、视频通话、互动课堂、直播连麦、远程协作办公、多人音视频通话、<br/>音视频会议、娱乐语聊、远程医疗等场景。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  更多文档
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/36066">音视频通话</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/47636">多人视频会议</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/37286">语音互动直播</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/36061">视频互动直播</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/41940">在线Karaoke</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6c27890223ea3351fe9caff6276e9145.svg"
                  data-nonescope="true" />
               <p class="titlename">Web SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Web">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35096">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35607">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35093">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35084">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35092">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35086">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/88fd6260e225ba6faa33d140946d7afe.svg"
                  data-nonescope="true" />
               <p class="titlename">Windows SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/46745">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/46748">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/64fac45b91100ae4e506c61b604fe515.svg"
                  data-nonescope="true" />
               <p class="titlename">MacOS SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Mac">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35094">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35086">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/50efefd0ebb90dd9d7c858b78b9be0c7.svg"
                  data-nonescope="true" />
               <p class="titlename">Electron SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">ZIP
                  下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Electron">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35097">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35089">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://pub.dev/packages/tencent_trtc_cloud/versions">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/c1avie/trtc_demo">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35098">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/39243">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/d630b605c8979b5587aa2a74de36b567.svg"
                  data-nonescope="true" />
               <p class="titlename">React Native SDK下载</p>
            </div>
            <div class="card-content">
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/tencentyun/TRTCReactNative">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/43298">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/43297">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/9d3dec1fb7625eb8589d6742c986a328.svg"
                  data-nonescope="true" />
               <p class="titlename">Unity SDK下载</p>
            </div>
            <div class="card-content">
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Unity">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/TRTC_Unity/blob/main/SDK/README-zh_CN.md">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/TRTC_Unity/blob/main/TRTC-Simple-Demo/README-zh_CN.md">运行
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>
   :::
   ::: 直播SDK
   <div class="card-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/84d2e781bab936bf2ba076ab353df34c.svg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  应用场景
               </div>
            </div>
            <div class="section-content">
               娱乐直播、电商直播、活动直播、游戏直播等场景。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  更多文档
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/1071/38156">集成指引</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Live_Android_latest.zip">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/1071/38156">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/1071/38147">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Live_iOS_latest.zip">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/1071/38155">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/1071/38147">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://pub.dev/packages/live_flutter_plugin/versions">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Flutter">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/71666">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/Live_Flutter/tree/main/Live-API-Example">运行
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>
   :::
   ::: 播放器SDK
   <div class="card-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/3d25e8feea02c32299d8616ce3056941.png" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  应用场景
               </div>
            </div>
            <div class="section-content">
               直播、长视频以及短视频在线视频观看场景。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  更多文档
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/266/33975">播放器组件</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/266/38294">加密视频播放</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Android_latest.zip">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/47849">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/42091">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_iOS_latest.zip">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/47840">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/42091">运行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDK下载</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://github.com/LiteAVSDK/Player_Flutter">ZIP 下载</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_Flutter">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/42099">集成指引</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/42091">运行
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>
   :::
   ::: 聊天SDK
   <div class="card-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/01db05070c5acefd30585e88a3479585.svg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  应用场景
               </div>
            </div>
            <div class="section-content">
               应用内聊天（In-App-Chat）、直播弹幕、用户资料与好友关系链等场景。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  更多文档
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/products/im?lang=en&amp;pg=">即时通讯IM</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
<div> 
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden"> 
       <div class="card-container">
         <div class="card">
           <div class="card-header">
             <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6c27890223ea3351fe9caff6276e9145.svg" data-nonescope="true" />
             <p class="titlename">Web SDK下载</p>
           </div>
           <div class="card-content">
             <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Web/IMSDK">GitHub</a>
             <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34309">集成指引</a>
             <a target="_blank" style="margin-left:10px" href="https://web.sdk.qcloud.com/im/demo/en/index.html#/home">运行
               Demo</a>
           </div>
         </div>
       </div>
       <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
            <p class="titlename">Android SDK下载</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Android/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34306">集成指引</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
            <p class="titlename">iOS SDK下载</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/iOS/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34307">集成指引</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/88fd6260e225ba6faa33d140946d7afe.svg" data-nonescope="true" />
            <p class="titlename">Windows SDK下载</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Windows">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34310">集成指引</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/64fac45b91100ae4e506c61b604fe515.svg" data-nonescope="true" />
            <p class="titlename">MacOS SDK下载</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/iOS/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34307">集成指引</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/50efefd0ebb90dd9d7c858b78b9be0c7.svg" data-nonescope="true" />
            <p class="titlename">Electron SDK下载</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Electron">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/43090">集成指引</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg" data-nonescope="true" />
            <p class="titlename">Flutter SDK下载</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Flutter">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46264">集成指引</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2514ea85f97244b9666138c76e5c6407.svg" data-nonescope="true" />
            <p class="titlename">Unreal Engine SDK下载</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/IMUnrealEngine">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46262">集成指引</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/9d3dec1fb7625eb8589d6742c986a328.svg" data-nonescope="true" />
            <p class="titlename">Unity SDK下载</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Flutter">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46263">集成指引</a>
          </div>
        </div>
      </div>
   </div>
</div>
   :::
   ::: 全功能SDK
   <div class="card-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/b35558b665ede349ded27711bb993237.jpeg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  应用场景
               </div>
            </div>
            <div class="section-content">
               覆盖音视频通话SDK，直播SDK，播放器SDK所有功能场景。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  更多文档
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/36066">音视频通话</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/47636">多人视频会议</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/37286">语音互动直播</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/36061">视频互动直播</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/41940">在线Karaoke</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/1071/38156">直播SDK集成指引</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/266/33975">播放器组件</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/b6904dc080d04538982887209022333b.svg" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
<div> 
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden"> 
       <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
            <p class="titlename">Android SDK下载</p>
          </div>
          <div class="card-content">
            <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">ZIP 下载</a>
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/647/35093">集成指引</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/647/35084">运行
              Demo</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
            <p class="titlename">iOS SDK下载</p>
          </div>
          <div class="card-content">
            <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">ZIP 下载</a>
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/647/35092">集成指引</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/647/35086">运行
              Demo</a>
          </div>
        </div>
      </div>
   </div>
</div>
   :::
</dx-tabs>

#### 功能列表

<style type="text/css">
   .tg  {border-collapse:collapse;border-spacing:0;}
   .tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
     overflow:hidden;padding:10px 5px;word-break:normal;}
   .tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
     font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
   .tg .tg-cly1{text-align:left;vertical-align:middle;}
   .tg .tg-ncfo{color:#272727;text-align:left;vertical-align:middle;}
   .tg .tg-nrix{text-align:center;vertical-align:middle;}
   .tg .select{color:#00a4ff;}
   .markdown-text-box table {
      width: 98%;
      border: 1px solid #d9d9d9;
      border-bottom: none;
      line-height: 1.5;
      margin: 0 auto 24px;
   }
   </style>
   <table class="tg">
   <thead>
     <tr>
       <th class="tg-ncfo">功能模块</th>
       <th class="tg-ncfo">功能详情</th>
       <th class="tg-ncfo">音视频通话 SDK</th>
       <th class="tg-ncfo">互动直播 SDK</th>
       <th class="tg-ncfo">播放器 SDK</th>
       <th class="tg-ncfo">聊天 SDK</th>
       <th class="tg-ncfo">全功能</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td class="tg-cly1">界面</td>
       <td class="tg-cly1">自定义UI</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="5">音视频通话</td>
       <td class="tg-cly1">双人通话</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">房间管理</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">屏幕分享</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">多人会议</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">跨房/同房连麦</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="19">采集拍摄</td>
       <td class="tg-cly1">屏比（高宽比）</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">横竖屏切换</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">清晰度（分辨率）</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">拍摄控制</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">水印</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">焦距</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">视频截图</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">背景音乐</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">变声/混响</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">音量调整</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">静音采集</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">录制</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">滤镜</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">美颜</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">高音质采集</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">3A处理</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">自定义音视频采集</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">自定义音视频渲染</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">SEI信息</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="2">编码传输</td>
       <td class="tg-cly1">H.264</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Qos流控策略</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="6">直播推流</td>
       <td class="tg-cly1">摄像头推流</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">录屏推流</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">纯音频推流</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">RTMP OVER QUIC</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">WebRTC</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">TRTC</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="4">直播播放</td>
       <td class="tg-cly1">支持RTMP、FLV、HLS、DASH等协议</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">WebRTC</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">直播时移</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">消息接收</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="11">公共播放</td>
       <td class="tg-cly1">音量调节</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">清晰度切换</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">横竖/全屏切换</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">视频截图</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">小窗播放</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">弹幕</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">亮度调节</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">锁定屏幕</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">播放器尺寸设置</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">镜像播放</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">视频自动旋转</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="30">播放器_点播播放</td>
       <td class="tg-cly1">支持HLS、DASH、MP4、MP3 等协议</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">支持HTTPS</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">多手势操作</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">进度条操作</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">进度条打点</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">进度条缩略图</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">屏幕填充适应</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">自定义启播时间</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">设置封面</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">互动浮窗</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">首屏秒开+预加载</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">快速seek</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">无缝循环播放</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">自适应码率</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">倍速/变速播放</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">边播边下</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">字幕配置</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">UI切换</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">视频缓存/本地缓存</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">播放列表</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">离线下载</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">视频试看</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">防盗链</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">播放加密视频</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">续播功能</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">暂停贴片+跳转链接</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">连续/自动播放</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">FileID播放</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Loading动画</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">数据上报</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="6">社交聊天</td>
       <td class="tg-cly1">单聊</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">群聊</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">消息推送</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">会话管理</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">用户资料与关系链管理</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">群组管理</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1 select">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
   </tbody>
   </table>


