このドキュメントでは、主にTRTC SDK(Android)をプロジェクトに迅速に統合する方法を紹介します。以下のステップにしたがって設定すれば、SDK統合のタスクを完了できます。

## 開発環境要件
- Android Studio 3.5+。
- Android 4.1（SDK API 16）およびそれ以上のシステム。

## SDKの統合（aar）

Gradleを使って自動でローディングするか、または手動でaarをダウンロードし、それをプロジェクトにインポートする方式を選択できます。

### 方法1：自動ローディング（aar）
TRTC SDK はjCenterでライブラリを公開していますので、Gradleを設定すれば、自動でダウンロードされ、更新されます。
Android Studioを使って SDKを統合したいプログラム（ここでの例は、[TRTCScenesDemo](https://github.com/tencentyun/LiteAVClassic/tree/master/Android/TRTCScenesDemo)）を開き、その後簡単な3つのステップで app/build.gradle ファイルを修正しさえすれば、SDKの統合が完成します。
![](https://main.qcloudimg.com/raw/47b8e9f7ee41895a479334f16dd50a12.png)

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
3．【Sync Now】をクリックし、自動でSDKをダウンロードし、プロジェクトに統合します。


### 方法2：手動ダウンロード（aar）
お客様のネットワークとjCenterの接続に問題がある場合は、SDKを手動でダウンロードし、プログラムに統合することができます。

1. 最新バージョンの[TRTC SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip)をダウンロードします。
2. ダウンロードした aar ファイルをプログラムの**app/libs** ディレクトリの下にコピーします。
3. プログラムのルートディレクトリの下の build.gradle の中に、**flatDir**を追加し、ローカルライブラリのパスを指定します。
![](https://main.qcloudimg.com/raw/3b07d38f105167ae52ffdda9a1712cec.png)
4. app/build.gradleの中に、aar パッケージのコードを追加して引用します。
![](https://main.qcloudimg.com/raw/143621f900eb6f7b867d89b71c0dd13d.png)
5.app/build.gradle的defaultConfigの中で、Appが使用するCPUアーキテクチャを指定します。
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?現在 TRTC SDKは、armeabi、armeabi-v7a、arm64-v8aをサポートしています。
6. 【Sync Now】をクリックして、TRTC SDK統合のタスクは完了です。


## SDKの統合（jar）
aarライブラリを統合したくない場合は、jarおよび soライブラリをインポートする方式で TRTC SDKを統合することが可能です。

1. 最新バージョンのjar 圧縮パッケージを[ダウンロード](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip) します。ファイルパスは`SDK/LiteAVSDK_TRTC_xxx.zip` （このうち xxx は TRTC SDKのバージョンナンバー）です。
2. 解凍するとlibsディレクトリが取得できます。中には主にjar ファイルと so ファイルフォルダが含まれています。
3. 解凍したjar ファイルおよび armeabi、 armeabi-v7a、 arm64-v8a ファイルフォルダを app/libs ディレクトリの下にコピーします。
![](https://main.qcloudimg.com/raw/c7b498b40bff8c248cd72fcd01f07933.png)
4. app/build.gradleの中に、jar ライブラリのコードを追加して引用します。
![](https://main.qcloudimg.com/raw/5369b8c9bbb855622b22c7843a591e2e.png)	
5. app/build.gradleの中に、soライブラリのコードを追加して引用します。
```
sourceSets {
       main {
           jniLibs.srcDirs = ['libs']
       }
}
```
![](https://main.qcloudimg.com/raw/7aa7eea5d26086b0b9c54ef7a910c6dd.png)
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
-keep class com.tencent.** { *; }
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
![](https://main.qcloudimg.com/raw/b847d95fc05d2b97f85ffdb0b89438cc.png)


[](id:using_cpp)
##  C++ インターフェースを介してSDKを使用（オプション）
開発にJavaではなくC++ インターフェースを使用したい場合は、この手順を実行できます。Java言語のみを使用してTRTC SDKを呼び出す場合は、この手順を無視してください。
1.まず、上記の指示に従ってjarおよび soライブラリをインポートする方式で TRTC SDKを統合します。
2.ヘッダーファイルをコピー：SDK中のC++ヘッダーファイルをプロジェクトにコピーし（パス：`SDK/LiteAVSDK_TRTC_xxx/libs/include`）、CMakeLists.txtでincludeフォルダーパスと soライブラリの動的リンクを設定します。
```
cmake_minimum_required(VERSION 3.6)

#  C++ インターフェースヘッダーファイルパスの設定
include_directories(
        ${CMAKE_CURRENT_SOURCE_DIR}/include  # SDK/LiteAVSDK_TRTC_xxx/libs/includeからコピーする
)

add_library(
        native-lib
        SHARED
        native-lib.cpp)

# libliteavsdk.so動的ライブラリパスの設定
add_library(libliteavsdk SHARED IMPORTED)
set_target_properties(libliteavsdk  PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/../../../libs/${ANDROID_ABI}/libliteavsdk.so)

find_library(
        log-lib
        log)

# libliteavsdk.so 動的リンクの設定
target_link_libraries(
        native-lib
        libliteavsdk
        ${log-lib})
```
3. ネームスペースの利用：C++ のすべてのプラットフォームのインターフェースのメソッド、タイプなどはいずれも trtc ネームスペースで定義されています。コードをより簡潔にするため、trtc ネームスペースを直接使用することをお勧めします。
```
using namespace trtc;
```

>?
>- Android Studio C/C++  開発環境の設定方法は、Android Studioの公式ドキュメントをご参照ください：[プロジェクトへのC/C++コードの追加](https://developer.android.com/studio/projects/add-native-code) 。 
>- 現在、TRTCバージョンのSDKのみがC++インターフェースをサポートしています。C++ インターフェースの使用方法については、 [全プラットフォーム（C++）APIの概要](https://intl.cloud.tencent.com/document/product/647/35131)をご参照ください。
