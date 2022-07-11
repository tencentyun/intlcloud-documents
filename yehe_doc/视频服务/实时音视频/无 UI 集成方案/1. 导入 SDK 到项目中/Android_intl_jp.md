このドキュメントでは、SDKのプロジェクトへのインポート方法を紹介します：
![](https://qcloudimg.tencent-cloud.cn/raw/956dded61564c3a29ea8e93238d9a4e1.png)

## 開発環境要件
- Android Studio 3.5+。
- Android 4.1 (SDK API 16）)以上のシステム。

## 手順1：SDKのインポート

### 方法１：自動ロード(aar)
TRTC SDK はmavenCentralライブラリにリリースされています。gradleを構成することにより、自動的にダウンロードと更新できます。
1. dependenciesの中にTRTCSDKの依存を追加します。
```
dependencies{
        implementation 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
```
defaultConfig {
        ndk {
                abiFilters "armeabi-v7a", "arm64-v8a"
        }
}
```
>?現在 TRTC SDKは、armeabi-v7a、arm64-v8aをサポートしています。
3. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)**Sync Now**をクリックして、SDKを自動的にダウンロードし、プロジェクトに統合します。


### 方法2：SDKのダウンロードと手動インポート
1. [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip)をダウンロードし、ローカルに解凍して開きます。
2. 解凍したaarファイルをプロジェクトの**app/libs**ディレクトリの下にコピーします。
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
6. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)**Sync Now**をクリックして、TRTC SDKの統合を完了します。

## 手順2：App権限の構成
AndroidManifest.xml の中で Appの権限を設定します。TRTC SDKには次の権限が必要となります：
```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```

>!  `android:hardwareAccelerated="false"`は設定しないでください。ハードウェアアクセラレーションを無効にすると、相手側のビデオストリームがレンダリングできなくなります。

## 手順3：混同規則の設定
proguard-rules.pro ファイルで、 TRTC SDK関連のクラスを非混同リストに追加します：
```java
-keep class com.tencent.** { *; }
```

[](id:using_cpp)
##  C++ インターフェースを介してSDKを使用（オプション）
開発にJavaではなくC++ インターフェースを使用したい場合は、この手順を実行できます。Java言語のみを使用してTRTC SDKを呼び出す場合は、この手順を無視してください。
1.まず、上記の指示に従ってjarおよび soライブラリをインポートする方式で TRTC SDKを統合します。
2.ヘッダーファイルをコピー：SDK中のC++ヘッダーファイルをプロジェクトにコピーし（パス：`SDK/LiteAVSDK_TRTC_xxx/libs/include`）、CMakeLists.txtでincludeフォルダーパスと soライブラリの動的リンクを設定します。
```java
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
3. ネームスペースの利用：C++ のすべてのプラットフォームのインターフェースのメソッド、タイプなどはいずれも trtc ネームスペースで定義されています。コードをより簡潔にするため、trtc ネームスペースを直接使用することをお勧めします
```
using namespace trtc;
```

>?
>- Android Studio C/C++  開発環境の設定方法は、Android Studioの公式ドキュメントをご参照ください：[プロジェクトへのC/C++コードの追加](https://developer.android.com/studio/projects/add-native-code) 。 
>- 現在、TRTCバージョンのSDKのみがC++インターフェースをサポートしています。C++ インターフェースの使用方法については、 [全プラットフォーム（C++）APIの概要](https://intl.cloud.tencent.com/document/product/647/35131)をご参照ください。


