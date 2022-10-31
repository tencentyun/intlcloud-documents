ここではSDKをプロジェクトにインポートする方法をご紹介します。
![](https://qcloudimg.tencent-cloud.cn/raw/f85f7ee54d462d85290fc6f50e5ed96a.png)
## 開発環境要件
- Xcode 9.0+。 
- iOS 9.0以上のiPhoneまたはiPadの実機。
- プロジェクトには有効な開発者の署名を設定。

## 第1段階：SDKのインポート
CocoaPodsソリューションを使用するか、またはまずSDKをローカルにダウンロードしてから手動で現在のプロジェクトにインポートするかを選択できます。

### 方法1：CocoaPodsを使用
1. **CocoaPodsのインストール**
ターミナルポートに以下のコマンド（事前にMacにRuby環境をインストールする必要があります）を入力します。
```
sudo gem install cocoapods
```
2. **Podfileファイルの新規作成**
項目のあるパスに入り、以下のコマンドラインを入力すると項目パスに一つのPodfileファイルが現れます。
```
pod init
```
3. **Podfileファイルの編集**
プロジェクトのニーズに応じて適切なバージョンを選択し、Podfileファイルを編集します。
  - **オプション1：TRTC簡易版**
インストールパッケージのボリューム増分が最も小さく、Tencent Real-Time Communication（TRTC）とライブストリーミングプレーヤー（TXLivePlayer）という2つの機能だけをサポートしています。このバージョンを選択した場合は、次の方法でPodfileファイルの編集を行ってください。
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_TRTC', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_TRTC.podspec'
  end
```
   - **オプション2：プロフェッショナル版（Professional）**
Tencent Real-Time Communication（TRTC）、ライブストリーミングプレーヤー（TXLivePlayer）、RTMPプッシュ（TXLivePusher）、VODプレーヤー（TXVodPlayer）およびショートビデオレコーディングおよび編集（UGSV）などの多くの機能が含まれます。このバージョンを選択した場合は、次の方法でPodfileファイルの編集を行ってください。
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_Professional', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
```
4. **SDKの更新およびインストール**
  - ターミナルポートに以下のコマンドを入力し、ローカルライブラリファイルを更新し、SDKをインストールします。
```
pod install
```
   - または以下のコマンドを使用しローカルライブラリバージョンを更新します。
```
pod update
```
podコマンドが実行されると、SDKに統合された.xcworkspaceサフィックスが付いたプロジェクトファイルが作成され、ダブルクリックして開くことができます。

### 方法2：SDKのダウンロードと手動でのインポート
1. [SDK](https://intl.cloud.tencent.com/document/product/647/34615)をダウンロードしてローカルに解凍します。
2. Xcodeプロジェクトを開き、動作させたいtargetを選択し、**Build Phases** 項目を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/f57f1da3efefefe98a4b8c03c688fd17.png)
3. **Link Binary with Libraries** をクリックして展開し、下辺の“+”のアイコンをクリックして依存ライブラリを追加します。
![](https://qcloudimg.tencent-cloud.cn/raw/25faf435d56c7c7df1f944a536dd8869.png)
4. ダウンロードした`TXLiteAVSDK_TRTC.Framework`（または`TXLiteAVSDK_Professional.Framework`）、`TXFFmpeg.xcframework`、`TXSoundTouch.xcframework`、およびその必要な依存ライブラリ`GLKit.framework`、`AssetsLibrary.framework`、`SystemConfiguration.framework`、`libsqlite3.0.tbd`、`CoreTelephony.framework`、`AVFoundation.framework`、`OpenGLES.framework`、`Accelerate.framework`、`MetalKit.framework`、`libresolv.tbd`、`MobileCoreServices.framework`、`libc++.tbd`、`CoreMedia.framework`を順に追加します。
![](https://qcloudimg.tencent-cloud.cn/raw/8f4b4dc4f794cd0bf4159cd5b0c2a507.png)
5. **General**をクリックして**Frameworks,Libraries,and Embedded Content**を選択し、TXLiteAVSDK_TRTC.frameworkに必要な動的ライブラリ**TXFFmpeg.xcframework**、**TXSoundTouch.xcframework**がすでに追加されているか、**Embed & Sign**が正しく選択されているかを確認し、まだであれば一番下の“**+**”のアイコンをクリックして順に追加します。
![](https://qcloudimg.tencent-cloud.cn/raw/a159c5fb799cf50611387bdae7275863.png)

## 第2段階：App権限の設定
1. SDKの提供するオーディオビデオ機能を使用したい場合は、Appにマイクとカメラの使用権限を承認する必要があります。AppのInfo.plistに次の2項目を追加します。これらはそれぞれマイクとカメラについて、システムから権限承認ダイアログボックスがポップアップされる際に表示される情報に対応します。
	- **Privacy - Microphone Usage Description**、かつマイクの使用目的のメッセージを記入します。
	- **Privacy - Camera Usage Description**、かつカメラの使用目的のメッセージを入力します。
![](https://main.qcloudimg.com/raw/7c483aae65f64cd2bf35b55d9c896a52.png)
2. Appがバックエンドに入っても関連の機能を実行するようにしたい場合は、下図に示すように、XCodeで現在のプロジェクトを選択し、**Capabilities**で設定項目**Background Modes** を**ON**に設定し、**Audio，AirPlay and Picture in Picture** にチェックを入れます。
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

## 第3段階：プロジェクトにおけるSDKの参照
第1段階のインポートと第2段階のデバイスへの権限承認が完了すると、SDKの提供するインターフェースAPIをプロジェクトで参照できるようになります。

### Objective-Cまたは Swiftインターフェースによる参照
Objective-CまたはSwiftコードの中でSDKを使用する方法は2つあります。
- **モジュールの引用**：プロジェクトでSDK APIを使用する必要のあるファイルにモジュール参照を追加します。
```
@import TXLiteAVSDK_TRTC;
```
- **ヘッダーファイルの引用**：プロジェクトでSDK APIを使用する必要のあるファイルに特定のヘッダーファイルを導入します。
```
#import "TXLiteAVSDK_TRTC/TRTCCloud.h"
```

>? Objective-Cインターフェースの使用方法については、 [iOS&Mac APIの概要](https://intl.cloud.tencent.com/document/product/647/35119)をご参照ください。

[](id:using_cpp)
### C++インターフェースによる参照(オプション)
プロジェクトがQTまたはElectronのようなクロスプラットフォームフレームワークによってSDKを参照している場合は、`TXLiteAVSDK_TRTC.framework/Headers/cpp_interface`ディレクトリ下のヘッダーファイルを参照してください。
```
#include "TXLiteAVSDK_TRTC/cpp_interface/ITRTCCloud.h"
```

>? C++インターフェースの使用方法については、 [全プラットフォーム（C++）APIの概要](https://intl.cloud.tencent.com/document/product/647/35131)をご参照ください。

