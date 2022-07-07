## シーンのペインポイントとソリューション
画面共有などのユースケースでは、システムオーディオを相互に共有する必要があります。Macコンピュータのデフォルトのサウンドカードはシステムオーディオのキャプチャをサポートしていないため、Macコンピューターでシステムオーディオを共有することは困難です。これに基づいて、TRTCは、このシーンのニーズを満たすためにMac側でシステムオーディオをレコーディングする機能を提供します。具体的なアクセス手順は次のとおりです。

## 統合の説明

[](id:step1)
### 手順1：TRTCPrivilegedTaskライブラリの統合  

SDKは、[TRTCPrivilegedTask](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TRTCPrivilegedTask/TRTCPrivilegedTask.tar.bz2)ライブラリを使用して、仮想サウンドカードプラグインTRTCAudioPlugin.driverをシステムディレクトリ`/ Library / Audio / Plug-Ins/HAL`にインストールするためのroot権限を取得してください。

<dx-tabs>
::: CocoaPodsによる統合  
1. 現在のプロジェクトのルートディレクトリの`Podfile`ファイルを開き、以下のコンテンツを追加します：
<dx-codeblock>
::: ruby ruby
platform :osx, '10.10'  

target 'Your Target' do
    pod 'TRTCPrivilegedTask', :podspec => 'https://pod-1252463788.cos.ap-guangzhou.myqcloud.com/liteavsdkspec/TRTCPrivilegedTask.podspec'
end
:::
</dx-codeblock>

2. `pod install`コマンドを実行し、**TRTCPrivilegedTask**ライブラリをインストールします。

<dx-alert infotype="explain">
<li>プロジェクトのルートディレクトリに`Podfile`ファイルがない場合は、まず`pod init`コマンドを実行しファイルを新規作成してから、以下の内容を追加してください。</li>
<li>CocoaPodsのインストール方法については、[CocoaPods公式サイトインストールの説明](https://guides.cocoapods.org/using/getting-started.html)をご参照ください。</li></dx-alert>

:::
::: 手動統合
1. [TRTCPrivilegedTask](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TRTCPrivilegedTask/TRTCPrivilegedTask.tar.bz2)ライブラリをダウンロードします。
2. Xcodeプロジェクトを開き、解凍後のファイルlibPrivilegedTask.aをプロジェクトへインポートします。
3. 実行されるtargetを選択し、Build Phasesアイテムを選択し、Link Binary with Librariesアイテムを展開し、その下の**+**をクリックし、依存ライブラリ`libPrivilegedTask.a`を追加します。  
![libPrivilegedTask.a](https://main.qcloudimg.com/raw/cc5b3365e72cee80cda7f0db0a4e1b62.png)  
:::
</dx-tabs> 


[](id:step2)
### 手順2：App Sandbox機能の無効化  
Appのentitlements説明ファイルから、**App Sandbox**エントリを削除します。  
![Sandbox](https://main.qcloudimg.com/raw/98fed5571040f24c2891f4b87ddce15e.png)  


[](id:step3)
### 手順3：仮想サウンドカードプラグインのパッケージ化  
[TRTCPrivilegedTaskライブラリの統合](#step1)と[App Sandbox機能の無効化](#step2)の後、システムオーディオレコーディング機能を初めて使用する場合、SDKは仮想サウンドカードプラグインをネットワークからダウンロードしてインストールします。このプロセスをアクセラレーションする場合は、`TXLiteAVSDK_TRTC_Mac.framework`のPlugInsディレクトリにある仮想サウンドカードプラグイン`TRTCAudioPlugin.driver`をAppBundleのResourcesディレクトリにパッケージ化できます。下図のとおりです：  
![プラグインのパッケージ化](https://main.qcloudimg.com/raw/b04b805d4848f2ecd6fd7dcc83176a9e.png)
またはApp BundleのPlugInsディレクトリにコピーします。下図のとおりで：  
![プラグインのパッケージ化2](https://main.qcloudimg.com/raw/05fb5c6ec4dba74c3b5fb880ed28033e.png)  


[](id:step4)
### 手順4：システム音声のキャプチャを開始します  
[startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486)インターフェースを呼び出して、システム音声のキャプチャを開始し、アップリンクオーディオストリームに混合します。インターフェースが実行された後、成功または失敗の結果は[onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676)を介してコールバックされます。
```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud startLocalAudio];
[trtcCloud startSystemAudioLoopback];
```

>! TRTCPrivilegedTaskライブラリの統合とApp Sandbox機能の無効化の後、startSystemAudioLoopbackを最初に呼び出す場合は、root権限を取得します。
>ユーザーが**OK**をクリックすると、仮想サウンドカードプラグインが自動的にインストールされます。



[](id:step5)

### 手順5：システム音声のキャプチャを停止します 

[stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486)インターフェースを呼び出して、システム音声のキャプチャを終了します。

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud stopSystemAudioLoopback];
```

[](id:step6)
### 手順6：システム音声のキャプチャボリュームを設定します

[setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486)インターフェースを呼び出して、システム音声のキャプチャボリュームを設定します。

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud setSystemAudioLoopbackVolume:80];
```

## 統合のまとめ

- Mac側では、TRTCは仮想サウンドカードプラグイン`TRTCAudioPlugin.driver`を使用してシステムオーディオをレコーディングします。この仮想サウンドカードプラグインをシステムディレクトリ`/Library/Audio/Plug-Ins/HAL`にコピーし、オーディオサービスを再起動して有効にする必要があります。仮想サウンドカードプラグインが正常にインストールされているかどうかは、`Launchpad`の`その他`フォルダにある`オーディオMIDI設定`アプリケーションで確認できます。このアプリケーションのデバイスリストに「TRTC Audio Device」という名前のデバイスがある場合は、TRTCの仮想サウンドカードプラグインが正常にインストールされていることを示します。  
- 前の手順での[TRTCPrivilegedTaskライブラリの統合](#step1)と[App Sandbox機能の無効化](#step2)は、仮想サウンドカードプラグインを自動的にインストールするためのTRTC SDKのroot権限を提供するためのものです。TRTCPrivilegedTaskライブラリが統合されておらず、App Sandbox機能が保持されている場合、SDKは仮想サウンドカードプラグインを自動的にインストールしませんが、仮想サウンドカードプラグインがシステムにインストールされている場合、システムオーディオレコーディング機能は引き続き正常に使用できます。
> ? 上記のスキームに加えて、仮想サウンドカードプラグインを手動でインストールして、この機能を統合することもできます。
> 1. `TXLiteAVSDK_TRTC_Mac.framework`のPlugInsディレクトリにある`TRTCAudioPlugin.driver`をシステムディレクトリ`/Library/Audio/Plug-Ins/HAL`にコピーします。
> 2. システムのオーディオサービスを再起動します。 

<dx-codeblock>
::: システムのオーディオサービスbashを再起動します。
 sudo cp -R TXLiteAVSDK_TRTC_Mac.framework/PlugIns/TRTCAudioPlugin.driver /Library/Audio/Plug-Ins/HAL  
 sudo kill -9 `ps ax|grep 'coreaudio[a-z]' |awk '{print $1}'`
:::
</dx-codeblock>


[](id:note)
## 注意事項
- App Sandbox機能を無効にすると、Appで取得したユーザーパスが変更されます。  
NSSearchPathForDirectoriesInDomainsなどのシステムメソッドによって取得された ` ~/Documents`、 `~/Library`などのディレクトリは、サンドボックスディレクトリからユーザーディレクトリ`/Users/ユーザー名/Documents`、`/Users/ユーザー名/Library`に切り替えられます。
- TRTCPrivilegedTaskライブラリを統合すると、AppがMac App Storeにリストされなくなる可能性があります。  
SDKが仮想サウンドカードプラグインを自動的にインストールする場合、App Sandbox機能を閉じてルート権限を取得する必要があります。AppがMac App Storeにリストされなくなる可能性があります。詳細については、[App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/#hardware-compatibility)をご参照ください。  
App Storeにリストしたり、Sandbox機能を使用したりする場合は、仮想オーディオプラグインを手動でインストールするスキームを選択することをお勧めします。  
