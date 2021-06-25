## 概要

Android Super Player SDKは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。簡単な数行のコードで、Tencent Videoのような強力な再生機能を備えることができます。画面の縦横切り替え、解像度の選択、ジェスチャー、ミニウィンドウなどの基本機能を備えるほか、ビデオキャッシュ、ソフトウェア/ハードウェアデコードの切り替え、倍速再生などの特殊機能もサポートしています。システムのプレーヤーよりも、サポートする形式が多く、互換性に優れ、機能もより強力です。同時に、トップ画面の秒速起動、低遅延などの優位性、ならびにビデオサムネイルなどの高度な機能も備えています。

## SDKのダウンロード

VOD Android Super Playerのプロジェクトのアドレスは、[SuperPlayer_Android](https://github.com/tencentyun/SuperPlayer_Android)です。

## 対象となる読者

このドキュメントの内容の一部は、Tencent Cloud専用の機能となっていますので、使用前に、[Tencent Cloud](https://intl.cloud.tencent.com/zh/)関連サービスのアクティブ化を行ってください。アカウント登録がないユーザーは登録し、[無料試用](https://intl.cloud.tencent.com/login)が可能です。

## クイックインテグレーション
### aar統合
1. SDK + Demo開発パッケージをダウンロードします。プロジェクトアドレスは、[Android](https://github.com/tencentyun/SuperPlayer_Android)です。
2. SDK/LiteAVSDK_XXX.aar`と`Demo/superplayerkit`という名のmoduleをインポートし、プログラムの中にコピーします。
3. `app/build.gradle`に依存を追加します。
<dx-codeblock>
::: java java
compile(name: 'LiteAVSDK_Player_7.4.9211', ext: 'aar')
compile project(':superplayerkit')
// Super Playerに弾幕を統合するためのサードパーティライブラリ
compile 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
:::
</dx-codeblock>
4. プロジェクトの`build.gradle`に追加します。
<dx-codeblock>
::: java java
...
allprojects {
    repositories {
        flatDir {
            dirs 'libs'
        }
        ...
    }
}
...
:::
</dx-codeblock>
5. 権限許可のステートメント。
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

### プレーヤーの使用

プレーヤーのメインクラスは、`SuperPlayerView`です。作成後すぐにビデオを再生できます。
```java
//ホットリンク防止は無効にします
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppIdを設定
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // FileIdを設定
mSuperPlayerView.playWithModel(model);

//ホットリンク防止を有効化するには、psignの入力が必要となり、psignはSuper Playerの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://cloud.tencent.com/document/product/266/42436
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329071;// AppIdを設定
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710173650"; // FileIdを設定
mSuperPlayerView.playWithModel(model);
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
mSuperPlayerView.playWithModel(model);
```



コードを実行すると、携帯電話で再生したビデオを視聴でき、インターフェース上の機能もほとんどが使用可能な状態になります。
<img src="https://main.qcloudimg.com/raw/128c45edfc77b319475868c21caec2de.png" width="550">

### FileIdの選択

ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。

1. クライアントからビデオが公開されると、サーバーがFileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、[アップロードの確認](https://intl.cloud.tencent.com/zh/document/product/266)の通知の中に対応するFileIdが含まれています。

ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。下図のように、IDのところにFileIdが表示されます。
![](https://main.qcloudimg.com/raw/1a3677d5fe618227a117d7502be42793.png)



### キーモーメント機能

時間の長いビデオの再生時は、キーモーメント情報が、視聴者に興味のあるポイントをみつけやすくしてくれます。[メディアファイル属性変更](https://intl.cloud.tencent.com/document/product/266/37570)APIを使用し、AddKeyFrameDescs.Nパラメータによって、ビデオにキーモーメント情報を設定することができます。

呼び出し後、プレーヤーのインターフェースに新しいエレメントが追加されます。
<img src="https://main.qcloudimg.com/raw/55ebce6d0c703dafa1ac131e1852e025.png" width="550">


### ミニウィンドウ再生
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

### 再生のリセット

プレーヤーが不要な時には、`resetPlayer`を呼び出してプレーヤー内部の状態を消去し、メモリを解放します。

```java
mSuperPlayerView.resetPlayer();
```

## その他の機能

完全な機能は、2次元コードをスキャニングし、ビデオクラウドツールキットをダウンロードして体験するか、またはプログラムのDemoを直接実行することもできます。
<img src="https://main.qcloudimg.com/raw/344d9d41fc5e305a17e22e104b9305da.png" width="150">


