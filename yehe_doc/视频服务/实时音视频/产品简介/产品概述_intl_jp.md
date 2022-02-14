
Tencent Real-Time Communication（TRTC）は、Tencentが長年にわたり蓄積したネットワークとオーディオビデオ技術をベースに、多人数のオーディオビデオ通話と低遅延インタラクティブライブストリーミングの、シナリオ化した2大ソリューションを提供し、Tencent Cloudのサービスを通じて開発者向けに開放します。これにより、開発者が低コスト、低遅延、高品質のインタラクティブなオーディオビデオソリューションを迅速に構築することを支援します。
- 多人数の音声ビデオ通話ソリューション
 Tencent Cloudのグローバルな専用線ネットワークに支えられ、全世界で相互通信が可能、さらに携帯電話やデスクトップなどの全プラットフォームをカバーするクライアントSDK およびクラウドAPIを提供します。ウェブページでも手軽に利用できます。
- 低遅延のインタラクティブライブストリーミングソリューション
 業界をリードするネットワークおよびオーディオビデオ技術の力と、Tencent Cloudの高品質なノードリソースを結合させ、開発者が、ラグ率がより低く、レイテンシー1秒未満のインタラクティブライブストリーミングを構築し、CDN 2.0時代に踏み出せるように支援をします。




## 製品アーキテクチャ
Tencent Real-Time Communication（TRTC）は、全プラットフォームでの相互通信による多人数のオーディオビデオ通話と低遅延でインタラクティブライブストリーミングのソリューションをメインに打ち出しています。ミニプログラム、Web、Android、iOS、Electron、Windows、macOSなどのプラットフォームのSDKを提供し、開発者がクイックインテグレーションを行い、Tencent Real-Time Communication（TRTC）クラウドサービスのバックエンドと連携できるようにしています。またTencent Cloudの様々な製品と連動させることで、TRTCとInstant Messaging（IM）、Cloud Streaming Services（CSS）、Video on Demand（VOD）などのクラウド製品の機能を同時に使用することができ、業務でのユースケースをより広げることが可能です。製品構成は下図のとおりです。
![](https://main.qcloudimg.com/raw/be1345a58328913f7dae524a4cc5e153.svg)

## サポートプラットフォーム
Tencent Real-Time Communicationは、**業界で真の全プラットフォーム相互通信を実現したソリューション**です。具体的なプラットフォームのサポートおよび開発環境要件は下表のとおりです。

<table>
<tr><th>プラットフォーム</th><th>開発環境要件</th></tr>
<tr>
<td>iOS</td>
<td>
  <li>iOS 9.0以上のiPhoneまたはiPadの実機をサポートしています</li>
  <li>Xcode 9.0+</li>
  <li>プロジェクトに有効な開発者の署名を設定済み</li>
</td>
</tr><tr>
<td>Android</td>
<td>
  <li>Android Studio 3.5+</li>
  <li>Android 4.1（SDK API Level 16）以上のシステムの使用を推奨します</li>
</td>
</tr><tr>
<td>Windows</td>
<td>
  <li>Windows 7以上のバージョンをサポートしています</li>
  <li>Visual Studio 2010以上のバージョン、Visual Studio 2015の使用を推奨します</li>
  <li>.Net Framework 4.0以上のバージョン</li>
</td>
</tr><tr>
<td>Mac OS</td>
<td>
  <li>Xcode 9.0+</li>
  <li>OS X10.10+のMacの実機</li>
  <li>プロジェクトに有効な開発者の署名を設定済み</li>
</td>
</tr><tr>
<td>Web</td>
<td>デスクトップ端末Chrome56+の使用を推奨、具体的な開発環境要件については、<a href="https://intl.cloud.tencent.com/document/product/647/35096">クイックインテグレーション(Web)</a>をご参照ください</td>
</tr><tr>
<td>Electron</td>
<td>
  <li>Windows 7以上のバージョン、Mac OS 10.10以上のバージョンをサポートしています</li>
  <li>Electron 4.0.0以上のバージョンをサポートしていますが、最新版のElectron SDKの使用を推奨します</li>
</td>
</tr><tr>
<td>WeChat Mini Program</td>
<td>
  <li>WeChat App iOS最低バージョン要件：7.0.9</li>
  <li>WeChat App Android最低バージョン要件：7.0.8</li>
  <li>ミニプログラムベースライブラリ最低バージョン要件：2.10.0</li>
  <li>ミニプログラム開発者ツールはネーティブコンポーネント（&lt;live-pusher&gt;および&lt;live-player&gt;タグ）をサポートしていないため、実機で体験を実行する必要があります</li>
</td>
</tr><tr>
<td>Flutter</td>
<td>iOS端末：
  <li>iOS 9.0以上のiPhoneまたはiPadの実機をサポートしています</li>
  <li>Xcode 9.0+</li>
  <li>プロジェクトに有効な開発者の署名を設定済み</li>Android端末：<li>Android Studio 3.5+</li>
  <li>Android 4.1（SDK API Level 16）以上のシステムの使用を推奨します</li>
</td>
</tr></table>

[](id:safe)
## セキュリティコンプライアンス
コンプライアンスはTencent Cloud TRTCの発展の基本です。Tencent Cloud TRTCは各国および業界のコンプライアンス要件を遵守し、提供するサービスの**セキュリティ、コンプライアンス、可用性、機密保持およびプライバシー**を保証するほか、TRTCを使用するお客様に関連のサポートを提供することで、**企業とその顧客の様々なコンプライアンス監督管理のニーズを満たし、会社と顧客による監査業務への重複投資を削減し、監査と管理の効率を向上させます。**

**TRTCは一連のSOC報告書（SOC 1、SOC 2、SOC 3を含む）、サイバーセキュリティ等級保護2.0、ISOシリーズ認証（ISO 9001、ISO 20000を含む）を取得済みです。**
![](https://main.qcloudimg.com/raw/3cd618fd25165dde224dd0c3781cf129.png)
