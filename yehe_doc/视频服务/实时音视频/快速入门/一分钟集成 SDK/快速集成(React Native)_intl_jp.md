ここでは、主にTencent Cloud TRTC SDK(React Native)をプロジェクトに素早く統合する方法をご紹介します。以下の手順に従って設定すれば、SDKの統合作業を完了できます。

## 環境要件
- ReactNative 0.63およびそれ以降のバージョン。
- Node & Watchman。nodeバージョンはv12以上が必要です。
- **Android端末向け開発：**
  -  Android Studio 3.5およびそれ以降のバージョン。
  -  AppにはAndroid 4.1およびそれ以降のバージョンのデバイスが必要です。
  - Java Development Kit
**iOS & macOS端末向け開発：**
  - Xcode 11.0およびそれ以降のバージョン。
  - osxシステムには10.11およびそれ以降のバージョンが必要です。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。
- 環境構築については、[公式ドキュメント](https://reactnative.cn/docs/environment-setup)をご参照ください。

## SDKの統合
ReactNative SDKは、[npm](https://www.npmjs.com/package/trtc-react-nativeですでに公開されています。`package.json`を設定することでセットアップできます。
1. プロジェクトの`package.json`に以下の依存を書き入れます。
```
"dependencies": {
  "trtc-react-native": "^2.0.0"
},
```
2. **カメラ**と**マイク**の許可が有効になると、音声通話機能が起動します。
<dx-tabs>
::: Android端末
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
1. `Info.plist`にカメラとマイクの許可申請を追加する必要があります。
```objectiveC
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
2. react nativeライブラリについては、[react native libraries](https://reactnative.cn/docs/linking-libraries-ios)をご参照ください。
::: 
</dx-tabs>



