
Tencent Real-Time Communication（TRTC）はTencentが21年間に蓄積したネットワーク及び音声ビデオ技術を、多人数の音声ビデオ通話と低遅延のインタラクティブライブストリーミングソリューションの形で、Tencent Cloudサービスを通じてお客様に開放します。低コスト、低遅延、高品質の音声ビデオのインタラクティブソリューションの構築が迅速的に開発できることを目的にお客様に提供します。
- 多人数の音声ビデオ通話ソリューション
 Tencent Cloudのグローバルな専用線ネットワークに支えられ、グローバルなインフラによるクロスリージョン接続能力及び、PC、モバイルの全プラットフォームをカバーする SDKを提供します。また、Wechat、QQ、Wechat Mini Program、Web サイトで簡単に利用でき、すべてのアプリケーションに「音声ビデオ通話」能力を付与することができます。
- 低遅延のインタラクティブライブストリーミングソリューション
 業界最先端のネットワーク及び音声ビデオ技術であり、Tencent Cloudの高品質のノードリソースにより、開発者により低いラグ率、1秒未満のレイテンシーのインタラクティブライブストリーミングサービスを構築することを支援します。ライブストリーミングをCDN 2.0時代に邁進させます。


## 製品アーキテクチャ
TRTCは、全プラットフォームでの相互接続による多人数の音声ビデオ通話と低遅延のインタラクティブライブストリーミングソリューションをメインに打ち出しています。WeChatミニプログラム、Web、Android、iOS、Electron、Windows、macOS、Linux等のプラットフォームのSDKを提供し、開発者が素早く統合し、TRTCクラウドサービスのバックエンドと連携できるようにしています。またTencent Cloudの様々な製品と連動させることで、TRTCとInstant Messaging（IM）、Live Video Broadcasting（LVB）、Video on Demand（VOD）等のクラウド製品の機能を一緒に使用することができ、業務でのユースケースをより広げることが可能です。製品アーキテクチャは下図の通りとなります。
![](https://main.qcloudimg.com/raw/be1345a58328913f7dae524a4cc5e153.svg)

## プラットフォームのサポート
TRTCは、**業界で真の全プラットフォームの相互接続を実現したソリューション**です。具体的なサポートされているプラ​​ットフォームおよび開発環境要件は下表の通りとなります。　

| プラットフォーム       | 開発環境要件                                                 | 
| :--------- | :----------------------------------------------------------- |
| iOS        |<li>iOS 9.0 以上のバージョンのiPhone または iPadをサポート。 </li><li>Xcode 9.0+</li><li>プログラムに有効な開発者署名を設定済み。</li> |
| Android    | <li>Android Studio 3.5+</li><li>Android 4.1（SDK API Level 16）以上のシステムを使用することを推奨。</li> |
| Windows    | <li>Windows 7 以上のバージョンをサポート。</li><li>Visual Studio 2010以上のバージョンは、Visual Studio 2015の使用を推奨。</li><li>.Net Framework 4.0以上のバージョン</li> |
| Mac OS     | <li>Xcode 9.0+</li><li>OS X10.10+ の Macマシン</li><li>プログラムに有効な開発者署名を設定済み。</li> |
| Web | デスクトップ版 Chrome 52+ の使用を推奨。 |
| Electron   | <li>Windows 7 以上、Mac OS 10.10 以上のバージョンをサポート。</li><li>Electron 4.0.0より上のバージョンをサポート。但し最新版のElectron SDKの使用を推奨。</li> |
| WeChat Mini Program | <li>WeChat App iOS版 最低バージョン要件：7.0.9</li><li>WeChat App Android版 最低バージョン要件：7.0.8</li><li>WeChat Mini Program 基本ライブラリ 最低バージョン要件：2.10.0</li><li>WeChat Mini Programの開発者ツールがネイティブコンポーネント（&lt;live-pusher&gt;  &lt;live-player&gt; タグ）をサポートしていないため、実際のデバイスでの運用体験が必要。</li> |
| Linux      | <li>CentOS 7.6 Server版の使用を推奨。組み込みまたはデスクトップ版 Linux ディストリビューションは未サポート。</li><li>Linux SDKはサーバープラットフォームのデプロイのみサポート。</li> |

>
- Linux用のSDKおよびセットのDemoソースコードのダウンロード は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してください。その他プラットフォーム用のSDK およびセットのDemoソースコードのダウンロードは、 [SDK ダウンロード](https://intl.cloud.tencent.com/document/product/647/34615)をご参照ください。
- LinuxプラットフォームのDemo体験は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category)してお申し込みください。その他プラットフォームのDemo体験は、[Demo 体験](https://intl.cloud.tencent.com/document/product/647/35076)をご参照ください。
