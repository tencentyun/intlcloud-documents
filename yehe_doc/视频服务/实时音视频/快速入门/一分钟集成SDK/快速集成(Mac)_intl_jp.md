このドキュメントでは、次の手順で、Tencent Cloud TRTC SDK for macOSをプロジェクトにすばやく統合する方法について説明します。


## 開発環境要件
- Xcode 9.0+。
- OS X10.10+ の Mac の実機。
- プロジェクトには有効な開発者署名があります。

## TRTC SDKの統合
CocoaPods自動ロード方法を選択、使用するか、またはまず手動でSDKをダウンロードしてから現在のプロジェクトにインポートします。

### CocoaPods
#### 1.  CocoaPodsのインストール
ターミナルウィンドウで以下のコマンド（事前にmacOSにRuby環境をインストールする必要があります）を入力します。
```
sudo gem install cocoapods
```

#### 2. Podfileファイルの新規作成
項目のあるパスに入り、以下のコマンドを入力すると、Podfileファイルがプロジェクトパスに表示されます。
```
pod init
```

#### 3. Podfileファイルの編集
Podfileファイルの編集には、以下の2種類の設定方法があります。
- 方法一：Tencent Cloud　LiteAV SDK の podパスを使用します。

```
	platform :osx, '10.10'

	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_TRTC_Mac.podspec'
	end
```

- 方法二：CocoaPod公式ソースを使用し、バージョン番号の選択をサポートします。

```
	platform :osx, '10.10'
	source 'https://github.com/CocoaPods/Specs.git'

	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac'
	end
```

#### 4. SDKのインストールと更新
ターミナルウィンドウで以下のコマンドを入力しTRTC SDKをインストールします：
```
pod install
```
または以下のコマンドを実行してローカルライブラリバージョンを更新します。
```
pod update
```

podコマンドが実行されると、SDKに統合された.xcworkspaceサフィックスが付いたプロジェクトファイルが生成され、ダブルクリックして開くことができます。

### 手動統合
1.  [TRTC-SDK ](https://github.com/tencentyun/TRTCSDK/tree/master/Mac) のmacOSバージョンをダウンロードします。

2. Xcode プロジェクトを開き、第一手順でダウンロードした framework をプロジェクトにインポートします。

3. 実行するターゲットを選択し、 Build Phases 項目を選択します。
![](https://main.qcloudimg.com/raw/b5097f8ac4cbaa5044d92b2a96ea2b9e.jpg)

4.  **Link Binary with Libraries** 項目をクリックして展開し、下辺の + のアイコンをクリックして依存ライブラリを追加します。
![](https://main.qcloudimg.com/raw/17046154417930f9d31b6452782df55d.jpg)

5. ダウンロードした SDK Framework および必要な依存ライブラリを順次追加します：`AudioUnit.framework`、`libc++.tbd` および `Accelerate.framework`。  
    
追加後は、下図に示すとおりです。
![](https://main.qcloudimg.com/raw/7bddb832347a971f3e69238480fa3e8d.jpg)

## カメラおよびマイクの使用権限の付与
SDKのオーディオ/ビデオ機能を使用して、マイクおよびカメラの使用権限を付与する必要があります。AppのInfo.plistで以下の2項を追加して、システム権限付与ダイアログをポップアップするときのマイクおよびカメラのプロンプトメッセージにそれぞれ対応します。
- **Privacy - Microphone Usage Description**、かつマイクの使用目的のプロンプトメッセージを記入します。
- **Privacy - Camera Usage Description**、かつカメラの使用目的のプロンプトメッセージを記入します。
下図に示すとおり：
![](https://main.qcloudimg.com/raw/ce02c335f1a6413fb37adb0ed20a9603.png)

 App が **App Sandbox** または **Hardened Runtime**を起動した場合は、 `Network`、`Camera` および `Audio Input`のこれらいくつかのオプションにチェックを入れる必要があります。
- App Sandbox 設定は下図に示すとおり。
![](https://main.qcloudimg.com/raw/b77d2ab814e6e14e8bed17efdcbee1a6.png)
- Hardened Runtime 設定は下図に示すとおり。
![](https://main.qcloudimg.com/raw/2b569e1c95bb4c97b7045112d6e3ce9c.png)

## TRTC SDKのインポート
プロジェクトコードでSDKを使用する方法は2つあります。
- 方法一：SDK APIを使用する必要があるプロジェクトのファイルにインポートモジュールを追加します。
```
@import TXLiteAVSDK_TRTC_Mac;
```

- 方法二：SDK APIを使用する必要があるプロジェクトのファイルに特定のヘッダーファイルをインポートします。
```
#import TXLiteAVSDK_TRTC_Mac/TRTCCloud.h
```


