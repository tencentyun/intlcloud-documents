このドキュメントでは、主に、Tencent Cloud TRTC SDK(Mac)を迅速にプロジェクトに統合する方法を紹介します。以下のステップにしたがって設定するだけで、SDK統合のタスクが完了します。


## 開発環境要件
- Xcode 9.0+。
- OS X10.10+ のMac 実機。
- プロジェクトに有効な開発者の署名が設定してあること。

## TRTC SDKの統合
CocoaPodsを使用して自動でローディングするか、または手動で、先ず SDKをダウンロードして、それを現在のプログラムのプロジェクトにインポートする方式を選択できます。

### CocoaPods
#### 1. CocoaPodsのインストール
端末のウィンドウに次のコマンドを入力します（事前にMac にRuby環境をインストールしておく必要があります ）。
```
sudo gem install cocoapods
```

#### 2. Podfile ファイルの作成
プロジェクトが存在するパスに入り、次のコマンドラインを入力するとプロジェクトパスの下にPodfile ファイルが現れます。
```
pod init
```

#### 3. Podfile ファイルの編集
Podfile ファイルを編集します。次の2種類の設定方法があります。
- 方式1：Tencent Cloud LiteAV SDK のpodパスを使用します。

```
	platform :osx, '10.10'

	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_TRTC_Mac.podspec'
	end
```

- 方式2：CocoaPodの公式ソースを使用します。バージョンナンバーの選択をサポートしています。

```
	platform :osx, '10.10'
	source 'https://github.com/CocoaPods/Specs.git'

	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac'
	end
```

#### 4. SDKのインストールおよび更新
端末のウィンドウに次のコマンドを入力して、TRTC SDKのインストールを実行します。
```
pod install
```
または次のコマンドを使用してローカルライブラリのバージョンを更新します。
```
pod update
```

pod コマンドの実行が完了すると、SDKが統合された.xcworkspace という拡張子のプログラムファイルが生成されますので、これをダブルクリックして開きます。

### 手動による統合
1. [TRTC-SDK ](https://github.com/tencentyun/TRTCSDK/tree/master/Mac) のMac版をダウンロードします 。

2. お客様のXcodeのプロジェクトを開き、第1ステップでダウンロードした framework をプログラムにインポートします。

3. 動作させたいtargetを選択し、Build Phasesの項目を選択します。
![](https://main.qcloudimg.com/raw/b5097f8ac4cbaa5044d92b2a96ea2b9e.jpg)

4. **Link Binary with Libraries** の項目をクリックして展開し、1番下の「+」記号のアイコンをクリックして依存ライブラリを追加します。
![](https://main.qcloudimg.com/raw/17046154417930f9d31b6452782df55d.jpg)

5. 順番に、ダウンロードした SDK Frameworkおよびそれに必要な依存ライブラリ：`AudioUnit.framework`、`libc++.tbd` 、`Accelerate.framework`を追加します。  
    
追加した後は次の図のようになります。
![](https://main.qcloudimg.com/raw/7bddb832347a971f3e69238480fa3e8d.jpg)

## カメラとマイクの使用権限の許可
SDK の音声ビデオ機能を使用するには、マイクとカメラの使用権限を許可する必要がありますので、AppのInfo.plistの中に次の2項目を追加します。それぞれマイクとカメラに対応し、システムが使用許可のダイヤログボックスをポップアップするときに表示される情報となります。
- **Privacy - Microphone Usage Description**、さらにマイク使用目的のプロンプトを記入します。
- **Privacy - Camera Usage Description**、さらにカメラ使用目的のプロンプトを記入します。
下図に示すように：
![](https://main.qcloudimg.com/raw/ce02c335f1a6413fb37adb0ed20a9603.png)

Appで **App Sandbox**または**Hardened Runtime**を有効にしている場合は、 `Network`、`Camera`、`Audio Input`の選択項目にチェックを入れる必要があります。
- App Sandbox の設定は次の図のとおりです。
![](https://main.qcloudimg.com/raw/b77d2ab814e6e14e8bed17efdcbee1a6.png)
- Hardened Runtime の設定は次の図のとおりです。
![](https://main.qcloudimg.com/raw/2b569e1c95bb4c97b7045112d6e3ce9c.png)

## TRTC SDKの引用
プロジェクトのコードの中で SDKを使用する方式は2種類あります。
- 方式1： プロジェクトのSDK APIを使用したいファイルの中に、コンポーネントを追加して引用します。
```
@import TXLiteAVSDK_TRTC_Mac;
```

- 方式2：プロジェクトのSDK APIを使用したいファイルの中に、具体的なヘッダーファイルをインポートします。
```
#import TXLiteAVSDK_TRTC_Mac/TRTCCloud.h
```


