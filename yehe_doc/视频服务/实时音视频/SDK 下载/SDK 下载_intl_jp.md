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
                  ユースケース
               </div>
            </div>
            <div class="section-content">
               メタバースオーディオビデオ通話、eラーニング、リモートコラボレーション、多人数のオーディオビデオ通話、多人数のリアルタイムミーティング、エンターテイメントボイスチャット、<br />リモート医療などのケースです。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  その他のドキュメント
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/36066">オーディオビデオ通話</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/47636">多人数ビデオミーティング</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/37286">ボイスインタラクティブストリーミング</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/36061">ビデオインタラクティブストリーミング</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/41940">オンラインKaraoke</a>
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
                  ユースケース
               </div>
            </div>
            <div class="section-content">
               エンターテイメントライブストリーミング、eコマースライブストリーミング、企業活動ライブストリーミング、ゲームライブストリーミングなどのケースです。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  その他のドキュメント
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/267/42140">統合ガイド</a>
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
                  ユースケース
               </div>
            </div>
            <div class="section-content">
               ライブストリーミング、オンデマンドの視聴シーンです。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  その他のドキュメント
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/266/33975">プレーヤーコンポーネント</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/266/38294">暗号化したビデオの再生</a>
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
                  ユースケース
               </div>
            </div>
            <div class="section-content">
               アプリ内チャット（In-App-Chat）、ライブストリーミング弾幕、ユーザープロファイルとフレンドリレーションシップチェーンなどのケースです。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  その他のドキュメント
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/products/im?lang=en&amp;pg=">Instant Messaging</a>

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
   ::: 全機能SDK
   <div class="markdown-text-box">
      <div class="left-section">
         <img src="https://qcloudimg.tencent-cloud.cn/raw/b35558b665ede349ded27711bb993237.jpeg" />
      </div>
      <div class="right-content">
         <div class="sence-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/9f0fab1370820a47d95b0cbc8899de3b.png" />
               <div class="header-text">
                  ユースケース
               </div>
            </div>
            <div class="section-content">
               TRTC SDK、MLVB SDK、Player SDKのすべての機能シナリオをカバーしています。
            </div>
         </div>
         <div class="doc-section">
            <div class="section-header">
               <img src="https://qcloudimg.tencent-cloud.cn/raw/64f48bd13505979bc8f77fae00990a6d.png" />
               <div class="header-text">
                  その他のドキュメント
               </div>
            </div>
            <div class="section-content">
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/36066">オーディオビデオ通話</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/47636">多人数ビデオミーティング</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/37286">ボイスインタラクティブストリーミング</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/36061">ビデオインタラクティブストリーミング</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/647/41940">オンラインKaraoke</a>
                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/267/42140">MLVB SDK統合ガイド</a>

                  </div>
                  <div class="doc-icon">
                     <img src="https://qcloudimg.tencent-cloud.cn/raw/a35d6e1ca39d7abe7348c5fab8acabee.png" />
                  </div>
               </div>
               <div class="doc-link">
                  <div class="doc-title">
                     <a href="https://www.tencentcloud.com/zh/document/product/266/33975">プレーヤーコンポーネント</a>
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

#### TRTC SDKのダウンロード

<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6c27890223ea3351fe9caff6276e9145.svg"
                  data-nonescope="true" />
               <p class="titlename">Web SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Web">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35096">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35607">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35093">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35084">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35092">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35086">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/88fd6260e225ba6faa33d140946d7afe.svg"
                  data-nonescope="true" />
               <p class="titlename">Windows SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/46745">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/46748">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/64fac45b91100ae4e506c61b604fe515.svg"
                  data-nonescope="true" />
               <p class="titlename">MacOS SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Mac">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35094">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35086">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/50efefd0ebb90dd9d7c858b78b9be0c7.svg"
                  data-nonescope="true" />
               <p class="titlename">Electron SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">ZIP
                  ダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Electron">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35097">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35089">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://pub.dev/packages/tencent_trtc_cloud/versions">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/c1avie/trtc_demo">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/35098">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/39243">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/d630b605c8979b5587aa2a74de36b567.svg"
                  data-nonescope="true" />
               <p class="titlename">React Native SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/tencentyun/TRTCReactNative">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/43298">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/document/product/647/43297">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/9d3dec1fb7625eb8589d6742c986a328.svg"
                  data-nonescope="true" />
               <p class="titlename">Unity SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/TRTC_Unity">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/TRTC_Unity/blob/main/SDK/README-zh_CN.md">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/TRTC_Unity/blob/main/TRTC-Simple-Demo/README-zh_CN.md">実行
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### MLVB SDKのダウンロード
<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Live_Android_latest.zip">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/56589">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/60984">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Live_iOS_latest.zip">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/56588">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/60985">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://pub.dev/packages/live_flutter_plugin/versions&quot;">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Live_Flutter">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://cloud.tencent.com/document/product/454/71666">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://github.com/LiteAVSDK/Live_Flutter/tree/main/Live-API-Example">実行
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### Player SDKのダウンロード

<div>
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden">
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg"
                  data-nonescope="true" />
               <p class="titlename">Android SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Android_latest.zip">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_Android">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/47849">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/42091">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg"
                  data-nonescope="true" />
               <p class="titlename">iOS SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box"
                  href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_iOS_latest.zip">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_iOS">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/47840">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/42091">実行
                  Demo</a>
            </div>
         </div>
      </div>
      <div class="card-container">
         <div class="card">
            <div class="card-header">
               <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg"
                  data-nonescope="true" />
               <p class="titlename">Flutter SDKのダウンロード</p>
            </div>
            <div class="card-content">
               <a class="with-box" href="https://github.com/LiteAVSDK/Player_Flutter">ZIPのダウンロード</a>
               <a target="_blank" style="margin-left:10px" href="https://github.com/LiteAVSDK/Player_Flutter">GitHub</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/42099">統合ガイド</a>
               <a target="_blank" style="margin-left:10px"
                  href="https://www.tencentcloud.com/zh/document/product/266/42091">実行
                  Demo</a>
            </div>
         </div>
      </div>
   </div>
</div>

#### IM SDKのダウンロード

<div> 
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden"> 
       <div class="card-container">
         <div class="card">
           <div class="card-header">
             <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6c27890223ea3351fe9caff6276e9145.svg" data-nonescope="true" />
             <p class="titlename">Web SDKのダウンロード</p>
           </div>
           <div class="card-content">
             <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Web/IMSDK">GitHub</a>
             <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34309">統合ガイド</a>
             <a target="_blank" style="margin-left:10px" href="https://web.sdk.qcloud.com/im/demo/en/index.html#/home">実行
               Demo</a>
           </div>
         </div>
       </div>
       <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
            <p class="titlename">Android SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Android/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34306">統合ガイド</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
            <p class="titlename">iOS SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/iOS/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34307">統合ガイド</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/88fd6260e225ba6faa33d140946d7afe.svg" data-nonescope="true" />
            <p class="titlename">Windows SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Windows">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34310">統合ガイド</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/64fac45b91100ae4e506c61b604fe515.svg" data-nonescope="true" />
            <p class="titlename">MacOS SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/iOS/IMSDK">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/34307">統合ガイド</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/50efefd0ebb90dd9d7c858b78b9be0c7.svg" data-nonescope="true" />
            <p class="titlename">Electron SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Electron">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/43090">統合ガイド</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/6f8c6743cf6c1c7392e583e470ba324e.svg" data-nonescope="true" />
            <p class="titlename">Flutter SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Flutter">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46264">統合ガイド</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2514ea85f97244b9666138c76e5c6407.svg" data-nonescope="true" />
            <p class="titlename">Unreal Engine SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/IMUnrealEngine">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46262">統合ガイド</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/9d3dec1fb7625eb8589d6742c986a328.svg" data-nonescope="true" />
            <p class="titlename">Unity SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a target="_blank" style="margin-left:10px" href="https://github.com/TencentCloud/TIMSDK/tree/master/Flutter">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://www.tencentcloud.com/document/product/1047/46263">統合ガイド</a>
          </div>
        </div>
      </div>
   </div>
</div>

#### 全機能SDKのダウンロード

<div> 
   <div style="position:relative;box-sizing:border-box;padding-bottom:10px;margin-bottom:10px;overflow:hidden"> 
       <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/2a1f6ca8bfd3bca7a221b9f2fcb8256b.svg" data-nonescope="true" />
            <p class="titlename">Android SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">ZIPのダウンロード</a>
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/647/32175">統合ガイド</a>
            <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/647/32166">実行
              Demo</a>
          </div>
        </div>
      </div>
      <div class="card-container">
        <div class="card">
          <div class="card-header">
            <img class="icon" src="https://qcloudimg.tencent-cloud.cn/raw/37070d9b1f2641a12c64e44de26161e1.svg" data-nonescope="true" />
            <p class="titlename">iOS SDKのダウンロード</p>
          </div>
          <div class="card-content">
            <a class="with-box" href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">ZIPのダウンロード</a>
            <a target="_blank" style="margin-left:10px" href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a>
            <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/647/32173">統合ガイド</a>
            <a target="_blank" style="margin-left:10px" href="https://cloud.tencent.com/document/product/647/32396">実行
              Demo</a>
          </div>
        </div>
      </div>
   </div>
</div>

#### 機能リスト

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
       <th class="tg-ncfo">機能モジュール</th>
       <th class="tg-ncfo">機能詳細</th>
       <th class="tg-ncfo">TRTC SDK</th>
       <th class="tg-ncfo">MLVB SDK</th>
       <th class="tg-ncfo">Player SDK</th>
       <th class="tg-ncfo">IM SDK</th>
       <th class="tg-ncfo">全機能</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td class="tg-cly1">インターフェース</td>
       <td class="tg-cly1">カスタムUI</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="5">オーディオビデオ通話</td>
       <td class="tg-cly1">2人制通話</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ルーム管理</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">画面共有</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">多人数ミーティング</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ルーム間/ルーム内マイク接続</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="19">キャプチャ・撮影</td>
       <td class="tg-cly1">アスペクト比（縦横比）</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">縦横画面の切り替え</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">解像度</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">撮影制御</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ウォーターマーク</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">焦点距離</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ビデオスクリーンキャプチャ</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">バックグラウンドミュージック</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ボイスチェンジ/リバーブ</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ボリューム調整</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ミュートキャプチャ</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">記録</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">フィルター</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">美顔</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">高音質キャプチャ</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">3A処理</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">オーディオビデオキャプチャのカスタマイズ</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">オーディオビデオレンダリングのカスタマイズ</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">SEI情報</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="2">エンコード送信</td>
       <td class="tg-cly1">H.264</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Qosフロー制御ポリシー</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="6">CSSプッシュ</td>
       <td class="tg-cly1">カメラプッシュ</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">スクリーンキャプチャプッシュ</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ピュアオーディオプッシュ</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">RTMP OVER QUIC</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">WebRTC</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">TRTC</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="4">ライブストリーミング再生</td>
       <td class="tg-cly1">RTMP/FLVマルチプロトコル</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">WebRTC</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">CSSタイムシフト</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">メッセージ受信</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="11">パブリック再生</td>
       <td class="tg-cly1">ボリューム調節</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">解像度の切り替え</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">縦横/全画面切り替え</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ビデオスクリーンキャプチャ</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ミニウィンドウ再生</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">弾幕</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">明るさ調節</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">画面をロック</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">プレーヤーサイズの設定</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">イメージ再生</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ビデオの自動回転</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="30">プレーヤー_オンデマンド再生</td>
       <td class="tg-cly1">複数形式をサポート</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">HTTPSをサポート</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">マルチジェスチャー操作</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">プログレスバー操作</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">プログレスバーとキーモーメント</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">プログレスバーとサムネイル</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">スクリーン塗りつぶしの適応</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">再生開始時間のカスタマイズ</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">カバーの設定</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">インタラクティブフローティングウィンドウ</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">最初のフレームの秒速開始+プリロード</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">クイックseek</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">シームレスなループ再生</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">アダプティブビットレート</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">倍速/可変速再生</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">再生とダウンロードの同時実行</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">字幕設定</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">UI切り替え</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ビデオキャッシュ/ローカルキャッシュ</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">再生リスト</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">オフラインダウンロード</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ビデオプレビュー</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">リンク不正アクセス防止</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">暗号化したビデオの再生</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">再生継続機能</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">ロール画像の一時停止+リダイレクトリンク</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">連続/自動再生</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">FileID再生</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">Loadingアニメーション</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-cly1">データレポート</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
     </tr>
     <tr>
       <td class="tg-nrix" rowspan="6">ソーシャルチャット</td>
       <td class="tg-cly1">シングルチャット</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
     </tr>
     <tr>
       <td class="tg-cly1">グループチャット</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
     </tr>
     <tr>
       <td class="tg-cly1">メッセージプッシュ</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
     </tr>
     <tr>
       <td class="tg-cly1">セッション管理</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
     </tr>
     <tr>
       <td class="tg-cly1">ユーザープロファイルとリレーションシップチェーン管理</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
     </tr>
     <tr>
       <td class="tg-cly1">グループ管理</td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1"> </td>
       <td class="tg-cly1">✓</td>
       <td class="tg-cly1"> </td>
     </tr>
   </tbody>
   </table>
