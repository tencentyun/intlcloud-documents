## 製品概要

Tencent Cloud View Cube Android Super Playerは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。簡単な数行のコードで、Tencent Videoのような強力な再生機能を備えることができます。画面の縦横切り替え、解像度の選択、ジェスチャー、ミニウィンドウなどの基本機能を備えるほか、ビデオキャッシュ、ソフトウェア/ハードウェアデコードの切り替え、倍速再生などの特殊機能もサポートしています。システムのプレーヤーよりも、サポートする形式が多く、互換性に優れ、機能もより強力です。同時に、トップ画面の秒速起動、低遅延などの優位性、ならびにビデオサムネイルなどの高度な機能も備えています。

## バージョンのサポート

このページのドキュメントで説明する機能のTencent Cloud View Cubeでのサポート状況は次のとおりです。

| バージョン名                            | 基本的なライブストリーミングSmart                                               | インタラクティブライブストリーミングLive                                                | User Generated Short Video（UGSV）                                                  | オーディオビデオ通話TRTC                                             | プレーヤーPlayer                                                | 全機能                                                       |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| サポート状況                            | -                                                            | -                                                            | -                                                            | -                                                           | &#10003;                                                     | &#10003;                                                     |
| SDKダウンロード <div style="width: 90px"/> | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=basicLive) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=interactivelive) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=shortVideo) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=video) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=player) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=allPart) |


## プロジェクトアドレス[](id:sdkDownload)

Tencent Cloud View Cube Android Super Playerのプロジェクトアドレスは[SuperPlayer_Android](https://github.com/tencentyun/SuperPlayer_Android)です。

## 対象となる読者

このドキュメントの内容の一部は、Tencent Cloud専用の機能となっていますので、使用前に、[Tencent Cloud](https://intl.cloud.tencent.com)関連サービスのアクティブ化を行ってください。アカウント登録がないユーザーは登録し、[無料試用](https://intl.cloud.tencent.com/login)が可能です。

## 統合ガイド[](id:guide)
Gradle自動ロード方法を選択、使用するか、または手動でaarをダウンロードしてから現在のプロジェクトにインポートします。

### 方法1：自動ロード（AAR）

1. SDK+Demo開発パッケージをダウンロードします。プロジェクトアドレスは、[Android](https://github.com/tencentyun/SuperPlayer_Android)です。
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
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
   }
   ```
3. gradleにmavenCentralライブラリを設定することで、LiteAVSDKの更新を自動的にダウンロードし、`app/build.gradle`を開き、以下の設定を行います。
![](https://main.qcloudimg.com/raw/65439d399ec584871a7a9bc88ccaef46.png)
   - dependenciesにLiteAVSDK_Playerの依存を追加します。
   ```xml
   dependencies {
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
       implementation project(':superplayerkit')
       // Super Playerに弾幕を統合するためのサードパーティライブラリ
       implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
   }
   ```
   - `app/build.gradle`defaultConfigで、Appが使用するCPUアーキテクチャを指定します（現在LiteAVSDKはarmeabi、armeabi-v7aおよびarm64-v8aをサポートしています。プロジェクトのニーズに応じて設定することができます）。
   ```xmsl
   ndk {
       abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
   }
   ```
   - プロジェクトディレクトリのbuild.gradleにmavenCentralライブラリを追加します。
   ```
   repositories {
       mavenCentral()
   }
   ```

4. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)Sync Nowボタンをクリックし、SDKを同期させます。mavenCentralへのネットワーク接続に問題がなければ、SDKが自動的にダウンロードされプロジェクトに統合されます。

### 方法2：手動によるダウンロード（AAR）
1. SDK+Demo開発パッケージをダウンロードします。プロジェクトアドレスは、[Android](https://github.com/tencentyun/SuperPlayer_Android)です。
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
   // Super Playerに弾幕を統合するためのサードパーティライブラリ
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
8. Sync Nowボタンをクリックし、SDKを同期させ、Super Playerの統合作業を完了します。

### 方法3：SDKの統合（jar+so）
aarライブラリを統合したくない場合は、jarおよびsoライブラリの方式をインポートしてLiteAVSDKを統合することもできます。
[](id:smallStep_1)
1. プロジェクトアドレス[Android](https://github.com/tencentyun/SuperPlayer_Android)で、SDK+Demo開発パッケージをダウンロードし、ダウンロードが完了したら解凍します。SDKディレクトリでSDK/LiteAVSDK_Player_XXX.zip（XXXはバージョン番号）を探して解凍し、jarファイルとsoフォルダを含むlibsディレクトリを取得します。ファイルリストは次のとおりです。
   ![](https://qcloudimg.tencent-cloud.cn/raw/9ac0f5b1b9b5d15a005fa2226dd960b6.png)
2. moduleの`Demo/superplayerkit`をプロジェクトにコピーし、その後、プロジェクトディレクトリのsetting.gradleに`superplayerkit`をインポートします。
   ```xml
   include ':superplayerkit'
   ```
3. [手順1](#smallStep_1)で解凍して取得したlibsフォルダを`superplayerkit`プロジェクトルートディレクトリにコピーします。
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
6. Sync Nowボタンをクリックし、SDKを同期させ、Super Playerの統合作業を完了します。

### App権限の設定

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

## 再生機能の使用

### プレーヤーの使用[](id:usePlayer)

プレーヤーのメインクラスは、`SuperPlayerView`です。作成後すぐにビデオを再生できます。
```java
//ホットリンク防止は無効にします
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppIdを設定
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // FileIdを設定
mSuperPlayerView.playWithModel(model);

//ホットリンク防止を有効化するには、psignの入力が必要となり、psignはSuper Playerの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://intl.cloud.tencent.com/document/product/266/38099
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329071;// AppIdを設定
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710173650"; // FileIdを設定
mSuperPlayerView.playWithModel(model);
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
mSuperPlayerView.playWithModel(model);
```



コードを実行すると、携帯電話で再生したビデオを視聴でき、インターフェース上の機能もほとんどが使用可能な状態になります。


### FileIdの選択[](id:FileId)

ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。

1. クライアントからビデオが公開されると、サーバーがFileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するFileIdが含まれています。

ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。



### キーモーメント機能

時間の長いビデオの再生時は、キーモーメント情報が、視聴者に興味のあるポイントをみつけやすくしてくれます。[メディアファイル属性変更](https://intl.cloud.tencent.com/document/product/266/37570)APIを使用し、AddKeyFrameDescs.Nパラメータによって、ビデオにキーモーメント情報を設定することができます。

呼び出し後、プレーヤーのインターフェースに新しいエレメントが追加されます。



### ミニウィンドウ再生[](id:smallWindow)
ミニウィンドウ再生は、すべてのActivity上にフロートさせて再生することが可能です。ミニウィンドウを使用した再生は非常に簡単で、再生開始前に次のコードを呼び出すだけで済みます。

```java
// プレーヤーの設定
SuperPlayerGlobalConfig prefs = SuperPlayerGlobalConfig.getInstance();
// フローティングウィンドウ再生の有効化
prefs.enableFloatWindow = true;
//フローティングウィンドウの初期の位置および幅・高さを設定します
SuperPlayerGlobalConfig.TXRect rect = new SuperPlayerGlobalConfig.TXRect();
rect.x = 0;
rect.y = 0;
rect.width = 810;
rect.height = 540;
// ...その他の設定
```

<img src="https://main.qcloudimg.com/raw/2cab897e43e4a01ee5f8e48372ce79a3.jpg" width="350">

### 再生の終了[](id:exitPlayer)

プレーヤーが不要な時には、`resetPlayer`を呼び出してプレーヤー内部の状態を消去し、メモリを解放します。

```java
mSuperPlayerView.resetPlayer();
```

## その他の機能[](id:moreFeature)

完全な機能は、2次元コードをスキャニングし、ビデオクラウドツールキットをダウンロードして体験するか、またはプログラムのDemoを直接実行することもできます。
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
