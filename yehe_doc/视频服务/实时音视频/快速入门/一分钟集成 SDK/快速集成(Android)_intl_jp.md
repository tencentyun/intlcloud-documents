このドキュメントでは、主にTencent Cloud TRTC SDK(Android)をプロジェクトに迅速に統合する方法を紹介します。以下のステップにしたがって設定すれば、SDK統合のタスクを完了できます。

## 開発環境要件
- Android Studio 3.5+。
- Android 4.1（SDK API 16）およびそれ以上のシステム。

## SDKの統合（aar）

Gradleを使って自動でローディングするか、または手動でaarをダウンロードし、それをプロジェクトにインポートする方式を選択できます。

### 方法1：自動ローディング（aar）
TRTC SDK はjCenterでライブラリを公開していますので、Gradleを設定すれば、自動でダウンロードされ、更新されます。
Android Studioを使って SDKを統合したいプログラム（ここでの例は、[TRTCSimpleDemo]）を開き、その後簡単な3つのステップで app/build.gradle ファイルを修正しさえすれば、SDKの統合が完成します。
![](https://main.qcloudimg.com/raw/fd01c252724cbf31ec7356286a931661.png)

1. dependenciesの中にTRTCSDKの依存を追加します。
 - 3.xバージョンの com.android.tools.build:gradle のツールを使用している場合は、次のコマンドを実行してください。
```
dependencies {
         implementation 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
 - 2.xバージョンの com.android.tools.build:gradle のツールを使用している場合は、次のコマンドを実行してください。
```
dependencies {
         compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. defaultConfigの中で、Appが使用するCPUアーキテクチャを指定します。
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?現在 TRTC SDKは、armeabi、armeabi-v7a、arm64-v8aをサポートしています。
>
3.【Sync Now】をクリックして、 SDKを自動ダウンロードし、プログラムに統合します。


### 方法2：手動ダウンロード（aar）
お客様のネットワークとjCenterの接続に問題がある場合は、SDKを手動でダウンロードし、プログラムに統合することができます。

1. 最新バージョンの[TRTC SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip)をダウンロードします。
2. ダウンロードした aar ファイルをプログラムの**app/libs** ディレクトリの下にコピーします。
3. プログラムのルートディレクトリの下の build.gradle の中に、**flatDir**を追加し、ローカルライブラリのパスを指定します。
![](https://main.qcloudimg.com/raw/bc3215028103fe980aedcbf011b97b02.png)
4. app/build.gradleの中に、aar パッケージのコードを追加して引用します。
![](https://main.qcloudimg.com/raw/449a4a2d8d7cb2503da9fb480beb9c32.png)
5.app/build.gradleのdefaultConfigの中で、Appが使用するCPUアーキテクチャを指定します。
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>現在TRTC SDKは、armeabi、armeabi-v7a、arm64-v8aをサポートしています。
>
6. 【Sync Now】をクリックして、TRTC SDK統合のタスクは完了です。


## SDKの統合（jar）
aarライブラリを統合したくない場合は、jarおよび soライブラリをインポートする方式で TRTC SDKを統合することが可能です。

1. 最新バージョンのjar 圧縮パッケージを[ダウンロード](http://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip) します。ファイルパスは`SDK/LiteAVSDK_TRTC_xxx.zip` （このうち xxx は TRTC SDKのバージョンナンバー）です。
2. 解凍するとlibsディレクトリが取得できます。中には主に jar ファイルと so ファイルフォルダが含まれています。
3. 解凍したjar ファイルおよび armeabi、 armeabi-v7a、 arm64-v8a ファイルフォルダを app/libs ディレクトリの下にコピーします。
![](https://main.qcloudimg.com/raw/5bf82ca89b3a14cca470fcedc048d7fa.png)
4. app/build.gradleの中に、jar ライブラリのコードを追加して引用します。
![](https://main.qcloudimg.com/raw/6ffbb4b79c06555376b137c849b43bb7.png)	
5. app/build.gradleの中に、soライブラリのコードを追加して引用します。
```
sourceSets {
       main {
           jniLibs.srcDirs = ['libs']
       }
}
```
![](https://main.qcloudimg.com/raw/299eeb5b3e8961e816f3ce17b97b4339.png)
6. app/build.gradleの defaultConfigの中で、Appが使用するCPUアーキテクチャを指定します。 
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?現在 TRTC SDKは、armeabi、armeabi-v7a、arm64-v8aをサポートしています。
>
7. 【Sync Now】をクリックして、TRTC SDK統合のタスクは完了です。


## App 権限の設定
AndroidManifest.xml の中で Appの権限を設定します。TRTC SDKには次の権限が必要となります。

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

## 混同ルールの設定
proguard-rules.pro ファイルで、 TRTC SDK関連のクラスを非混同リストに追加します。

```
-keep class com.tencent.** { *;}
```
## Appパッケージングのパラメータの設定
app/build.gradleの下に、次の情報を追加します。

```
packagingOptions {
	pickFirst '**/libc++_shared.so'
	doNotStrip "*/armeabi/libYTCommon.so"
	doNotStrip "*/armeabi-v7a/libYTCommon.so"
	doNotStrip "*/x86/libYTCommon.so"
	doNotStrip "*/arm64-v8a/libYTCommon.so"
}
```
![](https://main.qcloudimg.com/raw/e40d5c294a59d56a1f89f20960c7e4c1.png)


