## 製品概要

Tencent Cloud View Cube Android Super Player Adapterは、サードパーティのプレーヤーまたは自社開発のプレーヤーを使用して開放されたクラウドPAASリソースに接続を希望する顧客向けにVODのためのプレーヤープラグインを提供します。カスタムプレーヤー機能を必要とするユーザーにおいて一般的に使用されます。

[](id:sdkDownload)
## SDKのダウンロード

Tencent Cloud View Cube Android Super Player Adapter SDKとDemoプロジェクトのダウンロードアドレスは[TXCPlayerAdapterSDK_Android](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TXCPlayerAdapter/Release/1.0.0/TXCPlayerAdapterSDK_1.0.0_Android.zip)です。 

## 対象となる読者

このドキュメントの内容の一部は、Tencent Cloud専用の機能となっていますので、使用前に、[Tencent Cloud](https://intl.cloud.tencent.com)関連サービスのアクティブ化を行ってください。アカウント登録がないユーザーは登録し、[無料試用](https://intl.cloud.tencent.com/login)が可能です。

[](id:guide)
## 統合ガイド

SDKを統合し、TXCPlayerAdapter-release-1.0.0.aarをlibsディレクトリにコピーして、依存プロジェクトを追加します。

```groovy
implementation(name:'TXCPlayerAdapter-release-1.0.0', ext:'aar')
```

難読化したスクリプトを追加します

```xml
-keep class com.tencent.** { *; }
```


[](id:usePlayer)
### プレーヤーの使用

変数ステートメント。プレーヤーのメインクラスは`ITXCPlayerAssistor`です。作成後すぐにビデオを再生できます。

FileIdは、通常、ビデオのアップロード後にサーバーから返されます。

1. クライアントからビデオが公開されると、サーバーがfileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するfileIdが含まれています。


ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、対応するファイルを検索することができます。クリックして、右側のビデオ詳細で関連パラメータを確認することができます。

```java
//psignはSuper Playerの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://intl.cloud.tencent.com/document/product/266/38099
private String mFileId, mPSign;
ITXCPlayerAssistor mPlayerAssistor = TXCPlayerAdapter.createPlayerAssistor(mFileId, mPSign);
```

初期化

```java
// 初期化
TXCPlayerAdapter.init(appId); //appidをTencent Cloud VODで申請します
TXCPlayerAdapter.setLogEnable(true); //logを開きます

mSuperPlayerView = findViewById(R.id.sv_videoplayer);  
mPlayerAssistor = TXCPlayerAdapter.createPlayerAssistor(mFileId, mPSign);
```

ビデオリクエスト情報と再生

```java
mPlayerAssistor.requestVideoInfo(new ITXCRequestVideoInfoCallback() {

    @Override
    public void onError(int errCode, String msg) {
        Log.d(TAG, "onError msg = " + msg);
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                Toast.makeText(VideoActivity.this, "onError msg = " + msg, Toast.LENGTH_SHORT).show();
            }
        });
    }

    @Override
    public void onSuccess() {
        Log.d(TAG, "onSuccess");
        TXCStreamingInfo streamingInfo = mPlayerAssistor.getStreamingInfo();
        Log.d(TAG, "streamingInfo = " + streamingInfo);
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mPlayerAssistor.getStreamingInfo() != null) {
                  	//ビデオの再生
                    mSuperPlayerView.play(mPlayerAssistor.getStreamingInfo().playUrl);
                } else {
                    Toast.makeText(VideoActivity.this, "streamInfo = null", Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
});
```

使用後にPlayerを破棄します

```java
TXCPlayerAdapter.destroy();
```


[](id:sdkList)
## SDKインターフェースリスト

#### TXCPlayerAdatperの初期化

**説明**

Adapterを初期化します、毎回

**インターフェース**

```java
TXCPlayerAdapter.init(String appId);
```

**パラメータの説明**

appId：appidを入力します（サブアプリケーションを使用している場合はsubappidを入力）



#### TXCPlayerAdatperを破棄

**説明**

Adapterを破棄します。プロセス終了後に呼び出します。

**インターフェース**

```java
TXCPlayerAdapter.destroy();
```



#### プレーヤー補助クラスの作成

**説明**

プレーヤー補助クラスを介して再生fileId関連情報を取得し、DRM暗号化インターフェースなどを処置することができます。

**インターフェース**

```java
ITXCPlayerAssistor playerAssistor = TXCPlayerAdapter.createPlayerAssistor(String fileId, String pSign);
```

**パラメータの説明**

| パラメータ名 | タイプ   | 説明               |
| ------ | ------ | ------------------ |
| fileId | String | 再生したいビデオfileId |
| pSign  | String | Super Player署名     |



**プレーヤー補助クラスの破棄**

**説明**

補助クラスを破棄し、プレーヤーを終了するか、または次のビデオ再生に切り替える時に呼び出します。

**インターフェース**

```
TXCPlayerAdapter.destroyPlayerAssistor(ITXCPlayerAssistor assistor);
```



#### ビデオ再生情報のリクエスト

**説明**

このインターフェースでは、Tencent Cloud VODサーバーをリクエストし，ビデオ再生ストリーム情報などを取得することができます。

**インターフェース**

```java
playerAssistor.requestVideoInfo(ITXCRequestVideoInfoCallback callback);
```

**パラメータの説明**

| パラメータ名   | タイプ                         | 説明         |
| -------- | ---------------------------- | ------------ |
| callback | ITXCRequestVideoInfoCallback | 非同期コールバック関数 |





#### ビデオの基本情報を取得

**説明**

ビデオ情報の取得を有効にするには、playerAssistor.requestPlayInfoでコールバックする必要があります。

**インターフェース**

```java
TXCVideoBasicInfo playerAssistor.getVideoBasicInfo();
```

**パラメータの説明**

TXCVideoBasicInfo ：パラメータは次のとおりです。

| パラメータ名      | タイプ   | 説明                 |
| ----------- | ------ | -------------------- |
| name        | String | ビデオ名。           |
| duration    | Float  | ビデオの長さ。単位：秒。 |
| description | String | ビデオの説明。           |
| coverUrl    | String | ビデオカバー。           |



#### ビデオストリーム情報を取得

**説明**

ビデオストリーム情報リストの取得を有効にするには、playerAssistor.requestPlayInfoでコールバックする必要があります。

**インターフェース**

```java
TXCStreamingInfo playerAssistor.getStreamimgInfo();
```

**パラメータの説明**

TXCStreamingInfo

| パラメータ名     | タイプ   | 説明                                       |
| ---------- | ------ | ------------------------------------------ |
| playUrl    | String | 再生URL。                                 |
| subStreams | List   | アダプティブビットレートストリーミングサブストリーム情報。タイプはSubStreamInfoです。  |

SubStreamInfo

| パラメータ名         | タイプ   | 説明                                   |
| -------------- | ------ | -------------------------------------- |
| type | String | サブストリームのタイプ。現在設定可能な値はvideoのみです。 |
| width          | Int    | サブストリームのビデオの幅。単位：px。               |
| height         | Int    | サブストリームのビデオの高さ。単位：px。               |
| resolutionName | String | プレーヤーで表示するサブストリームのビデオの仕様名。       |



#### キーフレームキーモーメント情報を取得

**説明**

ビデオのキーフレームキーモーメント情報の取得を有効にするには、playerAssistor.requestPlayInfoでコールバックする必要があります。

**インターフェース**

```java
List<TXCKeyFrameDescInfo> playerAssistor.getKeyFrameDescInfo();
```

**パラメータの説明**

TXCKeyFrameDescInfo

| パラメータ名     | タイプ   | 説明          |
| ---------- | ------ | ------------- |
| timeOffset | Float  | 1.1           |
| content    | String | 「オープニングスタート...」 |



#### サムネイル情報を取得

**説明**

サムネイル情報の取得を有効にするには、playerAssistor.requestPlayInfoでコールバックする必要があります。

**インターフェース**

```java
TXCImageSpriteInfo playerAssistor.getImageSpriteInfo();
```

**パラメータの説明**

TCXImageSpriteInfo

| パラメータ名    | タイプ   | 説明                                  |
| --------- | ------ | ------------------------------------- |
| imageUrls | List   | サムネイルダウンロードURLアレイ。タイプはString。|
| webVttUrl | String | サムネイルVTTファイルダウンロードURL 。            |

