このドキュメントでは、SDKのプロジェクトへのインポート方法を紹介します：
![](https://qcloudimg.tencent-cloud.cn/raw/956dded61564c3a29ea8e93238d9a4e1.png)

## 開発環境要件
- Xcode 9.0+。 
- iOS 9.0 以上のiPhone または iPad 。
- プロジェクトに有効な開発者の署名が設定してあること。

## 手順1：SDKのインポート
CocoaPodsスキームを使用するか、SDKをローカルにダウンロードして、現在のプロジェクトに手動でインポートするかを選択できます。

### スキーム1：CocoaPodsの使用
1. **CocoaPodsのインストール**
端末のウィンドウに次のコマンドを入力します（事前にMac にRuby環境をインストールしておく必要があります ）：
```
sudo gem install cocoapods
```
2. **Podfileファイルの作成**
プロジェクトが存在するパスに入り、次のコマンドラインを入力するとプロジェクトパスの下にPodfile ファイルが現れます。
```
pod init
```
3. **Podfileファイルの編集**
プロジェクトのニーズに応じて適切なバージョンを選択し、Podfileを編集します：
  - **オプション1：TRTCライト版**
インストールパッケージの容量増加は最小ですが、Tencent Real-Time Communication (TRTC)とライブストリーミングプレーヤー(TXLivePlayer)の2つの機能のみをサポートします。このバージョンを選択する場合は、Podfileを次のように編集してください：
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_TRTC', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_TRTC.podspec'
  end
```
  - **オプション2：プロフェッショナル版**
Tencent Real-Time Communication TRTC)、ライブストリーミングプレーヤー(TXLivePlayer)、RTMPプッシュ(TXLivePusher)、VODプレーヤー(TXVodPlayer)およびショート動画のレコーディングと編集(UGSV)など、多くの機能が含まれています。このバージョンを選択する場合は、Podfileを次のように編集してください：
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_Professional', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
```
4. **SDKの更新およびインストール**
    - 端末のウィンドウに次のコマンドを入力してローカルライブラリファイルを更新し、SDKをインストールします。
```
pod install
```
  - または次のコマンドを使用してローカルライブラリのバージョンを更新します。
```
pod update
```
pod コマンドの実行が完了すると、SDKが統合された.xcworkspace という拡張子のプログラムファイルが生成されますので、これをダブルクリックして開きます。

### 方法2：SDKのダウンロードと手動インポート
1. [SDK](https://intl.cloud.tencent.com/document/product/647/34615)をダウンロードし、ローカルに解凍して開きます。
2. お客様のXcodeのプロジェクトを開き、動作させたいtargetを選択して、**Build Phases**の項目を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/f57f1da3efefefe98a4b8c03c688fd17.png)
3. **Link Binary with Libraries**の項目をクリックして展開し、一番下の「+」記号のアイコンをクリックして依存ライブラリを追加します。
![](https://qcloudimg.tencent-cloud.cn/raw/25faf435d56c7c7df1f944a536dd8869.png)
4. ダウンロードした**TXLiteAVSDK_TRTC.Framework**（または**TXLiteAVSDK_Professional.Framework**）および必要な依存ライブラリ**libc++.tbd**、**libresolv.tbd**、**Accelerate.framework**、**MetalKit.framework**、**MobileCoreServices.framework**、**SystemConfiguration.framework**、**ReplayKit.framework**、**CoreTelephony.framework**を順に追加します。
![](https://qcloudimg.tencent-cloud.cn/raw/8f4b4dc4f794cd0bf4159cd5b0c2a507.png)
5. **General**をクリックし、**Frameworks,Libraries,and Embedded Content**を選択します。一番下の「+」記号のアイコンをクリックして順にTXLiteAVSDK_TRTC.frameworkに必要なダイナミックライブラリ**TXFFmpeg.xcframework**、**TXSoundTouch.xcframework**を追加し、**Embed & Sign**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/a159c5fb799cf50611387bdae7275863.png)

## 手順2：App権限の構成
1. SDKのオーディオビデオ機能を使用するには、Appにマイクとカメラの使用権限を許可する必要がありますので、AppのInfo.plistの中に次の2項目を追加します。それぞれマイクとカメラに対応し、システムが使用許可のダイヤログボックスをポップアップするときに表示される情報となります。
- **Privacy - Microphone Usage Description**、さらにマイク使用目的のプロンプトを記入します。
- **Privacy - Camera Usage Description**、さらにカメラ使用目的のプロンプトを記入します。

![](https://main.qcloudimg.com/raw/7c483aae65f64cd2bf35b55d9c896a52.png)

2. Appがバックグラウンドに入っても、依然として関連機能が動作するようにしたい場合は、XCodeで現在のプログラムのプロジェクトを選択し、**Capabilities**の下の**Background Modes**の設定を**ON**にして、**Audio、AirPlay and Picture in Picture**にチェックを入れます。次の図のとおりです：
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

## 手順3：プロジェクトへのSDKのインポート
手順1のインポートと手順2のデバイス権限の承認を完了すると、プロジェクトへSDKにより提供されているAPIを参照できます。

### Objective-CまたはSwiftインターフェースによる参照
Objective-CまたはSwiftコードの中でSDKを使用する方式は2種類あります：
- **コンポーネントの引用**：プロジェクトのSDK APIを使用したいファイルの中に、コンポーネントを追加して引用します。
```
@import TXLiteAVSDK_TRTC;
```
- **ヘッダーファイルの引用**：プロジェクトのSDK APIを使用したいファイルの中に、具体的なヘッダーファイルをインポートします。
```
#import TXLiteAVSDK_TRTC/TRTCCloud.h
```

>? Objective-Cインターフェースの使用方法については、[iOS&Mac APIの概要](https://intl.cloud.tencent.com/document/product/647/35119)をご参照ください。

[](id:using_cpp)
### C++インターフェースによる参照（オプション）
プロジェクトがQTやElectronなどのクロスプラットフォームフレームワークを介してSDKを導入する場合は、`TXLiteAVSDK_TRTC.framework/Headers/cpp_interface`ディレクトリのヘッダーファイルを参照してください：
```
#include TXLiteAVSDK_TRTC/cpp_interface/ITRTCCloud.h
```

>?  C++ インターフェースの使用方法については、 [全プラットフォーム（C++）APIの概要](https://intl.cloud.tencent.com/document/product/647/35131)をご参照ください。
