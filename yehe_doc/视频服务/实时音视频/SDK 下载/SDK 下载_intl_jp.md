<style>
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
        padding-top: 10px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 30px;
        border: 1px solid #ebeef5;
        background-color: #fff;
        overflow: hidden;
        box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
        text-align: center;
    }
    
    .markdown-text-box img {
        box-shadow: none;
    }


    .titlename {
                color:#191919;
        position: relative;
        top: -2px;
                font-weight: bolder;
                font-size: larger;
    }
        
        @media (max-width: 768px){
                .card-container,
                .scene-card-container{
                        width: 100%;
                }
                .scene-card > div{
                        width: 100%!important;
                        margin-left: 0!important;
                }
                img {
        box-shadow: none;
    }
        }
</style>

## SDK のダウンロード
Tencent Real-Time Communication(TRTC)は、Tencent Cloudが提供する低遅延、高品質のオーディオおよびビデオ通信サービスのセットであり、Tencent　Cloudのお客様に安定した、高信頼で低コストのオーディオおよびビデオ転送機能を提供することを目的としています。本サービスは、グローバルなオーディオおよびビデオ転送ネットワークと1セットのターミナルSDKで構成されており、このページから、現在の主流のクライアントプラットフォームと人気フレームワークを含むTRTC SDK（オーディオビデオ通話SDK）をダウンロードできます。

>? 現在のネットワークでは、Githubへのアクセス速度が振るわない場合は、[ここをクリック](https://gitee.com/cloudtencent/TRTCSDK)してGiteeのイメージリポジトリにアクセスできます。

### Web SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
  <div class="card-container">
      <div class="card">
        <img src="https://main.qcloudimg.com/raw/7e2651085e3e3c6e32190e401a6dfd32.svg" data-nonescope="true">
        <p class="titlename">安定版(TRTC)SDK</p>
        <p style="color:#586376;">TRTC機能を備えており、アプリをインストールせずに音声通話とビデオ通話を行うことができます。主なデスクトップとモバイル端末のブラウザと互換性があります。</p>
        <a onclick="reportEvent({name: 'download-click-web', ext1: 'zip'})" target="_blank" href="https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip">ZIPダウンロード</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'github'})" target="_blank" href="https://github.com/LiteAVSDK/TRTC_Web">GitHub</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'doc-sdk'})" target="_blank" href="https://intl.cloud.tencent.com/document/product/647/35096">統合ガイド</a>
        <a style="margin-left: 10px;" onclick="reportEvent({name: 'download-click-web', ext1: 'doc-demo'})" target="_blank" href="https://intl.cloud.tencent.com/document/product/647/35607">Demoを実行</a>
      </div>
  </div>
</div>

### Android SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                            <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">簡易版(TRTC)SDK</p>
                <p style="color:#586376;">TRTCとライブストリーミング再生(TXLivePlayer)の2つの機能を備えており、サイズが小さく、機能が安定しています。</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/en/TXLiteAVSDK_TRTC_Android_en_latest.zip">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Android">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35093">統合ガイド</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35084">Demoを実行</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/b0211b0870806899009a17a4216ea65c.svg" data-nonescope="true">
                                <p class="titlename">フル機能版(Professional)SDK</p>
                <p style="color:#586376;">TRTC、ライブストリーミング、ショート動画、オン・デマンドなど、複数の機能が含まれており、SDKのサイズが簡易版よりやや大きい。</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_Android_latest.zip">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/LiteAVProfessional_Android">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35093">統合ガイド</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35084">Demoを実行</a>
            </div>
        </div>
</div>

### iOS SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">簡易版(TRTC)SDK</p>
                <p style="color:#586376;">TRTCとライブストリーミング再生(TXLivePlayer)の2つの機能を備えており、小型サイズで、機能が安定しています。</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_iOS">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35092">統合ガイド</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demoを実行</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img class="icon" src="https://main.qcloudimg.com/raw/613f2e15bed7c8297110676b52784b71.svg" data-nonescope="true">
                                <p class="titlename">フル機能版(Professional)SDK</p>
                 <p style="color:#586376;">TRTC、ライブストリーミング、ショート動画、オンデマンドなど、複数の機能が含まれており、SDKのサイズが簡易版よりやや大きいです。</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Professional_iOS_latest.zip">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/LiteAVProfessional_iOS">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35092">統合ガイド</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demoを実行</a>
            </div>
        </div>
</div>

### Windows SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                                <p class="titlename">Windows SDK（C++版）</p>
                <p style="color:#586376;">リアルタイムオーディオおよびビデオ（TRTC）、ライブブロードキャストプッシュ（TXLivePusher）、ライブブロードキャスト再生（TXLivePlayer）およびオンデマンド再生（TXVodPlayer）の4つの機能を備えています</p>
                          <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/46745">統合ガイド</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/46748">Demoを実行</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                                <img src="https://main.qcloudimg.com/raw/104e3aadbd4515f61c3f2f5378948cfb.svg" data-nonescope="true">
                                <p class="titlename">Windows SDK（C#版）</p>
                <p style="color:#586376;">リアルタイムオーディオおよびビデオ(TRTC)、ライブブロードキャストプッシュ(TXLivePusher)、ライブブロードキャスト再生(TXLivePlayer)およびオンデマンド再生(TXVodPlayer)の4つの機能を備えています。</p>
                          <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_CSharp_latest.zip">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Windows">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35095">統合ガイド</a>
            </div>
        </div>
</div>

### Mac OS SDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
                                <img src="https://qcloudimg.tencent-cloud.cn/raw/4f5b5b301babc3ddf4d2867b37c30ffc.png" data-nonescope="true">
                                <p class="titlename">Mac OS SDK</p>
                <p style="color:#586376;">リアルタイムオーディオおよびビデオ(TRTC)、ライブブロードキャストプッシュ(TXLivePlayer)、ライブブロードキャストプレーヤー(TXLivePlayer)およびオンデマンド再生(TXVodPlayer)の4つの機能を備えています。</p>
                                <a href="https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Mac">GitHub</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35094">統合ガイド</a>
                                <a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35086">Demoを実行</a>
            </div>
        </div>
</div>


### クロスプラットフォームSDK

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
        <div class="card-container">
            <div class="card">
									<img src="https://qcloudimg.tencent-cloud.cn/raw/d6fd52f011bdbb13302b2ae261e8a756.png" data-nonescope="true"/>
								<p class="titlename">Electron SDK</p>
                <p style="color:#586376;">Electronフレームワークに基づいてパッケージ化されています。Web技術により、WindowsとMacのプラットフォームでアプリケーションをすばやく構築できます。</p>
							<a href="https://web.sdk.qcloud.com/trtc/electron/download/TXLiteAVSDK_TRTC_Electron_latest.zip">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/LiteAVSDK/TRTC_Electron">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35097">統合ガイド</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35089">Demoを実行</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
									<img src="https://qcloudimg.tencent-cloud.cn/raw/3b6929f89ce1113bc2005873f2338de9.png" data-nonescope="true"/>
									<p class="titlename">Flutter SDK</p>
                <p style="color:#586376;">Flutterフレームワークに基づいてカプセル化されているTRTC SDKであり、1セットのコードで各プラットフォームで実行できるアプリをすばやく構築できます。</p>
								<a href="https://pub.dev/packages/tencent_trtc_cloud/versions">ZIPダウンロード</a>
                <a style="margin-left: 10px;" href="https://github.com/c1avie/trtc_demo">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/35098">統合ガイド</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/39243">Demoを実行</a>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                            <img src="https://qcloudimg.tencent-cloud.cn/raw/90f1ef49218b43d7042bb05b1c0a3959.png" data-nonescope="true">
                                <p class="titlename">React Native SDK</p>
                <p style="color:#586376;">React Nativeフレームワークに基づいてパッケージ化されています。1セットのコードでモバイル端末のアプリをすばやく構築できます。</p>
                <a style="margin-left: 10px;" href="https://github.com/tencentyun/TRTCReactNative">GitHub</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/43298">統合ガイド</a>
								<a style="margin-left: 10px;" href="https://intl.cloud.tencent.com/document/product/647/43297">Demoを実行</a>
            </div>
        </div>
</div>



## バージョン比較
<table>
  <tr>
    <th width="100px" style="text-align:center">機能モジュール</th>
    <th width="100px" style="text-align:center">機能の詳細</th>
    <th width="100px" style="text-align:center">TRTC簡易版</th>
    <th width="100px" style="text-align:center">フル機能版</th>
  </tr>
    <tr>
    <td rowspan='2' style="text-align:center">ビデオ通話</td>
    <td style="text-align:center">2人通話</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">多人数会議</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">ライブストリーミングマイク接続</td>
    <td style="text-align:center">同じルームでのコラボ配信</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">ルームをを跨いだコラボ配信</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">基本的な顔補正</td>
    <td style="text-align:center">美白と肌磨き</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">カラーフィルター</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
    <tr>
    <td rowspan='2' style="text-align:center">ライブブロードキャストプッシュ</td>
    <td style="text-align:center">カメラプッシュ</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">スクリーンキャプチャプッシュ</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">ライブストリーミング再生</td>
    <td style="text-align:center">RTMPプロトコル</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP - FLV</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">オンデマンド再生</td>
    <td style="text-align:center">MP4フォーマット</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM暗号化</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">UGSV</td>
    <td style="text-align:center">レコーディングおよび撮影</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">トリミング・スプライシング</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">「TikTok」特殊効果</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">ビデオのアップロード</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td rowspan='4' style="text-align:center">インストールパッケージの増分</td>
    <td style="text-align:center">Android</td>
    <td style="text-align:center">armv7: 3.97M<br>arm64: 4.33M</td>
    <td style="text-align:center">armv7: 9.15M<br>arm64: 10.4M</td>
  </tr>
    <tr>
    <td style="text-align:center">iOS</td>
    <td style="text-align:center">arm64: 3.15M</td>
    <td style="text-align:center">N/A</td>
  </tr>
</table>

>! Windows SDKとMac OS SDKには、リアルタイムオーディオおよびビデオ(TRTC)、ライブブロードキャストプッシュ(TXLivePusher)、ライブブロードキャスト再生(TXLivePlayer)およびオンデマンド再生(TXVodPlayer)の4つの機能を備えており、ショート動画関連の機能は現時点ではサポートされていません。簡易版とフル機能版の区別はありません。

<script src="https://cdn-go.cn/aegis/aegis-sdk/latest/aegis.min.js"></script>
<script>
let aegis;
if(Aegis) {
    aegis = new Aegis({
        id: 'iHWefAYqlXjjlfAkpx',
        uin: document.cookie.replace(/(?:(?:^|.*;\s*)uin\s*\=\s*([^;]*).*$)|^.*$/, "$1")|| '',
        reportApiSpeed: false,
        reportAssetSpeed: false
    });
}
function reportEvent(options){ aegis && aegis.reportEvent(options); }
</script>
