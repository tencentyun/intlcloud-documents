## シーンの弱点とソリューション
画面共有などのユースケースにおいて、システムオーディオを相手に共有する必要がよくありますが、Mac PCではデフォルトのサウンドカードがシステムオーディオのキャプチャをサポートしていないため、Mac PCでシステムオーディオを共有するのは比較的困難です。このため、TRTCはMacでシステム音声をレコーディングする機能を提供し、そのシーンのニーズを満たします。具体的な接続手順は、以下をご参照ください。

## 統合の説明

<span id="step1"></span>
### 手順1：TRTCPrivilegedTaskライブラリの統合  

SDKは[TRTCPrivilegedTask](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TRTCPrivilegedTask/TRTCPrivilegedTask.tar.bz2)ライブラリを使用してroot権限を取得する必要があるため、バーチャルサウンドカードプラグインTRTCAudioPlugin.driverをシステムディレクトリ`/Library/Audio/Plug-Ins/HAL`にインストールします。

#### CocoaPodsを使用して統合  
1. 現在の項目ルートディレクトリの`Podfile`ファイルを開き、以下のコンテンツを追加します。
```
platform :osx, '10.10'	
target 'Your Target' do
    pod 'TRTCPrivilegedTask', :podspec => 'https://pod-1252463788.cos.ap-guangzhou.myqcloud.com/liteavsdkspec/TRTCPrivilegedTask.podspec'
end
```
2. `pod install`コマンドを実行して**TRTCPrivilegedTask**ライブラリをインストールします。

>?
>- プロジェクトのルートディレクトリに`Podfile`ファイルがない場合は、まず`pod init`コマンドを実行しファイルを新規作成してから、以下の内容を追加してください。
>-  CocoaPodsのインストール方法は [CocoaPods公式サイトインストールの説明](https://guides.cocoapods.org/using/getting-started.html)をご参照ください。

#### 手動統合
1. [TRTCPrivilegedTask](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TRTCPrivilegedTask/TRTCPrivilegedTask.tar.bz2)ライブラリをダウンロードします。
2. Xcodeプロジェクトを開き、圧縮解除後のファイルlibPrivilegedTask.aをプロジェクトにインポートします。
3. 実行するtargetを選択し、Build Phasesを選択し、Link Binary with Librariesを開き、一番下の【+】をクリックし、依存ライブラリ`libPrivilegedTask.a`を追加します。  
![libPrivilegedTask.a](https://main.qcloudimg.com/raw/cc5b3365e72cee80cda7f0db0a4e1b62.png)  


<span id="step2"></span>
### 手順2：App Sandbox機能のキャンセル  
Appのentitlements説明ファイルのうち、**App Sandbox**項目を削除します。  
![Sandbox](https://main.qcloudimg.com/raw/98fed5571040f24c2891f4b87ddce15e.png)  


<span id="step3"></span>
### 手順3：バーチャルサウンドカードプラグインのパッケージ化  
[TRTCPrivilegedTaskライブラリの統合](#step1)と[App Sandbox機能のキャンセル](#step2)の後で、まずシステムオーディオレコーディング機能を使用する際、SDKはネットワークからバーチャルサウンドカードプラグインをダウンロードしてインストールします。このプロセスをアクセラレーションしたい場合は、`TXLiteAVSDK_TRTC_Mac.framework`のPlugInsディレクトリ下にあるバーチャルサウンドカードプラグイン`TRTCAudioPlugin.driver`をApp BundleのResourcesディレクトリにパッケージ化することができます。以下の画像をご参照ください。  
![プラグインのパッケージ化](https://main.qcloudimg.com/raw/b04b805d4848f2ecd6fd7dcc83176a9e.png)
または、App BundleのPlugInsディレクトリをコピーします。以下の画像をご参照ください。  
![プラグインのパッケージ化2](https://main.qcloudimg.com/raw/05fb5c6ec4dba74c3b5fb880ed28033e.png)  


<span id="step4"></span>
### 手順4：システム音声キャプチャの開始  
[startSystemAudioLoopback](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486)インターフェースをコールしてシステム音声キャプチャを開始し、それをアップリンクオーディオストリーム内に混ぜます。インターフェースの実行が完了すると、[onSystemAudioLoopbackError](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676)によって成功か失敗かの結果をコールバックします。
```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud startLocalAudio];
[trtcCloud startSystemAudioLoopback];
```

>! TRTCPrivilegedTaskライブラリの統合とApp Sandbox機能のキャンセルの後で、まずstartSystemAudioLoopbackをコールするとroot権限を取得できます。以下の画像をご参照ください。    
>ユーザーが【OK】をクリックすると、バーチャルサウンドカードプラグインの自動インストールが開始されます。



<span id="step5"></span>

### 手順5：システム音声キャプチャの停止 

[stopSystemAudioLoopback](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486)インターフェースをコールしてシステム音声キャプチャを停止します。

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud stopSystemAudioLoopback];
```

<span id="step6"></span>
### 手順6：システム音声キャプチャボリュームの設定

[setSystemAudioLoopbackVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486)インターフェースをコールしてシステム音声のキャプチャボリュームを設定します。

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud setSystemAudioLoopbackVolume:80];
```

## 統合のまとめ

- TRTCは、Macではバーチャルサウンドカードプラグイン`TRTCAudioPlugin.driver`によってオーディオをレコーディングします。このバーチャルサウンドカードプラグインはシステムディレクトリ`/Library/Audio/Plug-Ins/HAL`にコピーし、オーディオサービスを再起動してから有効化する必要があります。`Launchpad`の`その他`フォルダ内の`オーディオMIDI設定`アプリケーションによって、バーチャルサウンドカードプラグインがインストールに成功したかどうかを確認できます。そのアプリケーションのデバイスリストにおいて、「TRTC Audio Device」という名前のデバイスがあれば、TRTCのバーチャルサウンドカードプラグインのインストールに成功したことになります。  
- 上記手順における[TRTCPrivilegedTaskライブラリの統合](#step1)と[App Sandbox機能のキャンセル](#step2)は、TRTC SDKにバーチャルサウンドカードプラグインを自動インストールしてroot権限を提供します。TRTCPrivilegedTaskライブラリを統合せずにApp Sandbox機能を残したままにした場合、 SDKはバーチャルサウンドカードプラグインを自動インストールできませんが、システム内にバーチャルサウンドカードプラグインをインストール済みである場合、システムオーディオをレコーディングする機能はそのまま正常に使用できます。
> ? 上記方法以外に加えて、バーチャルサウンドカードプラグインを手動でインストールすることで、該当の機能を統合できます。
> 1. `TXLiteAVSDK_TRTC_Mac.framework`のPlugInsディレクトリ下にある`TRTCAudioPlugin.driver`をシステムディレクトリ`/Library/Audio/Plug-Ins/HAL`にコピーします。
> 2. システムのオーディオサービスを再起動します。 

#### システムのオーディオサービスbashの再起動
```
 sudo cp -R TXLiteAVSDK_TRTC_Mac.framework/PlugIns/TRTCAudioPlugin.driver /Library/Audio/Plug-Ins/HAL  
 sudo kill -9 `ps ax|grep 'coreaudio[a-z]' |awk '{print $1}'`
```
<span id="note"></span>

## 注意事項
- App Sandbox機能をキャンセルすると、App内で取得したユーザーパスが変更されます。  
NSSearchPathForDirectoriesInDomainsなどのシステムの手段によって取得した` ~/Documents`、 `~/Library`などのディレクトリは、サンドボックスディレクトリからユーザーディレクトリ`/Users/ユーザー名/Documents`、 `/Users/ユーザー名/Library`に切り替わります。
- TRTCPrivilegedTaskライブラリを統合すると、AppをMac App Storeに公開できない可能性があります。  
SDKがバーチャルサウンドカードプラグインを自動でインストールする際は、App Sandbox機能を無効化し、root権限を取得しなければ、AppをMac App Storeに公開できない可能性があります。詳細は、[App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/#hardware-compatibility)をご参照ください。  
App Storeに公開するか、またはSandbox機能を使用する場合、バーチャルオーディオプラグインを手動インストールする方法を推奨します。  
