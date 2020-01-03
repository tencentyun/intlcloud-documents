Tencent Cloud Gaming Multimedia Engine SDKを利用頂き、有難うございました。Androidを使う開発者たちがTencent Cloud Gaming Multimedia Engineの製品APIのデバッグ・アクセスを手軽に実行できるように、Androidでの開発に向けるプロジェクト構成について説明させていただきます。

## SDK準備

以下の方法でSDKを入手できます。

### SDKのダウンロード

[ダウンロードガイド](https://intl.cloud.tencent.com/document/product/607/18521)から関連DemoとSDKをダウンロードしてください。

インターフェースでAndroid向けのSDKリソースを見付けてください。

ダウンロードしたSDKリソースを解凍すると、以下の構成内容があります。

|ファイル名       | 説明           |
| ------------- |:-------------:|
| Libs     | 開発ツールキットLibs     |

## システム要件
SDKはAndroid 4.2以降のシステムでの動作をサポートしていますが、ハードウェアエンコードを有効にするには、（Android 4.3）API 18以降のシステムが必要です。

## 準備作業

## SDKファイルのインポート

図に示している通り、開発ツールキットのlibsディレクトリにあるmobilepb.jar、tmgsdk.jar、およびwup-1.0.0-SNAPSHOT.jarをAndroidプロジェクトのlibsディレクトリにコピーします（プロジェクトにlibsディレクトリがない場合、自分でそのディレクトリを作成してください、また、armeabiとarmeabi-V7aがない場合も、対応ファイルをlibsディレクトリにコピーしてください）。  
![](https://main.qcloudimg.com/raw/006cc0fab7b4c2f370b9b31fdbc93f90.png)

## プロジェクトの構成

プロジェクトAppディレクトリ中のbuild.gradleに、引用ライブラリのコードを追加します。  

```
sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
}
```

## App権限の設定

プロジェクトのAndroidManifest.xmlファイルに、下記の権限を追加します。


```
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
  <uses-permission android:name="android.permission.BLUETOOTH"/>
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/ >
```

オフライン音声を利用する場合は、リストファイルapplicationノードの下にオフライン音声を追加してください。
```
  <application android:usesCleartextTraffic="true" >
```

### Appの難読化関連
コードの難読化を実施するには、下記の構成が必要です。
```
-dontwarn com.tencent.**
-keep class com.tencent.** { *;}
-keepclassmembers class com.tencent.**{*;}
```

