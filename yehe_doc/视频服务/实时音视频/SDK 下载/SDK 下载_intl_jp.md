TRTCは、Tencent CloudのLiteAVシリーズ製品の1つです。LiteAVシステムのSDKはすべて同じ基本モジュールを使用するため、プロジェクトに2つ以上のLiteAVシステムSDKを同時に統合すると、シンボルの重複（symbol duplicate）という問題が発生します。そこで、さまざまな製品機能を統合した**簡易版（TRTC）**、**プロフェッショナル版（Professional）*および**エンタープライズ版（Enterprise）**を提供しています。実際のビジネスニーズに応じて、さまざまなバージョンを選択することができます。


<h2 id="TRTC">簡易版(TRTC)</h2> 
簡易版の機能はTRTCとライブストリーミングの再生(TXLivePlayer)という2つだけで、アプリのインストールパッケージのボリューム増分は最小限に留まり、TRTC関連機能のみを使用するお客様に適しています。

<table>
   <tr>
      <th width="0px" style="text-align:center">属するプラットフォーム</td>
      <th width="0px" style="text-align:center">ZIPパッケージ</td>
      <th width="0px"  style="text-align:center">Github</td>
      <th width="0px" style="text-align:center">Gitee</td>
      <th width="0px" style="text-align:center">Demo操作手順</td>
      <th width="0px" style="text-align:center">SDK統合ガイド</td>
      <th width="0px" style="text-align:center">インストールパッケージの増分</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_ios_trtc") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center">2.9M(arm64)</td>
   </tr>
     <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_android_trtc") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center">jar: 820K<br> so(armv7): 4.8M<br>so(arm64): 5.7M</td>
   </tr>
     <tr>
      <td style="text-align:center">Windows(C++)  </td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_cplusplus_trtc") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35085">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35095">DOC</a></td>
      <td style="text-align:center">12.7M(C++ x86)<br>15.6M(C++ x64)</td>
   </tr>
     <tr>
      <td style="text-align:center">Windows(C#) </td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_csharp_trtc") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35085">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35095">DOC</a></td>
      <td style="text-align:center">13.8M(C# x64)<br>13.3M(C# x86)</td>
   </tr>
     <tr>
      <td style="text-align:center">Mac</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_mac_trtc") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35094">DOC</a></td>
      <td style="text-align:center">2.05M(arm64)</td>
   </tr>
     <tr>
      <td style="text-align:center">デスクトップブラウザ</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_web_trtc") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/H5_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35607">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35096">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
   <tr>
      <td style="text-align:center">Electron  </td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_wxmini_trtc") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Electron_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/TRTCSDK">Github</a></td>
      <td style="text-align:center"><a href="https://gitee.com/cloudtencent/TRTCSDK">Gitee</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35089">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35097">DOC</a></td>
      <td style="text-align:center">N/A</td>
   </tr>
	    <tr>
      <td style="text-align:center">Flutter</td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a href="https://github.com/c1avie/trtc_demo">Github</a></td>
      <td style="text-align:center">N/A</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/39243">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35098">DOC</a></td>
      <td style="text-align:center">13M</td>
   </tr>
</table>

>? 
> - SDKによるインストールパッケージのボリューム増量を削減する必要がある場合は、[インストールパッケージのボリューム削減方法](https://intl.cloud.tencent.com/document/product/647/35165) をご参照ください。
> - 公式アカウントをよく読んで、SDKのバージョン更新および最新の技術的な動向について確認してください。
> ![](https://main.qcloudimg.com/raw/d8a8c8c130ef7799feff6efbc0260ea2.jpg)


<h2 id="Professional">プロフェッショナル版（Professional）</h2>

プロフェッショナル版には[モバイルライブストリーミング](https://intl.cloud.tencent.com/product/mlvb)および[UGSV](https://intl.cloud.tencent.com/product/ugsv) などを含む、TRTCを包含した複数のオーディオ・ビデオ関連のコア機能が統合され、基盤モジュールを高度に再利用することにより、プロフェッショナル版の容量増加は同時に2つの独立したSDKを統合させた場合よりも小さくなります。さらにシンボル重複（symbol duplicate）の問題も回避できます。

<table>
   <tr>
      <th width="0px" style="text-align:center">属するプラットフォーム</td>
      <th width="0px" style="text-align:center">ZIPパッケージ</td>
      <th width="0px"  style="text-align:center">Github</td>
      <th width="0px" style="text-align:center">64ビットのサポート</td>      
      <th width="0px" style="text-align:center">Demo操作手順</td>
      <th width="0px" style="text-align:center">SDK統合ガイド</td>
      <th width="0px" style="text-align:center">インストールパッケージの増分</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_ios_professional") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_Professional_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_iOS">Github</a></td>
      <td style="text-align:center">サポート</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center">4.08M(arm64)</td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_android_professional") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_Professional_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center"><a href="https://github.com/tencentyun/LiteAVProfessional_Android">Github</a></td>
      <td style="text-align:center">サポート</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center">jar: 1.5M<br> so(armeabi): 6.5M<br> so(armv7): 6.1M<br>so(arm64): 7.3M</td>
   </tr>
</table>

>? 
>- Windows版とMac版のSDKは現在1つしかバージョンがなく、簡易版、プロフェッショナル版とエンタープライズ版の違いはありません。
>- LiteAVシステムのSDKはすべて同じ基本モジュールを使用するため、プロジェクトにLiteAVシステムの2つ以上のSDKを同時に統合すると、シンボルの衝突(symbol duplicate)というトラブルが発生します。これを解決する方法は、1つのプロフェッショナル版のLiteAVSDKのみを統合することです。
>- SDKによるインストールパッケージのボリューム増量を削減する必要がある場合は、[インストールパッケージのボリューム削減方法](https://intl.cloud.tencent.com/document/product/647/35165) をご参照ください。


<h2 id="Enterprise">エンタープライズ版(Enterprise)</h2>

エンタープライズ版には、プロフェッショナル版のすべての機能が含まれているほか、AI特殊効果コンポーネントが統合され、デカ目、小顔、美肌加工及びキャラクターエフェクトなどの機能もサポートしています。実行するには、ダウンロード後に圧縮解凍パスワードとライセンスを取得する必要があります。解凍コードとライセンスについては、Tencent Cloudビジネスまでお問い合わせください。

<table>
   <tr>
      <th width="0px" style="text-align:center">属するプラットフォーム</td>
      <th width="0px" style="text-align:center">ZIPパッケージ</td>
      <th width="0px" style="text-align:center">64ビットのサポート</td>
      <th width="0px" style="text-align:center">Demo操作手順</td>
      <th width="0px" style="text-align:center">SDK統合ガイド</td>
      <th width="0px" style="text-align:center">インストールパッケージの増分</td>
   </tr>
   <tr>
      <td style="text-align:center">iOS</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_ios_enterprise") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_Enterprise_iOS_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center">サポート</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35086">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35092">DOC</a></td>
      <td style="text-align:center"> 6.15M(arm64)</td>
   </tr>
   <tr>
      <td style="text-align:center">Android</td>
      <td style="text-align:center"><a onclick=MtaH5.clickStat("trtc_sdk_download_android_enterprise") href="https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_Enterprise_Android_latest.zip">DOWNLOAD</a></td>
      <td style="text-align:center">サポート</td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35084">DOC</a></td>
      <td style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/35093">DOC</a></td>
      <td style="text-align:center"> jar: 2.3M<br>so(armeabi): 20.4M</td>
   </tr>
</table>

>?
>- Windows版とMac版のSDKには現在、AIフェイスエフェクトコンポーネントはなく、簡易版・プロフェッショナル版・エンタープライズ版の違いはありません。
>- SDKによるインストールパッケージのボリューム増量を削減する必要がある場合は、[インストールパッケージのボリューム削減方法](https://intl.cloud.tencent.com/document/product/647/35165) をご参照ください。


## 各バージョン差対照表

![](https://main.qcloudimg.com/raw/d3c876e8d751709e1df52faf4c0bf012.jpg)

<table>
  <tr>
    <th width="100px" style="text-align:center">機能モジュール</th>
    <th width="100px" style="text-align:center">機能項目</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1071/38150">ライブストリーミング簡易版</a><br>LiteAV_Smart</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/1069/37914">UGSV版</a><br>LiteAV_UGC</th>
    <th width="100px" style="text-align:center"><a href="https://intl.cloud.tencent.com/document/product/647/34615">TRTC版</a><br>LiteAV_TRTC</th>
    <th width="100px" style="text-align:center"><a href="https://cloud.tencent.com/document/product/881/20205">プレーヤー版</a><br>LiteAV_Player</th>
    <th width="100px" style="text-align:center"><a href="#Professional">プロフェッショナル版</a><br>Professional</th>
    <th width="100px" style="text-align:center"><a href="#Enterprise">エンタープライズ版</a><br>Enterprise</th>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">CSSプッシュ</td>
    <td style="text-align:center">カメラプッシュ</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">スクリーンキャプチャプッシュ</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">ライブストリーミング再生</td>
    <td style="text-align:center">RTMPプロトコル</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HTTP - FLV</td>
    <td style="text-align:center">&#10003;</td>
     <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='3' style="text-align:center">オンデマンド再生</td>
    <td style="text-align:center">MP4フォーマット</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">HLS(m3u8)</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
   <tr>
    <td style="text-align:center">DRM暗号化</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">美顔フィルター</td>
    <td style="text-align:center">基本の美顔</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">基本フィルター</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">ライブストリーミングマイク接続</td>
    <td style="text-align:center">マイク接続インタラクション</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">ルーム間PK</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='2' style="text-align:center">ビデオ通話</td>
    <td style="text-align:center">2人通話</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">ビデオミーティング</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">UGSV</td>
    <td style="text-align:center">レコーディングおよび撮影</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">トリミング・スプライシング</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">「TikTok」特殊効果</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">ビデオのアップロード</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td rowspan='4' style="text-align:center">AI美顔特殊効果</td>
    <td style="text-align:center">デカ目・小顔</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">シャープな顎・鼻筋加工</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">キャラクターエフェクト</td>
   <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
  </tr>
  <tr>
    <td style="text-align:center">クロマキーのトリミング</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">-</td>
    <td style="text-align:center">&#10003;</td>
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


