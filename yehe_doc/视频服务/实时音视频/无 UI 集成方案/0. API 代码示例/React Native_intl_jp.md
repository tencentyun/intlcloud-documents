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

##  前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com)をすでに行っていること。

## 操作手順

### ステップ1：アプリケーションの新規作成

1. TRTCコンソールにログインし、【[アプリケーション管理](https://console.tencentcloud.com/trtc/app)】を選択します。
2. 【アプリケーションの作成】をクリックし、`APIExample`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合は、【既存のアプリケーションを選択】にチェックを入れ、【次のステップ】をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### ステップ2：サンプルコードのダウンロード

1. UIなしの統合を選択後、ご自身の業務プラットフォームに合わせて、【[Github](https://github.com/LiteAVSDK/TRTC_ReactNative/tree/main/TRTC-Simple-Demo)】で、関連するSDKと付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【次のステップ】をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### ステップ3：プロジェクトの設定

1. サンプルプロジェクトのクイックスタート段階で【デバッグ段階】を選択します。その後、ご自身のSDKAppID、Secret keyを記録しておきます。
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. ダウンロードしたサンプルコードを開き、`/TRTC-Simple-Demo/debug/config.js`ファイルを見つけて開き、ファイル内の関連パラメータを設定します。
   - SDKAPPID：デフォルトはPLACEHOLDERです。実際のSDKAppIDを設定してください。
   - SECRETKEY：デフォルトはPLACEHOLDERです。実際のSecret keyを設定してください。
3. プロジェクトの設定はこれで完了です。【次のステップ】をクリックしてください。

>?
>- ここで言及したUserSigの発行方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのTRTC-Simple-Demoクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。 UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://www.tencentcloud.com/document/product/647/35166)をご参照ください。

### ステップ4：権限の設定

実行するにはAppの権限設定が必要です。

#### Android端末

1. `AndroidManifest.xml`の中でAppの権限を設定します。TRTC SDKでは以下の権限が必要です。

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

- `android:hardwareAccelerated="false"`は設定しないでください、ハードウェアのアクセラレーションを停止すると、先方のビデオストリームがレンダリングできなくなります。
- Androidのオーディオビデオの権限は手動でリクエストする必要があります。

```Java
if (Platform.OS === 'android') {
  await PermissionsAndroid.requestMultiple([
    PermissionsAndroid.PERMISSIONS.RECORD_AUDIO, //オーディオが必要
    PermissionsAndroid.PERMISSIONS.CAMERA, //ビデオが必要
  ]);
}
```

#### iOS端末

1. `Info.plist`の中でAppの権限を設定します。TRTC SDKには以下の権限が必要です

```ObjectiveC
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```

### ステップ 5：コンパイル実行

`npm install`を先に実行します

#### Android開発デバッグ

1. Demoディレクトリ下でMetrosを起動します

```
npx react-native start
```

2. Demoディレクトリ下で新しいウィンドウを開き、開発デバッグを起動します

```
npx react-native run-android
```

#### iOS開発デバッグ

1. Demo iosディレクトリで`pod install`を実行し、依存をインストールします。
2. Demoディレクトリ下でMetrosを起動します

```
npx react-native start
```

3. Demoディレクトリ下で新しいウィンドウを開き、開発デバッグを起動します（エラーが表示された場合はxcodeを開いてコンパイルとデバッグを行ってください）

```
npx react-native run-ios
```
