## 製品概要
Tencent Cloud View Cube Androidプレーヤーコンポーネントは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。品質モニタリング、ビデオ暗号化、超高速HD（TESHD）、解像度切り替え、ミニウィンドウ再生などの機能を一体化し、あらゆるオンデマンド（VOD）、ライブストリーミング再生のシーンに対応します。完備された機能をパッケージ化するとともに、上位層のUIを提供することで、市場で人気を博す各種ビデオアプリに引けを取らない再生ソフトウェアを短時間で作成することができます。

プレーヤーコンポーネントでは業務上の個別のニーズを満たせない場合で、なおかつお客様にある程度の開発経験がおありの場合は、Player+を統合し、プレーヤーインターフェースおよび再生機能のカスタム開発を行うことも可能です。



## 準備作業
1. より完全で全面的なプレーヤー機能を体験していただくために、[VOD](https://intl.cloud.tencent.com/product/vod) 関連サービスをアクティブ化することをお勧めします。アカウント登録がないユーザーは、アカウントを登録して[トライアル](https://intl.cloud.tencent.com/login)を行うことができます。VODサービスをご利用にならない場合はこの手順を省略できますが、統合後に使用できるのはプレーヤーの基本機能のみとなります。
2. Android Studioをダウンロードします。[Android Studio公式サイト](https://developer.android.com/studio)でダウンロードとインストールを行うことができます。ダウンロード済みの場合はこの手順を省略できます。

## ここでは次の内容について知ることができます
1. Tencent Cloud View Cube Androidプレーヤーコンポーネントの統合方法
2. プレーヤーの作成および使用方法


## 統合の準備
### ステップ1：プロジェクトのダウンロード
Tencent Cloud View Cube Androidプレーヤーコンポーネントのプロジェクトアドレスは[SuperPlayer_Android](https://github.com/LiteAVSDK/Player_Android)です。

**Tencent Cloud View Cube Androidプレーヤーコンポーネントプロジェクトのダウンロードは、**[プレーヤーコンポーネントZIPパッケージのダウンロード](#zip)**、または**[Gitコマンドでのダウンロード](#git)**のいずれかの方法で行えます。
<dx-tabs>
::: プレーヤーコンポーネントZIPパッケージのダウンロード[](id:zip)
次のプレーヤーコンポーネントZIPパッケージを直接ダウンロードできます。ページの**Code** > **Download ZIP**をクリックしてダウンロードしてください。
![](https://qcloudimg.tencent-cloud.cn/raw/a38a9995bfe13d645bcd1d2e5242a297.png)
:::
::: Gitコマンドでのダウンロード[](id:git)
1. 初めに、コンピュータにGitがインストールされていることをご確認ください。インストールされていない場合は、[Gitインストールチュートリアル](https://git-scm.com/downloads)を参照してインストールすることができます。
2. 次のコマンドを実行し、プレーヤーコンポーネントのプロジェクトコードをローカルにcloneします。
```shell
git clone git@github.com:tencentyun/SuperPlayer_Android.git
```
次のメッセージが表示されると、プロジェクトコードのローカルへのcloneは成功です。
```shell
'SuperPlayer_Android'にクローンしています...
remote: Enumerating objects: 2637, done.
remote: Counting objects: 100% (644/644), done.
remote: Compressing objects: 100% (333/333), done.
remote: Total 2637 (delta 227), reused 524 (delta 170), pack-reused 1993
オブジェクト受信のうち、100% (2637/2637), 571.20 MiB | 3.94 MiB/s, が完了しました
delta処理中: 100% (1019/1019), が完了しました
```
プロジェクトのダウンロード後、ソースコードの解凍後のディレクトリは次のようになります。

| ファイル名                      | 役割                                                         |
| --------------------------- | ------------------------------------------------------------ |
| LiteAVDemo(Player)          | プレーヤーコンポーネントDemoプロジェクト。Android Studioにインポートして直接実行できます   |
| app                         | メインインターフェースポータル                                                   |
| superplayerkit              | プレーヤーコンポーネント（SuperPlayerView）。再生、一時停止、ジェスチャー制御などの一般的な機能を備えています |
| superplayerdemo             | プレーヤーコンポーネントDemoコード                                         |
| common                      | ツールクラスモジュール                                                   |
| SDK                         | View Cube Player+。LiteAVSDK_Player_x.x.x.aar、aar形式のSDK、LiteAVSDK_Player_x.x.x.zip、lib、jar形式のSDKが含まれます |
| Playerr説明ドキュメント(Android).pdf | プレーヤーコンポーネント使用ドキュメント                                           |
:::
</dx-tabs>

### ステップ2：ガイドの統合
この手順ではプレーヤーの統合方法についてご説明します。Gradleによる自動でのロード方法、aarを手動でダウンロードしてから現在のプロジェクトにインポートする方法、またはjarおよびsoライブラリをインポートする方法を選択してプロジェクトの統合を行うことができます。
<dx-tabs>
::: Gradle自動ロード（AAR）
1. SDK+Demo開発パッケージをダウンロードします。プロジェクトアドレスは、[Android](https://github.com/LiteAVSDK/Player_Android)です。
2. moduleの`Demo/superplayerkit`をプロジェクトにコピーしてから、以下の設定を行います。
   - プロジェクトディレクトリのsetting.gradleに`superplayerkit`をインポートします。
   ```xml
   include ':superplayerkit'
   ```
   - `superplayerkit`プロジェクトのbuild.gradleファイルを開きcompileSdkVersion、buildToolsVersion、minSdkVersion、targetSdkVersionおよびrootProject.ext.liteavSdkの定量値を修正します。
     ![](https://main.qcloudimg.com/raw/fd6bc41bfd8b80fe5e82e3345b6ce73f.png)
   ```xmls
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   
   dependencies {
       //過去のバージョンを統合したい場合は、latest.releaseを対応するバージョンに変更します（例：8.5.290009）。
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
   }
   ```
   上記の手順を参照し、`common`モジュールをプロジェクトにインポートし、設定してください。
3. gradleにmavenCentralライブラリを設定することで、LiteAVSDKの更新を自動的にダウンロードし、`app/build.gradle`を開き、以下の設定を行います。
   ![](https://main.qcloudimg.com/raw/65439d399ec584871a7a9bc88ccaef46.png)
   
   1. dependenciesにLiteAVSDK_Playerの依存を追加します。
```xml
dependencies {
	 implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
	 implementation project(':superplayerkit')
	 // プレーヤーコンポーネントに弾幕を統合するサードパーティライブラリ
	 implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
}
```
   過去のバージョンのLiteAVSDK_Player SDKを統合したい場合は、[MavenCentral](https://repo1.maven.org/maven2/com/tencent/liteav/LiteAVSDK_Player/)で過去のバージョンを確認した後、次の方法によって統合することができます。 
```xml
dependencies {
	 // バージョン8.5.10033のLiteAVSDK_Player SDKを統合
	 implementation 'com.tencent.liteav:LiteAVSDK_Player:8.5.10033'
}
```
   2.  `app/build.gradle`defaultConfigで、Appが使用するCPUアーキテクチャを指定します（現在LiteAVSDKはarmeabi、armeabi-v7aおよびarm64-v8aをサポートしています。プロジェクトのニーズに応じて設定することができます）。
```xmsl
ndk {
	 abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
}
```
   これまでに9.4およびそれ以前のバージョンのSDKのダウンロードキャッシュ機能（TXVodDownloadManager内の関連インターフェース）を使用したことがなく、なおかつ9.5およびそれ以降のSDKバージョンで9.4およびそれ以前にキャッシュしたダウンロードファイルを再生する必要がない場合は、この機能のsoファイルをダウンロードしなくてよいため、インストールパッケージのボリュームを減らすことができます。 例えば、9.4およびそれ以前のバージョンでTXVodDownloadManagerクラスのsetDownloadPathとstartDownloadUrl関数を使用して該当のキャッシュファイルをダウンロードしており、なおかつアプリケーション内にTXVodDownloadManagerからコールバックされたgetPlayPathパスを保存してその後の再生に使用しているような場合は、このgetPlayPathパスファイルの再生にlibijkhlscache-master.soが必要ですが、そうでない場合は不要です。app/build.gradleに次を追加します。
```xml
packagingOptions {
	exclude "lib/armeabi/libijkhlscache-master.so"
	exclude "lib/armeabi-v7a/libijkhlscache-master.so"
	exclude "lib/arm64-v8a/libijkhlscache-master.so"
}
```
   3. プロジェクトディレクトリのbuild.gradleにmavenCentralリポジトリを追加します。
 ```
 repositories {
		 mavenCentral()
 }
 ```
4. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)Sync Nowボタンをクリックし、SDKを同期させます。mavenCentralへのネットワーク接続に問題がなければ、SDKが自動的にダウンロードされプロジェクトに統合されます。
:::
::: Gradle手動ダウンロード（AAR）
1. SDK+Demo開発パッケージをダウンロードします。プロジェクトアドレスは、[Android](https://github.com/LiteAVSDK/Player_Android)です。
2. `SDK/LiteAVSDK_Player_XXX.aar`（XXXはバージョン番号）をappのlibsフォルダにインポートし、moduleの`Demo/superplayerkit`をプロジェクトにコピーします。
3. プロジェクトディレクトリのsetting.gradleに`superplayerkit`をインポートします。
```
include ':superplayerkit'
```
4. `superplayerkit`プロジェクトのbuild.gradleファイルを開きcompileSdkVersion、buildToolsVersion、minSdkVersion、targetSdkVersionおよびrootProject.ext.liteavSdkの定量値を修正します。
![](https://main.qcloudimg.com/raw/479cb6ed7a29621998d1ee670e091437.png)
```xml
compileSdkVersion 26
buildToolsVersion "26.0.2"

defaultConfig {
	 targetSdkVersion 23
	 minSdkVersion 19
}

dependencies {
	 implementation(name:'LiteAVSDK_Player_8.9.10349', ext:'aar')
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
compile(name:'LiteAVSDK_Player_8.9.10349', ext:'aar')
implementation project(':superplayerkit')
// プレーヤーコンポーネントに弾幕を統合するサードパーティライブラリ
implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
```
6. プロジェクトの`build.gradle`に追加します。
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
これまでに9.4およびそれ以前のバージョンのSDKのダウンロードキャッシュ機能（TXVodDownloadManager内の関連インターフェース）を使用したことがなく、なおかつ9.5およびそれ以降のSDKバージョンで9.4およびそれ以前にキャッシュしたダウンロードファイルを再生する必要がない場合は、この機能のsoファイルをダウンロードしなくてよいため、インストールパッケージのボリュームを減らすことができます。 例えば、9.4およびそれ以前のバージョンでTXVodDownloadManagerクラスのsetDownloadPathとstartDownloadUrl関数を使用して該当のキャッシュファイルをダウンロードしており、なおかつアプリケーション内にTXVodDownloadManagerからコールバックされたgetPlayPathパスを保存してその後の再生に使用しているような場合は、このgetPlayPathパスファイルの再生にlibijkhlscache-master.soが必要ですが、そうでない場合は不要です。app/build.gradleに次を追加します。
```xml
packagingOptions {
	exclude "lib/armeabi/libijkhlscache-master.so"
	exclude "lib/armeabi-v7a/libijkhlscache-master.so"
	exclude "lib/arm64-v8a/libijkhlscache-master.so"
}
```
8. Sync Nowボタンをクリックし、SDKを同期させ、プレーヤーコンポーネントの統合作業を完了します。
:::
::: SDK（jar+so）を統合
aarライブラリを統合したくない場合は、jarおよびsoライブラリの方式をインポートしてLiteAVSDKを統合することもできます。
[](id:smallStep_1)
1. プロジェクトアドレス[Android](https://github.com/LiteAVSDK/Player_Android)で、SDK+Demo開発パッケージをダウンロードし、ダウンロードが完了したら解凍します。SDKディレクトリでSDK/LiteAVSDK_Player_XXX.zip（XXXはバージョン番号）を見つけて解凍し、jarファイルとsoフォルダを含むlibsディレクトリを取得します。ファイルリストは次のとおりです。
 ![](https://qcloudimg.tencent-cloud.cn/raw/9ac0f5b1b9b5d15a005fa2226dd960b6.png)
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

### ステップ3： App権限の設定
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

### ステップ4：難読化ルールの設定
proguard-rules.pro ファイルでは、 TRTC SDK 関連を非混同リストに追加します。
```xml
-keep class com.tencent.** { *; }
```
Tencent Cloud View Cube Androidプレーヤーコンポーネントapp権限設定手順はこれで完了です。

### ステップ5：プレーヤー機能の使用
このステップは、プレーヤーの作成および使用、ならびにプレーヤーを使用してビデオ再生を行う方法についてユーザーにご説明するためのものです。
1. **プレーヤーの作成**[](id:usePlayer)
プレーヤーのメインクラスは`SuperPlayerView`です。作成後すぐにビデオを再生できます。 FileIDまたはURLによる再生の統合をサポートしています。レイアウトファイルにSuperPlayerViewを作成します。
```xml
<!-- プレーヤーコンポーネント-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```


3. **ビデオの再生**[](id:playe)
この手順は、ビデオの再生方法についてユーザーにご説明するためのものです。Tencent Cloud View Cube AndroidプレーヤーコンポーネントはライブストリーミングとVODの両方の再生に使用できます。具体的には次のとおりです。
	- VOD再生：プレーヤーコンポーネントは2種類のVOD再生方式をサポートしています。Tencent CloudのVODメディアリソースを[FileIDで再生](#fileid)することも、[URL再生](#url)アドレスから直接再生することもできます。
	- ライブストリーミング再生：プレーヤーコンポーネントは[URL再生](#url)方式でライブストリーミング再生を実現できます。URLアドレスを渡すと、ライブストリーミングオーディオビデオストリームをプルしてライブストリーミングを再生することができます。Tencent Cloud CSSのURL生成方法については、[自身でのライブストリーミングURLの結合](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。
<dx-tabs>
::: URLによる再生（ライブストリーミング、VOD）[](id:url)
URLはVODファイルの再生アドレスと、ライブストリーミングのプルストリーミングアドレスのどちらでもかまいません。該当のURLを渡すと、該当のビデオファイルを再生することができます。
```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073; // AppIdを設定
model.url = "http://your_video_url.mp4";   // ビデオ再生URLを設定
mSuperPlayerView.playWithModel(model);
```
:::
::: FileIDからの再生（VOD）[](id:fileid)
ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。
1. クライアントからビデオが公開されると、サーバーがFileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するFileIdが含まれています。

ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。下図のように、IDのところにFileIdが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/f089346e01ab8e44e42f28c965809b9c.png)
<dx-alert infotype="notice">
<li> FileID経由で再生する場合は、初めにAdaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、または再生コンポーネントの署名psignを使用して再生するビデオを指定する必要があります。これらを行わないと、ビデオ再生が失敗する可能性があります。トランスコードのチュートリアルおよび説明については [プレーヤーコンポーネントを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)を、psign生成のチュートリアルについては[psignチュートリアル](https://intl.cloud.tencent.com/document/product/266/38099)をそれぞれご参照ください。</li>
<li> FileID経由での再生の際に「no v4 play info」エラーが表示された場合は、上記の問題が存在する可能性があることを示しているため、上記のチュートリアルに従って調整することをお勧めします。また、ソースビデオの再生リンクを直接取得し、[URLによる再生](#url) 方式で再生することもできます。</li>
<li> **トランスコードを行っていないソースビデオを再生すると、互換性がない場合がありますので、トランスコードをご使用後にビデオを再生することをお勧めします。**</li></dx-alert>
<dx-codeblock>
:::  java
//リンク不正アクセス防止を有効にせずに再生を行い、その途中で「no v4 play info」エラーが表示された場合は、Adaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはソースビデオの再生リンクを直接取得し、url方式で再生することをお勧めします。

SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppIdを設定
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710173650"; // FileIdを設定
//プライベートの暗号化再生にはpsignの入力が必要です。psignはプレーヤーコンポーネントの署名です。署名についての紹介および生成方法については、以下のリンクをご参照ください。https://intl.cloud.tencent.com/document/product/266/38099
//model.videoId.pSign = @"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
:::
</dx-codeblock>
:::
</dx-tabs>
3. **再生の終了**[](id:exitPlayer)
プレーヤーが不要な時には、`resetPlayer`を呼び出してプレーヤー内部の状態を消去し、メモリを解放します。
```java
mSuperPlayerView.resetPlayer();
```

これで、Tencent Cloud View Cube Androidプレーヤーコンポーネントの作成、ビデオ再生、再生終了機能の統合が完了しました。

## 機能の使用[](id:moreFeature)

この章では、いくつかの一般的なプレーヤー機能の使用方式をご紹介します。より完全な機能の使用方式は[Demo体験](#demo)を、プレーヤーコンポーネントがサポートする機能は[機能リスト](https://www.tencentcloud.com/document/product/266/42965)をそれぞれご参照ください。

### 1、全画面再生

プレーヤーコンポーネントは全画面再生をサポートしています。全画面再生のシーンでは、同時に画面ロック、ジェスチャーによる音量と明るさの制御、弾幕、スクリーンショット、解像度の切り替えなどの機能設定がサポートされます。機能の効果は**[Tencent Cloud View Cube App](#qrcode) > プレーヤー > プレーヤーコンポーネント**で体験できます。画面右下隅をクリックすると、全画面再生画面に進むことができます。

ウィンドウ再生モードでは、次のインターフェースを呼び出して全画面再生モードに進むことができます。
```java
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.FULLSCREEN);
```


<dx-tabs>
::: ウィンドウに戻る
**戻る**をクリックすると、ウィンドウ再生モードに戻ることができます。
```java
//クリックすると、次のインターフェースがトリガーされます。
mControllerCallback.onBackPressed(SuperPlayerDef.PlayerMode.FULLSCREEN);
onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```
:::
::: 画面ロック[](id:lockscreen)
画面ロック操作はユーザーが再生に集中したい場合に使用できます。
```java
// クリックするとトリガーされるインターフェース
toggleLockState();
```
:::
::: 弾幕[](id:barrage)
弾幕機能をオンにすると、画面上にユーザーの送信した文字を流すことができます。
```java
// ステップ1：弾幕Viewに弾幕を追加する
addDanmaku(String content, boolean withBorder);
// ステップ2：弾幕をオンまたはオフにする
toggleBarrage();
```
:::
::: スクリーンショット[](id:screenshot)
プレーヤーコンポーネントは再生中にその時点のビデオフレームを切り取ることができる機能をご提供します。画像を保存して共有することができます。画像の4か所のボタンをクリックするとスクリーンショットを作成することができ、切り取った画像はmSuperPlayer.snapshotインターフェースで保存できます。
```java
mSuperPlayer.snapshot(new TXLivePlayer.ITXSnapshotListener() {
  @Override
  public void onSnapshot(Bitmap bitmap) {
        //画像はここに保存できます
  }
});
```
:::
::: 解像度の切り替え[](id:resolution)
ユーザーはニーズに応じて、HD、SD、FHDなどのビデオ再生の解像度を選択することができます。
```java
// クリックするとトリガーされる解像度表示viewコードインターフェース
showQualityView();
//解像度オプションをクリックした際のコールバックインターフェース
mListView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
  @Override
  public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
    // 解像度ListViewのクリックイベント
    VideoQuality quality = mList.get(position);
    mCallback.onQualitySelect(quality);
  }
});
//最後に解像度のコールバックを変更
@Override
public void onQualityChange(VideoQuality quality) {
   mFullScreenPlayer.updateVideoQuality(quality);
   mSuperPlayer.switchStream(quality);
}
```
:::
</dx-tabs>


### 2、フローティングウィンドウ再生
プレーヤーコンポーネントはフローティングウィンドウによるミニウィンドウ再生をサポートしています。他のアプリケーションに切り替えてもビデオ再生が中断しない機能です。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント**で体験できます。画面左上隅の**戻る**をクリックすると、フローティングウィンドウ再生機能を体験できます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/e8a774cb9833f2de45fc1cf3cc928ee4.png" style="zoom:35%;" />
フローティングウィンドウ再生はAndroidManifest内の以下の権限に依存しています。
```java
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
```
```java
// フローティングウィンドウに切り替えるとトリガーされるコードインターフェース
mSuperPlayerView.switchPlayMode(SuperPlayerDef.PlayerMode.FLOAT);
//フローティングウィンドウの戻るウィンドウをクリックするとトリガーされるコードインターフェース
mControllerCallback.onSwitchPlayMode(SuperPlayerDef.PlayerMode.WINDOW);
```

### 3、ビデオカバー

プレーヤーコンポーネントはユーザーによるビデオカバーのカスタマイズをサポートしています。これはユーザーがビデオの最初のフレーム画面の再生コールバックを受信する前の表示に用いられます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **カバーカスタマイズのデモンストレーション**ビデオで体験できます。



* プレーヤーコンポーネントを自動再生モード`PLAY_ACTION_AUTO_PLAY`に設定すると、ビデオが自動再生されます。このとき、ビデオの最初のフレームをロードするまでの間はカバーが表示されます。
* プレーヤーコンポーネントを手動再生モード`PLAY_ACTION_MANUAL_PLAY`に設定すると、ユーザーが**再生**をクリックしなければ再生が開始されません。**再生**をクリックするまでの間はカバーが表示されます。**再生**をクリックした後、ビデオの最初のフレームをロードするまでの間もカバーが表示されます。

ビデオカバーはネットワークURLアドレスまたはローカルFileアドレスの使用をサポートしています。使用方法については下記のガイドをご参照ください。FileID方式でビデオを再生する場合は、VOD内で直接ビデオカバーを設定することができます。

```java
SuperPlayerModel model = new SuperPlayerModel();
model.appId = "お客様のappid"
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "お客様のfileId" 
//再生モードは、自動再生モード`PLAY_ACTION_AUTO_PLAY`または手動再生モード`PLAY_ACTION_MANUAL_PLAY`に設定することができます。
model.playAction = PLAY_ACTION_MANUAL_PLAY;
//カバーのアドレスをネットワークのurlアドレスに設定する場合、coverPictureUrlを設定しなければ、VODコンソールが設定したカバーが自動的に使用されます
model.coverPictureUrl = "http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/cc1e28208602268011087336518/MXUW1a5I9TsA.png" 
mSuperPlayerView.playWithModel(model);
```

### 4、ビデオリストの繰り返し再生

プレーヤーコンポーネントはビデオリストの繰り返し再生をサポートしています。ビデオリストを指定すると、次のようになります。

* 再生リスト内のビデオを順序に従って繰り返し再生できます。再生中は次のビデオの自動再生と、次のビデオへの手動切り替えのどちらも行うことができます。
* リスト内の最後のビデオの再生が完了すると、リスト内の最初のビデオの再生を自動的に開始します。

機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **ビデオリストの繰り返し再生のデモンストレーション**ビデオで体験できます。



```java
//ステップ1:繰り返し再生List<SuperPlayerModel>を作成する
ArrayList<SuperPlayerModel> list = new ArrayList<>();
SuperPlayerModel model = new VideoModel();
model = new SuperPlayerModel();
model.videoId = new SuperPlayerVideoId();
model.appid = 1252463788;
model.videoId.fileId = "4564972819219071568"; 
list.add(model);

model = new SuperPlayerModel();
model.videoId = new SuperPlayerVideoId();
model.appid = 1252463788;
model.videoId.fileId = "4564972819219071679"; 
list.add(model);
//ステップ2：繰り返し再生インターフェースを呼び出す
mSuperPlayerView.playWithModelList(list, true, 0);
```

```java
public void playWithModelList(List<SuperPlayerModel> models, boolean isLoopPlayList, int index);
```

インターフェースパラメータの説明

| パラメータ名         | タイプ                   | 説明                           |
| -------------- | ---------------------- | ------------------------------ |
| models         | List<SuperPlayerModel> | 繰り返し再生データリスト                   |
| isLoopPlayList | boolean                | 繰り返すかどうか                       |
| index          | int                    | 再生を開始するSuperPlayerModelのインデックス |

### 5、ビデオのプレビュー

プレーヤーコンポーネントはビデオプレビュー機能をサポートしています。これは非VIPプレビューなどのシーンに適用でき、開発者は異なるパラメータを渡してビデオのプレビュー時間、プロンプト情報、プレビュー終了画面などを制御することができます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **プレビュー機能のデモンストレーション**ビデオで体験できます。



```java
 方法1：
 //ステップ1：ビデオmodeの作成
 SuperPlayerModel mode = new SuperPlayerModel();
 //...ビデオソース情報を追加
 //ステップ2：プレビュー情報modeの作成
 VipWatchModel vipWatchModel = new VipWatchModel("%ssプレビュー可能、VIPをアクティブ化するとビデオ全体を視聴可能"、15);
 mode.vipWatchMode = vipWatchModel;
 //ステップ3：ビデオ再生メソッドを呼び出す
 mSuperPlayerView.playWithModel(mode);

 方法2：
 //ステップ1：プレビュー情報modeの作成
 VipWatchModel vipWatchModel = new VipWatchModel("%ssプレビュー可能、VIPをアクティブ化するとビデオ全体を視聴可能"、15);
  //ステップ2：プレビュー機能設定メソッドを呼び出す
 mSuperPlayerView.setVipWatchModel(vipWatchModel);
```

```java
public VipWatchModel(String tipStr, long canWatchTime)
```

VipWatchModelインターフェースパラメータの説明：

| パラメータ名          | タイプ     | 説明        |
| ------------ | ------ | --------- |
| tipStr       | String | プレビュープロンプト情報    |
| canWatchTime | Long   | プレビュー時間。単位は秒 |

### 6、動的ウォーターマーク

プレーヤーコンポーネントは再生画面での、不規則に動くテキストウォーターマークの追加をサポートし、不正録画を効果的に防止します。ウォーターマークは全画面再生モードおよびウィンドウ再生モードのどちらでも表示でき、開発者はウォーターマークのテキスト、文字サイズ、色を変更することができます。機能の効果は[**Tencent Cloud View Cube App**](#qrcode) > **プレーヤー** > **プレーヤーコンポーネント** > **動的ウォーターマーク**のデモンストレーションビデオで体験できます。



```java
 方法1：
 //ステップ1：ビデオmodeの作成
 SuperPlayerModel mode = new SuperPlayerModel();
 //...ビデオソース情報を追加
 //ステップ2：ウォーターマーク情報modeの作成
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
 mode.dynamicWaterConfig = dynamicWaterConfig;
 //ステップ3：ビデオ再生メソッドを呼び出す
 mSuperPlayerView.playWithModel(mode);

 方法2：
 //ステップ1：ウォーターマーク情報modeの作成
 DynamicWaterConfig dynamicWaterConfig = new DynamicWaterConfig("shipinyun", 30, Color.parseColor("#80FFFFFF"));
  //ステップ2：動的ウォーターマーク機能設定メソッドを呼び出す
 mSuperPlayerView.setDynamicWatermarkConfig(dynamicWaterConfig);
```

```java
public DynamicWaterConfig(String dynamicWatermarkTip, int tipTextSize, int tipTextColor)
```

インターフェースパラメータの説明

| パラメータ名                 | タイプ     | 説明     |
| ------------------- | ------ | ------ |
| dynamicWatermarkTip | String | ウォーターマークのテキスト情報 |
| tipTextSize         | int    | 文字サイズ   |
| tipTextColor        | int    | 文字の色   |

[](id:demo)
## Demo体験

さらに完全な機能は、プロジェクトのDemoを直接実行するか、または2次元コードをスキャンしてモバイル端末Demoをダウンロードし、Tencent Cloud View Cube Appで体験することができます。

### プロジェクトDemoの実行

1. Android Studioのナビゲーションバーで**File** > **Open**を選択し、ポップアップボックスで**Demo**プロジェクトディレクトリ： `$SuperPlayer_Android/Demo`を選択します。Demoプロジェクトへのインポートに成功後、**Run app**をクリックすると、Demoを正常に実行できます。
2. Demoが正常に実行された後、**プレーヤー** > **プレーヤーコンポーネント**と進むと、プレーヤーの機能を体験できます。

[](id:qrcode)
### Tencent Cloud View Cube App
**Tencent Cloud View Cube App** > **プレーヤー**で、より多くのプレーヤーコンポーネント機能を体験できます。
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
