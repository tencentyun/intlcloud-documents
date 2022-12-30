ここでは、主にTencent Cloud View Cube·Player SDKをプロジェクトに素早く統合する方法を紹介します。各バージョンのSDKの統合方法はすべて共通です。以下の手順に従って設定すれば、 SDKの統合作業を完了できます。

## 開発環境要件
- Android Studio 2.0+。
- Android 4.1（SDK API 16）およびそれ以上のシステム。

## SDKの統合（aar）
Gradleを使って自動でローディングするか、または手動でaarをダウンロードし、それをプロジェクトにインポートする方式を選択できます。

### 方法1：自動ローディング（aar） 
Player SDKは[mavenCentralリポジトリ](https://repo1.maven.org/maven2/com/tencent/liteav/LiteAVSDK_Player_Premium/)に公開済みです。gradleにmavenCentralリポジトリを設定することで、LiteAVSDK_Player_Premiumを自動的にダウンロードして更新できます。
Android Studioを使用すれば、SDKを統合したいプロジェクトを開き、その後簡単な4つの手順で`build.gradle`ファイルを変更するだけで、SDKの統合を完了できます。
![](https://qcloudimg.tencent-cloud.cn/raw/7de67c57e87f2803217b77ed308d537d.png)

1. プロジェクトのルートディレクトリ下のbuild.gradleにmavenCentralリポジトリを追加します。
```xml
repositories {
    mavenCentral()
}
```

2. app下のbuild.gradleを開き、dependenciesにLiteAVSDK_Playerの依存を追加します。
```
dependencies{
  // この設定ではデフォルトでLiteAVSDK_Player_Premiumの最新バージョンを統合します
	implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:latest.release'
  // バージョン10.8.0.29000などの過去バージョンを統合する場合は、次の方法で行えます
  // implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:10.8.0.29000'
}
```
3. defaultConfigで、Appが使用するCPUアーキテクチャを指定します（現在LiteAVSDK_Playerはarmeabi、armeabi-v7aおよびarm64-v8aをサポートしています）。
```
defaultConfig {
	ndk {
		abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
	}
}
```
4. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)Sync Nowボタンをクリックし、SDKを同期させます。mavenCentralへのネットワーク接続に問題がなければ、SDKが自動的にダウンロードされプロジェクトに統合されます。

### 方法2：手動ダウンロード（aar）
mavenCentralへのネットワーク接続に問題がある場合は、手動でSDKをダウンロードしてプロジェクトに統合することもできます。
1. [LiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_Android_latest.zip)をダウンロードし、ダウンロードが完了したら解凍します。
2. ダウンロードしたファイルを解凍後、SDKディレクトリ下のaarファイルをプロジェクトの**app/libs** ディレクトリにコピーします。
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab00ad0f12a271750d6f84f7333f8cd3.png)
3. プログラムのルートディレクトリの下の build.gradle の中に、**flatDir**を追加し、ローカルライブラリのパスを指定します。
    ![](https://main.qcloudimg.com/raw/726771558714a2b4fae8dc1a59c33ffc.png) 
4. LiteAVSDK_Player_Premiumの依存を追加し、app/build.gradleにaarパッケージを参照するコードを追加します。
    ![](https://qcloudimg.tencent-cloud.cn/raw/ac9ab42dda8992d435832c605f1e6798.png)
```
implementation(name:'LiteAVSDK_Player_10.8.0.29000', ext:'aar')
```
5. `app/build.gradle`のdefaultConfigで、Appが使用するCPUアーキテクチャを指定します（現在LiteAVSDK_Playerはarmeabi、armeabi-v7aおよびarm64-v8aをサポートしています）。
```
defaultConfig {
	ndk {
		abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
	}
}
```
6. Sync NowボタンをクリックしてSDKを同期させ、LiteAVSDKの統合作業を完了します。

## SDKの統合（jar）
aarライブラリを統合したくない場合は、jarおよびsoライブラリの方式をインポートしてLiteAVSDKを統合することもできます。

1. [LiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_Android_latest.zip)をダウンロードし、ダウンロードが完了したら解凍します。SDKディレクトリで`LiteAVSDK_Player_Premium_xxx.zip`（このうち`xxx`はLiteAVSDKのバージョン番号）を見つけ、解凍してlibsディレクトリを取得します。この中には主にjarファイルとsoフォルダが含まれます。ファイルリストは次のとおりです。
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab82529bd214ba8488f29b45b38f61f6.png)

  armeabiアーキテクチャのsoも必要な場合は、armeabi-v7aディレクトリをコピーし、armeabiとリネームします。

2. 解凍して得られた jarファイルおよび armeabi、armeabi-v7a、arm64-v8aフォルダを`app/libs`ディレクトリにコピーします。
    ![](https://main.qcloudimg.com/raw/d9b6339cb52fb85afda42de6001be337.png)
3. `app/build.gradle`に、jarライブラリを参照するコードを追加します。
    ![](https://main.qcloudimg.com/raw/695520309d9a01b19ce2f50439a42890.png)      
```
dependencies{
	implementation fileTree(dir:'libs',include:['*.jar'])
}
```
4. プログラムのルートディレクトリの下の build.gradle の中に、**flatDir**を追加し、ローカルライブラリのパスを指定します。
![](https://main.qcloudimg.com/raw/6c68b846f6f7258ae4d96bc1d95d7816.png)
5．`app/build.gradle`に、soライブラリを参照するコードを追加します。
![](https://main.qcloudimg.com/raw/e0f2f39c5f53a9fd5ca084febdd4e637.png)
6. `app/build.gradle`のdefaultConfigで、Appが使用するCPUアーキテクチャを指定します（現在LiteAVSDKはarmeabi、armeabi-v7aおよび 
```
defaultConfig {
    ndk {
        abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
    }
}
```
7. Sync NowボタンをクリックしてSDKを同期させ、LiteAVSDKの統合作業を完了します。

## Appパッケージパラメータの設定
![](https://main.qcloudimg.com/raw/dabfd69ee06e4d38bb3b51fc436c0ad1.png)
```
packagingOptions {
	pickFirst '**/libc++_shared.so'
	doNotStrip "*/armeabi/libYTCommon.so"
	doNotStrip "*/armeabi-v7a/libYTCommon.so"
	doNotStrip "*/x86/libYTCommon.so"
	doNotStrip "*/arm64-v8a/libYTCommon.so"
} 
```

## App 権限の設定

AndroidManifest.xmlにAppの権限を設定するには、LiteAVSDKに以下の権限が必要です。

```
<!--ネットワーク権限-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--Storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

## 混同ルールの設定
proguard-rules.proファイルで、 LiteAVSDK関連クラスを非難読化リストに追加します。

```
-keep class com.tencent.** { *; }
```

## License権限承認の設定

[License申請](https://www.tencentcloud.com/document/product/266/51098)をクリックし、テスト用Licenseを取得します。Licenseを設定しないとビデオ再生に失敗します。具体的な操作については[テスト版License](https://www.tencentcloud.com/document/product/266/51098#.E7.94.B3.E8.AF.B7.E6.B5.8B.E8.AF.95.E7.89.88-license)をご参照ください。取得する2つの文字列のうち、1つはlicenseURL、もう1つは復号keyです。

AppがSDKの関連機能を呼び出す前に以下の設定を行います（Applicationクラスに設定することをお勧めします）。

```java
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // 取得したlicence url
        String licenｃeKey = ""; // 取得したlicence key
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
        TXLiveBase.setListener(new TXLiveBaseListener() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
    }
}
```

## 確認方法

License設定に成功後（しばらくかかります。時間の長さはネットワークの状況に応じて異なります）、次のメソッドを呼び出してLicense情報を確認することができます。

```java
TXLiveBase.getInstance().getLicenceInfo();
```

## よくあるご質問

1. プロジェクト内にMLVB SDK/TRTC/プレーヤーなどの、LiteAVSDKシリーズの複数のSDKを統合し、シンボル競合の問題が発生した場合、どのように解決すればよいですか。

2つ以上の製品（ライブストリーミング、プレーヤー、TRTC、UGSV）のLiteAVSDKバージョンを統合した場合、コンパイルの際にライブラリ競合の問題が発生する場合があります。これは、SDKの下層ライブラリに同一のシンボルファイルが存在するためで、ここでは全機能版SDK1つのみを統合することでの解決をお勧めします。全機能版ではライブストリーミング、プレーヤー、TRTC、UGSVがすべて1つのSDKに含まれています。具体的には[SDKダウンロード](https://www.tencentcloud.com/document/product/266/50561)をご参照ください。
