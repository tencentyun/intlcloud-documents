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

   .markdown-text-box {
      background: #F2F6F9;
      border-radius: 10px;
      padding: 20px 30px;
      height: 358px;
      box-sizing: border-box;
      white-space: nowrap;
   }

   .markdown-text-box .left-section {
      display: inline-block;
      height: 193px;
   }

   .markdown-text-box .left-section img {
      background-color: #F2F6F9;
      box-shadow: none;
      max-width: 100%;
      max-height: 100%;
      display: block;
      margin: auto;
   }

   .markdown-text-box .right-content {
      display: inline-block;
      vertical-align: top;
      margin-left: 25px;
   }

   .markdown-text-box .section-content {
      display: block;
   }

   .markdown-text-box .doc-section .section-content {
      width: 470px;
      overflow: hidden;
   }

   .markdown-text-box .right-content img {
      background-color: #F2F6F9;
      box-shadow: none;
   }

   .markdown-text-box .section-header {
      font-weight: 500;
      font-size: 14px;
      line-height: 26px;
   }

   .markdown-text-box .section-header img {
      display: inline-block;
      vertical-align: middle;
   }

   .markdown-text-box .header-text {
      display: inline-block;
      vertical-align: middle;
      margin-left: 9px;
   }

   .markdown-text-box .doc-section {
      margin-top: 18px;
   }

   .markdown-text-box .doc-section .doc-link:nth-child(2n+1) {
      margin-left: 0;
   }

   .markdown-text-box .doc-section .doc-link {
      float: left;
      background: #FFFFFF;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.02);
      border-radius: 24px;
      padding: 5px 15px;
      text-align: center;
      margin-left: 10px;
      margin-top: 10px;
   }

   .markdown-text-box .doc-section .doc-title {
      margin-bottom: 0px;
      margin-right: 7px;
      display: inline-block;
   }

   .markdown-text-box .doc-section .doc-icon {
      display: inline-block;
   }

   .markdown-text-box .doc-section .doc-icon img {
      width: 5px;
   }

   .card-container {
      width: 380px;
      display: block;
      float: left;
      padding-left: 15px;
      padding-right: 15px;
      box-sizing: border-box;
   }

   .card {
      border-radius: 10px;
      padding: 17px 16px;
      margin-top: 30px;
      border: 1px solid #ebeef5;
      background-color: #fff;
      overflow: hidden;
      box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
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

   .markdown-text-box img {
      box-shadow: none;
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
   ::: TRTC SDK
   <div class="markdown-text-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/2dab7b72bfab9b3d38f471b89294e7c6.svg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  Use Cases
               </div>
            </div>
            <div class="section-content">
               Metaverse audio/video calls, online classes, remote work, group audio/video calls, group conference, audio chat,<br />online healthcare
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  Learn more
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/36066">Audio/Video Call</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/47636">Group Conference</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/37286">Interactive Audio Streaming</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/36061">Interactive Video Streaming</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/41940">Online Karaoke</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
   :::
   ::: MLVB SDK
   <div class="markdown-text-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/84d2e781bab936bf2ba076ab353df34c.svg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  Use Cases
               </div>
            </div>
            <div class="section-content">
               Live streaming for entertainment, e-commerce, corporate events, and games
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  Learn more
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/267/42140">SDK Integration</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
   :::
   ::: Player SDK
   <div class="markdown-text-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/3d25e8feea02c32299d8616ce3056941.png" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  Use Cases
               </div>
            </div>
            <div class="section-content">
               Playing videos live or on demand
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  Learn more
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/266/33975">Player SDK Integration</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/266/38294">Playing Encrypted Videos</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
   :::
   ::: IM SDK
   <div class="markdown-text-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/01db05070c5acefd30585e88a3479585.svg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  Use Cases
               </div>
            </div>
            <div class="section-content">
               In-app messaging, on-screen commenting, user profiles, relationship chains
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  Learn more
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/products/im?lang=en&amp;pg=">Tencent Cloud Instant Messaging</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
   :::
   ::: All-in-One SDK
   <div class="markdown-text-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/b35558b665ede349ded27711bb993237.jpeg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  Use Cases
               </div>
            </div>
            <div class="section-content">
               Includes the use cases of the TRTC SDK, MLVB SDK, and Player SDK
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  Learn more
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/36066">Audio/Video Call</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/47636">Group Conference</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/37286">Interactive Audio Streaming</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/36061">Interactive Video Streaming</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/647/41940">Online Karaoke</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/267/42140">Live SDK Integration</a>
    
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/document/product/266/33975">Player SDK Integration</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
   :::
</dx-tabs>

#### TRTC SDK download

<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6c27890223ea3351fe9caff6276e9145.svg"
                  data-nonescope="true" />
               <p class="titlename">Web</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Web">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35096">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35607">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/en/TXLiteAVSDK_TRTC_Android_en_latest.zip">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35093">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35084">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/en/TXLiteAVSDK_TRTC_iOS_en_latest.zip">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35092">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35086">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/88fd6260e225ba6faa33d140946d7afe.svg"
                  data-nonescope="true" />
               <p class="titlename">Windows</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/46745">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/46748">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/64fac45b91100ae4e506c61b604fe515.svg"
                  data-nonescope="true" />
               <p class="titlename">MacOS</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Mac">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35094">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35086">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/50efefd0ebb90dd9d7c858b78b9be0c7.svg"
                  data-nonescope="true" />
               <p class="titlename">Electron</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">ZIP 
                  file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Electron">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35097">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35089">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://pub.dev/packages/tencent_trtc_cloud/versions">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/c1avie/trtc_demo">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35098">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/39243">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/d630b605c8979b5587aa2a74de36b567.svg"
                  data-nonescope="true" />
               <p class="titlename">React Native</p>
            </div>
            <div class="card-content">
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/tencentyun/TRTCReactNative">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/43298">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/43297">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/9d3dec1fb7625eb8589d6742c986a328.svg"
                  data-nonescope="true" />
               <p class="titlename">Unity</p>
            </div>
            <div class="card-content">
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Unity">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/TRTC_Unity/blob/main/SDK/README-zh_CN.md">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/TRTC_Unity/blob/main/TRTC-Simple-Demo/README-zh_CN.md">
                  Demo run</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### Live SDK download
<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
               <p class="titlename">Android</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Live_Android_latest.zip">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1071/38156">Integration guide</a>
               <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1071/38147">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
               <p class="titlename">iOS</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Live_iOS_latest.zip">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1071/38155">Integration guide</a>
               <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1071/38147">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg" data-nonescope="true" />
               <p class="titlename">Flutter</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://pub.dev/packages/live_flutter_plugin/versions&quot;">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Flutter">GitHub</a>
               <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/454/71666">Integration guide</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Flutter/tree/main/Live-API-Example">
                  Demo run</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### Player SDK download

<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Android_latest.zip">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/47849">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/42091">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_iOS_latest.zip">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/47840">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/42091">
                  Demo run</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://github.com/LiteAVSDK/Player_Flutter">ZIP file</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_Flutter">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/42099">Integration guide</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/266/42091">
                  Demo run</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### IM SDK download

<div> 
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden"> 
       <div class="card-container">
         <div class="card">
           <div class="card-header">
             <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6c27890223ea3351fe9caff6276e9145.svg" data-nonescope="true" />
             <p class="titlename">Web</p>
           </div>
           <div class="card-content">
             <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Web/IMSDK">GitHub</a>
             <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34309">Integration guide</a>
             <a target="_blank" style="margin-left:10px" href="https://web.sdk.qcloud.com/im/demo/en/index.html#/home">
               Demo run</a>
           </div>
         </div>
       </div>
       <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
            <p class="titlename">Android</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Android/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34306">Integration guide</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
            <p class="titlename">iOS</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/iOS/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34307">Integration guide</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/88fd6260e225ba6faa33d140946d7afe.svg" data-nonescope="true" />
            <p class="titlename">Windows</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Windows">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34310">Integration guide</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/64fac45b91100ae4e506c61b604fe515.svg" data-nonescope="true" />
            <p class="titlename">macOS</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/iOS/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34307">Integration guide</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/50efefd0ebb90dd9d7c858b78b9be0c7.svg" data-nonescope="true" />
            <p class="titlename">Electron</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Electron">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/43090">Integration guide</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg" data-nonescope="true" />
            <p class="titlename">Flutter</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Flutter">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46264">Integration guide</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2514ea85f97244b9666138c76e5c6407.svg" data-nonescope="true" />
            <p class="titlename">Unreal Engine</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/IMUnrealEngine">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46262">Integration guide</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/9d3dec1fb7625eb8589d6742c986a328.svg" data-nonescope="true" />
            <p class="titlename">Unity</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Flutter">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46263">Integration guide</a>
          </div>
        </div>
      </div>
   </div>
</div>

#### All-in-One SDK download

<div> 
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden"> 
       <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
            <p class="titlename">Android</p>
          </div>
          <div class="card-content">
            <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">ZIP file</a>
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/647/35093">Integration guide</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/647/35084">
              Demo run</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
            <p class="titlename">iOS</p>
          </div>
          <div class="card-content">
            <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">ZIP file</a>
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/647/35092">Integration guide</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/647/35086">
              Demo run</a>
          </div>
        </div>
      </div>
   </div>
</div>

#### Features

<style type="text/css">
   .tg  {border-collapse:collapse;border-spacing:0;}
   .tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
     overflow:hidden;padding:10px 5px;word-break:normal;}
   .tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
     font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
   .tg .tg-cly1{text-align:left;vertical-align:middle}
   .tg .tg-ncfo{color:#272727;text-align:left;vertical-align:middle}
   .tg .tg-nrix{text-align:center;vertical-align:middle}
   </style>
   <table class="tg">
   <thead>
     <tr>
       <th class="tg-ncfo">Module</th>
       <th class="tg-ncfo">Feature</th>
       <th class="tg-ncfo">TRTC SDK</th>
       <th class="tg-ncfo">MLVB SDK</th>
       <th class="tg-ncfo">Player SDK</th>
       <th class="tg-ncfo">IM SDK</th>
       <th class="tg-ncfo">All-in-One</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td class="tg-cly1">UI</td>
       <td class="tg-cly1">Custom UI</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="5">Audio/Video call</td>
       <td class="tg-cly1">One-to-one call</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Room management</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Screen sharing</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Group conference</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Cross/Same-room communication</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="19">Capturing</td>
       <td class="tg-cly1">Aspect ratio change</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Orientation change</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Video quality (resolution)</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Capturing control</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Watermarking</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Focal length change</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Screenshot</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Background music</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Voice change/Reverb</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Volume change</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Muting</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Recording</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Filters</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Beautification</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">High audio quality</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">3A processing</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Custom capturing</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Custom rendering</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">SEI messages</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="2">Encoding</td>
       <td class="tg-cly1">H.264</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">QoS control</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="6">Live push</td>
       <td class="tg-cly1">Push from camera</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Push from screen</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Audio-only push</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">RTMP over QUIC</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">WebRTC</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">TRTC</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="4">Live playback</td>
       <td class="tg-cly1">RTMP,FLV,HLS,and DASH playback</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">WebRTC</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Time shifting</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Message receiving</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="11">Live/On-demand playback</td>
       <td class="tg-cly1">Volume change</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Video quality change</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Orientation change</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Screenshot</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Floating window</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">On-screen comments</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Brightness adjustment</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Screen locking</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Custom player size</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Mirroring</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Auto rotation</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="30">Player - On-demand playback</td>
       <td class="tg-cly1">HLS,DASH,MP4,and MP3 playback</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">HTTPS</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Gesture control</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Progress bar</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Progress markers</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Thumbnail previews</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Fill mode</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Custom playback start time</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Video thumbnail</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Floating window</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Instant streaming + Preloading</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Quick seeking</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Playback looping</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Adaptive bitrate</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Playback speed change</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Play while downloading</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Subtitles</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">UI switch</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Video caching</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Playlist</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Video download</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Video preview</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Hotlink protection</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Play encrypted videos</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Resume playback</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Show linked images when playback is paused</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Autoplay</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Play by file ID</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Loading animation</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Data reporting</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="6">Instant messaging</td>
       <td class="tg-cly1">One-to-one chat</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">Group chat</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">Push messages</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">Chat management</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">User profiles and relationship chains</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">Group management</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
   </tbody>
   </table>
