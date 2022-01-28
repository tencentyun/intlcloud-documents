ここでは、主にTencent CloudのTRTC Demo(Unreal Engine)を素早く実行する方法をご紹介します。

>! 現時点ではWindows、MacOs、ios、Androidをサポートしています。

## 環境要件
- Unreal Engine 4.27.1およびそれ以降のバージョンを推奨します。
- **Android端末向け開発：**
  - Android Studio 4.0およびそれ以降のバージョン。
  - Visual Studio 2017 15.6以上のバージョン。
  - 実機デバッグのみサポートしています
**iOS & macOS端末向け開発：**
  - Xcode 11.0およびそれ以降のバージョン。
  - osxシステムには10.11およびそれ以降のバージョンが必要です。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。
- **Windows 端末向け開発：**
    - OS:Windows 7 SP1およびそれ以降のバージョン(x86-64に基づく64ビットOS）。
    - ディスク容量：IDEと一部のツールのインストールに必要な容量を除く、少なくとも1.64 GB以上の空き容量を確保するようにしてください。
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)をインストールします。

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com)を行い、実名認証が完了済みであること。

## 操作手順
[](id:step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、【開発支援】>【[快速跑通Demo](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【アプリケーションの作成】をクリックし、`TestTRTC`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合、【既存のアプリケーションを選択】をクリックします。
3. 実際の業務ニーズに応じてタグを追加または編集し、【作成】をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/f5fbbe70b7139531600e763846051a54.png)

>?
>- アプリケーション名には、数字、中国語と英語の文字、アンダーラインのみを含めることができ、15文字以内とします。
>- タグはTencent Cloudのさまざまなリソースを識別して管理するために使用されます。たとえば、企業に複数の事業部門があり、各部門に1つ以上のTRTCアプリケーションがある場合、企業はTRTCアプリケーションにタグを追加することで部門情報にマークを付けることができます。タグは入力必須ではありません。実際のビジネスニーズに応じてタグを追加または編集できます。

[](id:step2)
### ステップ2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに応じてSDKおよび付属する[Demoソースコード](https://comm.qq.com/sdk/trtc/UE4/TRTC_Demo.zip)をダウンロードします（ご質問があればQQグループ番号：764231117に参加してお問い合わせください）。
2. ダウンロード完了後、【ダウンロード済み。次へ】をクリックします。

[](id:step3)
### ステップ3：Demo プログラムファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `/TRTC_Demo/Source/debug/include/DebugDefs.h`のファイルを見つけて開きます。
3. `DebugDefs.h`のファイルの関連パラメータを設定します。
<ul><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
	<li/>SECRETKEY：デフォルトは""。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>

4. 貼り付け完了後、【貼り付けました。次へ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソールの概要ページに戻る】をクリックすればOKです。

>?
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを送信し、動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166#Server)をご参照ください。

[](id:step4)
### 手順4：コンパイルとパッケージ化の実行
1. `/TRTC_Demo/TRTC_Demo.uproject`をダブルクリックして開きます。
2. コンパイルを実行し、デバッグを行います。
<dx-tabs>
::: macOS\s端末
1. File -> Package Project -> Mac
2. 権限を設定します。前の手順でコンパイルしたxxx.appファイルを右クリックし、「パッケージの内容を表示」を選択します 
![](https://qcloudimg.tencent-cloud.cn/raw/3eb106ee3307c206dff5314a43920132.png)
3. 「Contents->Info.plist」に進みます
4. 「Information Property List」を選択し、次の2つの権限を追加します。
```
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
5. UE4のeditorで実行中の場合は、**UE4Editor.app**ファイルを見つけて、上記の手順に従って権限を追加する必要があります。
:::
::: Windows\s端末
1. File->Package Project->Windows->Windows(64-bit)
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s端末
1. iOS上でも次の権限が必要です。
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```
上記の権限をinfo.plistに追加するために、**Edit->Project Settings->Platforms: iOS**で 
```
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
上記をAdditional Plist Dataに追加することができます。
2. 最後にプロジェクトをパッケージ化します。File -> Package Project -> iOS
:::
:::  Android\s端末
1. 開発とデバッグ：[Androidクイックスタート](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/GettingStarted/)をご参照ください
2. プロジェクトのパッケージ化：[Androidプロジェクトのパッケージ化](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)をご参照ください
:::
</dx-tabs>
## Demoの実行
Demoでは1対1のビデオ通話が実現でき、テストおよび参考のために呼び出すことができます。APIドキュメントについては[C++ 全プラットフォームAPI](https://intl.cloud.tencent.com/document/product/647/35131)をご参照ください。
>? UIは部分的に調整され更新される可能性があります。最新バージョンを基準としてください。

![](https://qcloudimg.tencent-cloud.cn/raw/e81338b3f3cf22c73744bcfbcf8955d2.png)

## TRTC全プラットフォーム C++ APIドキュメント
[中国語ドキュメント](https://liteav.sdk.qcloud.com/doc/api/zh-cn/md_introduction_trtc_zh_Cplusplus_Brief.html)

[英語ドキュメント](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_Cplusplus_Brief.html)

## よくあるご質問
###  TRTCのログはどうやって確認しますか。
TRTCログは、デフォルトで圧縮および暗号化され、接尾辞は `.xlog`です。アドレスは次のとおりです。
- **iOS 端末**：sandbox の `Documents/log`。
- **Android 端末**：
	- 6.7とそれ以前のバージョン：`/sdcard/log/tencent/liteav`
	- 6.8以後のバージョン：`/sdcard/Android/data/パッケージ名/files/log/tencent/liteav/`

### macos UE4 editorのクラッシュ
**UE4Editor.app** info.plistでオーディオとビデオの権限を設定しているかを確認してください
```
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```

### Androidでの「Attempt to construct staged filesystem reference from absolute path"」エラー
UE4プロジェクトを閉じ、cmdを開きます
>adb shell
>cd sdcard
>ls (you should see the UE4Game directory listed)
>rm -r UE4Game
プロジェクトを再コンパイルします
