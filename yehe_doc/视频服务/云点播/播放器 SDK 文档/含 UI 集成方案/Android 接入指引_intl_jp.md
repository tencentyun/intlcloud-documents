## 製品概要
Tencent Cloud View Cube Androidプレーヤーコンポーネントは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。品質モニタリング、ビデオ暗号化、超高速HD（TESHD）、解像度切り替え、ミニウィンドウ再生などの機能を一体化し、あらゆるオンデマンド（VOD）、ライブストリーミング再生のシーンに対応します。完備された機能をパッケージ化するとともに、上位層のUIを提供することで、市場で人気を博す各種ビデオアプリに引けを取らない再生ソフトウェアを短時間で作成することができます。

プレーヤーコンポーネントでは業務上の個別のニーズを満たせない場合で、なおかつお客様にある程度の開発経験がおありの場合は、Player+を統合し、プレーヤーインターフェースおよび再生機能のカスタム開発を行うことも可能です。



## 準備作業
1. より完全で包括的なプレーヤー機能を体験するには、[VOD](https://intl.cloud.tencent.com/product/vod)関連サービスを有効化することをお勧めします。未登録のユーザーはアカウントを登録し、[試用](https://intl.cloud.tencent.com/login)できます。VODサービスを使用しない場合は、この手順をスキップできますが、統合後にプレーヤーの基本機能のみを利用できます。
2. Android Studioをダウンロードします。[Android Studio公式サイト](https://developer.android.com/studio)にアクセスし、ダウンロードしてインストールすることができます。すでにダウンロードしている場合は、この手順をスキップできます。

## このドキュメントから把握できること
1. Tencent Cloud View Cube Androidプレーヤーコンポーネントの統合方法
2. プレイヤーの作成・使用方法


## 統合の準備
### 手順1：プロジェクトのダウンロード
Tencent Cloud View Cube Androidプレーヤーコンポーネントのプロジェクトアドレスは[SuperPlayer_Android](https://github.com/LiteAVSDK/Player_Android)です。

**Tencent Cloud View Cube Androidプレーヤーコンポーネントプロジェクトのダウンロードは、**[プレーヤーコンポーネントZIPパッケージのダウンロード](#zip)**、または**[Gitコマンドでのダウンロード](#git)**のいずれかの方法で行えます。
<dx-tabs>
::: プレーヤーコンポーネントZIPパッケージのダウンロード[](id:zip)
画面の**Code** > **Download ZIP**をクリックして、プレーヤーコンポーネントZIPパッケージを直接ダウンロードすることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Gitコマンドのダウンロード[](id:git)
1. まず、Gitがコンピュータにインストールされていることを確認します。インストールされていない場合は、[Gitのインストールチュートリアル](https://git-scm.com/downloads)を参照し、インストールしてください。
2. 次のコマンドを実行し、プレーヤーコンポーネントのプロジェクトコードをローカルにcloneします。
```shell
git clone git@github.com:tencentyun/SuperPlayer_Android.git
```
以下のメッセージが表示されたら、プロジェクトコードがローカルにcloneされました。
```shell
'SuperPlayer_Android'に複製中...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
オブジェクトの受信中：100% (2637/2637)、571.20 MiB | 3.94 MiB/s、完了。
deltaの処理中：100% (1019/1019)、完了。
```
プロジェクトをダウンロードして、ソースコードを解凍した後のディレクトリは以下のとおりです。

| ファイル名                      | 機能                                                         |
| --------------------------- | ------------------------------------------------------------ |
| LiteAVDemo(Player)          | プレーヤーコンポーネントDemoプロジェクト。Android Studioにインポートして直接実行できます   |
| app                         | メインインターフェースエントリー                                                   |
| superplayerkit              | プレーヤーコンポーネント（SuperPlayerView）。再生、一時停止、ジェスチャー制御などの一般的な機能を備えています |
| superplayerdemo             | プレーヤーコンポーネントDemoコード                                         |
| common                      | ツールタイプのモジュール                                                   |
| SDK                         | View Cube Player SDKには、LiteAVSDK_Player_x.x.x.aar、aar形式で提供されるSDKおよびLiteAVSDK_Player_x.x.x.zip、lib、jar形式で提供されるSDKが含まれます |
| Player説明ドキュメント(Android).pdf | プレーヤーコンポーネント使用ドキュメント                                           |
:::
</dx-tabs>

### 手順2：統合ガイド
この手順では、プレーヤーを統合する方法について説明します。プロジェクトを統合するには、Gradleを使用して自動的に読み込むか、手動でaarをダウンロードし、現在のプロジェクトまたはjar、soライブラリにインポートするという2つの方法を選択できます。
<dx-tabs>
::: Gradle 自動読み込み（AAR）
1. SDK+Demo開発パッケージをダウンロードします。プロジェクトアドレスは、[Android](https://github.com/LiteAVSDK/Player_Android)です。
2. moduleの`Demo/superplayerkit`をプロジェクトにコピーしてから、以下の設定を行います。
   - プロジェクトディレクトリのsetting.gradleに`superplayerkit`をインポートします。
   ```xml
   include ':superplayerkit'
   ```
   - `superplayerkit`プロジェクトのbuild.gradleファイルを開きcompileSdkVersion、buildToolsVersion、minSdkVersion、targetSdkVersionおよびrootProject.ext.liteavSdkの定量値を変更します。
     ![](https://main.qcloudimg.com/raw/fd6bc41bfd8b80fe5e82e3345b6ce73f.png)
   ```xmls
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   
   dependencies{
       //過去のバージョンを統合する場合は、latest.releaseを対応するバージョン（例：10.8.0.29000）に変更できます。
       implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:latest.release'
   }
   ```
   上記の手順を参照し、`common`モジュールをプロジェクトにインポートし、設定してください。
3. gradleにmavenCentralリポジトリを設定することで、LiteAVSDKを自動的にダウンロードして更新します。`app/build.gradle`を開き、以下の設定を行います。
   ![](http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/ed597d17243791576461148950/WWCM0KnCcEQA.png)
   
   1. dependenciesにLiteAVSDK_Player_Premiumの依存を追加します。
```xml
dependencies{
	 implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:latest.release'
	 implementation project(':superplayerkit')
	 // プレーヤーコンポーネントに弾幕を統合するサードパーティライブラリ
	 implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
}
```
   過去のバージョンのLiteAVSDK_Player_Premium SDKを統合したい場合は、[MavenCentral](https://repo1.maven.org/maven2/com/tencent/liteav/LiteAVSDK_Player_Premium/)で過去のバージョンを確認した後、次の方法によって統合することができます。 
```xml
dependencies{
	 // バージョン10.8.0.29000のLiteAVSDK_Player_Premium SDKを統合します
	 implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:10.8.0.29000'
}
```
   2.  `app/build.gradle` defaultConfigで、Appが使用するCPUアーキテクチャを指定します（現在LiteAVSDKはarmeabi、armeabi-v7aおよびarm64-v8aをサポートしています。プロジェクトのニーズに応じて設定することができます）。
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
   3. プロジェクトディレクトリのbuild.gradleにmavenCentralライブラリを追加します。
 ```
 repositories {
		 mavenCentral()
 }
 ```
4. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)Sync Nowボタンをクリックし、SDKを同期させます。mavenCentralへのネットワーク接続に問題がなければ、SDKが直ちに自動的にダウンロードされ、プロジェクトに統合されます。
:::
::: Gradleの手動ダウンロード（AAR）
1. SDK+Demo開発パッケージをダウンロードします。プロジェクトアドレスは、[Android](https://github.com/LiteAVSDK/Player_Android)です。
2. `SDK/LiteAVSDK_Player_Premium_XXX.aar`（XXXはバージョン番号）をappのlibsフォルダにインポートし、moduleの`Demo/superplayerkit`をプロジェクトにコピーします。
3. プロジェクトディレクトリのsetting.gradleに`superplayerkit`をインポートします。
```
include ':superplayerkit'
```
4. `superplayerkit`プロジェクトのbuild.gradleファイルを開きcompileSdkVersion、buildToolsVersion、minSdkVersion、targetSdkVersionおよびrootProject.ext.liteavSdkの定量値を変更します。
![](http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/93519621243791576463697337/xuE8HZ2LdSIA.png)
```xml
compileSdkVersion 26
buildToolsVersion "26.0.2"

defaultConfig {
	 targetSdkVersion 23
	 minSdkVersion 19
}

dependencies{
	 implementation(name:'LiteAVSDK_Player_Premium_10.8.0.29000', ext:'aar')
}
```
上記の手順を参照し、`common`モジュールをプロジェクトにインポートし、設定してください。
   - repositoriesの設定
```xml
repositories {
	 flatDir {
			 dirs '../app/libs'
	 }
}
```
5. `app/build.gradle`に依存を追加します。
```xml
compile(name:'LiteAVSDK_Player_Premium_10.8.0.29000', ext:'aar')
implementation project(':superplayerkit')
// プレーヤーコンポーネントに弾幕を統合するサードパーティライブラリ
implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
```
6. プロジェクトの`build.gradle`に次を追加します。
```xml
allprojects {
	 repositories {
			 flatDir {
					 dirs 'libs'
			 }
	 }
}
```
7. `app/build.gradle` defaultConfigで、Appが使用するCPUアーキテクチャを指定します（現在LiteAVSDKはarmeabi、armeabi-v7aおよびarm64-v8aをサポートしています）。
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
8. Sync Nowボタンをクリックし、SDKを同期させ、プレーヤーコンポーネントの統合作業を完了します。
:::
::: SDKの統合（jar+so）
aarライブラリを統合したくない場合は、jarおよびsoライブラリの方式をインポートしてLiteAVSDKを統合することもできます。
[](id:smallStep_1)
1. プロジェクトアドレス[Android](https://github.com/LiteAVSDK/Player_Android)で、SDK+Demo開発パッケージをダウンロードし、ダウンロードが完了したら解凍します。SDKディレクトリでSDK/LiteAVSDK_Player_Premium_XXX.zip（XXXはバージョン番号）を見つけて解凍し、jarファイルとsoフォルダを含むlibsディレクトリを取得します。ファイルリストは次のとおりです。
 ![](https://qcloudimg.tencent-cloud.cn/raw/ab928524839c7944f78d504c0e637586.png)
2. moduleの`Demo/superplayerkit`をプロジェクトにコピーし、その後、プロジェクトディレクトリのsetting.gradleに`superplayerkit`をインポートします。
```xml
include ':superplayerkit'
```
3. [ステップ1](#smallStep_1)で解凍して取得したlibsフォルダを`superplayerkit`プロジェクトルートディレクトリにコピーします。
4. `superplayerkit/build.gradle`ファイルを修正します。
![](https://main.qcloudimg.com/raw/ed66e7d887bc5c28c2eff45807037c23.png)
```xml
compileSdkVersion 26
buildToolsVersion "26.0.2"

defaultConfig {
	 targetSdkVersion 23
	 minSdkVersion 19
}
```
上記の手順を参照し、`common`モジュールをプロジェクトにインポートし、設定してください。
   - sourceSetsを設定し、soライブラリ参照コードを追加します。
```xml
sourceSets{
		 main{
				 jniLibs.srcDirs = ['libs']
		 }
 }
```
   - repositoriesを設定し、flatDirを追加して、ローカルレジストリパスを指定します。
```xml
repositories {
	 flatDir {
			 dirs 'libs'
	 }
}
```
5. `app/build.gradle`defaultConfigで、Appが使用するCPUアーキテクチャを指定します（現在LiteAVSDKはarmeabi、armeabi-v7aおよびarm64-v8aをサポートしています）。
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
6. Sync Nowボタンをクリックし、SDKを同期させ、プレーヤーコンポーネントの統合作業を完了します。
:::
</dx-tabs>
Tencent Cloud View Cube Androidプレーヤーコンポーネントプロジェクトの統合手順はこれで完了です。

### 手順3： App権限の設定
AndroidManifest.xmlにAppの権限を設定するには、LiteAVSDKに以下の権限が必要です。

```java
<!--ネットワーク権限-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VODプレーヤーのフローティングウィンドウ権限-->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--Storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```


### 手順4：混同ルールの設定
proguard-rules.pro ファイルで、 TRTC SDK関連のクラスを非混同リストに追加します。
```xml
-keep class com.tencent.** { *; }
```
Tencent Cloud View Cube Androidプレーヤーコンポーネントapp権限設定手順はこれで完了です。

### 手順5：プレーヤー機能の使用
この手順は、ユーザーがプレーヤーを作成・使用し、プレーヤーでビデオを再生できるようにガイドするのに使用されます。
1. **プレーヤーの作成**[](id:usePlayer)
プレーヤーのメインクラスは`SuperPlayerView`です。作成後すぐにビデオを再生できます。 FileIDまたはURLによる再生の統合をサポートしています。レイアウトファイルにSuperPlayerViewを作成します。
```xml
<!-- プレーヤーコンポーネント-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```
2. **License権限承認の設定**
すでに関連するLicense権限承認を取得している場合は、[Tencent Cloud View Cubeコンソール](https://console.cloud.tencent.com/vcube)にて、License URLおよびLicense Keyを取得する必要があります。

License権限承認を取得していない場合は、先に<a href="https://cloud.tencent.com/document/product/881/74588">ビデオ再生License</a>をご参照の上、関連の権限承認を取得する必要があります。<br>
License情報を取得後、SDKの関連インターフェースを呼び出す前に、以下のインターフェースでLicenseを初期化します。Application類で以下の設定を行うことをお勧めします。
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

3. **ビデオの再生**[](id:playe)
この手順は、ビデオの再生方法についてユーザーにご説明するためのものです。Tencent Cloud View Cube AndroidプレーヤーコンポーネントはライブストリーミングとVODの両方の再生に使用できます。具体的には次のとおりです。
	- VOD再生：プレーヤーコンポーネントは2種類のVOD再生方式をサポートしています。Tencent CloudのVODメディアリソースを[FileIDで再生](#fileid)することも、[URL再生](#url)アドレスから直接再生することもできます。
	- ライブストリーミング再生：プレーヤーコンポーネントは[URL再生](#url)方式でライブストリーミング再生を実現できます。URLアドレスを渡すと、ライブストリーミングオーディオビデオストリームをプルしてライブストリーミングを再生することができます。Tencent Cloud CSSのURL生成方法については、[自身でのライブストリーミングURLの結合](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。

<dx-tabs>
::: URLによる再生（ライブストリーミング、オン・デマンド）[](id:url)
URLはVODファイルの再生アドレスと、ライブストリーミングのプルアドレスのどちらでもかまいません。該当のURLを渡すと、該当のビデオファイルを再生することができます。
```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppIdを設定
model.url = "http://your_video_url.mp4";   // ビデオ再生urlを設定
mSuperPlayerView.playWithModelNeedLicence(model);
```
:::
::: FileIDによる再生（オン・デマンド）[](id:fileid)
ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。
1. クライアントからビデオが公開されると、サーバーがFileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するFileIdが含まれています。

ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。下図のように、IDのところにFileIdが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
>!
>- FileIDを使用して再生する場合は、初めにAdaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはプレーヤーコンポーネントの署名psignを使用して再生するビデオを指定する必要があります。これらを行わないと、ビデオ再生が失敗する可能性があります。トランスコードのチュートリアルおよび説明については [プレーヤーコンポーネントを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)を、psign生成のチュートリアルについては[psignチュートリアル](https://intl.cloud.tencent.com/document/product/266/38099)をそれぞれご参照ください。
>- FileIDを使用して再生する際に「no v4 play info」エラーが表示された場合は、上記の問題が存在する可能性があることを示しているため、上記のチュートリアルに従って調整することをお勧めします。また、ソースビデオの再生リンクを直接取得し、[URLによる再生](#url) 方式で再生することもできます。
>- **トランスコーディングを実行していないソースビデオは、再生中に互換性がないという問題が発生する可能性があります。トランスコーディングを実行したビデオを使用して再生することをお勧めします。**

<dx-codeblock>
:::  java
//リンク不正アクセス防止を有効にせずに再生を行い、その途中で「no v4 play info」エラーが表示された場合は、Adaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはソースビデオの再生リンクを直接取得し、url方式で再生することをお勧めします。

```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329071;// AppIdを設定
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710173650"; // FileIdを設定
// psignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://intl.cloud.tencent.com/document/product/266/38099
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU";
mSuperPlayerView.playWithModelNeedLicence(model);
```

:::
</dx-codeblock>
:::
</dx-tabs>

3. **再生の終了**[](id:exitPlayer)
プレーヤーが不要な時には、`resetPlayer`を呼び出してプレーヤー内部の状態を消去し、メモリをリリースします。
```java
mSuperPlayerView.resetPlayer();
```

これで、Tencent Cloud View Cube Androidプレーヤーコンポーネントの作成、ビデオ再生、再生終了機能の統合が完了しました。

## 機能の使用[](id:moreFeature)

この章では、いくつかの一般的なプレーヤー機能の使用方式をご紹介します。より完全な機能の使用方式は[Demo体験](#demo)を、プレーヤーコンポーネントがサポートする機能は[機能リスト](https://cloud.tencent.com/document/product/881/61375)をそれぞれご参照ください。

### 1. 全画面再生

プレーヤーコンポーネントは全画面再生をサポートしています。全画面再生のシーンでは、同時に画面ロック、ジェスチャーによる音量と明るさの制御、弾幕、スクリーンショット、解像度の切り替えなどの機能設定がサポートされます。機能の効果は**[Tencent Cloud View Cube App](#qrcode) > プレーヤー > プレーヤーコンポーネント**で体験できます。画面右下隅をクリックすると、全画面再生画面に進むことができます。

ウィンドウ再生モードでは、次のインターフェースを呼び出すことで全画面再生モードに入ることができます。

```java
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.FULLSCREEN);
```

#### 全画面再生インターフェースの機能概要

<dx-tabs>
::: ウィンドウに戻る
**戻る**をクリックすると、ウィンドウ再生モードに戻ることができます。

```java
//クリックすると、以下のインターフェースがトリガーされます
mControllerCallback.onBackPressed(SuperPlayerDef.PlayerMode.FULLSCREEN);
onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```
:::
::: 画面ロック[](id:lockscreen)
画面ロック操作により、ユーザーは没入的な再生状態に入ることができます。
```java
//クリックした後にトリガーされるインターフェース
toggleLockState();
```
:::
::: 弾幕[](id:barrage)
弾幕機能をオンにすると、ユーザーが送信したテキストが画面に表示されます。
```java
// 手順1：弾幕Viewへの1つの弾幕の追加
addDanmaku(String content, boolean withBorder);
// 手順2：弾幕の表示または非表示
toggleBarrage();
```
:::
::: スクリーンショット[](id:screenshot)
プレーヤーコンポーネントは再生中にその時点のビデオフレームを切り取ることができる機能をご提供します。画像を保存して共有することができます。画像の4か所のボタンをクリックするとスクリーンショットを作成することができ、切り取った画像はmSuperPlayer.snapshotインターフェースで保存できます。
```java
mSuperPlayer.snapshot(new TXLivePlayer.ITXSnapshotListener() {
  @Override
  public void onSnapshot(Bitmap bitmap) {
        //スクリーンショットをここに保存できます
  }
});
```
:::
::: 解像度の切り替え[](id:resolution)
ユーザーは、HD、SD、UHDなど、ニーズに応じて異なるビデオ再生の解像度を選択できます。
```java
// クリックするとトリガーされる解像度表示viewコードインターフェース
showQualityView();
//以下の項目を選択して、解像度オプションのコールバックインターフェースを選択します
mListView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
  @Override
  public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
    // 解像度ListViewのクリックイベント
    VideoQuality quality = mList.get(position);
    mCallback.onQualitySelect(quality);
  }
});
//最後に解像度を変更するコールバック
@Override
public void onQualityChange(VideoQuality quality) {
   mFullScreenPlayer.updateVideoQuality(quality);
   mSuperPlayer.switchStream(quality);
}
```
:::
</dx-tabs>


### 2. フローティングウィンドウによる再生
プレーヤーコンポーネントはフローティングウィンドウによるミニウィンドウ再生をサポートしています。他のアプリケーションに切り替えてもビデオ再生が中断しない機能です。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント**で体験できます。画面左上隅の**戻る**をクリックすると、フローティングウィンドウ再生機能を体験できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" alt="img" style="zoom:25%;" />
フローティングウィンドウによる再生はAndroidManifestの以下の権限に依存しています。

```java
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
```
```java
// フローティングウィンドウの切り替えによってトリガーされるコードインターフェース
mSuperPlayerView.switchPlayMode(SuperPlayerDef.PlayerMode.FLOAT);
//フローティングウィンドウをクリックして、ウィンドウによってトリガーされたコードインターフェースに戻ります
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```

### 3. ビデオカバー

プレーヤーコンポーネントはユーザーによるビデオカバーのカスタマイズをサポートしています。これはユーザーがビデオの最初のフレーム画面の再生コールバックを受信する前の表示に用いられます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **カバーカスタマイズのデモンストレーション**ビデオで体験できます。


* プレーヤーコンポーネントを自動再生モード`PLAY_ACTION_AUTO_PLAY`に設定すると、ビデオが自動再生されます。このとき、ビデオの最初のフレームをロードするまでの間はカバーが表示されます。
* プレーヤーコンポーネントを手動再生モード`PLAY_ACTION_MANUAL_PLAY`に設定すると、ユーザーが**再生**をクリックしなければ再生が開始されません。**再生**をクリックするまでの間はカバーが表示されます。**再生**をクリックした後、ビデオの最初のフレームをロードするまでの間もカバーが表示されます。

ビデオカバーは、ネットワークURLアドレスまたはローカルFileアドレスの使用をサポートしています。使用方法については、下記のガイドをご参照ください。FileIDでビデオを再生する場合は、VODでビデオカバーを直接構成できます。

```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = "お客様のappid";
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "お客様のfileId"; 
//再生モードは、自動再生モード：PLAY_ACTION_AUTO_PLAYまたは手動再生モード：PLAY_ACTION_MANUAL_PLAYに設定できます
model.playAction = PLAY_ACTION_MANUAL_PLAY;
//カバーのアドレスをネットワークのurlアドレスに設定する場合、coverPictureUrlを設定しなければ、VODコンソールが設定したカバーが自動的に使用されます
model.coverPictureUrl = "http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png" 
mSuperPlayerView.playWithModelNeedLicence(model);
```

### 4. ビデオリストによるカルーセル

プレーヤーコンポーネントはビデオリストの繰り返し再生をサポートしています。ビデオリストを指定すると、次のようになります。

* リスト内のビデオを順番に繰り返し再生することをサポートし、再生プロセス中に次のビデオを自動的に再生すること、および次のビデオに手動で切り替えることをサポートします。
* リストにある最後のビデオの再生が終了すると、リスト内にある最初のビデオは自動的に再生されます。

機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **ビデオリストの繰り返し再生のデモンストレーション**ビデオで体験できます。



```java
//ステップ1:繰り返し再生List<SuperPlayerModel>を作成する
ArrayList<SuperPlayerModel> list = new ArrayList<>();
SuperPlayerModel model = new VideoModel();
model = new SuperPlayerModel();
model.videoId = new SuperPlayerVideoId();
model.appid = 1252463788;
model.videoId.fileId = "4564972819219071568"；
list.add(model);

model = new SuperPlayerModel();
model.videoId = new SuperPlayerVideoId();
model.appid = 1252463788;
model.videoId.fileId = "4564972819219071679"；
list.add(model);
//手順2：カルーセルインターフェースの呼び出し
mSuperPlayerView.playWithModelListNeedLicence(list, true, 0);
```

```java
public void playWithModelListNeedLicence(List<SuperPlayerModel> models, boolean isLoopPlayList, int index);
```

インターフェースパラメータの説明

| パラメータ名     | タイプ   | 説明                                                         |
| -------------- | ---------------------- | ------------------------------ |
| models         | List<SuperPlayerModel> | データリストのカルーセル                   |
| isLoopPlayList | boolean                | 繰り返すかどうか                       |
| index          | int                    | 再生を開始したSuperPlayerModelのインデックス |

### 5. ビデオのトライアル視聴

プレーヤーコンポーネントはビデオプレビュー機能をサポートしています。これは非VIPプレビューなどのシーンに適用でき、開発者は異なるパラメータを渡してビデオのプレビュー時間、プロンプト情報、プレビュー終了画面などを制御することができます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **プレビュー機能のデモンストレーション**ビデオで体験できます。



```java
 方法1：
 //ステップ1：ビデオmodeの作成
 SuperPlayerModel mode = new SuperPlayerModel();
 //...ビデオソース情報の追加
 //手順2：トライアル視聴情報modeの作成
 VipWatchModel vipWatchModel = new VipWatchModel（"%ssトライアル視聴できます。VIPを有効化してビデオの完全版を視聴しましょう"。15)；
 mode.vipWatchMode = vipWatchModel;
 //手順3：ビデオの呼び出し・再生方法
 mSuperPlayerView.playWithModelNeedLicence(mode);

 方法2：
 //手順1：トライアル視聴情報modeの作成
 VipWatchModel vipWatchModel = new VipWatchModel（"%ssトライアル視聴できます。VIPを有効化してビデオの完全版を視聴しましょう"。15)；
  //手順2：トライアル視聴機能の呼び出しと設定
 mSuperPlayerView.setVipWatchModel(vipWatchModel);
```

```java
public VipWatchModel(String tipStr, long canWatchTime)
```

VipWatchModel インターフェースパラメータの説明：

| パラメータ名         | タイプ   | 説明                                   |
| ------------ | ------ | --------- |
| tipStr       | String | トライアル視聴のヒント情報    |
| canWatchTime | Long   | トライアル視聴時間の長さ（単位：秒） |

### 6. ダイナミックウォーターマーク

プレーヤーコンポーネントは再生画面での、不規則に動くテキストウォーターマークの追加をサポートし、不正録画を効果的に防止します。ウォーターマークは全画面再生モードおよびウィンドウ再生モードのどちらでも表示でき、開発者はウォーターマークのテキスト、文字サイズ、色を変更することができます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **動的ウォーターマーク**のデモンストレーションビデオで体験できます。



```java
 方法1：
 //ステップ1：ビデオmodeの作成
 SuperPlayerModel mode = new SuperPlayerModel();
 //...ビデオソース情報の追加
 //ステップ2：ウォーターマーク情報modeの作成
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
 mode.dynamicWaterConfig = dynamicWaterConfig;
 //手順3：ビデオの呼び出し・再生方法
 mSuperPlayerView.playWithModelNeedLicence(mode);

 方法2：
 //ステップ1：ウォーターマーク情報modeの作成
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
  //手順2：ダイナミックウォーターマーク機能の呼び出し・設定方法
 mSuperPlayerView.setDynamicWatermarkConfig(dynamicWaterConfig);
```

```java
public DynamicWaterConfig(String dynamicWatermarkTip, int tipTextSize, int tipTextColor)
```

インターフェースパラメータの説明

| パラメータ名         | タイプ   | 説明                                   |
| ------------------- | ------ | ------ |
| dynamicWatermarkTip | String | ウォーターマークのテキスト情報 |
| tipTextSize         | int    | テキストサイズ   |
| tipTextColor        | int    | テキストの色   |

### 7. 動画のダウンロード

ユーザーがネットワークに接続している状態でビデオをキャッシュした場合、ネットワークに接続していない状態でもビデオを視聴することができます。またオフラインキャッシュしたビデオはクライアント内だけで視聴でき、ローカルへのダウンロードはできないため、ダウンロードしたビデオの違法配信を効果的に防止し、ビデオのセキュリティを保護することができます。
Tencent Cloud View Cube App > プレーヤー > プレーヤーコンポーネント > オフラインキャッシュ（全画面）のデモンストレーションビデオで、全画面視聴モードを使用して体験できます。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rUaM578_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1669772078943.png)

DownloadMenuListView（キャッシュ選択リストビュー）は、対応する解像度のビデオを選択してダウンロードするために使用します。左上隅で解像度を選択し、ダウンロードしたいビデオオプションをクリックし、チェックマークが表示された場合はダウンロードを開始したことを表します。下のvideo download listボタンをクリックすると、VideoDownloadListViewのあるActivityにリダイレクトします。

```java
// ステップ1：ダウンロードデータの初期化（パラメータは下のリストをご参照ください）
DownloadMenuListView mDownloadMenuView = findViewById(R.id.superplayer_cml_cache_menu);
mDownloadMenuView.initDownloadData(superPlayerModelList, mVideoQualityList, mDefaultVideoQuality, "default");
 
// ステップ2：再生中のビデオオプションの設定
mDownloadMenuView.setCurrentPlayVideo(mSuperplayerModel);

// ステップ3：video download listボタンのクリックイベントの設定
mDownloadMenuView.setOnCacheListClick(new OnClickListener() {
     @Override
     public void onClick(View v) {
       // VideoDownloadListViewのあるActivityにリダイレクトします
       startActivity(DownloadMeduListActivity.this,VideoDownloadListActivity.class);
     }
});

// ステップ4:アニメーションによるview表示
mDownloadMenuView.show();
```

```java
public void initDownloadData(List<SuperPlayerModel> superPlayerModelList,
                             List<VideoQuality> qualityList,
                             VideoQuality currentQuality,
                             String userName)
```

インターフェースパラメータの説明

| パラメータ名               | タイプ                   | 説明             |
| -------------------- | ---------------------- | ---------------- |
| superPlayerModelList | List<SuperPlayerModel> | ダウンロードしたビデオデータ   |
| qualityList          | List<VideoQuality>     | ビデオ解像度データ   |
| currentQuality       | VideoQuality           | 現在のビデオ解像度 |
| userName             | String                 | ユーザー名           |

VideoDownloadListView（ビデオダウンロードリスト）には、現在ダウンロード中およびダウンロードが完了したビデオのリストViewが表示されます。クリックすると、現在ダウンロード中の場合はダウンロードが一時停止します。ダウンロード一時停止中の場合はダウンロードを再開します。ダウンロードが完了している場合はジャンプして再生します。

<img src="http://1400155958.vod2.myqcloud.com/facd87c8vodcq1400155958/a69c6b2c387702307128674240/wt31IYPsdQoA.jpg" style="zoom: 33%;" />



```java
// ステップ1：コントロールのバインド
VideoDownloadListView mVideoDownloadListView = findViewById(R.id.video_download_list_view);

//ステップ2: データの追加  
mVideoDownloadListView.addCacheVideo(mDataList, true);

```

インターフェースパラメータの説明

```
public void addCacheVideo(List<TXVodDownloadMediaInfo> mediaInfoList, boolean isNeedClean); 
```

| パラメータ名        | タイプ                         | 説明               |
| ------------- | ---------------------------- | ------------------ |
| mediaInfoList | List<TXVodDownloadMediaInfo> | 追加したビデオデータのタイプ |
| isNeedClean   | boolean                      | 以前のデータをクリアするかどうか |



### 8、スプライトイメージおよびキーモーメント情報

#### キーモーメント情報

プログレスバーの重要な位置に文字説明を追加し、ユーザーがクリックするとキーモーメント位置の文字情報を表示できるようにすることで、現在の位置のビデオ情報を素早く把握することができます。ビデオ情報をクリックすると、キーモーメント情報の位置をseekすることができます。

Tencent Cloud View Cube App > プレーヤー > プレーヤーコンポーネント > Tencent Cloudビデオで、全画面視聴モードを使用して体験できます。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Qc3t442_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16697206995071%20%281%29.png)

#### スプライトイメージ

ユーザーがプログレスバーのドラッグまたは早送り操作を行う際に、ビデオのサムネイルを確認して指定の場所のビデオ内容をすぐに把握できるようにしています。サムネイルプレビューはビデオのスプライトイメージをベースにして実現します。VODコンソールでビデオファイルのスプライトイメージを生成するか、またはスプライトイメージファイルを直接生成することができます。
Tencent Cloud View Cube App > プレーヤー > プレーヤーコンポーネント > Tencent Cloudビデオで、全画面視聴モードを使用して体験できます。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ii2h727_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16697206895960%20%281%29.png)

```java
// ステップ1：再生するビデオのsuperplayerModelのurl変数が空で、かつvideoIdが空ではない場合のみ、PlayWithFieldで再生を行い、onPlayEventコールバックからキーモーメント情報とスプライトイメージのデータを取得することができます
mSuperplayerView.play(superplayerModel);

// ステップ2: PlayWithFileId再生の際は、VOD_PLAY_EVT_GET_PLAYINFO_SUCCコールバックイベントからキーモーメント情報とスプライトイメージの情報を取得します
public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    switch (event) {
        case TXVodConstants.VOD_PLAY_EVT_GET_PLAYINFO_SUCC:
    
            // スプライトイメージの画像リンクURLを取得します
            playImageSpriteInfo.imageUrls = param.getStringArrayList(TXVodConstants.EVT_IMAGESPRIT_IMAGEURL_LIST);
            // スプライトイメージのweb vttマニフェストファイルのダウンロードURLを取得します
            playImageSpriteInfo.webVttUrl = param.getString(TXVodConstants.EVT_IMAGESPRIT_WEBVTTURL);
            // キーモーメント情報を取得します    
           ArrayList<String> keyFrameContentList =
                    param.getStringArrayList(TXVodConstants.EVT_KEY_FRAME_CONTENT_LIST);
            // キーモーメント情報時刻情報を取得します
            float[] keyFrameTimeArray = param.getFloatArray(TXVodConstants.EVT_KEY_FRAME_TIME_LIST);
        
            // キーモーメント情報データリストを作成します
            if (keyFrameContentList != null && keyFrameTimeArray != null
                    && keyFrameContentList.size() == keyFrameTimeArray.length) {
                for (int i = 0; i < keyFrameContentList.size(); i++) {
                    PlayKeyFrameDescInfo frameDescInfo = new PlayKeyFrameDescInfo();
                    frameDescInfo.content = keyFrameContentList.get(i);
                    frameDescInfo.time = keyFrameTimeArray[i];
                    mKeyFrameDescInfoList.add(frameDescInfo);
                }
            }
            break;
        default:
            break;
　　}
}

// ステップ3: 取得したキーモーメント情報とスプライトイメージ情報をupdateVideoImageSpriteAndKeyFrameメソッドによって対応するviewに割り当てます。 
// スプライトイメージのviewはVideoProgressLayoutコンポーネント内のmIvThumbnailに対応します。
// キーモーメント情報のviewはPointSeekBarコンポーネント内のTCPointViewに対応します。
updateVideoImageSpriteAndKeyFrame(playImageSpriteInfo,keyFrameDescInfoList);
```

[](id:demo)

## Demo体験

より完全な機能を体験するには、プロジェクトDemoを直接実行するか、QRコードをスキャンしてモバイルDemoであるTencent Cloud View Cube　Appをダウンロードしてください。

### プロジェクトDemoの実行

1. Android Studioのナビゲーションバーで**File**>**Open**を選択し、ポップアップボックスで**Demo**プロジェクトディレクトリ：`$SuperPlayer_Android/Demo`を選択します。Demoプロジェクトを正常にインポートした後、**Run app**をクリックすると、Demoを正常に実行できます。
2. 下図のようにDemoが正常に実行された後、**プレーヤー** > **プレーヤーコンポーネント**と進むと、プレーヤーの機能を体験できます。
