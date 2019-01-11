Tencent Cloudゲームマルチメディアエンジン（GME）SDKへようこそ。Android開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、ここでAndroid開発のためのプロジェクト構成を紹介します。

## SDKの準備

SDKは以下の方法で入手できます。

### SDKのダウンロード

[ダウンロードガイド](https://cloud.tencent.com/document/product/607/18521)で関連のDemoとSDKをダウンロードしてください。

画面でAndroidバージョンのSDKリソースを見つけます。

ダウンロードしたSDKリソースを解凍後に次の内容が含まれます。

|ファイル名       | 説明           
| ------------- |:-------------:|
| Libs     	| 開発キットLibs     |

## システム要件
SDKはAndroid 4.2以上のシステムでサポートされますが、ハードウェアコーディングを有効にできるのは、（Android 4.3）API 18以上のみです。

## 準備作業

### SDKファイルのインポート

下図のように、開発キットのlibsディレクトリからmobilepb.jar、tmgsdk.jar、およびwup-1.0.0-SNAPSHOT.jarをAndroidプロジェクトのlibsディレクトリにコピーします（プロジェクトにlibsディレクトリがない場合は、libsディレクトリを作成します。armeabiとarmeabi-v7aがない場合は、あわせてlibsディレクトリにコピーします）。  
![](https://main.qcloudimg.com/raw/006cc0fab7b4c2f370b9b31fdbc93f90.png)

### プロジェクトの構成

プロジェクトのAppディレクトリのbuild.gradleに、参照ライブラリのコードを追加します。  

```
sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
}
```

### App権限の構成

プロジェクトのAndroidManifest.xmlファイルに以下の権限を追加します：

```
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
  <uses-permission android:name="android.permission.READ_PHONE_STATE" />
  <uses-permission android:name="android.permission.BLUETOOTH"/>
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
  <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS"/>
	```

