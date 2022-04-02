このドキュメントでは、主にTRTC SDK（Mac）を迅速にプロジェクトに統合する方法を紹介します。以下のステップにしたがって設定するだけで、SDK統合のタスクが完了します。


## 開発環境要件
- Xcode 9.0+。
- OS X10.10+ のMac実機。
- プロジェクトに有効な開発者の署名が設定してあること。

## TRTC SDKの統合
CocoaPodsを使用して自動でローディングするか、または手動で、先ずSDKをダウンロードして、それを現在のプログラムのプロジェクトにインポートする方式を選択できます。

### CocoaPods
#### 1. CocoaPodsのインストール
端末のウィンドウに次のコマンドを入力します（事前にMacにRuby環境をインストールしておく必要があります）。
```
sudo gem install cocoapods
```

#### 2. Podfileファイルの作成
プロジェクトが存在するパスに入り、次のコマンドラインを入力するとプロジェクトパスの下にPodfileファイルが現れます。
```
pod init
```

#### 3. Podfileファイルの編集
Podfileファイルを編集します。次の2種類の設定方法があります。
- 方式1：Tencent Cloud LiteAV SDKのpodパスを使用します。
<dx-codeblock>
::: podパス
	platform :osx, '10.10'
	
	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_TRTC_Mac.podspec'
	end
:::
</dx-codeblock>
- 方式2：CocoaPodの公式ソースを使用します。バージョンナンバーの選択をサポートしています。
<dx-codeblock>
::: podパス
	platform :osx, '10.10'
	source 'https://github.com/CocoaPods/Specs.git'
	
	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac'
	end
:::
</dx-codeblock>

#### 4. SDKのインストールおよび更新
端末のウィンドウに次のコマンドを入力して、TRTC SDKのインストールを実行します。
```
pod install
```
または次のコマンドを使用してローカルライブラリのバージョンを更新します。
```
pod update
```

podコマンドの実行が完了すると、SDKを統合した`.xcworkspace`という拡張子のプログラムファイルが生成されますので、これをダブルクリックして開きます。

### 手動による統合
1. [TRTC-SDK ](https://github.com/LiteAVSDK/TRTC_Mac)のMacバージョンをダウンロードします。
2. お客様のXcodeのプロジェクトを開き、ステップ1でダウンロードしたframeworkプロジェクトにインポートします。
3. 動作させたいtargetを選択し、Build Phasesの項目を選択します。
![](https://main.qcloudimg.com/raw/b5097f8ac4cbaa5044d92b2a96ea2b9e.jpg)
4. **Link Binary with Libraries**の項目をクリックして展開し、一番下の「+」アイコンをクリックして依存ライブラリを追加します。
![](https://main.qcloudimg.com/raw/17046154417930f9d31b6452782df55d.jpg)
5. 順番に、ダウンロードしたSDK Frameworkおよびそれに必要な依存ライブラリ：`AudioUnit.framework`、`libc++.tbd`、`Accelerate.framework`を追加します。  
追加した後は以下の通りです。
![](https://main.qcloudimg.com/raw/258ffc87c493d23cf591bb2ff9102677.png)

## カメラとマイクの使用権限の許可
SDKの音声ビデオ機能を使用するには、マイクとカメラの使用権限を許可する必要がありますので、AppのInfo.plistの中に次の2項目を追加します。システムが使用許可のダイヤログボックスをポップアップするときに表示されるマイクとカメラの情報にそれぞれ対応します。
- **Privacy - Microphone Usage Description**、さらにマイク使用目的のプロンプトを記入します。
- **Privacy - Camera Usage Description**、さらにカメラ使用目的のプロンプトを記入します。
以下の通りです。
![](https://main.qcloudimg.com/raw/ce02c335f1a6413fb37adb0ed20a9603.png) 

Appで**App Sandbox**または**Hardened Runtime**を有効にしている場合は、`Network`、`Camera`、`Audio Input`の選択項目にチェックを入れる必要があります。
- App Sandboxの設定は以下の通りです。
![](https://main.qcloudimg.com/raw/b77d2ab814e6e14e8bed17efdcbee1a6.png)
- Hardened Runtimeの設定は以下の通りです。
![](https://main.qcloudimg.com/raw/2b569e1c95bb4c97b7045112d6e3ce9c.png)

## TRTC SDKの引用
TRTC SDKでは2種類の呼び出し方式をサポートしていますので、いずれかをお選びください。
### 方式1：Objective-CまたはSwiftインターフェースによるTRTC SDKの引用
Objective-CまたはSwiftコードの中でSDKを使用する方式は2種類あります。
- **モジュールの引用**：プロジェクトのSDK APIを使用したいファイルの中に、モジュールを追加して引用します。
```
@import TXLiteAVSDK_TRTC_Mac;
```
- **ヘッダーファイルの引用**：プロジェクトのSDK APIを使用したいファイルの中に、具体的なヘッダーファイルをインポートします。
```
#import TXLiteAVSDK_TRTC_Mac/TRTCCloud.h
```

[](id:using_cpp)
### 方式2：C++インターフェースによるTRTC SDKの引用
1. **ヘッダーファイルの引用**：C++インターフェースを使用してMacアプリケーションを開発したい場合は、`TXLiteAVSDK_TRTC_Mac.framework/Headers/cpp_interface`ディレクトリの下のヘッダーファイルをインポートしてください。
```
#include TXLiteAVSDK_TRTC_Mac/cpp_interface/ITRTCCloud.h
```
2. **ネームスペースの利用**：C++の全プラットフォームのインターフェースのメソッド、タイプなどはいずれもtrtcネームスペースの中に定義されています。コードをより簡潔にするため、trtcネームスペースを直接使用することをお勧めします。
```
using namespace trtc;
```

>? C++インターフェースの使用方法については、[全プラットフォーム（C++）APIの概要](https://intl.cloud.tencent.com/document/product/647/35131)をご参照ください。
