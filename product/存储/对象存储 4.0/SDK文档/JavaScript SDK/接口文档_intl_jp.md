> 本書では、JavaScript SDK APIを詳細に説明します。

JavaScript SDK githubアドレス：[tencentyun/cos-js-sdk-v5](https://github.com/tencentyun/cos-js-sdk-v5)。

下記コードに表記されるCOSはSDKのクラス名を表し、cosはSDKのインスタンスを表します。

以下のSecretId、SecretKey、Bucket、Regionなどの名称の意味と取得方法については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

下記パラメータ名の前の「-」は「サブパラメータ」を表します。



## 構造関数

### new COS({})

直接scriptタグ引用SDKを参照する際に、SDKがグローバル変数名COSを使用し、その構造関数でSDKインスタンスを作成できます。

#### 使用例

COS SDKインスタンスを作成します。COS SDKは以下のフォーマットで作成られます。

- フォーマット1（推奨）：バックエンドが一時的な暗号鍵を取得しフロントエンドに送り、フロントエンドにて署名を計算します。
```js
var cos = new COS({
    // 選択必須パラメータ
    getAuthorization: function (options, callback) {
        // サーバーJSとPHP例：https://github.com/tencentyun/cos-js-sdk-v5/blob/master/server/
        // サーバーの他の参考言語COS STS SDK ：https://github.com/tencentyun/qcloud-cos-sts-sdk
        // STS詳細ドキュメント：https://cloud.tencent.com/document/product/436/14048
        $.get('http://example.com/server/sts.php', {
            bucket: options.Bucket,
            region: options.Region,
        }, function (data) {
            callback({
                TmpSecretId: data.TmpSecretId,
                TmpSecretKey: data.TmpSecretKey,
                XCosSecurityToken: data.XCosSecurityToken,
                ExpiredTime: data.ExpiredTime, // SDKがExpiredTime時間前にgetAuthorizationを再び呼び出すことはしません
            });
        });
    }
});
```

- フォーマット2（推奨）：細い粒度権限コントロール。バックエンドが一時的な暗号鍵を取得しフロントエンドに送り、フロントエンドが同じリクエストだけで一時的な暗号鍵を繰り返して使用するが、バックエンドがScope細い粒度で権限をコントロールできます。
```js
var cos = new COS({
    // 選択必須パラメータ
    getAuthorization: function (options, callback) {
        // サーバー例：https://github.com/tencentyun/qcloud-cos-sts-sdk/edit/master/scope.md
        $.ajax({
            method: 'POST',
            url: 'http://example.com/sts-scope.php',
            data: JSON.stringify(options.Scope),
            beforeSend: function () {
                xhr.setRequestHeader('Content-Type', 'application/json');
            },
            dataType: 'json',
            success: function (data) {
                var credentials = data.credentials;
                callback({
                    TmpSecretId: credentials.tmpSecretId,
                    TmpSecretKey: credentials.tmpSecretKey,
                    XCosSecurityToken: credentials.sessionToken, // sessionTokenを提供する必要があります 
                    ExpiredTime: data.expiredTime,
                    ScopeLimit: true, // 細い粒度権限コントロールをtrueに設定すると、暗号鍵を同じリクエストでのみ繰り返し使用するよう制限します
                });
            }
        });
    }
});
```

- フォーマット3（非推奨）：フロントエンドがリクエスト前ごとにgetAuthorizationを介して署名を取得する必要があります。バックエンドが固定の暗号鍵または一時的な暗号鍵で計算した署名をフロントエンドに返します。このフォーマットのシャードアップロード権限をコントロールしにくいので、おすすめしません。
```
var cos = new COS({
    // 選択必須パラメータ
    getAuthorization: function (options, callback) {
        // サーバーでの署名取得について、対応言語のCOS SDK：https://cloud.tencent.com/document/product/436/6474を参照してください
        // 注意：セキュリティリスクがあります。バックエンドではmethod、pathnameにより権限をコントロールしなければなりません。例えば、put /の禁止などです
        $.get('http://example.com/server/auth.php', {
            method: options.Method,
            pathname: '/' + options.Key,
        }, function (data) {
            callback({
                Authorization: data.authorization,
                // XCosSecurityToken: data.sessionToken。 //一時的な暗号鍵を使用するには、sessionTokenをXCosSecurityTokenに渡す必要があります
            });
        });
    },
    // 選択可能なパラメータ
    FileParallelLimit: 3,    // ファイルアップロード同時接続数のコントロール
    ChunkParallelLimit: 3,   // 単一ファイルのシャードアップロード同時接続数のコントロール
    ProgressInterval: 1000,  // アップロードするonProgressのコールバック間隔のコントロール
});
```

- フォーマット4（非推奨）：フロントエンドが固定暗号鍵で署名を計算します。このフォーマットがフロントエンドデバッグに適します。このフォーマットを使う場合、暗号鍵の漏えいを避けてください。
```
var cos = new COS({
    SecretId: 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
    SecretKey: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
});
```

#### 構造関数パラメータについて

| パラメータ名             | パラメータ説明                                                     | タイプ     | 必須項目 |
| ------------------ | ------------------------------------------------------------ | -------- | ---- |
| SecretId           | ユーザーのSecretId                                              | String   | いいえ   |
| SecretKey          | ユーザーのSecretKey。暗号鍵の漏えいを避けるためにフロントエンドデバッグのみでの使用をおすすめします       | String   | いいえ   |
| FileParallelLimit  | 同一インスタンスのアップロードするファイル同時接続数。デフォルト値は3                        | Number   | いいえ   |
| ChunkParallelLimit | 同一アップロードファイルのシャード同時接続数。デフォルト値は3                          | Number   | いいえ   |
| ChunkSize          | シャードアップロードの場合の各シャードのサイズ。デフォルト値は1048576 (1MB)            | Number   | いいえ   |
| ProgressInterval   | アップロード進捗のコールバックメソッドonProgressのコールバック頻度（単位ms）。デフォルト値は1000 | Number   | いいえ   |
| Protocol           | カスタマイズしたリクエストプロトコル。オプション項目は「https:」、「http:」。デフォルトで現在のページが「http:」であると判断した場合、「http:」を使用します。さもなければ「https:」を使用します | String   | いいえ   |
| getAthorization    | 署名を取得するコールバックメソッド。SecretId、SecretKeyがなければ、このパラメータは選択必須 | Function | いいえ   |

#### getAuthorizationコールバック関数の説明（フォーマット1を使用）

```
getAuthorization: function(options, callback) { ... }
```

getAuthorizationのコールバックパラメータ説明：

| パラメータ名   | パラメータ説明                                                    | タイプ     |
| -------- | ------------------------------------------------------------ | -------- |
| options  | 一時的な暗号鍵を取得するために必要なパラメータオブジェクト                                   | Function |
| - Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String   |
| - Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String   |
| callback | 一時的な暗号鍵を取得した後の返し方法                                 | Function |

一時的な暗号鍵を取得した後、callbackで1つのオブジェクトを返します。返されたオブジェクトの属性リストは以下のとおりです。

| 属性名            | パラメータ説明                                                     | タイプ   | 必須項目 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| TmpSecretId       | 取得した一時的な暗号鍵のtmpSecretId                             | String | はい   |
| TmpSecretKey      | 取得した一時的な暗号鍵のtmpSecretKey                            | String | いいえ   |
| XCosSecurityToken | 取得した一時的な暗号鍵のsessionToken。headerのx-cos-security-tokenフィールドに対応します | String | いいえ   |
| ExpiredTime       | 取得した一時的な暗号鍵のexpiredTime。タイムアウト時間                   | String | いいえ   |

#### getAuthorizationコールバック関数の説明（フォーマット2を使用）

```
getAuthorization: function(options, callback) { ... }
```

getAuthorizationの関数説明コールバックパラメータの説明：

| パラメータ名    | パラメータ説明                                                     | タイプ     | 必須項目 |
| --------- | ------------------------------------------------------------ | -------- | ---- |
| options   | 署名を取得するために必要なパラメータオブジェクト                                       | Function | いいえ   |
| - Method  | 現在のリクエストのMethod                                            | Function | いいえ   |
| - Key     | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。詳細については、[オブジェクトのキーについて](https://cloud.tencent.com/document/product/436/13324)を参照してください | String   | いいえ   |
| - Query   | 現在のリクエストのqueryパラメータオブジェクト。{key: 'val'}のフォーマット               | Object   | いいえ   |
| - Headers | 現在のリクエストのheaderパラメータオブジェクト。{key: 'val'}のフォーマット              | Function | いいえ   |
| callback  | 一時的な暗号鍵を取得した後のコールバック                                     | Function | いいえ   |

getAuthorization計算完了後、callbackで署名文字列または1つのオブジェクトを返します。
署名文字列を返す際、文字列タイプを返します。使用するHeader認証情報フィールドAuthorizationです。
オブジェクトを返す際に、返されるオブジェクト属性リストは以下のとおりです。

| 属性名            | パラメータ説明                                                     | タイプ   | 必須項目 |
| ----------------- | ------------------------------------------------------------ | ------ | ---- |
| Authorization     | 取得した一時的な暗号鍵の                                        | String | はい   |
| XCosSecurityToken | 取得した一時的な暗号鍵のsessionToken。headerのx-cos-security-tokenフィールドに対応します | String | いいえ   |

#### 認証情報の取得

インスタンス自体の認証情報はインスタンス化のときに渡されたパラメータを用いて取得方法をコントロールします。以下3つの取得方法があります。

1.インスタンス化のとき、SecretId、SecretKeyが渡されると、インスタンス内部で署名を計算します。
2.インスタンス化のとき、getAuthorizationコールバックが渡されると、このコールバックで署名を計算して署名をインスタンスに返します。
3.インスタンス化のとき、getSTSコールバックが渡されると、一時的な暗号鍵をこのコールバック完了後にインスタンスに返します。リクエストごとにインスタンス内部で一時的な暗号鍵を用いて署名を算出します。



## 静的方法

### COS.getAuthorization

COS XML APIのリクエストの場合、プライベートリソース操作には認証情報Authorizationが必要であり、それで現在のリクエストが正当であるかどうかを判断します。

認証情報の使用方法は以下2つあります。

1. headerパラメータに入れて使用する。フィールド名：authorization
2. urlパラメータに入れて使用する。フィールド名：sign

COS.getAuthorizationメソッドは認証情報（Authorization）の計算に使用され、リクエストの正当性の署名情報を検証できます。

> !このメソッドをフロントエンドデバッグのときにのみ使用することをおすすめします。プロジェクト運営開始の場合、フロントエンドでの署名計算方法をおすすめしません。暗号鍵を漏えいするリスクがあります。

#### 使用例

ファイルダウンロードの認証情報を取得します：

```
var Authorization = COS.getAuthorization({
    SecretId: 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
    SecretKey: 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
    Method: 'get',
    Key: 'a.jpg',
    Expires: 60,
    Query: {},
    Headers: {}
});
```

#### パラメータ説明

| パラメータ名    | パラメータ説明                                                     | タイプ   | 必須項目 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| SecretId  | ユーザーのSecretId                                              | String | はい   |
| SecretKey | ユーザーのSecretKey                                             | String | はい   |
| Method    | 操作方法。例えば、get、post、delete、headなどのHTTP方法           | String | はい   |
| Key       | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。**リクエスト操作対象がファイルであれば、ファイル名とし、必須パラメータです**。操作対象がBucketであれば、空白とします | String | いいえ   |
| Expires   | 署名タイムアウト時間（秒）。デフォルトは900秒                                      | Number | いいえ   |
| Query     | リクエストするqueryパラメータオブジェクト                                        | Object | いいえ   |
| Headers   | リクエストするheaderパラメータオブジェクト                                       | Object | いいえ   |

#### 戻り値の説明

戻り値は算出された認証情報文字列authorizationです。



## ツール方法

### Get Object Url

#### 使用例

例1：署名付きではないObject Urlを取得します。

```
var url = cos.getObjectUrl({
    Key: '1.jpg',
    Sign: false
});
```

例2：署名付きObject Urlを取得します。

```
var url = cos.getObjectUrl({
    Key: '1.jpg'
});
```

例3：署名プロセスは非同期取得です。callbackで署名付きUrlを取得する必要があります。

```
cos.getObjectUrl({
    Key: '1.jpg',
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

例4：署名済みPut ObjectのアップロードUrlを取得します。

```
cos.getObjectUrl({
    Method: 'PUT',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    console.log(err || data.Url);
});
```

例5：ファイルUrlを取得しファイルをダウンロードします。

```
cos.getObjectUrl({
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (!err) {
        var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment'; // 強制的にダウンロードするパラメータの補充
        window.open(downloadUrl); // ここに新ウィンドウでUrlを開きます。現在のウィンドウから開く必要があれば、非表示のiframeでダウンロードするか、aタグのdownload属性を使ってダウンロードします
    }
});
```

#### パラメータ説明

| パラメータ名  | パラメータ説明                                                     | タイプ    | 必須項目 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String  | はい   |
| Region  | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String  | はい   |
| Key     | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。**リクエスト操作対象がファイルであれば、ファイル名とし、必須パラメータです**。操作対象がBucketであれば、空白とします | String | はい   |
| Sign    | 署名付きUrlであるかどうか                                       | Boolean | いいえ   |
| Method  | 操作方法。例えば、get、post、delete、 headなどのHTTP方法。デフォルトはget | String  | いいえ   |
| Query   | 署名計算に参加するqueryパラメータオブジェクト                                | Object  | いいえ   |
| Headers | 署名計算に参加するheaderパラメータオブジェクト                               | Object  | いいえ   |

#### 戻り値の説明

戻り値は以下の２種類の文字列です。

1. 署名計算が同期計算（例えば、インスタンス化のときにSecretIdとSecretKeyが渡された）であれば、デフォルトで署名付きUrlを返します。
2. さもなければ署名付きではないUrlを返します。

####コールバック関数の説明

```
function(err, data) { ... }
```

| パラメータ名 | パラメータ説明                                                     | タイプ   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| data   | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - Url  | 算出されたUrl                                               | String |

### ブラウザからのダウンロードファイル

ブラウザからのダウンロードファイルはcos.getObjectUrlによりUrlを取得した後にダウンロードを呼び出す必要があります。下記ダウンロード例は参考にしてください。

ブラウザのダウンロードプロセスはブラウザより直接的に送信されるGet Objectリクエストです。具体的なパラメータについては、cos.getObjectメソッドを参照してください。

#### 使用例

例1：ファイルUrlを取得してファイルをダウンロードします。

```
cos.getObjectUrl({
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    if (!err) {
        var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment'; // 強制的にダウンロードするパラメータの補充
        window.open(downloadUrl); // ここに新ウィンドウでUrlを開きます。現在のウィンドウから開く必要があれば、非表示のiframeでダウンロードするか、aタグのdownload属性を使ってダウンロードします
    }
});
```

例2：非表示のiframeによりダウンロードします。

```
<iframe id="downloadTarget" style="width:0;height:0;" frameborder="0"></iframe>
<a id="downloadLink" href="javascript:void(0)">ダウンロード</a>
<script>
document.getElementById('downloadLink').onclick = function () {
    document.getElementById('downloadTarget').src = downloadUrl; // 例1で取得したダウンロードUrl
};
</script>
```

例3：非表示のaタグのdownload属性を使用します。

> !download属性は低バージョンブラウザをサポートしません。

```
<iframe id="downloadTarget" style="width:0;height:0;" frameborder="0"></iframe>
<!-- 例1のdownloadUrlを下記aタグのhrefパラメータに入れます -->
<a id="downloadLink" href="{downloadUrl}" download="1.jpg">ダウンロード</a>
```



## Bucket操作

### Head Bucket



Head Bucketリクエストにより、このBucketが存在するかどうか、アクセス権限があるかどうかを確認できます。Headの権限がReadと一致します。このBucketが存在する場合、HTTPステータスコード200を返します。このBucketにアクセス権限がなければ、HTTPステータスコード403を返します。このBucketが存在しない場合、HTTPステータスコード404を返します。詳細については、[Head Bucket API説明](https://cloud.tencent.com/document/product/436/7735)を参照してください。

#### 使用例

```
cos.headBucket({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',     /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Get Bucket



Get BucketリクエストがList Objectリクエストと同等です。このBucket配下の部分またはすべてのObjectを一覧表示できます。このAPIの呼び出し者にはBucketのRead権限が必要です。詳細については、[Get Bucket API説明](https://cloud.tencent.com/document/product/436/7734)を参照してください。

#### 使用例

例1：ディレクトリaのすべてのファイルを一覧表示します。

```
cos.getBucket({
    Bucket: 'test-1250000000',/* 必須 */
    Region: 'ap-guangzhou',     /* 必須 */
    Prefix: 'a/',          /* 非必須 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

戻り値の書式：

```
{
    "Name": "test-1250000000",
    "Prefix": "",
    "Marker": "a/",
    "MaxKeys": "1000",
    "Delimiter": "",
    "IsTruncated": "false",
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

例2：ディレクトリaのファイルを一覧表示します。深い階層への走査はしません。

```
cos.getBucket({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',   /* 必須 */
    Prefix: 'a/',              /* 非必須 */
    Delimiter: '/',           /* 非必須 */
}, function(err, data) {
    console.log(err || data.CommonPrefix);
});
```

戻り値の書式：

```
{
    "Name": "test-1250000000",
    "Prefix": "a/",
    "Marker": "",
    "MaxKeys": "1000",
    "Delimiter": "/",
    "IsTruncated": "false",
    "CommonPrefixes": [{
        "Prefix": "a/1/"
    }],
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### パラメータ説明

| パラメータ名       | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region       | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Prefix       | プレフィックスのマッチング。返されたファイルのプレフィックスアドレスの設定に使用されます                         | String | いいえ   |
| Delimiter    | 境界記号は区切り記号で、"/"を渡すことは一般的です。Prefixがあれば、Prefixからdelimiterまでの同じパスを同じ種類にし、Common Prefixと定義します。そしてすべてのCommon Prefixを一覧表示します。Prefixがなければ、パス開始点から開始します | String | いいえ   |
| Marker       | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されたエントリーはmarkerから開始します  | String | いいえ   |
| MaxKeys      | 単回返される最大エントリー数。デフォルトは1000                             | String | いいえ   |
| EncodingType | 戻り値のエンコード方法を決めます。選択可能な値：url                            | String | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名           | パラメータ説明                                                     | タイプ        |
| ---------------- | ------------------------------------------------------------ | ----------- |
| err              | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| - statusCode     | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers        | リクエストによって返されたヘッダー情報                                           | Object      |
| data             | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - headers        | リクエストによって返されたヘッダー情報                                           | Object      |
| - statusCode     | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - CommonPrefixes | Prefixとdelimiterの間の同じパスが1つのタイプに分類され、Common Prefixと定義します | ObjectArray |
| - - Prefix       | 同じCommonのプレフィックス                                           | String      |
| - - Name         | Bucketの情報を説明します                                           | String      |
| - Prefix         | プレフィックスのマッチング。返されたファイルのプレフィックスアドレスの設定に使用されます                         | String      |
| - Marker         | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されたエントリーはmarkerから開始します  | String      |
| - MaxKeys        | リクエストに単回応答する期間内に結果を返した最大エントリー数                       | String      |
| - IsTruncated    | リクエストに応答するエントリーが切り捨てられたかどうか。文字列：「true」または「false」          | String      |
| - NextMarker     | 返されたエントリーが遮断された場合、NextMarkerを返す、この点は次のエントリーの開始点とします     | String      |
| - Encoding-Type  | 戻り値の符号化方式。Delimiter、Marker、Prefix、NextMarker、Keyに適用します | String      |
| - Contents       | メタデータ情報                                                   | ObjectArray |
| - - ETag         | ファイルのMD-5アルゴリズムチェック値。例えば、`"22ca88419e2ed4721c23807c678adbe4c08a7880"`、**注意：前後にダブルコーテーションが付きます** | String      |
| - - Size         | ファイルサイズを説明します。単位はByteです                                    | String      |
| - - Key          | Object名                                                   | String      |
| - - LastModified | Objectが最後に変更された時間。例えば、2017-06-23T12:33:27.000Z       | String      |
| - - Owner        | Bucket所有者情報                                            | Object      |
| - ID             | BucketのAppID                                              | String      |
| - StorageClass   | Objectのストレージレベル。列挙値：STANDARD、STANDARD_IA             | String      |


### List Object Versions

List Object Versions APIにより、このBucket配下の一部または全部のObjectのVersionを一覧表示できます。このAPIの呼び出し者にはBucketのRead権限が必要です。

#### 使用例

例1：ディレクトリaのすべてのファイルのバージョンを一覧表示します。

```
cos.listObjectVersions({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Prefix: 'a/',           /* 非必須 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

戻り値の書式：

```
{
    "Name": "test-1250000000",
    "Prefix": "",
    "KeyMarker": "",
    "VersionIdMarker": "",
    "MaxKeys": "1000",
    "IsTruncated": "false",
    "DeleteMarkers": [{
        "Key": "0001.txt",
        "VersionId": "MTg0NDY3NDI1MzM4MzI5OTg5MjM",
        "IsLatest": "false",
        "LastModified": "2018-10-18T15:29:12.000Z",
        "Owner": {"UID": "1250000000"}
    }],
    "Versions": [{
        "Key": "0001.txt",
        "VersionId": "MTg0NDY3NDI1MzM4MzI5OTI2NzU",
        "IsLatest": "true",
        "LastModified": "2018-10-18T15:29:18.000Z",
        "ETag": "\"5a8dd3ad0756a93ded72b823b19dd877\"",
        "Size": "6",
        "StorageClass": "STANDARD",
        "Owner": {"UID": "1250000000"}
    }, {
        "Key": "0001.txt",
        "VersionId": "MTg0NDY3NDI1MzM4MzMwMTk3NzQ",
        "IsLatest": "false",
        "LastModified": "2018-10-18T15:28:51.000Z",
        "ETag": "\"5a8dd3ad0756a93ded72b823b19dd877\"",
        "Size": "6",
        "StorageClass": "STANDARD",
        "Owner": {"UID": "1250000000"}
    }],
    "statusCode": 200,
    "headers": {}
}
```

例2：ディレクトリaのファイルを一覧表示します。深い階層への走査はしません。

```
cos.listObjectVersions({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',   /* 必須 */
    Prefix: '',              /* 非必須 */
    Delimiter: '/',           /* 非必須 */
}, function(err, data) {
    if (err) {
        console.log(err);
    } else {
        console.log(data.CommonPrefix);
        console.log(data.Conents);
    }
});
```

戻り値の書式：

```
{
    "Name": "test-1250000000",
    "Prefix": "1mb.zip",
    "KeyMarker": "",
    "VersionIdMarker": "",
    "MaxKeys": "1000",
    "IsTruncated": "false",
    "DeleteMarkers": [{
        "Key": "1mb.zip",
        "VersionId": "MTg0NDY3NDI1MzM4NzM3NTU1NDE",
        "IsLatest": "true",
        "LastModified": "2018-10-18T04:09:56.000Z",
        "Owner": {"UID": "1250000000"}
    }],
    "Versions": [{
        "Key": "1mb.zip",
        "VersionId": "MTg0NDY3NDI1MzM5Mjg1ODk4OTI",
        "IsLatest": "false",
        "LastModified": "2018-10-17T12:56:01.000Z",
        "ETag": "\"b6d81b360a5672d80c27430f39153e2c\"",
        "Size": "1048576",
        "StorageClass": "STANDARD",
        "Owner": {"UID": "1250000000"}
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### パラメータ説明

| パラメータ名          | パラメータ説明                                                     | タイプ   | 必須項目 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region          | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Prefix          | プレフィックスのマッチング。返されたファイルのプレフィックスアドレスの設定に使用されます                         | String | いいえ   |
| Delimiter       | 境界記号は区切り記号で、"/"を渡すことは一般的です。Prefixがあれば、Prefixからdelimiterまでの同じパスを同じ種類にし、Common Prefixと定義します。そしてすべてのCommon Prefixを一覧表示します。Prefixがなければ、パス開始点から開始します | String | いいえ   |
| KeyMarker       | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されたObjectエントリーはKeyMarkerから始まります | String | いいえ   |
| VersionIdMarker | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されたVersionIdエントリーはVersionIdMarkerから開始します | String | いいえ   |
| MaxKeys         | 単回返される最大エントリー数。デフォルトは1000                             | String | いいえ   |
| EncodingType    | 戻り値のエンコード方法を決めます。選択可能な値：url                            | String | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名            | パラメータ説明                                                     | タイプ        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| - statusCode      | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers         | リクエストによって返されたヘッダー情報                                           | Object      |
| data              | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - headers         | リクエストによって返されたヘッダー情報                                           | Object      |
| - statusCode      | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - CommonPrefixes  | Prefixとdelimiterの間の同じパスが1つのタイプに分類され、Common Prefixと定義します | ObjectArray |
| - - Prefix        | 同じCommonのプレフィックス                                           | String      |
| - - Name          | Bucketの情報を説明します                                           | String      |
| - Prefix          | プレフィックスのマッチング。返されたファイルのプレフィックスアドレスの設定に使用されます                         | String      |
| - KeyMarker       | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されたObjectエントリーはKeyMarkerから始まります | String      |
| - VersionIdMarker | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されたVersionIdエントリーはVersionIdMarkerから開始します | String      |
| - MaxKeys         | リクエストに単回応答する期間内に結果を返した最大エントリー数                       | String      |
| - IsTruncated     | リクエストに応答するエントリーが切り捨てられたかどうか。文字列：「true」または「false」          | String      |
| - NextMarker      | 返されたエントリーが遮断された場合、NextMarkerを返す、この点は次のエントリーの開始点とします     | String      |
| - Encoding-Type   | 戻り値の符号化方式。Delimiter、Marker、Prefix、NextMarker、Keyに適用します | String      |
| - DeleteMarkers   | バケットはマルチバージョンが有効になっている場合、削除操作によりデフォルトで1つのDeleteMarkerタグが新規追加されることになります | ObjectArray |
| - - ETag          | ファイルのMD-5アルゴリズムチェック値。例えば、`"22ca88419e2ed4721c23807c678adbe4c08a7880"`、**注意：前後にダブルコーテーションが付きます** | String      |
| - - Size          | ファイルサイズを説明します。単位はByteです                                    | String      |
| - - Key           | Object名                                                   | String      |
| - - IsLatest      | 最新バージョンであるかどうか。列挙値："true"、"false"                        | String      |
| - - LastModified  | Objectが最後に変更された時間。例えば、2017-06-23T12:33:27.000Z       | String      |
| - - Owner         | Bucket所有者情報                                            | Object      |
| - - - ID          | BucketのAppID                                              | String      |
| - Versions        | メタデータ情報                                                   | ObjectArray |
| - - ETag          | ファイルのMD-5アルゴリズムチェック値。例えば、`"22ca88419e2ed4721c23807c678adbe4c08a7880"`、**注意：前後にダブルコーテーションが付きます** | String      |
| - - Size          | ファイルサイズを説明します。単位はByteです                                    | String      |
| - - Key           | Object名                                                   | String      |
| - - IsLatest      | 最新バージョンであるかどうか。列挙値："true"、"false"                        | String      |
| - - LastModified  | Objectが最後に変更された時間。例えば、2017-06-23T12:33:27.000Z       | String      |
| - - StorageClass  | Objectのストレージレベル。列挙値：STANDARD、STANDARD_IA             | String      |
| - - Owner         | Bucket所有者情報                                            | Object      |
| - - - ID          | BucketのAppID                                              | String      |

### Delete Bucket

 

Delete Bucket APIのリクエストは、指定するアカウントでBucketを削除することになります。削除前にBucketの内容が空白であるかを確認します。Bucket内の情報を削除しないとBucket自体が削除されません。注意：削除成功の場合、返されたHTTPステータスコードは200または204になります。詳細については、[Delete Bucket API説明](https://cloud.tencent.com/document/product/436/7732)を参照してください。

#### 使用例

```
cos.deleteBucket({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou'     /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Get Bucket ACL



Get Bucket ACL APIは、BucketのACL(access control list)、すなわち、バケット（Bucket）のアクセス権限コントロールリストを取得するために使用されます。このAPIについて、Bucketの所有者のみが操作権限があります。詳細については、[Get Bucket ACL API説明](https://cloud.tencent.com/document/product/436/7733)を参照してください。

#### 使用例

```
cos.getBucketAcl({
    Bucket: 'test-1250000000',/* 必須 */
    Region: 'ap-guangzhou'     /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 戻り例

```
{
    "GrantFullControl": "",
    "GrantWrite": "",
    "GrantRead": "",
    "GrantReadAcp": "id=\"qcs::cam::uin/10002:uin/10002\"",
    "GrantWriteAcp": "id=\"qcs::cam::uin/10002:uin/10002\"",
    "ACL": "private",
    "Owner": {
        "ID": "qcs::cam::uin/10001:uin/10001",
        "DisplayName": "qcs::cam::uin/10001:uin/10001"
    },
    "Grants": [{
        "Grantee": {
            "ID": "qcs::cam::uin/10002:uin/10002",
            "DisplayName": "qcs::cam::uin/10002:uin/10002"
        },
        "Permission": "READ"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名             | パラメータ説明                                                     | タイプ        |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err                | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります。 | Object      |
| - statusCode       | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers          | リクエストによって返されたヘッダー情報                                           | Object      |
| data               | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - statusCode       | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers          | リクエストによって返されたヘッダー情報                                           | Object      |
| - ACL              | Bucket保有者情報                                            | Object      |
| - GrantRead        | 認証対象者に読取権限を付与します                                         | String      |
| - GrantWrite       | 認証対象者に書込権限を付与します                                         | String      |
| - GrantReadAcp     | 認証対象者にAclとPolicyの読取権限を付与します                            | String      |
| - GrantWriteAcp    | 認証対象者にAclとPolicyの書込権限を付与します                              | String      |
| - GrantFullControl | 認証対象者に読書権限を付与します                                         | String      |
| - Owner            | Bucket所有者情報                                            | Object      |
| - - DisplayName    | Bucket所有者の名称                                          | String      |
| - - ID             | Bucket所有者のID。<br>フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> <br>ルートアカウントの場合、&lt;OwnerUin>と&lt;SubUin>が同じ値です | String      |
| - Grants           | 認証対象者情報と権限情報リスト                                   | ObjectArray |
| - - Permission     | 認証対象者に付与する権限情報を指定します。列挙値：READ、WRITE、READ_ACP、WRITE_ACP、FULL_CONTROL | String      |
| - - Grantee        | 認証対象者の情報を説明します。typeタイプは、RootAccount、Subaccountです。<br>typeタイプがRootAccountの場合、IDはルートアカウントを表します。<br>typeタイプがSubaccountの場合、IDはサブアカウントを表します | Object      |
| - - - DisplayName  | ユーザー名                                                   | String      |
| - - - ID           | ユーザーのID。<br>ルートアカウントの場合、フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin> <br>またはqcs::cam::anyone:anyone （すべてのユーザー）<br>サブアカウントの場合、フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> | String      |

### Put Bucket ACL

 

Put Bucket ACL APIは、BucketのACLテーブルへの書込みに使用されます。Header："x-cos-acl"、"x-cos-grant-read"、"x-cos-grant-write"、"x-cos-grant-full-control"を介してACL情報を取得でき、またはBodyを介してXML形式でACL情報を取得できます。詳細については、[Put Bucket ACL API説明](https://cloud.tencent.com/document/product/436/7737)を参照してください。

#### 使用例

Bucketのパブリック読取を設定します：

```
cos.putBucketAcl({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    ACL: 'public-read'
}, function(err, data) {
    console.log(err || data);
});
```

ユーザーにBucketの読書権限を付与します：

```
cos.putBucketAcl({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    GrantFullControl: 'id="qcs::cam::uin/1001:uin/1001",id="qcs::cam::uin/1002:uin/1002"' // 1001はuin
}, function(err, data) {
    console.log(err || data);
});
```

ユーザーにBucketの読書権限を付与します：

```
cos.putBucketAcl({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    GrantFullControl: 'id="qcs::cam::uin/1001:uin/1001",id="qcs::cam::uin/1002:uin/1002"' // 1001はuin
}, function(err, data) {
    console.log(err || data);
});
```

AccessControlPolicyによりBucket権限を変更します：

```
cos.putBucketAcl({
    Bucket: 'test-1250000000',/* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicyにはownerが含まれることが必要
            "ID": 'qcs::cam::uin/459000000:uin/459000000' // 459000000 はBucket所属ユーザーのQQ番号
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/10002:uin/10002", // 10002はQQ番号
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名              | パラメータ説明                                                     | タイプ        | 必須項目 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region              | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| ACL                 | ObjectのACL属性を定義します。有効値：private、public-read、public-read-write。デフォルト値：private | String      | いいえ   |
| GrantRead           | 認証対象者に読取権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String      | いいえ   |
| GrantWrite          | 認証対象者に書込権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String      | いいえ   |
| GrantReadAcp        | 認証対象者にAclとPolicyの読取権限を付与します。フォーマット：id=" ",id=" "；<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String      | いいえ   |
| GrantWriteAcp       | 認証対象者にAclとPolicyの書込権限を付与します。フォーマット：id=" ",id=" "；<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String      | いいえ   |
| GrantFullControl    | 認証対象者に読書権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String      | いいえ   |
| AccessControlPolicy | クロスオリジンリソース共有構成を説明するすべての情報リスト                           | Object      | いいえ   |
| - Owner             | バケット所有者のオブジェクトを表します                                       | Object      | いいえ   |
| - - ID              | ユーザーIDの文字列を表します。フォーマット：qcs::cam::uin/1001:uin/1001、1001はuin | Object      | いいえ   |
| - Grants            | クロスオリジンリソース共有構成を説明するすべての情報リスト                           | Object      | いいえ   |
| - - Permission      | クロスオリジンリソース共有構成を説明するすべての情報リスト。オプション項目：READ、WRITE、READ_ACP、WRITE_ACP、FULL_CONTROL | String      | いいえ   |
| - - Grantee         | クロスオリジンリソース共有構成を説明するすべての情報リスト                           | ObjectArray | いいえ   |
| - - - ID            | ユーザーIDの文字列を表します。フォーマット：qcs::cam::uin/1001:uin/1001、1001はuin | String      | いいえ   |
| - - - DisplayName   | ユーザー名の文字列を表します。通常、IDと一致する文字列を入力します           | String      | いいえ   |

####コールバック関数の説明

```
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。リクエスト成功の場合、空白となります。[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Get Bucket CORS



Get Bucket CORS APIは、Bucket所有者によってBucketでクロスオリジンリソース共有が行われる情報構成を実現します。（CORSはW3C規格であり、「クロスオリジンリソース共有：Cross-origin Resource Sharing」という）。デフォルトでは、Bucket所有者がこのAPIを使用する権限があります。Bucket所有者が権限を他のユーザに付与することもできます。詳細については、[Get Bucket CORS API説明](https://cloud.tencent.com/document/product/436/8274)を参照してください。

#### 使用例

```
cos.getBucketCors({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 戻り例

```
{
    "CORSRules": [{
        "MaxAgeSeconds": "5",
        "AllowedOrigins": ["*"],
        "AllowedHeaders": ["*"],
        "AllowedMethods": ["GET", "POST", "PUT", "DELETE", "HEAD"],
        "ExposeHeaders": ["ETag", "Content-Length", "x-cos-acl", "x-cos-version-id", "x-cos-request-id", "x-cos-delete-marker", "x-cos-server-side-encryption"]
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名             | パラメータ説明                                                     | タイプ        |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err                | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。リクエスト成功の場合、空白となります。[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730) | Object      |
| data               | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - CORSRules        | クロスオリジンリソース共有構成を説明するすべての情報リスト                           | ObjectArray |
| - - AllowedMethods | 許可されるHTTP操作。列挙値：GET、PUT、HEAD、POST、DELETE       | StringArray |
| - - AllowedOrigins | 許可されたアクセスソース。ワイルドカード * をサポートします。フォーマット：プロトコル://ドメイン名[:ポート]例えば：`http://www.qq.com` | StringArray |
| - - AllowedHeaders | OPTIONSリクエストを送信するときにサーバーに対し、次のリクエストがどのようなカスタマイズしたHTTPリクエストヘッダーを使用できるかを通知します。ワイルドカード * をサポートします | StringArray |
| - - ExposeHeaders  | ブラウザがサーバーから受信されるカスタムヘッダー情報を設定します           | StringArray |
| - - MaxAgeSeconds  | OPTIONSクロスオリジン情報のキャッシュ秒数を設定します                                | String      |
| - - ID             | 構成規則のID                                                | String      |


### Put Bucket CORS

> ! 
> 1. フロントエンドでクロスオリジンアクセス構成を変更するには、このBucket自体がクロスオリジンをサポートする必要があります。コンソールでクロスオリジンアクセス構成を行います。詳細については、[開発環境](https://cloud.tencent.com/document/product/436/13318)を参照してください。
> 2. クロスオリジンアクセス構成を変更するときには、現在のOriginのクロスオリジンリクエストに影響しないよう気をつけてください。


Put Bucket CORS APIは、Bucketのクロスオリジンリソース共有権限の設定リクエストを行うために使用されます。XML形式の構成ファイルをインポートすることにより構成を行うことができます。ファイルの大きさ制限は64KBです。デフォルトでは、Bucketの所有者がこのAPIを使用する権限があります。Bucketの所有者が権限を他のユーザーに付与することもできます。詳細については、[Put Bucket CORS API説明](https://cloud.tencent.com/document/product/436/8279)を参照してください。

#### 使用例

```
cos.putBucketCors({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    CORSRules: [{
        "AllowedOrigin": ["*"],
        "AllowedMethod": ["GET", "POST", "PUT", "DELETE", "HEAD"],
        "AllowedHeader": ["*"],
        "ExposeHeader": ["ETag", "x-cos-acl", "x-cos-version-id", "x-cos-delete-marker", "x-cos-server-side-encryption"],
        "MaxAgeSeconds": "5"
    }]
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名           | パラメータ説明                                                     | タイプ        | 必須項目 |
| ---------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket           | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region           | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| CORSRules        | クロスオリジンリソース共有構成を説明するすべての情報リスト                           | ObjectArray | いいえ   |
| - ID             | 構成規則のID。選択入力                                        | String      | いいえ   |
| - AllowedMethods | 許可されるHTTP操作。列挙値：GET、PUT、HEAD、POST、DELETE       | StringArray | はい   |
| - AllowedOrigins | 許可されたアクセスソース。ワイルドカード * をサポートします。フォーマット：プロトコル://ドメイン名[:ポート]例えば：`http://www.qq.com` | StringArray | はい   |
| - AllowedHeaders | OPTIONSリクエストを送信するときにサーバーに対し、次のリクエストがどのようなカスタマイズしたHTTPリクエストヘッダーを使用できるかを通知します。ワイルドカード * をサポートします | StringArray | 否   |
| - ExposeHeaders  | ブラウザがサーバーから受信されるカスタムヘッダー情報を設定します           | StringArray | いいえ   |
| - MaxAgeSeconds  | OPTIONSリクエストが取得される結果の有効期間を設定します                            | String      | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。リクエスト成功の場合、空白となります。[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Delete Bucket CORS

> !
> 1. 現在のBucketのクロスオリジンアクセス構成情報を削除すると、すべてのリクエストのクロスオリジンに失敗します。よくご確認のうえ操作してください。
> 2. ブラウザ側でこの方法をおすすめしません。



Delete Bucket CORS APIのリクエストは、クロスオリジンアクセス構成情報の削除を実現します。詳細については、[Delete Bucket CORS API説明](https://cloud.tencent.com/document/product/436/8283)を参照してください。

#### 使用例

```
cos.deleteBucketCors({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket　 | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |


### Get Bucket Location

Get Bucket Location APIは、Bucketの所在地域の情報を取得するために使用されます。このGET操作は、locationサブリソースを用いてBucketの所在地域を返します。このAPIの操作権限を持つのはBucketの所有者のみです。詳細については、[Get Bucket Location API説明](https://cloud.tencent.com/document/product/436/8275)を参照してください。

#### 使用例

```
cos.getBucketLocation({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```
function(err, data) { ... }
```

| パラメータ名               | パラメータ説明                                                     | タイプ    |
| -------------------- | ------------------------------------------------------------ | ------ |
| err                  | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode         | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers            | リクエストによって返されたヘッダー情報                                           | Object |
| data                 | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode         | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers            | リクエストによって返されたヘッダー情報                                           | Object |
| - LocationConstraint | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String |

### Get Bucket Tagging

Get Bucket Tagging APIは、バケットのTaggingタグ情報の取得を実現します。詳細については、[Get Bucket Tagging API説明](https://cloud.tencent.com/document/product/436/8276)を参照してください。

#### 使用例

```
cos.getBucketTagging({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 戻り例

```
{
    "Tags": [
        {"Key": "k1", "Value": "v1"},
        {"Key": "k2", "Value": "v2"}
    ],
    "statusCode": 200,
    "headers": {}
}
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ        |
| ------------ | ------------------------------------------------------------ | ----------- |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object      |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object      |
| - Tags       | タグ情報                                                     | ObjectArray |
| - - Key      | タグ名                                                       | String      |
| - - Value    | タグ値                                                       | String      |

### Put Bucket Tagging

Put Bucket Tagging APIは、バケットのTaggingタグ情報の設定を実現します。詳細については、[Put Bucket Tagging API説明](https://cloud.tencent.com/document/product/436/8276)を参照してください。

#### 使用例

```
cos.putBucketTagging({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Tagging: {
        "Tags": [
            {"Key": "k1", "Value": "v1"},
            {"Key": "k2", "Value": "v2"}
        ]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名    | パラメータ説明                                                     | タイプ        | 必須項目 |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket    | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region    | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| Tagging   | タグ情報                                                     | Object      | はい   |
| - Tags    | タグ情報                                                     | ObjectArray | はい   |
| - - Key   | タグ名                                                       | String      | はい   |
| - - Value | タグ値                                                       | String      | はい   |

####コールバック関数の説明

```
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |



### Delete Bucket Tagging

Delete Bucket Tagging APIは、バケットのTaggingタグ情報の削除を実現します。詳細については、[Delete Bucket Tagging API説明](https://cloud.tencent.com/document/product/436/8276)を参照してください。

#### 使用例

```
cos.deleteBucketTagging({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Get Bucket Policy

Get Bucket Policy APIは、Bucket権限ポリシー規則の取得を実現します。詳細については、[Get Bucket Policy API説明](https://cloud.tencent.com/document/product/436/8276)を参照してください。

#### 使用例

```
cos.getBucketPolicy({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 戻り例

```
{
    "Policy": {
        "version": "2.0",
        "Statement": [{
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/10001:uin/10001"]
            },
            "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:test-1250000000/*"],
            "Sid": "costs-1539833197000000307620-46518-39"
        }]
    },
    "statusCode": 200,
    "headers": {}
}
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名          | パラメータ説明                                                     | タイプ        |
| --------------- | ------------------------------------------------------------ | ----------- |
| err             | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| data            | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - Policy        | 権限ポリシー。[アクセス管理ポリシー構文](https://cloud.tencent.com/document/product/436/12469#.E8.AE.BF.E9.97.AE.E7.AE.A1.E7.90.86.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95)を参照してください | Object      |
| - - version     | バージョン番号。固定 2.0                                             | ObjectArray |
| - - statement   | 権限ポリシーライフサイクルリスト                                             | ObjectArray |
| - - - effect    | 効果。列挙値：allow、deny                                    | String      |
| - - - principal | 身元情報                                                     | ObjectArray |
| - - - - qcs     | 身元情報識別文字列。フォーマット：qcs::cam::uin/10001:uin/10002。その中、10001はメインアカウント、10002はサブアカウント | String      |
| - - - action    | ポリシー有効に関するActionリスト。ワイルドカード * をサポートします                     | StringArray |
| - - - resource  | 関連するリソース識別文字列リスト。フォーマット：qcs::cos:&ltRegion>:uid/&ltAppId>:&ltShortBucketName>/\*、例えば：qcs::cos:ap-guangzhou:uid/1250000000:test/\*" | StringArray |
| - - - condition | 有効または無効のリソースリスト。文字列                               | ObjectArray |



### Put Bucket Policy

Put Bucket Policy APIは、Bucket権限ポリシー規則の設定を実現します。詳細については、[Put Bucket Policy API説明](https://cloud.tencent.com/document/product/436/8282)を参照してください。

#### 使用例

```
cos.putBucketPolicy({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Policy: {
        "version": "2.0",
        "Statement": [{
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/10001:uin/10001"]
            },
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:test-1250000000/*"],
        }]
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名        | パラメータ説明                                                     | タイプ        | 必須項目 |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket        | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region        | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| Policy        | 権限ポリシー。[アクセス管理ポリシー構文](https://cloud.tencent.com/document/product/436/12469#.E8.AE.BF.E9.97.AE.E7.AE.A1.E7.90.86.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95)を参照してください | Object      | はい   |
| - version     | バージョン番号。固定 2.0                                             | ObjectArray | はい   |
| - statement   | 権限ポリシーライフサイクルリスト                                             | ObjectArray | はい   |
| - - effect    | 効果。列挙値：allow、deny                                    | String      | はい   |
| - - principal | 身元情報                                                     | ObjectArray | はい   |
| - - - qcs     | 身元情報識別文字列。フォーマット：qcs::cam::uin/10001:uin/10002。その中、10001はメインアカウント、10002はサブアカウント | String      | 是   |
| - - action    | ポリシー有効に関するActionリスト。ワイルドカード * をサポートします                     | StringArray | はい   |
| - - resource  | 関連するリソース識別文字列リスト。フォーマット：qcs::cos:&ltRegion>:uid/&ltAppId>:&ltShortBucketName>/\*、例えば：qcs::cos:ap-guangzhou:uid/1250000000:test/\*" | StringArray | はい   |
| - - condition | 有効または無効のリソースリスト。文字列                               | ObjectArray | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |



### Delete Bucket Policy

Delete Bucket Policy APIは、バケットの権限ポリシーを削除することができます。詳細については、[Delete Bucket Policy API説明](https://cloud.tencent.com/document/product/436/8285)を参照してください。

#### 使用例

```
cos.deleteBucketPolicy({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |



### Get Bucket Lifecycle

Get Bucket Lifecycle APIは、バケットのライフサイクル規則を取得することができます。詳細については、[Get Bucket Lifecycle API説明](https://cloud.tencent.com/document/product/436/8278)を参照してください。

#### 使用例

```
cos.getBucketLifecycle({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 戻り例

```
{
    "Rules": [{
        "ID": "1",
        "Filter": "",
        "Status": "Enabled",
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }, {
        "ID": "2",
        "Filter": {
            "Prefix": "dir/"
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }, {
        "ID": "3",
        "Filter": "",
        "Status": "Enabled",
        "Expiration": {
            "Days": "180"
        }
    }, {
        "ID": "4",
        "Filter": "",
        "Status": "Enabled",
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名                             | パラメータ説明                                                     | タイプ        |
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err                                | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| - statusCode                       | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers                          | リクエストによって返されたヘッダー情報                                           | Object      |
| data                               | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - statusCode                       | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers                          | リクエストによって返されたヘッダー情報                                           | Object      |
| - Rules                            | リクエストによって返されたヘッダー情報                                           | ObjectArray |
| - - ID                             | 規則の唯一の識別ID                                            | String      |
| - - Status                         | 規則のオン状態。列挙値：Enabled、Disabled                    | String      |
| - - Filter                         | フィルタリング条件を指定します                                                 | String      |
| - - - Prefix                       | 規則とマッチングするObjectプレフィックス                                   | String      |
| - - Transition                     | Objectへのトランジションを表します                                           | Object      |
| - - - Days                         | 規則の有効日数。ファイルアップロード時間から計算します。正の整数とします             | Object      |
| - - - StorageClass                 | Objectを保存する対象保存タイプ。列挙値：STANDARD、STANDARD_IA、デフォルト値：STANDARD | Object      |
| - - Expiration                     | Objectへの削除を表します                                           | Object      |
| - - - Days                         | 規則の有効日数。ファイルアップロード時間から計算します。正の整数とします             | Object      |
| - - AbortIncompleteMultipartUpload | フラグメントの削除を表します                                                 | Object      |
| - - - Days                         | 規則の有効日数。ファイルアップロード時間から計算します。正の整数とします             | Object      |


### Put Bucket Lifecycle
[Put Bucket Lifecycle API](https://cloud.tencent.com/document/product/436/8280)は、バケットのライフサイクル規則を設定できます。

#### 使用例

例1：アップロード30日後、低周波数のストレージにトランジションします。

```
cos.putBucketLifecycle({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Rules: [{
        "ID": "1",
        "Status": "Enabled",
        "Filter": {},
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

例2：ディレクトリのプレフィックスを`dir/`に指定し、アップロード90日後、CASにトランジションします。

```
cos.putBucketLifecycle({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Rules: [{
        "ID": "2",
        "Filter": {
            "Prefix": "dir/",
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

例3：アップロード180日後、ファイルを削除します。

```
cos.putBucketLifecycle({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Rules: [{
        "ID": "3",
        "Status": "Enabled",
        "Filter": {},
        "Expiration": {
            "Days": "180"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

例4：アップロード30日後、フラグメントを削除します。

```
cos.putBucketLifecycle({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Rules: [{
        "ID": "4",
        "Status": "Enabled",
        "Filter": {},
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名                             | パラメータ説明                                                     | タイプ        | 必須項目 |
| ---------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                             | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region                             | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| LifecycleConfiguration             | ライフサイクル規則を指定します                                             | Object      | はい   |
| - Rules                            | リクエストによって返されたヘッダー情報                                           | ObjectArray | はい   |
| - - ID                             | 規則の唯一の識別ID                                            | String      | はい   |
| - - Status                         | 規則のオン状態。列挙値：Enabled、Disabled                    | String      | はい   |
| - - Filter                         | フィルタリング条件を指定します                                                 | String      | はい   |
| - - - Prefix                       | 規則とマッチングするObjectプレフィックス                                   | String      | いいえ   |
| - - Transition                     | Objectへのトランジションを表します                                           | Object      | いいえ   |
| - - - Days                         | 規則の有効日数。ファイルアップロード時間から計算します。正の整数とします             | Object      | 是   |
| - - - StorageClass                 | Objectを保存する対象保存タイプ。列挙値：STANDARD、STANDARD_IA、デフォルト値：STANDARD | Object      | いいえ   |
| - - Expiration                     | Objectへの削除を表します                                           | Object      | いいえ   |
| - - - Days                         | 規則の有効日数。ファイルアップロード時間から計算します。正の整数とします             | Object      | 是   |
| - - AbortIncompleteMultipartUpload | フラグメント削除を表します                                                 | Object      | いいえ   |
| - - - Days                         | 規則の有効日数。ファイルアップロード時間から計算します。正の整数とします             | Object      | 是   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |


### Delete Bucket Lifecycle

[Delete Bucket Lifecycle API](https://cloud.tencent.com/document/product/436/8284)は、バケットのライフサイクル規則を削除できます。

#### 使用例

```
cos.deleteBucketLifecycle({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Get Bucket Versioning

Get Bucket Versioning APIは、バケットのマルチバージョン構成を取得できます。

#### 使用例

```
cos.getBucketVersioning({
    Bucket: 'test-1250000000',  /* 必須 */
    Region: 'ap-guangzhou',     /* 必須 */
}, function (err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名                    | パラメータ説明                                                     | タイプ   |
| ------------------------- | ------------------------------------------------------------ | ------ |
| err                       | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode              | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers                 | リクエストによって返されたヘッダー情報                                           | Object |
| data                      | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode              | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers                 | リクエストによって返されたヘッダー情報                                           | Object |
| - VersioningConfiguration | バケットのマルチバージョン構成情報                                       | Object |
| - - Status                | マルチバージョンがオン状態であるかどうか。列挙値：空白、Enabled、Suspended         | String |

### Put Bucket Versioning

Put Bucket Versioning APIは、バケットのマルチバージョン構成をオンまたはオフにできます。

#### 使用例

```
cos.putBucketVersioning({
    Bucket: 'test-1250000000',  /* 必須 */
    Region: 'ap-guangzhou',     /* 必須 */
    VersioningConfiguration: {
        Status: "Enabled"
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名                  | パラメータ説明                                                     | タイプ   | 必須項目 |
| ----------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                  | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region                  | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| VersioningConfiguration | バケットのマルチバージョン構成情報を定義します                                   | Object | はい   |
| - Status                | マルチバージョンがオン状態であるかどうか。列挙値：Enabled、Suspended。Enabledはオン、Suspendedはオフ | String | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Get Bucket Replication

Get Bucket Replication APIは、バケットのクロスリージョンレプリケーション規則の取得を実現します。

#### 使用例

```
cos.getBucketReplication({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 戻り例

```
{
    "ReplicationConfiguration": {
        "Role": "qcs::cam::uin/459000000:uin/459000000",
        "Rules": {
            "ID": "1",
            "Status": "Enabled",
            "Prefix": "sync/",
            "Destination": {
                "Bucket": "qcs:id/0:cos:ap-chengdu:appid/1250000000:backup",
                "StorageClass": "Standard"
            }
        }
    },
    "statusCode": 200,
    "headers": {}
}
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名                     | パラメータ説明                                                     | タイプ        |
| -------------------------- | ------------------------------------------------------------ | ----------- |
| err                        | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| data                       | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - ReplicationConfiguration | クロスリージョンレプリケーション規則                                               | Object      |
| - - Role                   | レプリケーションプロセスのロール。フォーマット：qcs::cam::uin/10001:uin/10002、その中、10001はメインアカウント、10002はサブアカウント | Object      |
| - - Rules                  | レプリケーション詳細規則リスト                                             | ObjectArray |
| - - - ID                   | タスク識別ID                                                  | String      |
| - - - Status               | 規則状態。列挙値：Enabled、Disabled                          | String      |
| - - - Prefix               | レプリケーションするObjectプレフィックス                                         | String      |
| - - - Destination          | レプリケーションするObjectプレフィックス                                         | Object      |
| - - - - Bucket             | レプリケーション先バケット。フォーマット：qcs:id/0:cos:&lt;Region>:appid/&lt;AppId>:&lt;ShortBucketName>、例えば：qcs:id/0:cos:ap-guangzhou:appid/1250000000:backup | Object      |
| - - - - StorageClass       | レプリケーション後のストレージタイプ。列挙値：STANDARD、STANDARD_IA、デフォルト値：STANDARD | Object      |


### Put Bucket Replication

Put Bucket Replication APIは、バケットのクロスリージョンレプリケーション規則の設定を実現します。

#### 使用例

```
cos.putBucketReplication({
    Bucket: 'test-1250000000',  /* 必須 */
    Region: 'ap-guangzhou',     /* 必須 */
    ReplicationConfiguration: { /* 必須 */
        Role: "qcs::cam::uin/459000000:uin/459000000",
        Rules: [{
            ID: "1",
            Status: "Enabled",
            Prefix: "sync/",
            Destination: {
                Bucket: "qcs:id/0:cos:ap-chengdu:appid/1250000000:backup",
                StorageClass: "Standard",
            }
        }]
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名                   | パラメータ説明                                                     | タイプ        | 必須項目 |
| ------------------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                   | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region                   | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| ReplicationConfiguration | クロスリージョンレプリケーション規則を定義します                                           | Object      | はい   |
| - - Role                   | レプリケーションプロセスのロール。フォーマット：qcs::cam::uin/10001:uin/10002、その中、10001はメインアカウント、10002はサブアカウント | Object      | いいえ   |
| - Rules                  | レプリケーション詳細規則リスト                                             | ObjectArray | はい   |
| - - ID                   | タスク識別ID                                                  | String      | いいえ   |
| - - Status               | 規則状態。列挙値：Enabled、Disabled                          | String      | はい   |
| - - Prefix               | レプリケーションするObjectプレフィックス                                         | String      | いいえ   |
| - - Destination          | レプリケーションするObjectプレフィックス                                         | Object      | はい   |
| - - - Bucket             | レプリケーション先バケット。フォーマット：qcs:id/0:cos:&lt;Region>:appid/&lt;AppId>:&lt;ShortBucketName>、例えば：qcs:id/0:cos:ap-guangzhou:appid/1250000000:backup | Object      | はい   |
| - - - StorageClass       | レプリケーション後のストレージタイプ。列挙値：STANDARD、STANDARD_IA、デフォルト値：STANDARD | Object      | いいえ   |


####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Delete Bucket Replication

Delete Bucket Replication APIは、バケットのクロスリージョンレプリケーション規則を削除できます。

#### 使用例

```
cos.deleteBucketReplication({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |



## オブジェクト操作

### Head Object

Head Object APIリクエストは対応するオブジェクトのmeta情報データを取得することができます。HEADの権限はGETの権限と一致します。

#### 使用例

```
cos.headObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',               /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名          | パラメータ説明                                                     | タイプ   | 必須項目 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region          | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key             | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |
| IfModifiedSince | Objectが指定時間後に変更された場合、対応するObjectのmeta情報を返します。さもなければ304を返します | String | いいえ   |

####コールバック関数の説明

```
function(err, data) { ... }
```

| パラメータ名                | パラメータ説明                                                     | タイプ    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。リクエスト成功の場合、空白となります。[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730) | Object  |
| - statusCode          | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number  |
| - headers             | リクエストによって返されたヘッダー情報                                           | Object  |
| data                  | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object  |
| - statusCode          | リクエストによって返されたHTTPステータスコード。例えば、200、304など。指定時間後に変更されていない場合、304を返します | Number  |
| - headers             | リクエストによって返されたヘッダー情報                                           | Object  |
| - x-cos-object-type   | Objectがアップロードを追加できるかどうかを表します。列挙値：normal、appendable | String  |
| - x-cos-storage-class | Objectのストレージレベル。列挙値：STANDARD、STANDARD_IA             | String  |
| - x-cos-meta- *       | ユーザーがカスタマイズしたmeta                                            | String  |
| - NotModified         | Objectは指定時間後に変更されていないかどうか                              | Boolean |

### Get Object

Get Object APIのリクエストは、バケットで指定したファイルの内容を取得できます。取得したファイル内容は文字列です。

この操作は、リクエスト元が対象Objectの読取権限があるか、または対象ObjectがEveryoneに読取権限（パブリック読取）を付与する必要があります。

> !このAPIはファイルのダウンロードに適用しません。ファイルをダウンロードするには、cos.getObjectUrlよりurlを取得した後、自らダウンロードする必要があります。詳細については、上記のcos.getObjectUrl APIを参照してください。

#### 使用例

```
cos.getObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Rangeパラメータで取得するファイルの内容を指定します：
```
cos.getObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    Range: 'bytes=1-3',        /* 非必須 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### パラメータ説明

| パラメータ名                     | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                     | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region                     | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key                        | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |
| ResponseContentType        | 応答ヘッダーのContent-Typeパラメータを設定します                           | String | いいえ   |
| ResponseContentLanguage    | 応答ヘッダーのContent-Languageパラメータを設定します                       | String | いいえ   |
| ResponseExpires            | 応答ヘッダーのContent-Expiresパラメータを設定します                        | String | いいえ   |
| ResponseCacheControl       | 応答ヘッダーのCache-Controlパラメータを設定します                          | String | いいえ   |
| ResponseContentDisposition | 応答ヘッダーのContent-Dispositionパラメータを設定します                    | String | いいえ   |
| ResponseContentEncoding    | 応答ヘッダーのContent-Encodingパラメータを設定します                       | String | いいえ   |
| Range                      | RFC 2616で定義される指定ファイルのダウンロード範囲。単位はバイト（bytes）。例えば、Renge: 'bytes=1-3' | String | いいえ   |
| IfModifiedSince            | Objectが指定時間後に変更された場合、対応するObjectのmeta情報を返します。さもなければ304を返します | String | いいえ   |
| IfUnmodifiedSince          | ファイルの変更時間が指定時間より早いか、同じであれば、ファイル内容を返します。さもなければ、412 (precondition failed)を返します | String | いいえ   |
| IfMatch                    | ETagが指定した内容と一致した場合、ファイルを返します。さもなければ412（precondition failed）を返します | String | いいえ   |
| IfNoneMatch                | ETagが指定した内容と一致していない場合、ファイルを返します。さもなければ304（not modified）を返します | String | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名                | パラメータ説明                                                     | タイプ    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object  |
| - statusCode          | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number  |
| - headers             | リクエストによって返されたヘッダー情報                                           | Object  |
| data                  | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object  |
| - statusCode          | リクエストによって返されたHTTPステータスコード。例えば、200、304、403、404など               | Number  |
| - headers             | リクエストによって返されたヘッダー情報                                           | Object  |
| - x-cos-object-type   | Objectがアップロードを追加できるかどうかを表します。列挙値：normal、appendable | String  |
| - x-cos-storage-class | Objectのストレージレベル。列挙値：STANDARD、STANDARD_IA、<br>**注意：このヘッダーが返されなかった場合、ファイルストレージレベルがSTANDARD（標準ストレージ）であることを示します** | String  |
| - x-cos-meta- *       | ユーザーがカスタマイズしたメタデータ                                           | String  |
| - NotModified         | リクエストのときにIfModifiedSinceが含まれた場合、この属性を返します。ファイルが変更された場合、trueです。さもなければ、falseです | Boolean |
| - Body                | 返されたファイル内容。デフォルトはString型です                           | String  |

### Put Object

Put Object APIのリクエストは、ローカルのファイル（Object）を指定されるBucketにアップロードします。この操作は、リクエスト元のBucketのWRITE権限が必要です。

> !
> 1. Key（ファイル名）は`/`で終わることができません。さもなければ、フォルダとして扱われます。
> 2. 現在のアクセスポリシーエントリは1000件までとします。オブジェクトACLのコントロールが必要とされない場合、アップロードときに設定しないでください。デフォルトでは、Bucket権限が継承されます。
> 3. アップロード後、同じ`key`で署名済みリンクを作成できます。（ダウンロードの場合、methodを`GET`にします）。APIの詳細について下文を参照し、その他の端末に共有してダウンロードします。ただし、もしファイルはプライベート読取権限であれば、署名済みリンクが一定の有効期間があります。

#### 使用例

```
cos.putObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    StorageClass: 'STANDARD',
    Body: file, // アップロードするファイルのオブジェクト
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

アップロード文字列をファイル内容とします：
```
cos.putObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

アップロード文字列をファイル内容とします：
```
cos.putObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

ディレクトリを作成します：
```
cos.putObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: 'a/',              /* 必須 */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名                 | パラメータ説明                                                     | タイプ             | 必須項目 |
| ---------------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket                 | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String           | はい   |
| Region                 | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String           | はい   |
| Key                    | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String           | はい   |
| CacheControl           | RFC 2616で定義されたキャッシュポリシー。Objectメタデータとして保存されます           | String           | いいえ   |
| ContentDisposition     | RFC 2616で定義されたファイル名。Objectメタデータとして保存されます           | String           | いいえ   |
| ContentEncoding        | RFC 2616で定義されたエンコードフォーマット。Objectメタデータとして保存されます           | String           | いいえ   |
| ContentLength          | RFC 2616で定義されたHTTPリクエスト内容の長さ（バイト）                   | String           | いいえ   |
| ContentType            | RFC 2616で定義された内容タイプ（MIME）。Objectメタデータとして保存されます   | String           | いいえ   |
| Expect                 | Expect: 100-continueを使用するとき、サーバーからの確認を受信した後、リクエスト内容を送信します | String           | いいえ   |
| Expires                | RFC 2616で定義された期限切れ時間。Objectメタデータとして保存されます           | String           | いいえ   |
| ACL                 | ObjectのACL属性を定義します。有効値：private、public-read、public-read-write。デフォルト値：private | String           | いいえ   |
| GrantRead              | 認証対象者に読取権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String           | いいえ   |
| GrantWrite             | 認証対象者に書込権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String           | いいえ   |
| GrantFullControl       | 認証対象者に読書権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String           | いいえ   |
| StorageClass           | Objectのストレージレベルを設定します。列挙値：STANDARD、STANDARD_IA、デフォルト値：STANDARD | String           | いいえ   |
| x-cos-meta- *          | ユーザーによってカスタマイズされたヘッダー情報が許可されます。Objectメタデータとして返します。大きさは2Kまで | String           | いいえ   |
| Body                   | アップロードするファイルの内容。`文字列`、`Fileオブジェクト`または`Blobオブジェクト`にすることができます  | String\File\Blob | はい   |
| onProgress             | 進捗のコールバック関数。進捗コールバック応答オブジェクト（progressData）属性は以下のとおりです     | Function         | いいえ   |
| - progressData.loaded  | ダウンロードしたファイルの大きさ。単位はバイト（bytes）                | Number           | いいえ   |
| - progressData.total   | ファイル全体のサイズ。単位はバイト（Bytes）                        | Number           | いいえ   |
| - progressData.speed   | ファイルのダウンロード速度。単位はバイト/秒（Bytes/s）                   | Number           | いいえ   |
| - progressData.percent | ファイルのダウンロード比率。小数で表されます。例えば：ダウンロード50%は0.5       | Number           | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| - ETag       | ファイルのMD5アルゴリズムチェック値を返します。ETagの値を使用して、アップロード処理中にObjectが破損していないかどうかをチェックできます。<br>**注意：ここのETag値の文字列の前後にダブルコーテーションが付きます。例えば、`"09cba091df696af91549de27b8e7d0f6"`** | String |

### Delete Object

Delete Object APIリクエストは、COSのバケット内のファイル（オブジェクト）を削除することができます。この操作は、リクエスト者がバケットに対する書き込み権限を持っている必要があります。

#### 使用例

```
cos.deleteObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg'                            /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key    | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、204、403、404など。**削除成功、またはファイルが存在しない場合、204または200を返します。指定のBucketが見つからなかった場合、404を返します** | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Options Object

Options Object APIは、Objectクロスオリジンアクセス構成のプリフライトリクエストを実現します。クロスオリジンリクエストを送信する前にOPTIONSリクエストを送信し、その同時に特定のリクエスト元ドメイン、HTTPメソッド、HEADER情報などをCOSに伝送することにより、真のクロスオリジンリクエストを送信するかどうかを決定します。CORS構成が存在しない場合、リクエストによって403 Forbiddenを返します。
**Put Bucket CORS APIによってBucketのCORS対応を有効にします。**

#### 使用例

```
cos.optionsObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    Origin: 'https://www.qq.com',      /* 必須 */
    AccessControlRequestMethod: 'PUT', /* 必須 */
    AccessControlRequestHeaders: 'origin,accept,content-type' /* 非必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名                      | パラメータ説明                                                     | タイプ   | 必須項目 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region                      | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key                         | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |
| Origin                      | クロスオリジンアクセスをシミュレートするリクエスト元ドメイン名                                   | String | はい   |
| AccessControlRequestMethod  | クロスオリジンアクセスをシミュレートするHTTPリクエストメソッド                                 | String | はい   |
| AccessControlRequestHeaders | クロスオリジンアクセスをシミュレートするリクエストヘッダー                                       | String | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名                       | パラメータ説明                                                     | タイプ    |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err                          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object  |
| - statusCode                 | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number  |
| - headers                    | リクエストによって返されたヘッダー情報                                           | Object  |
| data                         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object  |
| - headers                    | リクエストによって返されたヘッダー情報                                           | Object  |
| - statusCode                 | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number  |
| - AccessControlAllowOrigin   | クロスオリジンアクセスをシミュレートするリクエスト元ドメイン名。カンマで区切ります。リクエスト元が許可されない場合、このHeaderは返されません。例えば：\* | String  |
| - AccessControlAllowMethods  | クロスオリジンアクセスをシミュレートするHTTPリクエストメソッド。カンマで区切ります。リクエストメソッドが許可されない場合、このHeaderは返されません。例えば：PUT、GET、POST、DELETE、HEAD | String  |
| - AccessControlAllowHeaders  | クロスオリジンアクセスをシミュレートするリクエストヘッダー。カンマで区切ります。リクエストヘッダーのシミュレートが許可されない場合、このHeaderがこのリクエストヘッダーを返しません。例えば：accept、content-type、origin、authorization | String  |
| - AccessControlExposeHeaders | クロスオリジンリクエストは戻りヘッダーをサポートし、カンマで区切ります。例えば：ETag                 | String  |
| - AccessControlMaxAge        | OPTIONSリクエストの結果を取得する有効期間を設定します。例えば：3600                | String  |
| - OptionsForbidden           | OPTIONSリクエストが無効になっているかどうか。返されたHTTPステータスコードが403であれば、trueです | Boolean |

### Get Object ACL

Get Object ACL APIは、特定のBucketのObjectアクセス権限を取得するために使用されます。Bucketの所有者のみが操作権限があります。

#### 使用例

```
cos.getObjectAcl({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket　 | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key    | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名            | パラメータ説明                                                     | タイプ        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| - statusCode      | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers         | リクエストによって返されたヘッダー情報                                           | Object      |
| data              | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - statusCode      | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers         | リクエストによって返されたヘッダー情報                                           | Object      |
| - ACL             | ObjectのACL属性。列挙値：private、public-read、public-read-write、default | Object      |
| - Owner           | リソースの所有者を識別します                                             | Object      |
| - - ID            | Object所有者のID。フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/lt;SubUin> <br>ルートアカウントの場合、&lt;OwnerUin>と&lt;SubUin>が同じ値です | String      |
| - - DisplayName   | Object所有者の名称                                          | String      |
| - Grants          | 認証対象者情報と権限情報リスト                                   | ObjectArray |
| - - Permission    | 認証対象者に付与する権限情報を指定します。列挙値：READ、WRITE、READ_ACP、WRITE_ACP、FULL_CONTROL | String      |
| - - Grantee       | 認証対象者の情報を説明します。typeタイプはRootAccount、Subaccountにすることができます。typeタイプがRootAccountの場合、IDはルートアカウントを表します。typeタイプがSubaccountの場合、IDはサブアカウントを表します | Object      |
| - - - DisplayName | ユーザー名                                                   | String      |
| - - - ID           | ユーザーのID。ルートアカウントの場合、フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin> <br>またはqcs::cam::anyone:anyone （すべてのユーザー）サブアカウントの場合、<br>フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> | String      |

### Put Object ACL

Put Object ACL APIは、特定のBucketのObjectに対しACLテーブル構成を行うために使用されます。

> !現在のアクセスポリシーエントリは1000に制限され、オブジェクトのACL制御を行う必要がない場合、設定しないでください。デフォルトではバケット権限を継承します。

#### 使用例

```
cos.putObjectAcl({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    ACL: 'public-read',        /* 非必須 */
}, function(err, data) {
    console.log(err || data);
});
```

ユーザーにファイル読書権限を付与します：
```
cos.putObjectAcl({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    GrantFullControl: 'id="qcs::cam::uin/1001:uin/1001",id="qcs::cam::uin/1002:uin/1002"' // 1001はuin
}, function(err, data) {
    console.log(err || data);
});
```

AccessControlPolicyによりBucket権限を変更します：
```
cos.putObjectAcl({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicyにはownerが含まれることが必要
            "ID": 'qcs::cam::uin/459000000:uin/459000000' // 459000000 はBucket所属ユーザーのQQ番号
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/10002:uin/10002", // 10002はQQ番号
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名              | パラメータ説明                                                     | タイプ        | 必須項目 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region              | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| Key                 | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String      | はい   |
| ACL                 | ObjectのACL属性を定義します。有効値：private、public-read、public-read-write、default；デフォルト値：private；defaultの場合、ファイル権限をクリアし、権限を継承権限に復元します | String      | いいえ   |
| GrantRead           | 認証対象者に読取権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String      | いいえ   |
| GrantWrite          | 認証対象者に書込権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String      | いいえ   |
| GrantFullControl    | 認証対象者に読書権限を付与します。<br>フォーマット：id=" ",id=" "。サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String      | いいえ   |
| AccessControlPolicy | ObjectのACL JSON定義フォーマット                                  | Object      |      |
| - Owner             | リソースの所有者を識別します                                             | Object      |      |
| - - ID              | Object所有者のID。フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/lt;SubUin> <br>ルートアカウントの場合、&lt;OwnerUin>と&lt;SubUin>が同じ値です | String      |      |
| - - DisplayName     | Object所有者の名称                                          | String      |      |
| - Grants            | 認証対象者情報と権限情報リスト                                   | ObjectArray |      |
| - - Permission      | 認証対象者に付与する権限情報を指定します。列挙値：READ、WRITE、READ_ACP、WRITE_ACP、FULL_CONTROL | String      |      |
| - - Grantee         | 認証対象者の情報を説明します。typeタイプはRootAccount、Subaccountにすることができます。typeタイプがRootAccountの場合、IDはルートアカウントを表します。typeタイプがSubaccountの場合、IDはサブアカウントを表します | Object      |      |
| - - - DisplayName   | ユーザー名                                                   | String      |      |
| - - - ID            | ユーザーのID。ルートアカウントの場合、フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin> <br>またはqcs::cam::anyone:anyone （すべてのユーザー）サブアカウントの場合、<br>フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> | String      |      |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、204、403、404など               | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### Delete Multiple Object

Delete Multiple Object APIリクエストは、指定されたバケット内のオブジェクトの一括削除を実現し、単回リクエストで最大1000個のオブジェクトの一括削除をサポートします。応答結果に対して、COSはVerboseとQuietという2つのモードを提供します：Verboseモードは各オブジェクトの削除結果を返します；Quietモードはエラーのオブジェクト情報のみを返します。

#### 使用例

複数ファイルの削除：

```
cos.deleteMultipleObject({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Objects: [
        {Key: '1.jpg'},
        {Key: '2.zip'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名      | パラメータ説明                                                     | タイプ        | 必須項目 |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket      | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region      | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| Quiet       | ブール値。この値はQuietモードを起動するかどうかを決定します。値はtrueである場合、Quietモードを起動します。falseである場合、Verboseモードを起動します。デフォルト値はfalseです | Boolean     | いいえ   |
| Objects     | 削除するファイルリスト                                             | ObjectArray | はい   |
| - Key       | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String      | はい   |
| - VersionId | 削除するObjectまたはDeleteMarkerバージョンID                      | String      |      |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名                    | パラメータ説明                                                     | タイプ        |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err                       | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| - statusCode              | リクエストによって返されたHTTPステータスコード。例えば、200、204、403、404など               | Number      |
| - headers                 | リクエストによって返されたヘッダー情報                                           | Object      |
| data                      | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - statusCode              | リクエストによって返されたHTTPステータスコード。例えば、200、204、403、404など               | Number      |
| - headers                 | リクエストによって返されたヘッダー情報                                           | Object      |
| - Deleted                 | 今回削除に成功したObject情報を説明します                               | ObjectArray |
| - - Key                   | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String      |
| - - VersionId             | パラメータにVersionIdが渡された場合、返されたときにVersionIdが含まれます。操作したObjectまたはDeleteMarkerのバージョンを示します | String      |
| - - DeleteMarker          | マルチバージョンが有効になり、パラメータにVersionIdが含まれていない場合、今回の削除は、ファイル内容をクリアせず、可視ファイルを削除したことを示すDeleteMarkerを新規追加します。列挙値：true、false | String      |
| - - DeleteMarkerVersionId | 返されたDeleteMarkerがtrueであれば、新規追加したDeleteMarkerのVersionIdを返します | String      |
| - Error                   | 今回削除に失敗したObject情報を説明します                               | ObjectArray |
| - - Key                   | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String      |
| - - Code                  | 削除失敗のエラーコード                                             | String      |
| - - Message               | 削除エラー情報                                                 | String      |

### Put Object Copy

Put Object Copy リクエストは、1つのファイルをソースパスから対象パスにコピーできます。ファイルの大きさは1MB～5GBをおすすめします。5GB以上のファイルについて、分割アップロードUpload - Copyを使用してください。コピー過程で、ファイル元属性とACLが変更されることができます。ユーザーがこのAPIを用いてファイルのコピー、ファイル属性の変更（ソースファイルと対象ファイルの属性が同じ）、ファイルの移動または名前変更（コピーしてから単独で削除APIを呼び出す）を実行できます。

#### 使用例

```
cos.putObjectCopy({
    Bucket: 'test-1250000000',                               /* 必須 */
    Region: 'ap-guangzhou',                                  /* 必須 */
    Key: '1.jpg',                                            /* 必須 */
    CopySource: 'test1-1250000000.cos.ap-guangzhou.myqcloud.com/2.jpg', /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名                      | パラメータ説明                                                     | タイプ   | 必須項目 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region                      | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key                         | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |
| CopySource                  | ソースファイルURLパス。versionidサブリソースを通して、履歴バージョンを指定します       | String | はい   |
| ACL                         | ObjectのACL属性を定義します。有効値：private、public-read、public-read-write。デフォルト値：private | String | いいえ   |
| GrantRead                   | 認証対象者に読取権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String | いいえ   |
| GrantWrite                  | 認証対象者に書込権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String | いいえ   |
| GrantFullControl           | 認証対象者に読書権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String | いいえ   |
| MetadataDirective           | メタデータをコピーするかどうか。列挙値：Copy、Replaced、デフォルト値はCopy。マークがCopyの場合、このままHeaderのユーザーメタデータ情報をコピーします。マークがReplacedの場合、Header情報を参照しメタデータを変更します。**対象パスとソースパスが一致する場合、つまりユーザーがメタデータを変更しようとしている時、Replacedである必要があります** | String | いいえ   |
| CopySourceIfModifiedSince   | Objectが指定時間後に変更された場合、操作を実行します。さもなければ412を返します。**CopySourceIfNoneMatchとともに使用できます。別の条件に合わせて使用すると競合を返します** | String | いいえ   |
| CopySourceIfUnmodifiedSince | Objectが指定時間後に変更されなかった場合、操作を実行します。さもなければ412を返します。**CopySourceIfMatchとともに使用できます。別の条件に合わせて使用すると競合を返します** | String | いいえ   |
| CopySourceIfMatch           | ObjectのEtagと設定値が一致する場合、操作を行います。さもなければ412を返します。**CopySourceIfUnmodifiedSinceとともに使用できます。別の条件に合わせて使用すると競合を返します** | String | いいえ   |
| CopySourceIfNoneMatch           | ObjectのEtagと設定値が一致しない場合、操作を行います。さもなければ412を返します。**CopySourceIfModifiedSinceとともに使用できます。別の条件に合わせて使用すると競合を返します** | String | いいえ   |
| StorageClass                | ストレージレベル。列挙値：ストレージレベル、列挙値：Standard, Standard_IA。デフォルト値：Standard | String | いいえ   |
| x-cos-meta- *               | その他のカスタマイズしたファイルヘッダー                                         | String | いいえ   |
| CacheControl                | すべてのキャッシュメカニズムがリクエスト/レスポンスチェーンで守らなければならない命令を指定します            | String | いいえ   |
| ContentDisposition          | MIMEプロトコルの拡張。MIMEプロトコルは、MIMEユーザーエージェントが追加のファイルをどう表示するかを指示します | String | いいえ   |
| ContentEncoding             | HTTPにて「テキストを伝送するエンコードフォーマット」を決定する1対のヘッダーフィールド | String | いいえ   |
| ContentType                 | RFC 2616で定義されたHTTPリクエスト内容のタイプ（MIME）。例えば、`text/plain` | String | いいえ   |
| Expect                      | リクエストを行う特定のサーバー行動                                       | String | いいえ   |
| Expires                     | 応答期限が切れる日付と時間                                         | String | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名         | パラメータ説明                                                     | タイプ   |
| -------------- | ------------------------------------------------------------ | ------ |
| err            | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode   | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers      | リクエストによって返されたヘッダー情報                                           | Object |
| data           | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode   | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers      | リクエストによって返されたヘッダー情報                                           | Object |
| - ETag         | ファイルのMD-5アルゴリズムチェック値。例えば、`"22ca88419e2ed4721c23807c678adbe4c08a7880"`、**注意：前後にダブルコーテーションが付きます** | String |
| - LastModified | Objectが最後に変更された時間。例えば、2017-06-23T12:33:27.000Z       | String |



## マルチパートアップロード操作

### Initiate Multipart Upload

Initiate Multipart Uploadリクエストは、シャードアップロードの初期化を実現します。このリクエストを実行した後にUpload IDを返します。今後のUpload Partリクエストに使用されます

#### 使用例

```
cos.multipartInit({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名             | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region              Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key                | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |
| CacheControl       | RFC 2616で定義されたキャッシュポリシー。Objectメタデータとして保存されます           | String | いいえ   |
| ContentDisposition | RFC 2616で定義されたファイル名。Objectメタデータとして保存されます          | String | いいえ   |
| ContentEncoding    | RFC 2616で定義されたエンコードフォーマット。Objectメタデータとして保存されます          | String | いいえ   |
| ContentType        | RFC 2616で定義された内容タイプ（MIME）。Objectメタデータとして保存されます  | String | いいえ   |
| Expires            | RFC 2616で定義された期限切れ時間。Objectメタデータとして保存されます           | String | いいえ   |
| ACL                 | ObjectのACL属性を定義します。有効値：private、public-read、public-read-write。デフォルト値：private | String | いいえ   |
| GrantRead           | 認証対象者に読取権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String | いいえ   |
| GrantWrite           | 認証対象者に書込権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String | いいえ   |
| GrantFullControl   | 認証対象者に読書権限を付与します。フォーマット：id=" ",id=" "。<br>サブアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"、<br>ルートアカウントに権限を付与する必要があれば、id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"、<br>例えば：'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"' | String | いいえ   |
| StorageClass       | Objectのストレージレベルを設定します。列挙値：STANDARD、STANDARD_IA、デフォルト値：STANDARD | String | いいえ   |
| x-cos-meta- *      | ユーザーによってカスタマイズされたヘッダー情報が許可されます。Objectメタデータとして返します。大きさは2Kまで | String | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名   | パラメータ説明                                                     | タイプ   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| data     | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| Bucket   | シャードアップロードする対象Bucket                                        | String |
| Key      | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String |
| UploadId | 今後アップロードときに使用するID                                        | String |

### Upload Part

Upload Part APIリクエストは、初期化後のマルチパートアップロードを実現します。サポートされているパート数は1～10000で、パートサイズは1MB～5GBです。
Initiate Multipart Upload APIを使ってシャードアップロードを初期化するときにuploadIdが取得されます。このIDは、このパートデータを一意に識別するだけでなく、このパートデータはファイル全体における相対位置も識別します。Upload Partのリクエストを行うたび、partNumberとuploadIdを渡す必要があります。partNumberはパート番号で、アウトオブオーダーアップロードをサポートします。
渡されたuploadIdとpartNumberが同じ場合、後で渡されるパートは前に渡されたパートを上書きします。uploadIdが存在しない場合は、404エラーNoSuchUploadを返します。

#### 使用例

```
cos.multipartUpload({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',       /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名        | パラメータ説明                                                     | タイプ             | 必須項目 |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket        | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String           | はい   |
| Region        | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String           | はい   |
| Key             | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String           | はい   |
| ContentLength | RFC 2616で定義されたHTTPリクエスト内容の長さ（バイト）                  | String           | はい   |
| PartNumber    | パート番号                                                   | String           | はい   |
| UploadId      | アップロードタスク番号                                                 | String           | はい   |
| Body          | アップロードするファイルパートの内容。`文字列`、`Fileオブジェクト`または`Blobオブジェクト`にすることができます | String\File\Blob | はい   |
| Expect        | `Expect: 100-continue`を使用するとき、サーバーからの確認を受信した後、リクエスト内容を送信します | String           | いいえ   |
| ContentMD5    | RFC 1864で定義された、Base64エンコードされた128-bit内容MD5チェック値。このヘッダーは、ファイルの内容が変化されたかどうかをチェックするために使用されます | String           | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| - ETag       | ファイルのMD-5アルゴリズムチェック値。例えば、`"22ca88419e2ed4721c23807c678adbe4c08a7880"`、**注意：前後にダブルコーテーションが付きます** | String |

### Complete Multipart Upload

Complete Multipart Upload APIリクエストは、全体のマルチパートアップロードを完了するために使用されます。Upload Partsを使用してすべてのパートをアップロードした後、ファイル全体のマルチパートアップロードを完了するためにAPIを呼び出す必要があります。このAPIを使用するとき、パートの正確さを検証するために、リクエストボディの各パートにPartNumberとETagを指定する必要があります。
マルチパートアップロード後にマージする必要があり、マージに数分かかるため、パートのマージが開始されると、COSはすぐにステータスコード200を返します。マージ中、COSは定期的にスペース情報を返して接続を保持します。マージが完了してから、COSがボディのなかでマージされたパートの内容を返します。

- アップロードパートが1MB未満の場合、APIが呼び出されると、400 EntityTooSmallが返されます。
- アップロードパート番号が連続していない場合、該当APIが呼び出されると400 InvalidPartが返されます。
- リクエストBodyのパート情報が番号の昇順に並んでいない場合、APIが呼び出されたときに400 InvalidPartOrderが返されます。
- UploadIdが存在しない場合は、APIが呼び出されたときに404 NoSuchUploadが返されます。

#### 使用例

```
cos.multipartComplete({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.zip',              /* 必須 */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f472941c0fb8c6b7f3528a2', /* 必須 */
    Parts: [
        {PartNumber: '1', ETag: '"0cce40bdbaf2fa0ff204c20fc965dd3f"'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名       | パラメータ説明                                                     | タイプ       | 必須項目 |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket       | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String      | はい   |
| Region       | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String      | はい   |
| Key          | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String      | はい   |
| UploadId     | アップロードタスク番号                                                 | String      | はい   |
| Parts        | 今回のマルチパートアップロードするパートの情報リストを説明します                           | ObjectArray | はい   |
| - PartNumber | パート番号                                                   | String      | はい   |
| - ETag       | 各パートファイルのMD5アルゴリズムチェック値。例えば、`"22ca88419e2ed4721c23807c678adbe4c08a7880"`、**注意：前後にダブルコーテーションが付きます** | String      | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| - Location   | 作成したObjectのインターネットアクセスドメイン名                                 | String |
| - Bucket     | マルチパートアップロードする対象Bucket                                        | String |
| - Key        | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String |
| - ETag       | マージ後のファイルのMD5アルゴリズムチェック値。例えば、`"22ca88419e2ed4721c23807c678adbe4c08a7880"`、**注意：前後にダブルコーテーションが付きます** | String |

### List Parts

List Partsは、特定のマルチパートアップロードでアップロードされたパートを照合するために使用されます。つまり、指定されたUploadIdが属するすべてのアップロードに成功したパートをリストするために使用されます。

#### 使用例

```
cos.multipartListPart({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.jpg',              /* 必須 */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f47294ec0fb8c6b7f3528a2',                      /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名           | パラメータ説明                                                     | タイプ   | 必須項目 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region           | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key              | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |
| UploadId         | 今回のマルチパートアップロードIDを識別します。Initiate Multipart Upload APIを使ってシャードアップロードを初期化するとき、uploadIdが取得されます。このIDは、このパートデータを一意に識別するだけでなく、ファイル全体におけるこのパートデータの相対位置も識別します。 | String | はい   |
| EncodingType     | 戻り値のエンコード方法を決めます                                         | String | いいえ   |
| MaxParts         | 単回返される最大エントリー数。デフォルトは1000                            | String | いいえ   |
| PartNumberMarker | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されたエントリーはmarkerから開始します  | String | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名                 | パラメータ説明                                                     | タイプ        |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err                    | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| - statusCode           | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers              | リクエストによって返されたヘッダー情報                                           | Object      |
| data                   | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - statusCode           | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers              | リクエストによって返されたヘッダー情報                                           | Object      |
| - Bucket               | マルチパートアップロードする対象Bucket                                        | String      |
| - Encoding-type        | 戻り値のエンコード方法を決めます                                         | String      |
| - Key                  | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String      |
| - UploadId             | 今回のマルチパートアップロードIDを識別します                                        | String      |
| - Initiator            | 今回のアップロード送信者の情報を示すために使用されます                                 | Object      |
| - - DisplayName        | アップロード送信者の名称                                             | String      |
| - - ID                 | アップロード送信者ID。フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> <br>ルートアカウントの場合、&lt;OwnerUin>と&lt;SubUin>が同じ値です | String      |
| - Owner                | これらのパート所有者の情報を示すために使用されます                                 | Object      |
| - - DisplayName        | Bucket所有者の名称                                          | String      |
| - - ID                 | Bucket所有者ID。通常はユーザーのUINです                           | String      |
| - StorageClass         | これらのパートのストレージレベルを示すために使用されます。列挙値：Standard、Standard_IA    | String      |
| - PartNumberMarker     | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されるエントリーはmarkerから開始します  | String      |
| - NextPartNumberMarker | 返されたエントリーが切り捨てられた場合、返されたNextMarkerを次のエントリー開始点とします   | String      |
| - MaxParts             | 単回返される最大エントリー数                                       | String      |
| - IsTruncated          | 返されるエントリーが切り捨てられたかどうか。'true'または'false'                      | String      |
| - Part                 | パート情報リスト                                                 | ObjectArray |
| - - PartNumber         | パート番号                                                     | String      |
| - - LastModified       | パートの最終変更時間                                               | String      |
| - - ETag               | パートのMD5アルゴリズムチェック値                                          | String      |
| - - Size               | パートサイズ。単位はByteです                                            | String      |

### Abort Multipart Upload

Abort Multipart Uploadは、1つのマルチパートアップロードを破棄し、アップロードされたパートを削除するために使用されます。このAbort Multipart Uploadを呼び出すとき、このUpload Partsを使用しているリクエストがあると、Upload Partsは失敗を返します。このUploadIdが存在していなければ、404 NoSuchUploadを返します。

**アップロードされたが終了していないパートはストレージスペースを占有し、ストレージコストを発生させるため、タイムリーにマルチパートアップロードを完了するか、またはマルチパートアップロードを破棄することをお勧めします。**

#### 使用例

```
cos.multipartAbort({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.zip',                           /* 必須 */
    UploadId: '1521389146c60e7e198202e4e6670c5c78ea5d1c60ad62f1862f47294ec0fb8c6b7f3528a2'                       /* 必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名   | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket   | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region   | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key      | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String | はい   |
| UploadId | 今回のマルチパートアップロードIDを識別します。Initiate Multipart Upload APIを使ってシャードアップロードを初期化するとき、uploadIdが取得されます。このIDは、このパートデータを一意に識別するだけでなく、ファイル全体におけるこのパートデータの相対位置も識別します | String | はい   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |

### List Multipart Uploads

List Multiparts Uploadsは、実行中のマルチパートアップロードを照合するために使用されます。単回リクエスト操作で、最大1000個の実行中のマルチパートアップロードがリストされます。

#### 使用例

プレフィックスが1.zipの未完了UploadIdリストを取得します

```
cos.multipartList({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Prefix: '1.zip',                        /* 非必須 */
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名       | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region       | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Delimiter    | 区切りは記号の1つです。Object名に含まれた指定のプレフィックスと最初出現したdelimiterの間にあるObjectを同じ要素セットとします：common prefix。prefixがなければ、パスの先頭から始めます | String | いいえ   |
| EncodingType | 戻り値のエンコードフォーマットを決めます。正しい値：url                            | String | いいえ   |
| Prefix       | 返したObject keyはPrefixの値をプレフィックスとする必要があります。prefixを使って照合する場合、返したkeyにはまだPrefixが含まれることをご注意ください | String | いいえ   |
| MaxUploads   | 返したmultipartの最大数量を設定します。正しい値は1～1000です。デフォルトは1000です   | String | いいえ   |
| KeyMarker    | upload-id-markerと一緒に使用します。<br> <li> upload-id-markerが指定されていない場合は、<br>ObjectNameがkey-markerの後ろ（アルファベット順）にあるエントリーがリストされます。<br><li>upload-id-markerが指定されている場合、<br>ObjectNameがkey-markerの後ろ（アルファベット順）にあるエントリーがリストされます。<br>ObjectNameがアルファベット順でkey-markerと同じ、同時にUploadIDがupload-id-markerの後ろ（アルファベット順）にあるエントリーがリストされます。 | String | いいえ   |
| UploadIdMarker | key-markerと一緒に使用します。<br><li>key-markerが指定されていない場合、<br>upload-id-markerが無視されます。<br><li>key-markerが指定された場合、<br>ObjectNameがkey-markerの後ろ（アルファベット順）にあるエントリがリストされます。<br>ObjectNameがアルファベット順でkey-markerと同じ、同時にUploadIDがupload-id-markerの後ろ（アルファベット順）にあるエントリがリストされます。 | String | いいえ |</li>


####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名               | パラメータ説明                                                     | タイプ        |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err                  | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object      |
| - statusCode         | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers            | リクエストによって返されたヘッダー情報                                           | Object      |
| data                 | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object      |
| - statusCode         | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number      |
| - headers            | リクエストによって返されたヘッダー情報                                           | Object      |
| - Bucket             | マルチパートアップロードする対象Bucket                                        | String      |
| - Encoding-Type      | 戻り値のエンコードフォーマットを指定します。正しい値：url                            | String      |
| - KeyMarker          | キー値から始まるエントリーをリストします                                      | String      |
| - UploadIdMarker     | 該当UploadId値から始まるエントリーをリストします                                 | String      |
| - NextKeyMarker      | 返されたエントリーが切り捨てられた場合、返されたNextKeyMarkerを次のエントリー開始点とします | String      |
| - NextUploadIdMarker | 返されたエントリーが切り捨てられた場合、返されたUploadIdを次のエントリー開始点とします     | String      |
| - MaxUploads         | 返したmultipartの最大数量を設定します。正しい値は1～1000です          | String      |
| - IsTruncated        | 返されるエントリーが切り捨てられたかどうか。'true'または'false'                      | String      |
| - Delimiter          | 区切りは記号の1つです。object名に含まれた指定のプレフィックスと最初出現したdelimiterの間にあるobjectを同じ要素セットとします：common prefix。prefixがなければ、パスの先頭から始めます | String      |
| - Prefix             | 返したObject keyはPrefixの値をプレフィックスとする必要があります。prefixを使って照合する場合、返したkeyにはまだPrefixが含まれることをご注意ください | String      |
| - CommonPrefixs      | prefixとdelimiterの間の同じパスが1つのタイプに分類され、Common Prefixと定義します | ObjectArray |
| - - Prefix           | 具体的なCommonPrefixsを表示します                                     | String      |
| - Upload             | Uploadの情報集合                                            | ObjectArray |
| - - Key              | Object名                                                | String      |
| - - UploadId         | 今回のマルチパートアップロードIDを示します                                        | String      |
| - StorageClass       | パートのストレージレベルを示すために使用されます。列挙値：STANDARD、STANDARD_IA        | String      |
| - Initiator          | 今回のアップロード送信者の情報を示すために使用されます                                 | Object      |
| - - DisplayName      | アップロード送信者の名称                                             | String      |
| - - ID               | アップロード送信者ID。フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> ルートアカウントの場合、&lt;OwnerUin>と&lt;SubUin>が同じ値です | String      |
| - Owner              | これらのパート所有者の情報を示すために使用されます                                 | Object      |
| - - DisplayName      | Bucket所有者の名称                                          | String      |
| - - ID               | Bucket所有者ID。フォーマット：qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> ルートアカウントの場合、&lt;OwnerUin>と&lt;SubUin> は同じ値です | String      |
| - Initiated          | マルチパートアップロードの開始時間                                           | String      |



## マルチパートアップロード / レプリケーションタスク操作

このメソッドは上記ネイティブメソッドをカプセル化したものです。マルチパートアップロード / レプリケーションの全プロセスを実現します。同時マルチパートアップロード / レプリケーション、一時停止/再開、アップロードタスクの取消、一時停止、再開などをサポートします。

### Slice Upload File

Slice Upload Fileは、ファイルのマルチパートアップロードを実現するために使用されます。

#### 使用例

```
cos.sliceUploadFile({
    Bucket: 'test-1250000000', /* 必須 */
    Region: 'ap-guangzhou',    /* 必須 */
    Key: '1.zip',              /* 必須 */
    Body: file,                /* 必須 */
    TaskReady: function(taskId) {                   /* 非必須 */
        console.log(taskId);
    },
    onHashProgress: function (progressData) {       /* 非必須 */
        console.log(JSON.stringify(progressData));
    },
    onProgress: function (progressData) {           /* 非必須 */
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### パラメータ説明

| パラメータ名                 | パラメータ説明                                                     | タイプ      | 必須項目 |
| ---------------------- | ------------------------------------------------------------ | --------- | ---- |
| Bucket                 | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String    | はい   |
| Region                 | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String    | はい   |
| Key                    | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String    | はい   |
| Body                   | アップロードするファイルの内容。FileオブジェクトまたはBlobオブジェクトにすることができます           | File\Blob | はい   |
| SliceSize              | パートサイズ                                                     | String    | いいえ   |
| AsyncLimit             | パートの同時接続量                                                 | String    | いいえ   |
| StorageClass           | Objectのストレージレベル。列挙値：STANDARD、STANDARD_IA             | String    | いいえ   |
| TaskReady              | アップロードタスク作成ときのコールバック関数。taskIdを返します。アップロードタスクの唯一の識別子です。アップロードタスクの取消（cancelTask）、一時停止（pauseTask）と再開（restartTask）に使用されます | Function  | いいえ   |
| - taskId               | アップロードタスクの番号                                               | String    | いいえ   |
| onHashProgress         | ファイルMD5値を計算する進捗コールバック関数。コールバックパラメータは進捗オブジェクトprogressDataです | Function  | いいえ   |
| - progressData.loaded  | チェックされたファイル分のサイズ。単位はバイト（bytes）です                | Number    | いいえ   |
| - progressData.total   | ファイル全体のサイズ。単位はバイト（Bytes）                        | Number    | いいえ   |
| - progressData.speed   | ファイルのチェック速度。単位はバイト/秒（bytes/s）                   | Number    | いいえ   |
| - progressData.percent | ファイルのチェック比率。小数で表されます。例えば：ダウンロード50%は0.5    | Number    | いいえ   |
| onProgress             | アップロードファイルの進捗コールバック関数。コールバックパラメータは進捗オブジェクトprogressDataです      | Function  | いいえ   |
| - progressData.loaded  | アップロードしたファイル分のサイズ。単位はバイト（bytes）                | Number    | いいえ   |
| - progressData.total   | ファイル全体のサイズ。単位はバイト（Bytes）                        | Number    | いいえ   |
| - progressData.speed   | ファイルのアップロード速度。単位はバイト/秒（bytes/s）                   | Number    | いいえ   |
| - progressData.percent | ファイルのアップロード比率。小数で表されます。例えば：ダウンロード50%は0.5    | Number    | いいえ   |


####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| - Location   | 作成したObjectのインターネットアクセスドメイン名                                 | String |
| - Bucket     | マルチパートアップロードする対象Bucket                                        | String |
| - Key        | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String |
| - ETag       | マージ後のファイルのMD5アルゴリズムチェック値。例えば、`"22ca88419e2ed4721c23807c678adbe4c08a7880"`、**注意：前後にダブルコーテーションが付きます** | String |

### Cancel Task

taskIdによりマルチパートアップロードタスクを取消します。

#### 使用例

```
var taskId = 'xxxxx';                   /* 必須 */
cos.cancelTask(taskId);
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ファイルアップロードタスクの番号。sliceUploadFileメソッドを呼び出すとき、そのTaskReadyコールバックによってこのアップロードタスクのtaskIdを返します | String | はい   |

### Pause Task

taskIdによりマルチパートアップロードタスクを一時停止します。

#### 使用例

```
var taskId = 'xxxxx';                   /* 必須 */
cos.pauseTask(taskId);
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ファイルアップロードタスクの番号。sliceUploadFileメソッドを呼び出すとき、そのTaskReadyコールバックによってこのアップロードタスクのtaskIdを返します | String | はい   |

### Restart Task

taskIdによりアップロードタスクを再開します。ユーザーの手動による停止（ pauseTaskの呼び出しによる停止）、またはアップロードエラーによる停止のアップロードタスクに使用されます。

#### 使用例

```
var taskId = 'xxxxx';                   /* 必須 */
cos.restartTask(taskId);
```

#### パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | ファイルアップロードタスクの番号。sliceUploadFileメソッドを呼び出すとき、そのTaskReadyコールバックによってこのアップロードタスクのtaskIdを返します | String | はい   |

### Slice Copy File

Slice Copy Fileは、パートレプリケーションにより1つのファイルをソースパスから対象パスにレプリケーションします。コピー過程で、ファイル元属性とACLが変更されることができます。ユーザーは、このAPIでファイル移動、ファイル名変更、ファイル属性の変更とコピー作成を実現します。

#### 操作方法プロトタイプ

Slice Copy Fileを呼び出して操作します：

```
cos.sliceCopyFile({
    Bucket: 'test-1250000000',                               /* 必須 */
    Region: 'ap-guangzhou',                                  /* 必須 */
    Key: '1.zip',                                            /* 必須 */
    CopySource: 'test1.cos.ap-guangzhou.myqcloud.com/2.zip', /* 必須 */
    onProgress:function (progressData) {                     /* 非必須 */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### 操作パラメータ説明

| パラメータ名                 | パラメータ説明                                                     | タイプ     | 必須項目 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String   | はい   |
| Region                 | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String   | はい   |
| Key                    | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String   | はい   |
| CopySource                  | ソースファイルURLパス。versionidサブリソースを通して、履歴バージョンを指定します       | String   | はい   |
| ChunkSize              | シャードレプリケーションの場合の各シャードのサイズ。デフォルト値は1048576 (1MB)           | Number   | いいえ   |
| SliceSize              | シャードレプリケーションを行うファイルの大きさ。デフォルト値は5G                            | Number   | いいえ   |
| onProgress             | アップロードファイルの進捗コールバック関数。コールバックパラメータは進捗オブジェクトprogressDataです      | Function | いいえ   |
| - progressData.loaded  | アップロードしたファイル分のサイズ。単位はバイト（bytes）                | Number   | いいえ   |
| - progressData.total   | ファイル全体のサイズ。単位はバイト（Bytes）                        | Number   | いいえ   |
| - progressData.speed   | ファイルのアップロード速度。単位はバイト/秒（bytes/s）                   | Number   | いいえ   |
| - progressData.percent | ファイルのアップロード比率。小数で表されます。例えば：ダウンロード50%は0.5    | Number   | いいえ   |

####コールバック関数の説明

```shell
function(err, data) { ... }
```

| パラメータ名       | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | リクエストエラーのときに返されるオブジェクトです。ネットワークエラーと業務エラーを含みます。処理対策については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の場合は空白となります | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| data         | リクエスト成功の場合で返されたオブジェクトです。リクエストエラーの場合、空白となります               | Object |
| - statusCode | リクエストによって返されたHTTPステータスコード。例えば、200、403、404など                    | Number |
| - headers    | リクエストによって返されたヘッダー情報                                           | Object |
| - Location   | 作成したObjectのインターネットアクセスドメイン名                                 | String |
| - Bucket     | マルチパートアップロードする対象Bucket                                        | String |
| - Key        | オブジェクトのキー（Object名）。バケットでのオブジェクトの唯一の識別子です。[オブジェクトのキーの説明](https://cloud.tencent.com/document/product/436/13324) | String |
| - ETag       | マージ後のファイルのMD5アルゴリズムチェック値。例えば、"22ca88419e2ed4721c23807c678adbe4c08a7880"、注意：前後にダブルコーテーションが付きます | String |

