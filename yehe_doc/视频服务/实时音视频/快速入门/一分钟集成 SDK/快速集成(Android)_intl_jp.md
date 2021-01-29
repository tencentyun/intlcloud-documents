このドキュメントでは、次の手順でTencent Cloud TRTC SDK for Androidをプロジェクトにすばやく統合する方法について説明します。

## 開発環境の要件
- Android Studio 3.5+。
- Android 4.1（SDK API 16）以上のシステム。

## SDKの統合（aar）

Gradle自動ロード方法を選択、使用するか、または手動でaarをダウンロードしてから現在のプロジェクトにインポートします。

### 方法１：自動ロード（aar）
TRTC SDK は、jcenterリポジトリにリリースされ、更新を自動的にダウンロードするようにGradleを設定できます。
Android Studioを使用して SDK を統合する必要のあるプロジェクト（ここでは [TRTCSimpleDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCSimpleDemo)を例にしています）を開いて、その後簡単な三つの手順によって app/build.gradleファイルを変更してSDKの統合を完了します。
![](https://main.qcloudimg.com/raw/fd01c252724cbf31ec7356286a931661.png)

1. TRTCSDKの依存関係をdependencies に追加します。
 - 3.xバージョンの com.android.tools.build:gradle ツールを使用する場合は、以下のコマンドを実行してください：
```
dependencies {
         implementation 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
 - 2.xバージョンの com.android.tools.build:gradle ツールを使用する場合は、以下のコマンドを実行してください：
```
dependencies {
         compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2.  defaultConfig で Appを使用するCPU アーキテクチャを指定します。
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>現在 TRTC SDK は armeabi 、 armeabi-v7a および arm64-v8aをサポートしています。
>
3．【Sync Now】をクリックし、SDKを自動的にダウンロードしてプロジェクトに統合します。


### 方法二：手動によるダウンロード（aar）
JCenterに接続できない場合は、SDKを手動でダウンロードして、プロジェクトに統合することもできます。

1. 最新バージョンの [TRTC SDK](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)をダウンロードします。
2. ダウンロードした aar ファイルをプロジェクトの **app/libs** ディレクトリにコピーします。
3. プロジェクトルートディレクトリの build.gradleにおいて、 **flatDir**を追加し、ローカルリポジトリパスを指定します。
![](https://main.qcloudimg.com/raw/bc3215028103fe980aedcbf011b97b02.png)
4．aarライブラリをインポートするコードをapp / build.gradleに追加します。
![](https://main.qcloudimg.com/raw/449a4a2d8d7cb2503da9fb480beb9c32.png)
5．app/build.gradleのdefaultConfig では、 Appを使用するCPUアーキテクチャを指定します。 
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>現在 TRTC SDK は armeabi 、 armeabi-v7a および arm64-v8aをサポートしています。
>
6. 【Sync Now】をクリックし、TRTC SDK の統合作業を完了します。


## SDK (jar) を統合
aarライブラリを統合したくない場合は、jarなどのライブラリをインポートしてTRTC SDKを統合することを選択できます。

1. 最新バージョンのjar 圧縮パッケージを[ダウンロード](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)し、ファイルパスは`SDK/LiteAVSDK_TRTC_xxx.zip` になります（xxxはTRTC SDKのバージョン番号を示します）。
2．解凍後、jarファイルなどのフォルダを含むlibsディレクトリを取得できます。
3. 解凍によって得られた jar ファイルおよび armeabi， armeabi-v7a， arm64-v8a フォルダを app/libs ディレクトリにコピーします。
![](https://main.qcloudimg.com/raw/5bf82ca89b3a14cca470fcedc048d7fa.png)
4. jarライブラリをインポートするコードをapp/build.gradle に追加します。
![](https://main.qcloudimg.com/raw/6ffbb4b79c06555376b137c849b43bb7.png)	
5．soライブラリをインポートするコードをapp/build.gradle に追加します。
```
sourceSets {
       main {
           jniLibs.srcDirs = ['libs']
       }
}
```
![](https://main.qcloudimg.com/raw/299eeb5b3e8961e816f3ce17b97b4339.png)
6.  app/build.gradle の defaultConfig で、 App で使用する CPU アーキテクチャを指定します。 
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?現在の TRTC SDK では armeabi、armeabi-v7a および arm64-v8aをサポートしています。
>
7．【Sync Now】をクリックし、TRTC SDKの統合作業を完了します。


## App権限の設定
 AndroidManifest.xml に Appの権限を設定するには、TRTC SDK は以下の権限が必要です：

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/ >
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/ >
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```
>!  `android:hardwareAccelerated="false"`を設定しないでください。ハードウェアアクセラレーションを停止すると、先方のビデオストリームがレンダリングできなくなります。

## 難読化ルールの設定
 proguard-rules.pro ファイルでは、 TRTC SDK 関連を非難読化リストに追加します。

```
-keep class com.tencent.** { *;}
```
## アプリケーションパッケージパラメータの設定
次のコードをapp/build.gradleに追加します。

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


