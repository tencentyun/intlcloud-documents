VODは、Androidプラットフォームでビデオをアップロードするシナリオ向けに、AndroidアップロードSDKを提供しています。アップロードのフローについては、[クライアントからのアップロードガイド](https://intl.cloud.tencent.com/document/product/266/33921) をご参照ください。

## ソースコードのダウンロード

1. [クリックしてダウンロード](https://liteav.sdk.qcloud.com/download/ugc/LiteAVSDK_UGC_Upload_Android.zip) して、AndroidアップロードDemoとソースコードをダウンロードします。
2. ダウンロードした圧縮パッケージを解凍すると、Demoディレクトリが表示されます。アップロードソースコードは、`Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload`ディレクトリにあります。

## アップロードライブラリとソースコードの統合

1. ソースコードディレクトリ`Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload`をプロジェクトディレクトリにコピーして、package名を手動で変更する必要があります。
2. `Demo/app/build.gradle`を参照して、プロジェクトに依存関係を追加します。
    ```
    implementation ('com.tencent.qcloud:cosxml:5.5.3') {
        exclude group: 'com.tencent.qcloud', module: 'mtaUtils' //mtaレポート機能を無効にする}
    }
    ```
>?[手動統合](https://intl.cloud.tencent.com/document/product/436/12159) を参照して、対応するバージョンの依存ライブラリを統合することもできます。
3. ビデオアップロードを使用するには、ネットワークとストレージ関連のアクセス許可が必要です。`AndroidManifest.xml`に次の許可ステートメントを追加することができます。
	```xml
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
	<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
		<intent-filter>
			<!--ネットワーク変更を検出するaction-->
			<action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
			<category android:name="android.intent.category.DEFAULT" />
		</intent-filter>
	</receiver>
	```

##  シンプルアップロード
#### アップロードオブジェクトの初期化

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### アップロードオブジェクトのコールバックの設定

```java
mVideoPublish.setListener(new TXUGCPublishTypeDef.ITXVideoPublishListener() {
    @Override
    public void onPublishProgress(long uploadBytes, long totalBytes) {
        mProgress.setProgress((int) (100*uploadBytes/totalBytes));
    }

    @Override
    public void onPublishComplete(TXUGCPublishTypeDef.TXPublishResult result) {
        mResultMsg.setText(result.retCode + " Msg:" + (result.retCode == 0 ? result.videoURL : result.descMsg));
    }
});
```

#### アップロードパラメータの作成

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();

param.signature = "xxx";
param.videoPath = "xxx";
```
> `signature`の計算ルールについては、[クライアントからのアップロード署名 ](https://intl.cloud.tencent.com/document/product/266/33922)をご参照ください。

#### アップロードの呼び出し

```java
int publishCode = mVideoPublish.publishVideo(param);
```

## 簡単な画像アップロード

#### アップロードオブジェクトの初期化

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### アップロードオブジェクトのコールバックの設定

```java
mVideoPublish.setListener(new TXUGCPublishTypeDef.ITXMediaPublishListener() {
    @Override
    public void onMediaPublishProgress(long uploadBytes, long totalBytes) {
        mProgress.setProgress((int) (100*uploadBytes/totalBytes));
    }
    @Override
    public void onMediaPublishComplete(TXUGCPublishTypeDef.TXMediaPublishResult mediaResult) {
        mResultMsg.setText(result.retCode + " Msg:" + (result.retCode == 0 ? result.videoURL : result.descMsg));
    }
});
```

#### アップロードパラメータの作成

```java
TXUGCPublishTypeDef.TXMediaPublishParam param = new TXUGCPublishTypeDef.TXMediaPublishParam();

param.signature = "xxx";
param.mediaPath = "xxx";
```

> `signature`の計算ルールについては、[クライアントからのアップロード署名 ](https://intl.cloud.tencent.com/document/product/266/33922)をご参照ください。

#### アップロードの呼び出し

```java
int publishCode = mVideoPublish.publishMedia(param);
```

>?
>- アップロード方法は、ファイルのサイズに応じて、通常アップロードとマルチパートアップロードが自動的に選択されます。マルチパートアップロードの各手順を気にすることなく、マルチパートアップロードを行うことができます。
>- 指定されたサブアプリケーションにアップロードする必要がある場合は、[サブアプリケーションシステム-クライアントからのアップロード](https://intl.cloud.tencent.com/document/product/266/33987)をご参照ください。
>
## 高度な機能

#### カバーの付加

アップロードパラメータとしてカバーへのパスを追加します。

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();
param.signature = "xxx";
param.videoPath = "xxx";
param.coverPath = "xxx";
```
 `signature`の計算ルールについては、[クライアントからのアップロード署名 ](https://intl.cloud.tencent.com/document/product/266/33922)をご参照ください。

#### アップロードのキャンセルと再開

アップロードをキャンセルするには、`TXUGCPublish`の`canclePublish()`インターフェースを呼び出します。

```java
mVideoPublish.canclePublish();
```

アップロードを再開するには、同じアップロードパラメータを使用し（ビデオパスとカバーパスは変更されません）`TXUGCPublish`の`publishVideo`を再度呼び出します。

#### 中断からの再開

VODはビデオのアップロード中、中断からの再開をサポートします。アップロードが予期せず終了した場合に、中断ポイントからアップロードを再開できるため、アップロード時間を短縮できます。

中断からの再開の有効時間は1日です。つまり、ビデオのアップロードが中断しても、1日以内に同じビデオを再度アップロードすると、中断したポイントからアップロードすることができます。1日を超えると、デフォルトでビデオ全体が再度アップロードされます。

アップロードパラメータの`enableResume`は、中断からの再開のスイッチであり、デフォルトで有効になっています。

#### 事前アップロード

実際のアップロード中に発生するエラーのほとんどは、ネットワーク接続の障害またはタイムアウトに起因しています。このような問題を最適化するために、最適化された事前アップロードロジックを追加しました。事前アップロードには、HTTPDNSの解決 、推奨されるアップロードリージョンの取得および最適なアップロードリージョンの検出が含まれます。

Appを起動するときに`TXUGCPublishOptCenter.getInstance().prepareUpload(signature)`を呼び出すことをお勧めします。事前アップロードモジュールは、`<ドメイン名，IP>`マッピングテーブルと最適なアップロードリージョンをローカルにキャッシュします。ネットワークスイッチが検出されると、キャッシュを自動的にパージして更新します。

>!必ず`AndroidManifest.xml`にネットワーク監視モジュールを登録してください。
```xml
<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
  <intent-filter>
    <!--ネットワーク変更を検出するaction-->
    <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
    <category android:name="android.intent.category.DEFAULT" />
  </intent-filter>
</receiver>
```

`signature`の計算ルールについては、[クライアントからのアップロード署名 ](https://intl.cloud.tencent.com/document/product/266/33922)をご参照ください。


## ビデオアップロードインターフェースの説明

アップロードオブジェクトの初期化：`TXUGCPublish`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| context   | applicationコンテキスト。        | Context | はい    |
| customKey | ユーザーを区別するために使用されます。今後の問題特定を容易にするためにAppのアカウントIDを使用することをお勧めします。 | String  | いいえ    |

VOD appIdの設定：`TXUGCPublish.setAppId`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| appId   |VOD appId。        | int | はい    |


アップロードビデオ：`TXUGCPublish.publishVideo`

| パラメータ名  | パラメータの説明 | タイプ                                 | 入力必須   |
| ----- | ---- | ---------------------------------- | ---- |
| param | アップロードパラメータ。 | TXUGCPublishTypeDef.TXPublishParam | はい    |

アップロードパラメータ：`TXUGCPublishTypeDef.TXPublishParam`

| パラメータ名         | パラメータの説明                               | タイプ      | 入力必須   |
| ------------ | ---------------------------------- | ------- | ---- |
| signature    | [クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)。 | String  | はい    |
| videoPath    | ローカルビデオファイルパス。                           | String  | はい    |
| coverPath    | ローカルカバーファイルパス。デフォルトではカバーファイルは含まれません。                  | String  | いいえ    |
| enableResume | 中断ポイントからの再開の有効無効を指定。デフォルトでは有効になっています。                      | boolean | いいえ    |
| enableHttps  | HTTPSの有効無効を指定。デフォルトでは無効になっています。                      | boolean | いいえ    |
| fileName     | Tencent Cloudにアップロードされたビデオファイル名。空のままの場合、デフォルトでローカルファイル名が使用されます。 | String  | いいえ    |

アップロードコールバックの設定：`TXUGCPublish.setListener`

| パラメータ名     | パラメータの説明        | タイプ                                       | 入力必須   |
| -------- | ----------- | ---------------------------------------- | ---- |
| listener | アップロードの進行状況と結果のコールバックを監視します。 | TXUGCPublishTypeDef.ITXVideoPublishListener | はい    |


進行状況コールバック：`TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishProgress`

| 変数名        | 変数の説明     | タイプ   |
| ----------- | -------- | ---- |
| uploadBytes | アップロード済みのバイト数。 | long |
| totalBytes  | 合計バイト数。     | long |

結果コールバック：`TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishComplete`

| 変数名   | 変数の説明 | タイプ                                  |
| ------ | ---- | ----------------------------------- |
| result | アップロード結果。 | TXUGCPublishTypeDef.TXPublishResult |

アップロード結果：`TXUGCPublishTypeDef.TXPublishResult`

| メンバー変数名   | 変数の説明      | タイプ     |
| -------- | --------- | ------ |
| retCode  | 結果コード。       | int    |
| descMsg  | アップロード失敗のエラー説明。 | String |
| videoId  | VODビデオファイルID。  | String |
| videoURL | ビデオストレージアドレス。    | String |
| coverURL | カバーストレージアドレス。    | String |

事前アップロード：`TXUGCPublishOptCenter.prepareUpload`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| signature   | [クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)。        | String | はい    |

## 画像アップロードインターフェースの説明

アップロードオブジェクトの初期化：`TXUGCPublish`

| パラメータ名  | パラメータの説明                                                  | タイプ    | 入力必須 |
| --------- | --------------------------------------------------------- | ------- | ---- |
| context   | applicationコンテキスト。                                        | Context | はい   |
| customKey | ユーザーを区別するために使用されます。今後の問題特定を容易にするためにAppのアカウントIDを使用することをお勧めします。 | String  | いいえ    |

VOD appIdの設定：`TXUGCPublish.setAppId`

| パラメータ名 | パラメータの説明  | タイプ | 入力必須 |
| -------- | --------- | ---- | ---- |
| appId    | VOD appId。 | int  | はい   |

アップロード画像：`TXUGCPublish.publishMedia`

| パラメータ名 | パラメータの説明 | タイプ                                    | 入力必須 |
| -------- | -------- | --------------------------------------- | ---- |
| param    | アップロードパラメータ。 | TXUGCPublishTypeDef.TXMediaPublishParam | はい   |

アップロードパラメータ：`TXUGCPublishTypeDef.TXMediaPublishParam`

| パラメータ名     | パラメータの説明                                           | タイプ    | 入力必須 |
| ------------ | -------------------------------------------------- | ------- | ---- |
| signature    | [クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)。       | String  | はい   |
| mediaPath    | ローカル画像ファイルパス。                                   | String  | はい   |
| enableResume | 中断ポイントからの再開の有効無効を指定。デフォルトでは有効になっています。                      | boolean | いいえ    |
| enableHttps  | HTTPSの有効無効を指定。デフォルトでは無効になっています。                      | boolean | いいえ    |
| fileName     | Tencent Cloudにアップロードされたビデオファイル名です。空のままの場合、デフォルトでローカルファイル名が使用されます。 | String  | いいえ    |

アップロードコールバックの設定：`TXUGCPublish.setListener`

| パラメータ名 | パラメータの説明               | タイプ                                        | 入力必須 |
| -------- | ---------------------- | ------------------------------------------- | ---- |
| listener | アップロードの進行状況と結果のコールバックを監視します。 | TXUGCPublishTypeDef.ITXMediaPublishListener | はい   |

進行状況コールバック：`TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishProgress`

| 変数名    | 変数の説明         | タイプ |
| ----------- | ---------------- | ---- |
| uploadBytes | アップロード済みのバイト数。 | long |
| totalBytes  | 合計バイト数。         | long |

結果コールバック：`TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishComplete`

| 変数名 | 変数の説明 | タイプ                                |
| -------- | -------- | ----------------------------------- |
| result   | アップロード結果。 | TXUGCPublishTypeDef.TXPublishResult |

アップロード結果：`TXUGCPublishTypeDef.TXMediaPublishResult`

| メンバー変数名 | 変数の説明           | タイプ   |
| ------------ | ------------------ | ------ |
| retCode      | 結果コード。             | int    |
| descMsg      | アップロード失敗のエラー説明。 | String |
| mediaId      | VODビデオファイルID。 | String |
| mediaURL     | メディアリソースストレージアドレス。   | String |

事前アップロード：`TXUGCPublishOptCenter.prepareUpload`

| パラメータ名  | パラメータの説明                                     | タイプ   | 入力必須 |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)。 | String | はい   |

## エラーコード

SDKは、`TXUGCPublishTypeDef.ITXVideoPublishListene\ITXMediaPublishListener`インターフェースを介してビデオのアップロードのステータスを監視します。従って、`TXUGCPublishTypeDef.TXPublishResult\TXMediaPublishResult`の`retCode`を使用して、ビデオのアップロード状況を確認することができます。

| ステータスコード  | TVCConstantsにおいて対応する定数         | 意味                     |
| :--: | :----------------------------- | :--------------------- |
|  0   | NO_ERROR                       | アップロードに成功しました。                   |
| 1001 | ERR_UGC_REQUEST_FAILED         |  アップロードリクエストが失敗しました。通常、クライアントの署名が期限切れまたは無効になっており、Appに別の署名を再申請する必要があります。                 |
| 1002 | ERR_UGC_PARSE_FAILED           | リクエスト情報の解析に失敗しました。               |
| 1003 | ERR_UPLOAD_VIDEO_FAILED        | ビデオのアップロードに失敗しました。                 |
| 1004 | ERR_UPLOAD_COVER_FAILED        | カバーのアップロードに失敗しました。                 |
| 1005 | ERR_UGC_FINISH_REQUEST_FAILED  | アップロード終了リクエストに失敗しました。               |
| 1006 | ERR_UGC_FINISH_RESPONSE_FAILED |アップロード終了の応答に失敗しました。               |
| 1007 | ERR_CLIENT_BUSY                | クライアントはビジーです（オブジェクトはそれ以上のリクエストを処理できません）。      |
| 1008 | ERR_FILE_NOEXIT                | アップロードファイルが存在しません。                |
| 1009 | ERR_UGC_PUBLISHING             | ビデオのアップロード中です。                |
| 1010 | ERR_UGC_INVALID_PARAM          | アップロードパラメータが空です。                 |
| 1012 | ERR_UGC_INVALID_SIGNATURE      | ビデオアップロードのsignatureが空です。        |
| 1013 | ERR_UGC_INVALID_VIDOPATH       | ビデオファイルのパスが空です。              |
| 1014 | ERR_UGC_INVALID_VIDEO_FILE     | 現在のパスにビデオファイルが存在しません。           |
| 1015 | ERR_UGC_FILE_NAME              | 動画アップロードファイル名が長すぎる（40を超える）か、または特殊文字が含まれています。 |
| 1016 | ERR_UGC_INVALID_COVER_PATH     | ビデオファイルのカバーパスが間違っており、ファイルが存在しません。       |
| 1017 | ERR_USER_CANCEL                | ユーザーがアップロードをキャンセルしました。       |
| 1018 | ERR_UPLOAD_VOD                 | 5M未満のファイルのVODへの直接アップロードに失敗しました。       |


