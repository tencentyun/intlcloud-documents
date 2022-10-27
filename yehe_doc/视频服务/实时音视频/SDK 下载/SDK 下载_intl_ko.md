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
      height: 238px;
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

   .markdown-text-box .doc-section .doc-link:nth-child(3n+1) {
      margin-left: 0;
   }

   .markdown-text-box .doc-section .doc-link {
      width: 120px;
      float: left;
      background: #FFFFFF;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.02);
      border-radius: 24px;
      padding: 5px;
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
                  사용 사례
               </div>
            </div>
            <div class="section-content">
               메타버스 음성/영상 통화, 온라인 수업, 원격 근무, 그룹 음성/영상 통화, 그룹 실시간 회의, 음성 채팅,<br />원격 진료 등 시나리오.
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  더 알아보기
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/36066">음성/영상 통화</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/47636">그룹 화상 회의</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/37286">인터랙티브 오디오 스트리밍</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/36061">인터랙티브 비디오 스트리밍</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/41940">온라인 Karaoke</a>
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
                  사용 사례
               </div>
            </div>
            <div class="section-content">
               엔터테인먼트, 전자 상거래, 기업 이벤트 및 게임을 위한 라이브 스트리밍
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  더 알아보기
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/267/42140">SDK 통합</a>
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
   ::: 플레이어 SDK
   <div class="markdown-text-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/3d25e8feea02c32299d8616ce3056941.png" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  사용 사례
               </div>
            </div>
            <div class="section-content">
               라이브 또는 주문형 비디오 재생
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  더 알아보기
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/266/33975">Player SDK 통합</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/266/38294">암호화된 비디오 재생</a>
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
                  사용 사례
               </div>
            </div>
            <div class="section-content">
               인앱 채팅(In-App-Chat), 화면 댓글, 사용자 프로필, 관계 체인 등 시나리오
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  더 알아보기
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/products/im?lang=en&amp;pg=">Tencent Cloud IM</a>

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
   ::: 올인원 SDK
   <div class="markdown-text-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/b35558b665ede349ded27711bb993237.jpeg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  사용 사례
               </div>
            </div>
            <div class="section-content">
               TRTC SDK, MLVB SDK 및 Player SDK의 사용 사례 포함
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  더 알아보기
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/36066">음성/영상 통화</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/47636">그룹 화상 회의</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/37286">인터랙티브 오디오 스트리밍</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/36061">인터랙티브 비디오 스트리밍</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/41940">온라인 Karaoke</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/267/42140">MLVB SDK 통합</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/266/33975">Player SDK 통합</a>
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

#### TRTC SDK 다운로드

<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6c27890223ea3351fe9caff6276e9145.svg"
                  data-nonescope="true" />
               <p class="titlename">Web SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Web">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35096">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35607">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35093">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35084">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35092">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35086">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/88fd6260e225ba6faa33d140946d7afe.svg"
                  data-nonescope="true" />
               <p class="titlename">Windows SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/46745">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/46748">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/64fac45b91100ae4e506c61b604fe515.svg"
                  data-nonescope="true" />
               <p class="titlename">MacOS SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Mac">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35094">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35086">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/50efefd0ebb90dd9d7c858b78b9be0c7.svg"
                  data-nonescope="true" />
               <p class="titlename">Electron SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">ZIP
                  다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Electron">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35097">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35089">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://pub.dev/packages/tencent_trtc_cloud/versions">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/c1avie/trtc_demo">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35098">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/39243">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/d630b605c8979b5587aa2a74de36b567.svg"
                  data-nonescope="true" />
               <p class="titlename">React Native SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/tencentyun/TRTCReactNative">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/43298">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/43297">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/9d3dec1fb7625eb8589d6742c986a328.svg"
                  data-nonescope="true" />
               <p class="titlename">Unity SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Unity">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/TRTC_Unity/blob/main/SDK/README-zh_CN.md">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/TRTC_Unity/blob/main/TRTC-Simple-Demo/README-zh_CN.md">실행
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### MLVB SDK 다운로드
<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Live_Android_latest.zip">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/56589">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/60984">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Live_iOS_latest.zip">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/56588">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/60985">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://pub.dev/packages/live_flutter_plugin/versions&quot;">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Flutter">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/71666">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/Live_Flutter/tree/main/Live-API-Example">실행
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### Player SDK 다운로드

<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Android_latest.zip">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/47849">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/42091">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_iOS_latest.zip">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/47840">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/42091">실행
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDK 다운로드</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://github.com/LiteAVSDK/Player_Flutter">ZIP 다운로드</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_Flutter">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/42099">통합 가이드</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/42091">실행
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### IM SDK 다운로드

<div> 
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden"> 
       <div class="card-container">
         <div class="card">
           <div class="card-header">
             <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6c27890223ea3351fe9caff6276e9145.svg" data-nonescope="true" />
             <p class="titlename">Web SDK 다운로드</p>
           </div>
           <div class="card-content">
             <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Web/IMSDK">GitHub</a>
             <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34309">통합 가이드</a>
             <a target="_blank" style="margin-left:10px" href="https://web.sdk.qcloud.com/im/demo/en/index.html#/home">실행
               Demo</a>
           </div>
         </div>
       </div>
       <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
            <p class="titlename">Android SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Android/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34306">통합 가이드</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
            <p class="titlename">iOS SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/iOS/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34307">통합 가이드</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/88fd6260e225ba6faa33d140946d7afe.svg" data-nonescope="true" />
            <p class="titlename">Windows SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Windows">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34310">통합 가이드</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/64fac45b91100ae4e506c61b604fe515.svg" data-nonescope="true" />
            <p class="titlename">MacOS SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/iOS/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34307">통합 가이드</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/50efefd0ebb90dd9d7c858b78b9be0c7.svg" data-nonescope="true" />
            <p class="titlename">Electron SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Electron">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/43090">통합 가이드</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg" data-nonescope="true" />
            <p class="titlename">Flutter SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Flutter">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46264">통합 가이드</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2514ea85f97244b9666138c76e5c6407.svg" data-nonescope="true" />
            <p class="titlename">Unreal Engine SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/IMUnrealEngine">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46262">통합 가이드</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/9d3dec1fb7625eb8589d6742c986a328.svg" data-nonescope="true" />
            <p class="titlename">Unity SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Flutter">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46263">통합 가이드</a>
          </div>
        </div>
      </div>
   </div>
</div>

#### 올인원 SDK 다운로드

<div> 
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden"> 
       <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
            <p class="titlename">Android SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">ZIP 다운로드</a>
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/647/32175">통합 가이드</a>
            <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/647/32166">실행
              Demo</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
            <p class="titlename">iOS SDK 다운로드</p>
          </div>
          <div class="card-content">
            <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">ZIP 다운로드</a>
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/647/32173">통합 가이드</a>
            <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/647/32396">실행
              Demo</a>
          </div>
        </div>
      </div>
   </div>
</div>

#### 기능 리스트

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
       <th class="tg-ncfo">기능 모듈</th>
       <th class="tg-ncfo">기능 세부 정보</th>
       <th class="tg-ncfo">TRTC SDK</th>
       <th class="tg-ncfo">MLVB SDK</th>
       <th class="tg-ncfo">Player SDK</th>
       <th class="tg-ncfo">IM SDK</th>
       <th class="tg-ncfo"올인원 기능</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td class="tg-cly1">UI</td>
       <td class="tg-cly1">사용자 정의 UI</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="5">음성/영상 통화</td>
       <td class="tg-cly1">1v1 통화</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">방 관리</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">화면 공유</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">그룹 회의</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">크로스 룸/동일 룸 통신</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="19">캡처</td>
       <td class="tg-cly1">종횡비 변경</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">가로 세로 화면 전환</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">비디오 품질(해상도)</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">캡처 제어</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">워터마크</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">초점 거리 변경</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">스크린샷</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">배경 음악</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">음성 변조/리버브</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">볼륨 변경</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">음소거</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">녹화</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">필터</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">뷰티 필터</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">고음질 캡처</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">3A 처리</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">사용자 정의 캡처</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">사용자 정의 렌더링</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">SEI 메시지</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="2">인코딩</td>
       <td class="tg-cly1">H.264</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">QoS 제어</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="6">라이브 푸시</td>
       <td class="tg-cly1">카메라 푸시</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">화면 푸시</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">오디오 전용 푸시</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">RTMP OVER QUIC</td>
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
       <td class="tg-nrix" rowspan="4">라이브 재생</td>
       <td class="tg-cly1">RTMP/FLV</td>
       <td class="tg-cly1">✓</td>
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
       <td class="tg-cly1">타임 시프트</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">메시지 수신</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="11">라이브/주문형 재생</td>
       <td class="tg-cly1">볼륨 변경</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">비디오 품질 변경</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">가로 세로 화면 전환</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">스크린샷</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">플로팅 창</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">화면 댓글</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">밝기 조정</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">화면 잠금</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">플레이어 크기 설정</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">미러링</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">자동 회전</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="30">플레이어 - 주문형 재생</td>
       <td class="tg-cly1">여러 형식</td>
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
       <td class="tg-cly1">제스처 제어</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">진행률 표시줄</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">진행률 마커</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">썸네일 미리보기</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">채우기 모드</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">사용자 지정 재생 시작 시간</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">동영상 썸네일</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">플로팅 창</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">인스턴트 스트리밍 + 사전 로딩</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">빠른 seek</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">재생 반복</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">어댑티브 비트 레이트</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">재생 속도 변경</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">다운로드하면서 재생</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">자막</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">UI 전환</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">비디오 캐시</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">재생 목록</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">비디오 다운로드</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">비디오 미리보기</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">링크 도용 방지</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">암호화된 비디오 재생</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">재생 재개</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">재생이 일시 중지되면 링크된 이미지 표시</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">자동 재생</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">FileID로 재생</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">애니메이션 Loading</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">데이터 리포트</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="6">인스턴트 메시징</td>
       <td class="tg-cly1">1대1 채팅</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">그룹 채팅</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">메시지 푸시</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">채팅 관리</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">사용자 프로필 및 관계 체인</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
     <tr>
       <td class="tg-cly1">그룹 관리</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">　</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">　</td>
     </tr>
   </tbody>
   </table>
