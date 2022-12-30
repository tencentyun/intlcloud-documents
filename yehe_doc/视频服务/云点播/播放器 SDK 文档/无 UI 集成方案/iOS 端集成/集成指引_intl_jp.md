ここでは、主にTencent Cloud View Cube·プレーヤーLiteAVSDK_Player（iOS）をプロジェクトに素早く統合する方法を紹介します。以下の手順に従って設定すれば、 SDKの統合作業を完了できます。


## 開発環境要件
- Xcode 9.0+。
- iOS 9.0 以上のiPhone または iPad 。
- プロジェクトに有効な開発者の署名が設定してあること。

## LiteAVSDKの統合
CocoaPodsの自動ロード方法を選択、使用するか、またはまずSDKをダウンロードしてから、現在のプロジェクトにインポートすることができます。

[](id:cocoapods)
### CocoaPodsによる統合
1. **CocoaPodsのインストール**
端末のウィンドウに次のコマンドを入力します（事前にMac にRuby環境をインストールしておく必要があります ）。
```
sudo gem install cocoapods
```
2. **Podfileファイルの作成**
プロジェクトが存在するパスに入り、次のコマンドラインを入力するとプロジェクトパスの下にPodfile ファイルが現れます。
```
pod init
```
3. **Podfileファイルの編集**
	CocoaPod公式ソースを使用すると、バージョン番号を選択できます。Podfileファイルを編集します。
	
	Pod方式で最新バージョンのTXLiteAVSDK_Player_Premiumを直接統合します。
```objective
platform :ios, '9.0'
source 'https://github.com/CocoaPods/Specs.git'

target 'App' do
pod 'TXLiteAVSDK_Player_Premium'
end
```
特定のバージョンを指定する必要がある場合は、podfileファイルに以下の依存関係を追加することができます。
```objective-c
pod 'TXLiteAVSDK_Player', '~> 110.8.29000'
```

4. **SDKの更新およびインストール**
  - 端末ウィンドウに次のコマンドを入力し、ローカルライブラリファイルを更新し、LiteAVSDKをインストールします。
```
pod install
```

  - または次のコマンドを使用してローカルライブラリのバージョンを更新します。
```
pod update
```
podコマンドの実行が完了すると、SDKを統合した`.xcworkspace`という拡張子のプログラムファイルが生成されますので、これをダブルクリックして開きます。

[](id:manual)
### SDKの手動統合
1. 最新バージョン[TXLiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_iOS_latest.zip)のSDK + Demo開発キットをダウンロードします。
2. 統合するプロジェクトにSDK/TXLiteAVSDK_Player_Premium.frameworkを追加し、`Do Not Embed`にチェックを入れます。
3. プロジェクトTargetの-ObjCを設定する必要があります。設定しない場合、SDKのクラスがロードされないので、Crashが発生することがあります。

```objective-c
Xcodeを開き、-> 対応するTargetを選択し、-> "Build Setting" Tabを選択し、-> "Other Link Flag"を検索して、-> "-ObjC"を入力します
```

4. 適切なライブラリファイルを追加します（SDKディレクトリ内）
   **TXFFmpeg.xcframework**：.xcframeworkファイルをプロジェクトに追加し、「General - Frameworks, Libraries, and Embedded Content」の「Embed&Sign」に設定します。また、「Project Setting - Build Phases - Embed Frameworks」で検査を行い、オプション「Code Sign On Copy」を下図のようにチェックを入れた状態にします。
    **TXSoundTouch.xcframework**：.xcframeworkファイルをプロジェクトに追加し、「General - Frameworks, Libraries, and Embedded Content」の「Embed&Sign」に設定します。また、「Project Setting - Build Phases - Embed Frameworks」で検査を行い、オプション「Code Sign On Copy」を下図のようにチェックを入れた状態にします。<br>
    <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b226decc76c33eff8c3f5b4cc4246bea.png" />
   <br>
   また、Xcodeの「Build Settings - Search Paths」に切り替えて、「Framework Search Paths」に上記Frameworkにあるパスを追加します。
	
	 **MetalKit.framework**：Xcodeを開き、「project setting - Build  Phases - Link Binary With Libraries」に切り替え、左下隅の記号「+」を選択して「MetalKit」と入力し、下図のようにプロジェクトに追加します。<br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8ab7576dcc8bbe7b36396955ca06b186.png" />
   <br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8480798e5ba897077ed3cef8ebc12f2e.png" />
   <br>

	 **ReplayKit.framework**：Xcodeを開き、「project setting - Build  Phases - Link Binary With Libraries」に切り替え、左下隅の記号「+」を選択して「ReplayKit」と入力し、下図のようにプロジェクトに追加します。<br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/aa07f3d4963ee703505a14a743f61a68.png" />
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/12491d4a64aa6df44e6a966e80ca54de.png" />
   <br>
   同じ方法で、以下のシステムライブラリも追加します。
   <br><b>システムFrameworkライブラリ</b>：SystemConfiguration, CoreTelephony, VideoToolbox, CoreGraphics, AVFoundation, Accelerate, MobileCoreServices<br>
   <b>システムLibraryライブラリ:</b> libz, libresolv,  libiconv, libc++, libsqlite3

#### ピクチャーインピクチャー機能

ピクチャーインピクチャー機能を使用する必要がある場合は、下図の方法で設定してください。不要な場合は無視してかまいません。

1、iOSのピクチャーインピクチャー（Picture-In-Picture）を使用するには、SDKをバージョン10.3以上にアップグレードしてください
2、ピクチャーインピクチャー機能を使用する場合、バックグラウンドモードを開く必要があります。XCodeは対応するTarget -> Signing & Capabilities -> Background Modesを選択し、図のように「Audio, AirPlay, and Picture in Picture」にチェックを入れます。
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/116e1e741f80d810502221fd143d8434.png" />

## SDKのプロジェクトへのインポート
プロジェクトのコードの中で SDKを使用する方式は2種類あります。
- **方法1：**プロジェクトでSDK APIを使用する必要のあるファイルにモジュール参照を追加します。
```
@import TXLiteAVSDK_Player_Premium;
```
- **方法2：**プロジェクトでSDK APIを使用する必要のあるファイルに特定のヘッダーファイルをインポートします。
```
#import "TXLiteAVSDK_Player_Premium/TXLiteAVSDK.h"
```

## SDKへのLicense権限承認の設定
1. [License申請](https://www.tencentcloud.com/document/product/266/51098)をクリックし、テスト用Licenseを取得します。Licenseを設定しないとビデオ再生に失敗します。具体的な操作については[テスト版License](https://www.tencentcloud.com/document/product/266/51098#.E7.94.B3.E8.AF.B7.E6.B5.8B.E8.AF.95.E7.89.88-license)をご参照ください。取得する2つの文字列のうち、1つはlicenseURL、もう1つは復号keyです。
2. AppがLiteAVSDKの関連機能を呼び出す前に以下の設定を行います（`- [AppDelegate application:didFinishLaunchingWithOptions:]` に設定することをお勧めします）。
```objc
@import TXLiteAVSDK_Player_Premium;
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<取得したlicenseUrl>";
    NSString * const licenceKey = @"<取得したkey>";
    
    //TXLiveBaseは"TXLiveBase.h"ヘッダーファイルの中にあります
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    // TXLiveBase.delegate = self;
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}

#pragma mark - TXLiveBaseDelegate
- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason {
    NSLog(@"onLicenceLoaded: result:%d reason:%@", result, reason);
}
@end
```

## 確認方法

License設定に成功後（しばらくかかります。時間の長さはネットワークの状況に応じて異なります）、次のメソッドを呼び出してLicense情報を確認することができます。

```swift
NSLog(@"%@", [TXLiveBase getLicenceInfo]);
```

[](id:faq)

## よくあるご質問
1. プロジェクト内にMLVB SDK/TRTC/プレーヤーなどの、LiteAVSDKシリーズの複数のSDKを統合し、シンボル競合の問題が発生した場合、どのように解決すればよいですか。

2つ以上の製品（ライブストリーミング、プレーヤー、TRTC、UGSV）のLiteAVSDKバージョンを統合した場合、コンパイルの際にライブラリ競合の問題が発生する場合があります。これは、SDKの下層ライブラリに同一のシンボルファイルが存在するためで、ここでは全機能版SDK1つのみを統合することでの解決をお勧めします。全機能版ではライブストリーミング、プレーヤー、TRTC、UGSVがすべて1つのSDKに含まれています。具体的には[SDKダウンロード](https://www.tencentcloud.com/document/product/266/50561)をご参照ください。

