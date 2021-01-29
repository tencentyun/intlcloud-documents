このドキュメントでは、次の手順でTencent Cloud TRTC SDK for iOSをプロジェクトにすばやく統合する方法について説明します。

## 開発環境要件
- Xcode 9.0+。
- iOS 9.0 以上のiPhoneまたはiPad。
- プロジェクトには有効な開発者署名があります。

## TRTC SDKの統合
CocoaPodsの自動ロード方法を選択、使用するか、またはまずSDKをダウンロードしてから現在のプロジェクトにインポートします。

### CocoaPods
#### 1.  CocoaPodsのインストール
ターミナルウィンドウで以下のコマンド（事前にmacOSにRuby環境をインストールする必要があります）を入力します。
```
sudo gem install cocoapods
```

#### 2. Podfileファイルの新規作成
プロジェクトのあるパスに移動し、次のコマンドを入力すると、Podfileファイルがプロジェクトパスに表示されます。
```
pod init
```

#### 3. Podfileファイルの編集
Podfileファイルを編集し、ニーズに応じて適切なSDKバージョンを選択します。
- [簡易版](https://intl.cloud.tencent.com/document/product/647/34615)：インストールパケットの容量は最小ですが、 TRTCおよびCDN 再生（TXLivePlayer）機能のみサポートしています。
```
  platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_TRTC', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_TRTC.podspec'
  end
```

- [プロフェッショナルバージョン](https://intl.cloud.tencent.com/document/product/647/34615)： TRTCのほか、 RTMP プッシュ（TXLivePusher）、CDN 再生（TXLivePlayer）、VOD再生（TXVodPlayer）およびショート動画（UGSV）などの多機能があります。
```
  platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_Professional', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
```

CocoaPod公式ソースも使用できますが、ダウンロード速度は遅くなることがあります。
```
   platform :ios, '8.0'
   source 'https://github.com/CocoaPods/Specs.git'
   
   target 'App' do
   pod 'TXLiteAVSDK_TRTC'
   end
```

#### 4. SDKの更新及びインストール
ターミナルウィンドウで以下のコマンドを入力し、ローカルライブラリファイルを更新し、TRTC SDKをインストールします。
```
pod install
```
または以下のコマンドを使用しローカルライブラリバージョンを更新します。
```
pod update
```

podコマンドが実行されると、SDKに統合された.xcworkspaceサフィックスが付いたプロジェクトファイルが作成され、ダブルクリックして開くことができます。
>? 必要な依存ライブラリ**Accelerate.framework**を手動で追加する必要があります。

### 手動統合
1.  [TRTC - SDK ](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/SDK) をダウンロードして解凍します。
2. Xcode プロジェクトを開き、実行するターゲットを選択して、**Build Phases** 項目を選択します。
 ![](https://main.qcloudimg.com/raw/85509cc24bd958e7b9978e11937597c5.png)
3.  **Link Binary with Libraries** 項目をクリックして展開し、下辺の“+”のアイコンをクリックして依存ライブラリを追加します。
 ![](https://main.qcloudimg.com/raw/54be71cc14ec79ce642216612544a8a4.png)
4. ダウンロードしたTRTC SDTRTC SDK Frameworkおよび必要とする依存ライブラリ**libc++** 、**Accelerate.framework**を順次追加します。
 ![](https://main.qcloudimg.com/raw/2fa94b7f81c7e9c4ac09733782e79c10.png)


## カメラおよびマイクの使用権限の付与
SDKのオーディオ/ビデオ機能を使用して、マイクおよびカメラの使用権限を付与する必要があります。AppのInfo.plistで以下の2項を追加して、システム権限付与ダイアログをポップアップするときのマイクおよびカメラのメッセージ情報にそれぞれ対応します。
- **Privacy - Microphone Usage Description**、かつマイクの使用目的のプロンプトメッセージを記入します。
- **Privacy - Camera Usage Description**，かつカメラの使用目的のプロンプトメッセージを記入します。

![](https://main.qcloudimg.com/raw/54cc6989a8225700ff57494cba819c7b.jpg)


##  TRTC SDKのインポート
プロジェクトコードでSDKを使用する方法は2つあります。
- 方法一：SDK APIを使用する必要があるプロジェクトのファイルにインポートモジュールを追加します。
```
@import TXLiteAVSDK_TRTC;
```

- 方法二：SDK APIを使用する必要があるプロジェクトのファイルに特定のヘッダーファイルをインポートします。
```
#import TXLiteAVSDK_TRTC/TRTCCloud.h
```

## よくあるご質問
### 1. TRTC SDK はバックグラウンドでの実行をサポートしていますか？
サポートしています。以前の関連機能を実行するためにバックグラウンドに入る必要がある場合は、現在のプロジェクトを選択できます。 **Capabilities** の**Background Modes** を**ON**に設定して、 **Audio，AirPlay and Picture in Picture** にチェックを入れます。下図に示すとおりです。　
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)
