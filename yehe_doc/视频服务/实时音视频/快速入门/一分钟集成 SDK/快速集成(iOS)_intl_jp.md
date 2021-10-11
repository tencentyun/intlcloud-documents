このドキュメントでは、主に TRTC SDK（iOS）を迅速にプロジェクトに統合する方法を紹介します。以下のステップにしたがって設定するだけで、SDK統合のタスクが完了します。

## 開発環境要件
- Xcode 9.0+。 
- iOS 9.0 以上のiPhone または iPad 。
- プロジェクトに有効な開発者の署名が設定してあること。

## TRTC SDKの統合
CocoaPodsを使用して自動でローディングする方式か、または先に SDKをダウンロードして、それを現在のプログラムのプロジェクトにインポートする方式を選択できます。

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
Podfile ファイルを編集し、必要に応じて適切な SDKのバージョンを選択します。
- [簡易版](https://intl.cloud.tencent.com/document/product/647/34615)：インストールパッケージの容量増加は最小ですが、TRTCとCDN再生（TXLivePlayer）機能のみのサポートとなります。
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_TRTC', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_TRTC.podspec'
  end
```

- [プロフェッショナル版](https://intl.cloud.tencent.com/document/product/647/34615)：TRTCの外に、RTMP プッシュ（TXLivePusher）、CDN 再生（TXLivePlayer）、オン・デマンド再生（TXVodPlayer）、User Generated Short Video（UGSV）などの多数の機能が含まれています。
```
 platform :ios, '8.0'
  
  target 'App' do
  pod 'TXLiteAVSDK_Professional', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
```

CocoaPod の公式ソースを使用することもできますが、ダウンロードスピードは遅くなります。
```
   platform :ios, '8.0'
   source 'https://github.com/CocoaPods/Specs.git'
   
   target 'App' do
   pod 'TXLiteAVSDK_TRTC'
   end
```

#### 4. SDKの更新およびインストール
端末のウィンドウに以下のコマンドを入力してローカルライブラリのファイルを更新し、TRTC SDKをインストールします。
```
pod install
```
または次のコマンドを使用してローカルライブラリのバージョンを更新します。
```
pod update
```

pod コマンドの実行が完了すると、SDKを統合した.xcworkspace という拡張子のプログラムファイルが生成されますので、これをダブルクリックして開きます。
>? 必要なシステムの依存ライブラリ **Accelerate.framework**を手動で追加する必要があります。

### 手動による統合
1.  [TRTC - SDK ](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/SDK)をダウンロードし 、ダウンロードが完了したら解凍を行います。
2. お客様のXcodeのプロジェクトを開き、動作させたいtargetを選択して、**Build Phases**の項目を選択します。
 ![](https://main.qcloudimg.com/raw/85509cc24bd958e7b9978e11937597c5.png)
3. **Link Binary with Libraries**の項目をクリックして展開し、一番下の「+」記号のアイコンをクリックして依存ライブラリを追加します。
 ![](https://main.qcloudimg.com/raw/54be71cc14ec79ce642216612544a8a4.png)
4. 順番に、ダウンロードした TRTC SDK Frameworkおよびそれに必要な依存ライブラリ  **libc++.tbd** 、**Accelerate.framework** 和 **libresolv.tbd**、**AVFoundation.framework**を追加します。
 ![](https://main.qcloudimg.com/raw/2fa94b7f81c7e9c4ac09733782e79c10.png)


## カメラとマイクの使用権限の許可
SDK の音声ビデオ機能を使用するには、マイクとカメラの使用権限を許可する必要がありますので、AppのInfo.plistの中に次の2項目を追加します。それぞれマイクとカメラに対応し、システムが使用許可のダイヤログボックスをポップアップするときに表示される情報となります。
- **Privacy - Microphone Usage Description**、さらにマイク使用目的のプロンプトを追加します。
- **Privacy - Camera Usage Description**、さらにカメラ使用目的のプロンプトを記入します。

![](https://main.qcloudimg.com/raw/7c483aae65f64cd2bf35b55d9c896a52.png)


## TRTC SDKの引用
TRTC SDK では2種類の呼び出し方式をサポートしていますので、いずれかをお選びください
### 方式1： Objective-Cまたは SwiftインターフェースによるTRTC SDKの引用
Objective-CまたはSwiftコードの中でSDKを使用する方式は2種類あります。
- **コンポーネントの引用**：プロジェクトのSDK APIを使用したいファイルの中に、コンポーネントを追加して引用します。
```
@import TXLiteAVSDK_TRTC;
```
- **ヘッダーファイルの引用**：プロジェクトのSDK APIを使用したいファイルの中に、具体的なヘッダーファイルをインポートします。
```
#import TXLiteAVSDK_TRTC/TRTCCloud.h
```


[](id:using_cpp)
### 方式2： C++インターフェースによるTRTC SDKの引用
1. **ヘッダーファイルの引用**： C++ インターフェースを使用してiOSアプリケーションを開発したい場合は、`TXLiteAVSDK_TRTC.framework/Headers/cpp_interface` ディレクトリの下のヘッダーファイルを引用してください。
```
#include TXLiteAVSDK_TRTC/cpp_interface/ITRTCCloud.h
```
2. **ネームスペースの利用**：C++ の全てのプラットフォームのインターフェースのメソッド、タイプなどはいずれも trtc ネームスペースの中に定義されています。コードをより簡潔にするため、trtc ネームスペースを直接使用することをお勧めします
```
using namespace trtc;
```

>?  C++ インターフェースの使用方法については、 [全プラットフォーム（C++）APIの概要](https://intl.cloud.tencent.com/document/product/647/35131)をご参照ください。

## よくあるご質問
### 1. TRTC SDK はバックグラウンドでの動作をサポートしていますか？
サポートしています。バックグラウンドに入っても、依然として関連機能が動作するようにしたい場合は、現在のプログラムのプロジェクトを選択し、**Capabilities** の下の**Background Modes**の設定を **ON**にして、**Audio、AirPlay and Picture in Picture**にチェックを入れます。次の図のとおりです。
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)
