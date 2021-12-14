ここでは、主にTencent CloudのTRTC Demo(React Native)を素早く実行する方法をご紹介します。

## 環境要件
- ReactNative 0.63およびそれ以降のバージョン
- Node & Watchman。nodeバージョンはv12以上が必要です。
- **Android端末向け開発：**
  -  Android Studio 3.5およびそれ以降のバージョン。
  -  AppにはAndroid 4.1およびそれ以降のバージョンのデバイスが必要です。
**iOS & macOS端末向け開発：**
  - Xcode 11.0およびそれ以降のバージョン。
  - osxシステムには10.11およびそれ以降のバージョンが必要です。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。
- 環境構築については、[公式ドキュメント](https://reactnative.cn/docs/environment-setup)をご参照ください。

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com)を行い、実名認証が完了済みであること。

## 操作手順
[](id:step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援>[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2．**アプリケーションの作成**をクリックし、`TestTRTC`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合、**既存のアプリケーションを選択**をクリックします。
3. 実際の業務ニーズに応じてタグを追加または編集し、**作成**をクリックします。


>?
>-アプリケーション名には、数字、中国語と英語の文字、アンダーラインのみを含めることができ、15文字以内とします。
タグはTencent Cloudのさまざまなリソースを識別して管理するために使用されます。たとえば、企業に複数の事業部門があり、各部門に1つ以上のTRTCアプリケーションがある場合、企業はTRTCアプリケーションにタグを追加することで部門情報にマークを付けることができます。タグは入力必須ではありません。実際のビジネスニーズに応じてタグを追加または編集できます。

[](id:step2)
### ステップ2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務のニーズに応じて、SDKと付属の[Demoソースコード](https://github.com/c1avie/TRTCReactNativeDemo)をダウンロードします。
2. ダウンロード完了後、**ダウンロードしました。次のステップ**をクリックします。

>! 現在、コンソールからはReactNative Demoをダウンロードできません。**直接上記のリンクからDemoソースコードをダウンロードしてください**。

[](id:step3)
### ステップ3：Demo プログラムファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `/debug/config.js`ファイルを見つけて開きます。
3. `SDKAPPID`と`SECRETKEY`パラメータを設定します。
<ul><li/>SDKAPPID：デフォルトはPLACEHOLDER、実際のSDKAppIDを設定してください。
    <li/>SECRETKEY：デフォルトはPLACEHOLDER、実際のキー情報を設定してください。</ul>
    <img src="https://main.qcloudimg.com/raw/fba60aa9a44a94455fe31b809433cfa4.png"/>
4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>?
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:step4)
### ステップ4：権限の設定
実行するにはAppの権限設定が必要です。
<dx-tabs>
::: Android端末
1. `AndroidManifest.xml`の中でAppの権限を設定します。TRTC SDKには以下の権限が必要です。
```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```
>!  `android:hardwareAccelerated="false"`は設定しないでください。ハードウェアアクセラレーションを無効にすると、相手側のビデオストリームがレンダリングできなくなります。
2. Android端末のオーディオ/ビデオの権限は手動でリクエストする必要があります。
```java
if (Platform.OS === 'android') {
  await PermissionsAndroid.requestMultiple([
    PermissionsAndroid.PERMISSIONS.RECORD_AUDIO, //オーディオが必要
    PermissionsAndroid.PERMISSIONS.CAMERA, //ビデオが必要
  ]);
}
```
:::
::: iOS端末
`Info.plist`の中でAppの権限を設定します。TRTC SDKには以下の権限が必要です。
```objectiveC
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
:::
</dx-tabs>

[](id:step5)
### 手順5：コンパイル動作
Metroを起動し、React Nativeプロジェクトディレクトリ下で`npx react-native start`を実行します。
<dx-tabs>
:::  Android端末
新しいウィンドウが開き、開発/デバックが起動します。
```
npx react-native run-android
```
:::
::: iOS端末
1. iOSのディレクトリで`pod install`を実行し、依存をインストールします。
2. iOSのディレクトリ下で`.xcworkspace`を開いて、iOSプロジェクトを起動し、iOSプロジェクトディレクトリに空のswift ファイルを新規作成します。
![](https://qcloudimg.tencent-cloud.cn/raw/1b243c324d9e1e93d113d2431922c4de.jpeg)
3. その後すぐにポップアップウィンドウが開き、ブリッジングヘッダーファイルを作成するか尋ねてきますので、**Create Bridging Header**をクリックして確定します。
![](https://qcloudimg.tencent-cloud.cn/raw/8329b913890721ceef19be314462905d.png)
2. 新しいウィンドウが開き、開発/デバックが起動します。
```
npx react-native run-ios
```
::: 
</dx-tabs>

​                   