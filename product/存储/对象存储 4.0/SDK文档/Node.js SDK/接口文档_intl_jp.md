>?文章に記載されているSecretId、SecretKey、Bucketなどの名前の意味および取得方式については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

Node.js SDK githubアドレス：[tencentyun/cos-nodejs-sdk-v5](https://github.com/tencentyun/cos-nodejs-sdk-v5)

## Service操作

### Get Service

##### 機能説明

Get Service APIは、このユーザーにおけるすべてのバケットリストを取得することを実現します。このAPIはAuthorization署名認証を使用する必要があり、かつ署名におけるAccessIDが属するアカウントのバケットリストのみを取得できます。

#### 操作方法プロトタイプ

Get Serviceの呼び出し操作：

```js
cos.getService(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

- **特別なパラメータはありません** 

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| err        | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data       | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Owner      | バケット所有者の情報                                     | Object |
| uin        | バケット所有者のUIN                                          | String |
| Buckets    | 今回返されたバケットリストのすべての情報を説明します                         | Array  |
| Name       | バケットの名称                                                  | String |
| CreateDate | バケット作成時間。ISO8601フォーマット                                | String |



## ツール方法

### 事前署名リンクの取得

#### 使用例

例1：署名付きではないObject Urlを取得します。

```js
var url = cos.getObjectUrl({
    Key: '1.jpg',
    Sign: false
});
```

例2：署名付きObject Urlを取得します。

```js
var url = cos.getObjectUrl({
    Key: '1.jpg'
});
```

例3：署名プロセスは非同期取得です。callbackで署名付きUrlを取得する必要があります。

```js
cos.getObjectUrl({
    Key: '1.jpg',
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

例4：署名済みPut ObjectのアップロードUrlを取得します。

```js
cos.getObjectUrl({
    Method: 'PUT',
    Key: '1.jpg',
    Sign: true
}, function (err, data) {
    console.log(err || data.Url);
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

1. 署名計算が同期的に計算できる場合（例え：インスタンス化の際にSecretIdとSecretKeyをインバウンドします）、デフォルトでは、署名付きのurlを返します
2. そうでない場合、署名なしのurlを返します

####コールバック関数の説明

```js
function(err, data) { ... }
```

| パラメータ名 | パラメータ説明                                                     | タイプ   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data   | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| - Url  | 算出されたUrl                                               | String |



## Bucket操作

### Head Bucket

##### 機能説明

Head Bucketリクエストはこのバケットが存在するかどうか、アクセス権限を持っているかどうかを確認することができ、Headの権限はReadと一致しています。

#### 操作方法プロトタイプ

Head Bucketの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE'		/* 必須 */
};

cos.headBucket(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名      | パラメータ説明                                                     | タイプ    |
| ----------- | ------------------------------------------------------------ | ------- |
| err         | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data        | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| BucketExist | バケットが存在しているかどうか                                              | Boolean |
| BucketAuth  | このバケットの権限を持っているかどうか                                     | Boolean |

### Get Bucket

##### 機能説明 

Get BucketリクエストはList Objectリクエストに等しく、当該Bucekt下の一部あるいははすべてのObjectをリストすることができます。当該リクエストを出すには、Read権限が必要です。

#### 操作方法プロトタイプ

Get Bucketの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE',	/* 必須 */
	Prefix : 'STRING_VALUE',	/* 非必須 */
	Delimiter : 'STRING_VALUE', /* 非必須 */
	Marker : 'STRING_VALUE',	/* 非必須 */
	MaxKeys : 'STRING_VALUE',	/* 非必須 */
	EncodingType : 'STRING_VALUE',	/* 非必須 */
};

cos.getBucket(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名       | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region       | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Prefix       | プレフィックスマッチング、返されたオブジェクト鍵のプレフィックスアドレスを規定するために使用されます                       | String | いいえ   |
| Delimiter    | 区切り文字は記号であり、プレフィックスがある場合、プレフィックスからデリミターまでの間にある同じパスが1つのタイプに分類され、Common Prefixとして定義し、その後、すべてのCommon Prefixをリストアウトされます。プレフィックスがない場合、パスの先頭から開始します | String | 否   |
| Marker       | デフォルトでは、エントリがUTF-8二進法の順でリストされ、すべてのリストされたエントリはmarkerから始まります    | String | いいえ   |
| MaxKeys      | 一度に返されたエントリの最大数。デフォルトでは1000です                            | String | いいえ   |
| EncodingType | 戻り値のエンコーディング方式を規定します                                         | String | いいえ   |



####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名         | パラメータ説明                                                     | タイプ     |
| -------------- | ------------------------------------------------------------ | -------- |
| err            | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object   |
| data           | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object   |
| CommonPrefixes | プレフィックスからデリミターの間にある同じパスが1つのタイプに分類され、Common Prefixとして定義されます | Array    |
| Prefix         | プレフィックスマッチング、返されたオブジェクト鍵のプレフィックスアドレスを規定するために使用されます                       | String   |
| Name           | バケットの名称                                                  | String   |
| Prefix         | オブジェクト鍵のプレフィックス                                                 | String   |
| Marker         | デフォルトでは、エントリがUTF-8二進法の順でリストされ、すべてのリストされたエントリはmarkerから始まります    | String |
| MaxKeys        | 一度に返されたエントリの最大数                                       | String   |
| IsTruncated    | 返されたエントリが遮断されたかどうか、'true'または'false'                     | String   |
| NextMarker     | 仮に返されたエントリが遮断された場合、返されたNextMarkerは次のエントリの起点です   | String   |
| Encoding-Type  | エンコーディングタイプは、Delimiter、Marker、Prefix、NextMarker、Keyに適用されます   | String   |
| Contents       | メタデータ情報                                                   | Array    |
| ETag           | ファイルのSHA-1アルゴリズムチェック値                                      | String   |
| Size           | ファイルサイズ。単位 Byte                                          | String   |
| Key            | オブジェクト鍵（オブジェクトの名称）、バケットにあるオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String   |
| LastModified   | オブジェクト最終変更時間                                          | String   |
| Owner          | バケット所有者の情報                                            | Object   |
| ID             | バケット所有者のUID情報                                     | String   |



### Put Bucket

##### 機能説明

Put Bucketリクエストは指定アカウントで1つのバケットを作成できます。

#### 操作方法プロトタイプ

Put Bucketの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE',	/* 必須 */
	ACL : 'STRING_VALUE',	/* 非必須 */
	GrantRead : 'STRING_VALUE', /* 非必須 */
	GrantWrite : 'STRING_VALUE',	/* 非必須 */
	GrantFullControl : 'STRING_VALUE'	/* 非必須 */
};

cos.putBucket(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名           | パラメータ説明                                                     | タイプ   | 必須項目 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region           | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| ACL              | ユーザーにファイル権限のカスタマイズを許可します。有効値：private、public-read、public-read-write。デフォルト値：private。 | String | いいえ   |
| GrantRead        | 権限が付与された者に読み取り権限を授与し、フォーマットx-cos-grant-read: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| GrantWrite       | 権限が付与された者に書き込み権限を授与し、フォーマットx-cos-grant-write: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| GrantFullControl | 権限が付与された者に読み書き権限を授与し、フォーマットはx-cos-grant-full-control: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名   | パラメータ説明                                                     | タイプ   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data     | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Location | 作成に成功した後のバケットの操作アドレス                                | String |

### Delete Bucket

##### 機能説明

Delete Bucketリクエストは指定されたアカウントでバケットを削除でき、削除する前にバケットをブランクにする必要があります。

#### 操作方法プロトタイプ

 Delete Bucketの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE'		/* 必須 */
};

cos.deleteBucket(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名              | パラメータ説明                                                     | タイプ    |
| ------------------- | ------------------------------------------------------------ | ------- |
| err                 | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| DeleteBucketSuccess | 削除が成功したかどうか                                                | Boolean |

### Get Bucket ACL

##### 機能説明

APIを使用してバケットのACLテーブルを読み取り、所有者のみがその操作権限を持っています。

#### 操作方法プロトタイプ

Get Bucket ACLの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE'		/* 必須 */
};

cos.getBucketAcl(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名            | パラメータ説明                                                     | タイプ   |
| ----------------- | ------------------------------------------------------------ | ------ |
| err               | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data              | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Owner             | リソースを識別する所有者                                             | Object |
| uin               | ユーザーQQ番号                                                     | String |
| AccessControlList | 権限が付与された者情報と権限情報                                       | Object |
| Grant             | 具体的な授権情報                                               | Array  |
| Permission        | 権限情報。列挙値：READ、WRITE、FULL_CONTROL                  | String |
| Grantee           | 権限が付与された者情報                                             | Object |
| uin               | 権限が付与された者情報QQ番号または'anonymous'                           | String |
| Subacount         | サブアカウントQQアカウント                                               | String |

### Put Bucket ACL

##### 機能説明

APIを使用してバケットのACLテーブルに書き込み、Put Bucket ACLは上書き操作であり、新しいACLを渡すと、元のACLを上書きします。所有者のみがその操作権限を持っています。

#### 操作方法プロトタイプ

Put Bucket ACLの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',			/* 必須 */
	Region : 'STRING_VALUE',			/* 必須 */
	ACL : 'STRING_VALUE',				/* 非必須 */
	GrantRead : 'STRING_VALUE', 		/* 非必須 */
	GrantWrite : 'STRING_VALUE',		/* 非必須 */
	GrantFullControl : 'STRING_VALUE'	/* 非必須 */
};

cos.putBucketAcl(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名           | パラメータ説明                                                     | タイプ   | 必須項目 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region           | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| ACL              | ユーザーにファイル権限のカスタマイズを許可します。有効値：private、public-read。デフォルト値：private。 | String | いいえ   |
| GrantRead        | 権限が付与された者に読み取り権限を授与し、フォーマットx-cos-grant-read: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| GrantWrite       | 権限が付与された者に書き込み権限を授与し、フォーマットx-cos-grant-write: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| GrantFullControl | 権限が付与された者に読み書き権限を授与し、フォーマットはx-cos-grant-full-control: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名             | パラメータ説明                                                     | タイプ    |
| ------------------ | ------------------------------------------------------------ | ------- |
| err                | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はクランクです | Object  |
| data               | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| BucketGrantSuccess | 授権が成功したかどうか                                                 | Boolean |

### Get Bucket CORS

##### 機能説明

Get Bucket CORSはクロスオリジンアクセス読み取りを実現します。

#### 操作方法プロトタイプ

- Get Bucket CORSの呼び出し操作

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE'		/* 必須 */
};

cos.getBucketCors(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名        | パラメータ説明                                                     | タイプ   |
| ------------- | ------------------------------------------------------------ | ------ |
| err           | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data          | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| CORSRule      | 構成の情報集合                                               | Array  |
| AllowedMethod | 許可されるHTTP操作。列挙値：Get、Put、Head、Post、Delete       | Array  |
| AllowedOrigin | 許可されるアクセスソース。『 * 』ワイルドカードをサポートします                            | Array  |
| AllowedHeader | オプションリクエストを送信する時に、後続のリクエストがどのカスタムHTTPリクエストヘッダーを使用できるかをサーバーに通知します | Array  |
| ExposeHeader  | ブラウザが受信できるサーバーからのカスタムヘッダー情報を設定します           | Array  |
| MaxAgeSeconds | オプションリクエストの結果が得られる有効期間を設定します                            | String |
| ID            | 規則名称                                                     | String |

### Put Bucket CORS

##### 機能説明

Put Bucket CORSはクロスオリジンアクセス読み書きを実現します。

#### 操作方法プロトタイプ

Put Bucket CORSの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 必須 */
	Region : 'STRING_VALUE',		/* 必須 */
	CORSRules : [
		{
			ID : 'STRING_VALUE',	/* 非必須 */
			AllowedMethods: [ 		/* 必須 */
			  'STRING_VALUE',
			  ...
			],
			AllowedOrigins: [		 /* 必須 */
			  'STRING_VALUE',
			  ...
			],
			AllowedHeaders: [		/* 非必須 */
			  'STRING_VALUE',
			  ...
			],
			ExposeHeaders: [		/* 非必須 */
				'STRING_VALUE',
				...
			],
			MaxAgeSeconds: 'STRING_VALUE'	/* 非必須 */
		  },
		  ....
	]
};

cos.putBucketCors(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名         | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket         | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String | はい   |
| Region         | バケットが位置する地域。列挙値については、[バケット地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| CORSRules      | クロスオリジン規則集合                                                 | Array  | いいえ   |
| ID             | 規則名称                                                     | String | いいえ   |
| AllowedMethods | 許可されるHTTP操作。列挙値：Get、Put、Head、Post、Delete         | Array  | はい   |
| AllowedOrigins | 許可されるアクセスソース。『 * 』ワイルドカードをサポートし、プロトコル、ポートおよびドメイン名は一致する必要があります  | Array  | はい   |
| AllowedHeaders | オプションリクエストを送信する時に、後続のリクエストがどのカスタムHTTPリクエストヘッダーを使用できるかをサーバーに通知し、『 * 』ワイルドカードをサポートします | Array  | いいえ   |
| ExposeHeaders  | ブラウザが受信できるサーバーからのカスタムヘッダー情報を設定します           | Array  | いいえ   |
| MaxAgeSeconds  | オプションリクエストの結果が得られる有効期間を設定します                            | String | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名               | パラメータ説明                                                     | タイプ    |
| -------------------- | ------------------------------------------------------------ | ------- |
| err                  | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                 | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| PutBucketCorsSucesss | Bucket CORSの設定が成功したかどうか                                     | Boolean |

### Delete Bucket CORS

##### 機能説明

Delete Bucket CORSはクロスオリジンアクセス読み取りを実現します。

#### 操作方法プロトタイプ

Delete Bucket CORSの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 必須 */
	Region : 'STRING_VALUE'			/* 必須 */
};

cos.deleteBucketCors(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名                  | パラメータ説明                                                     | タイプ    |
| ----------------------- | ------------------------------------------------------------ | ------- |
| err                     |  ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                    | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| DeleteBucketCorsSuccess | Bucket CORSの削除が成功したかどうか                                    | Boolean |

### Get Bucket Location

##### 機能説明

Get Bucket Location APIはバケットが所在している地域の情報を取得し、バケットの所有者のみが情報を読み取る権限を持っています。

#### 操作方法プロトタイプ

Get Bucket Locationの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 必須 */
	Region : 'STRING_VALUE'			/* 必須 */
};

cos.getBucketLocation(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名             | パラメータ説明                                                     | タイプ   |
| ------------------ | ------------------------------------------------------------ | ------ |
| err                | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data               | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| LocationConstraint | バケットが所在している地域。列挙値：china-east、china-south、china-north、china-west、singapore | String |

### Get Bucket Tagging

##### 機能説明

Get Bucket Tagging APIは、指定されたバケットのタグの取得を実現します。

#### 操作方法プロトタイプ

Get Bucket Taggingの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE'		/* 必須 */
};

cos.getBucketTagging(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名 | パラメータ説明                                                     | タイプ   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data   | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Tags   | バケットのタグ集合                                            | Array  |
| Key    | Tagのカテゴリ名称                                               | String |
| Value  | Tagの値                                                     | String |

### Put Bucket Tagging

##### 機能説明

Put Bucket Tagging APIは、指定されたバケットのタグ付けを実現します。

#### 操作パラメータ説明

 Put Bucket Taggingの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE',	/* 必須 */
	Tags :  [
		{
			Key : 'key1',		/* 必須 */
			Value : 'value1'	/* 必須 */
		},
		...
	]
};

cos.putBucketTagging(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Tags   | バケットのタグ集合                                            | Array  | はい   |
| Key    | Tagのカテゴリ名称                                               | String | はい   |
| Value  | Tagの値                                                     | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名                  | パラメータ説明                                                     | タイプ    |
| ----------------------- | ------------------------------------------------------------ | ------- |
| err                     |  ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                    | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| PutBucketTaggingSuccess | Tagの設定が成功したかどうか                                            | Boolean |

### Delete Bucket Tagging

##### 機能説明

Delete Bucket Tagging APIは、指定されたバケットのタグの削除を実現します。

#### 操作方法プロトタイプ

Delete Bucket Taggingの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',	/* 必須 */
	Region : 'STRING_VALUE'		/* 必須 */
};

cos.deleteBucketTagging(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名                     | パラメータ説明                                                     | タイプ    |
| -------------------------- | ------------------------------------------------------------ | ------- |
| err                        | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                       | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| DeleteBucketTaggingSuccess | バケットタグの削除が成功したかどうか                                    | Boolean |

## オブジェクト操作

### Head Object

##### 機能説明

Head Objectリクエストは、対応するオブジェクトのメタデータを取り戻すことができ、Headの権限はGetの権限と一致します。

#### 操作方法プロトタイプ

Head Objectの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 必須 */
	Region : 'STRING_VALUE',		/* 必須 */
	Key : 'STRING_VALUE',			/* 必須 */
	IfModifiedSince : 'STRING_VALUE'	/* 非必須 */
};

cos.headObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名          | パラメータ説明                                                     | タイプ   | 必須項目 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region          | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key             | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String | はい   |
| IfModifiedSince | 指定された時間が経過した後にオブジェクトが変更される場合、対応するオブジェクトのメタ情報を返します       | String | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名              | パラメータ説明                                                     | タイプ    |
| ------------------- | ------------------------------------------------------------ | ------- |
| err                 | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| x-cos-object-type   | オブジェクトを追加でアップロードできるかどうかを示すために使用されます。列挙値：normalまたはappendable | String  |
| x-cos-storage-class | オブジェクトのストレージレベル。列挙値：Standard、Standard_IA              | String  |
| x-cos-meta- *       | ユーザーカスタマイズのメタデータ                                           | String  |
| NotModified         | リクエストの時にIfModifiedSinceがあり、かつファイルが変更されていない場合、trueにします   | Boolean |

### Get Object

##### 機能説明

Get Objectリクエストによりファイル（オブジェクト）をローカルにダウンロードできます。当該操作については、目標Objectにリード権限があり、あるいは目標Objectが全員にリード権限を開放する必要があります（パブリック読み取り）。

#### 操作方法プロトタイプ

Get Objectの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Key : 'STRING_VALUE',							/* 必須 */
	ResponseContentType : 'STRING_VALUE',			/* 非必須 */
	ResponseContentLanguage : 'STRING_VALUE',		/* 非必須 */
	ResponseExpires : 'STRING_VALUE',				/* 非必須 */
	ResponseCacheControl : 'STRING_VALUE',			/* 非必須 */
	ResponseContentDisposition : 'STRING_VALUE',	/* 非必須 */
	ResponseContentEncoding : 'STRING_VALUE',		/* 非必須 */
	Range : 'STRING_VALUE',							/* 非必須 */
	IfModifiedSince : 'STRING_VALUE',				/* 非必須 */
	Output : 'STRING_VALUE' || 'WRITE_STRING'		/* 必須 */
};

cos.getObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名                     | パラメータ説明                                                     | タイプ                 | 必須項目 |
| -------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| Bucket                     | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String               | はい   |
| Region                     | バケットが所在している地域。列挙値については、[バケット地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String               | はい   |
| Key                        | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String               | はい   |
| ResponseContentType        | ヘッダー内の Content-Type パラメータを返すように設定します                           | String               | いいえ   |
| ResponseContentLanguage    | ヘッダー内のContent-Languageパラメータを返すように設定します                       | String               | いいえ   |
| ResponseExpires            | ヘッダー内のContent-Expiresパラメータを返すように設定します                        | String               | いいえ   |
| ResponseCacheControl       | ヘッダー内のCache-Controlパラメータを返すように設定します                          | String               | いいえ   |
| ResponseContentDisposition | ヘッダー内のContent-Dispositionパラメータを返すように設定します                    | String               | いいえ   |
| ResponseContentEncoding    | ヘッダー内のContent-Encodingパラメータを返すように設定します                       | String               | いいえ   |
| Range                      | RFC 2616で定義されたファイルダウンロードの指定範囲、単位はバイト（bytes）です      | String               | いいえ   |
| IfModifiedSince            | ファイル変更時間が指定された時間よりも遅い場合、ファイルの内容を返します                 | String               | いいえ   |
| Output                     | 出力されるファイルパスまたは書き込みストリーム                               | String / WriteStream | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名              | パラメータ説明                                                     | タイプ    |
| ------------------- | ------------------------------------------------------------ | ------- |
| err                 | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| x-cos-object-type   | オブジェクトを追加でアップロードできるかどうかを示すために使用されます。列挙値：normalまたはappendable | String  |
| x-cos-storage-class | オブジェクトのストレージレベル。列挙値：Standard、Standard_IA              | String  |
| x-cos-meta- *       | ユーザーカスタマイズのメタデータ                                           | String  |
| NotModified         | リクエストの時にIfModifiedSinceがあり、かつファイルが変更されていない場合、trueにします   | Boolean |

### Put Object

##### 機能説明

Put Objectリクエストは1つのファイル（Object）を指定のBucketにアップロードできます。

> !

1. Key（ファイル名）は `/` で終わることができず、そうしないとフォルダとして識別されます。
2. 現在のアクセスポリシーエントリは 1000に制限され、オブジェクトのACL制御を行う必要がない場合、アップロードする時に設定しないでください。デフォルトではバケット権限を継承します。

#### 操作方法プロトタイプ

Put Objectの呼び出し操作：

```js
cos.putObject({
    Bucket : 'STRING_VALUE',                        /* 必須 */
    Region : 'STRING_VALUE',                        /* 必須 */
    Key : 'STRING_VALUE',                           /* 必須 */
    Body: fs.createReadStream('./a.zip'),           /* 必須 */
    onProgress: function (progressData) {
        console.log(progressData);
    },
}, function(err, data) {
    if(err) {
        console.log(err);
    } else {
        console.log(data);
    }
});
```

#### 操作パラメータ説明

| パラメータ名             | パラメータ説明                                                     | タイプ            | 必須項目 |
| ------------------ | ------------------------------------------------------------ | -------------- | ---- |
| Bucket             | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String         | はい   |
| Region             | バケットが所在している地域。列挙値については、[バケット地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String               | はい   |
| Key                | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String         | はい   |
| CacheControl       | RFC 2616で定義されたキャッシュポリシーは、オブジェクトメタデータとして保存されます          | String         | いいえ   |
| ContentDisposition | RFC 2616で定義されたファイル名称は、ブジェクトメタデータとして保存されます          | String         | いいえ   |
| ContentEncoding    | RFC 2616で定義されたエンコーディングフォーマットは、オブジェクトメタデータとして保存されます          | String         | いいえ   |
| ContentLength      | RFC 2616で定義されたHTTPリクエスト内容の長さ（バイト）                  | String         | はい   |
| ContentType        | RFC 2616で定義された内容タイプ（MIME）は、オブジェクトメタデータとして保存されます  | String         |いいえ   |
| Expect             | Expect：100-continueを使用する場合、サーバーから承認を受け取らないと、リクエスト内容を送信しません | String         | いいえ   |
| Expires            | RFC 2616で定義された期限切れ時間は、オブジェクトメタデータとして保存されます          | String         | いいえ   |
| ContentSha1        | RFC 3174で定義された160-bit内容SHA-1アルゴリズムチェック値              | String         | いいえ   |
| ACL                | ユーザーにファイル権限のカスタマイズを許可します。有効値：private、public-read         | String         | いいえ   |
| GrantRead        | 権限が付与された者に読み取り権限を授与し、フォーマットx-cos-grant-read: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID" | String | いいえ   |
| GrantWrite       | 権限が付与された者に書き込み権限を授与し、フォーマットx-cos-grant-write: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| GrantFullControl | 権限が付与された者に読み書き権限を授与し、フォーマットはx-cos-grant-full-control: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| x-cos-meta- *      | ユーザーカスタムを許可するヘッダー情報をオブジェクトメタデータとして返されます。サイズを2Kに制限します。 | String         | いいえ   |
| Body               | インバウンドファイルパスまたはファイルストリーム                                         | String/ Stream | はい   |
| onProgress         | 進行コールバック関数。コールバックはオブジェクトであり、進行情報を含みます                   | Function       | いいえ   |



####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名 | パラメータ説明                                                     | タイプ   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data   | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| ETag   | ファイルのMD5アルゴリズムチェック値を返します。ETagの値はオブジェクトの内容が変更されたかどうかを確認するために使用できます | String |

### Delete Object

##### 機能説明

Delete Objectリクエストは1つのファイル（オブジェクト）を削除できます。

#### 操作方法プロトタイプ

Delete Objectの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Key : 'STRING_VALUE'							/* 必須 */
};

cos.deleteObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key    | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String         | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名              | パラメータ説明                                                     | タイプ    |
| ------------------- | ------------------------------------------------------------ | ------- |
| err                 | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object  |
| DeleteObjectSuccess | ファイルの削除が成功したかどうか                                             | Boolean |
| BucketNotFound      | 指定されたバケットが見つからない場合、trueです                          | Boolean |

### Options Object

##### 機能説明

Options Objectリクエストはクロスオリジンアクセスの事前リクエストを実現します。即ちオプションリクエストをサーバーに送信してクロスオリジン操作を行うことができるかどうかを確認します。

#### 操作方法プロトタイプ

Options Objectの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',		/* 必須 */
	Region : 'STRING_VALUE',		/* 必須 */
	Key : 'STRING_VALUE',			/* 必須 */
	Origin : 'STRING_VALUE', 		/* 必須 */
	AccessControlRequestMethod : 'STRING_VALUE', 		/* 必須 */
	AccessControlRequestHeaders : 'STRING_VALUE'		/* 非必須 */
};

cos.optionsObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名                      | パラメータ説明                                                     | タイプ   | 必須項目 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region                      | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key                         | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String         | はい   |
| Origin                      | クロスオリジンアクセスをシミュレートするリクエスト元ドメイン名                                   | String | はい   |
| AccessControlRequestMethod  | クロスオリジンアクセスをシミュレートするHTTPリクエスト方法                                   | String | はい   |
| AccessControlRequestHeaders | クロスオリジンアクセスをシミュレートするリクエストヘッダー                                       | String | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名                     | パラメータ説明                                                     | タイプ   |
| -------------------------- | ------------------------------------------------------------ | ------ |
| err                        | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data                       | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| AccessControlAllowOrigin   | クロスオリジンアクセスをシミュレートするリクエストソースドメイン名。リクエスト元が許可されない場合、このヘッダーは返しません | String |
| AccessControlAllowMethods  | クロスオリジンアクセスをシミュレートするHTTPリクエスト方法。リクエスト方法が許可されない場合、このヘッダーは返しません | String |
| AccessControlAllowHeaders  | クロスオリジンアクセスをシミュレートするリクエストヘッダー。何らかのリクエストヘッダーのシミュレートが許可されない場合、このヘッダーはこのリクエストヘッダーを返しません | String |
| AccessControlExposeHeaders | CORSリクエストは戻りヘッダーをサポートし、カンマで区切ります                                 | String |
| AccessControlMaxAge        | オプションリクエストが得られる有効期間を設定します                            | String |

### Get Object ACL

##### 機能説明

Get Object ACL APIは、APIを使用してオブジェクトのACLテーブルを読み取ることを実現し、所有者だけがその操作権限を持っています。

#### 操作方法プロトタイプ

Get Object ACLの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Key : 'STRING_VALUE'							/* 必須 */
};

cos.getObjectAcl(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名 | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key    | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String         | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名            | パラメータ説明                                                     | タイプ   |
| ----------------- | ------------------------------------------------------------ | ------ |
| err               | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data              | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Owner             | リソースを識別する所有者                                             | Object |
| uin               | ユーザーQQ番号                                                     | String |
| AccessControlList | 権限が付与された者情報と権限情報                                       | Object |
| Grant             | 具体的な授権情報                                               | Array  |
| Permission        | 権限情報。列挙値：READ、WRITE、FULL_CONTROL                  | String |
| Grantee           | 権限が付与された者情報                                             | Object |
| uin               | 権限が付与された者情報QQ番号または'anonymous'                           | String |
| Subacount         | サブアカウントQQアカウント                                               | String |

### Put Object ACL

##### 機能説明

Put Object ACLはAPIを使用してオブジェクトのACLテーブルに書き込みます。現在のアクセスポリシーエントリは1000に制限され、オブジェクトのACL制御を行う必要がない場合、設定しないでください、デフォルトではバケット権限を継承します。

#### 操作方法プロトタイプ

 Put Object ACLの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',			/* 必須 */
	Region : 'STRING_VALUE',			/* 必須 */
	Key : 'STRING_VALUE',				/* 必須 */
	ACL : 'STRING_VALUE',				/* 非必須 */
	GrantRead : 'STRING_VALUE', 		/* 非必須 */
	GrantWrite : 'STRING_VALUE',		/* 非必須 */
	GrantFullControl : 'STRING_VALUE'	/* 非必須 */
};

cos.putObjectAcl(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名           | パラメータ説明                                                     | タイプ   | 必須項目 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region           | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key              | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String | はい   |
| ACL              | ユーザーにファイル権限のカスタマイズを許可します。有効値：private、public-read、public-read-write。デフォルト値：private。 | String | いいえ   |
| GrantRead        | 権限が付与された者に読み取り権限を授与し、フォーマットx-cos-grant-read: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| GrantWrite       | 権限が付与された者に書き込み権限を授与し、フォーマットx-cos-grant-write: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| GrantFullControl | 権限が付与された者に読み書き権限を授与し、フォーマットはx-cos-grant-full-control: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名 | パラメータ説明                                                     | タイプ   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data   | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |

### Delete Multiple Object

##### 機能説明

Delete Multiple Objectリクエストは、ファイルの一括削除を実現し、単回リクエストで最大1000個のファイルの一括削除をサポートします。戻り結果に対して、COSはVerboseとQuietという2つのモードを提供します：Verboseモードは各オブジェクトの削除結果を返します；Quietモードはエラーのオブジェクト情報のみを返します。

#### 操作方法プロトタイプ

 Delete Multiple Objectの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Quiet : 'BOOLEAN_VALUE',						/* 非必須 */
	Objects :  [
	    {
	        Key : 'STRING_VALUE'					/* 必須 */
        }
    ]
};

cos.deleteMultipleObject(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名  | パラメータ説明                                                     | タイプ    | 必須項目 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String  | はい   |
| Region  | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String  | はい   |
| Quiet   | ブール値、この値はQuietモードを起動するかどうかを決定します。Trueの場合は、Quietモードを起動し、Falseの場合はVerboseモードを起動し、デフォルトではFalseです | Boolean | いいえ   |
| Objects | 削除されるファイルのリスト                                             | Array   | いいえ   |
| Key     | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String  | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名  | パラメータ説明                                                     | タイプ   |
| ------- | ------------------------------------------------------------ | ------ |
| err     | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data    | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時に空です                         | Object |
| Deleted | 今回削除に成功したオブジェクト情報を説明します                               | Array  |
| Key     | オブジェクト鍵（オブジェクトの名称）、バケットにあるオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String   |
| Error   | 今回削除に失敗したオブジェクト情報を説明します                               | Array  |
| Key     | オブジェクト鍵（オブジェクトの名称）、バケットにあるオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String   |
| Code    | 削除に失敗したエラーコード                                             | String |
| Message | 削除したエラーメッセージ                                                 | String |

## マルチパートアップロード操作

### Initiate Multipart Upload

##### 機能説明

Initiate Multipart Uploadリクエストは、シャードアップロードの初期化を実現します。このリクエストを実行した後にUpload IDを返します。今後のUpload Partリクエストに使用されます。

#### 操作方法プロトタイプ

 Initiate Multipart Uploadの呼び出し操作：

```js
cos.multipartInit({
    Bucket : 'STRING_VALUE',						/* 必須 */
    Region : 'STRING_VALUE',						/* 必須 */
    Key : 'STRING_VALUE',							/* 必須 */
}, function(err, data) {
    if(err) {
        console.log(err);
    } else {
        console.log(data);
    }
});
```

#### 操作パラメータ説明

| パラメータ名             | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region              Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key                | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String  | はい   |
| CacheControl       | RFC 2616で定義されたキャッシュポリシー。Objectメタデータとして保存されます           | String | いいえ   |
| ContentDisposition | RFC 2616で定義されたファイル名。Objectメタデータとして保存されます          | String | いいえ   |
| ContentEncoding    | RFC 2616で定義されたエンコードフォーマット。Objectメタデータとして保存されます          | String | いいえ   |
| ContentType        | RFC 2616で定義された内容タイプ（MIME）。Objectメタデータとして保存されます  | String | いいえ   |
| Expires            | RFC 2616で定義された期限切れ時間。Objectメタデータとして保存されます           | String | いいえ   |
| ACL                | ユーザーにファイル権限のカスタマイズを許可します。有効値：private、public-read         | String | いいえ   |
| GrantRead        | 権限が付与された者に読み取り権限を授与し、フォーマットx-cos-grant-read: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID" | String | いいえ   |
| GrantWrite       | 権限が付与された者に書き込み権限を授与し、フォーマットx-cos-grant-write: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| GrantFullControl | 権限が付与された者に読み書き権限を授与し、フォーマットはx-cos-grant-full-control: uin=" ",uin=" "、<br>サブアカウントに授権する必要がある時、uin="RootAcountID/SubAccountID"、<br>ルートアカウントに授権する必要がある時、uin="RootAcountID"。 | String | いいえ   |
| StorageClass       | オブジェクトのストレージレベルを設定し、列挙値：Standard、Standard_IA。デフォルト値：Standard（現在はSouth China Campusのみをサポートしています） | String | いいえ   |
| x-cos-meta- *      | ユーザーカスタムを許可するヘッダー情報をオブジェクトメタデータとして返されます。サイズを2Kに制限します。 | String | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名   | パラメータ説明                                                     | タイプ   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data     | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Bucket   | シャードアップロードする対象Bucket                                        | String |
| Key      | オブジェクトの名称                                                | String |
| UploadId | 後続のアップロードで使用されるID                                         | String |

### Upload Part

##### 機能説明

Upload Partリクエストは、初期化後のマルチパートアップロードを実行し、サポートされるパート数は1から10000までであり、パートのサイズは1MBから5GBまでです。Upload Partをリクエストするたびに、partNumberとuploadIDを運ぶ必要があり、partNumberはパートの番号であり、アウトオブオーダアップロードをサポートします。

#### 操作方法プロトタイプ

Upload Partの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Key : 'STRING_VALUE',							/* 必須 */
	ContentLength : 'STRING_VALUE',					/* 必須 */
	Expect : 'STRING_VALUE',						/* 非必須 */
	ContentSha1 : 'STRING_VALUE',					/* 非必須 */
	PartNumber : 'STRING_VALUE',					/* 必須 */
	UploadId : 'STRING_VALUE',						/* 必須 */
};

cos.multipartUpload(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名        | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket        | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String | はい   |
| Region        | バケットが所在している地域。列挙値については、[バケット地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key           | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String  | はい   |
| ContentLength | RFC 2616で定義されたHTTPリクエスト内容の長さ（バイト）                  | String         | はい   |
| Expect        | Expect：100-continueを使用する場合、サーバーから承認を受け取らないと、リクエスト内容を送信しません | String | いいえ   |
| ContentSha1   | RFC 3174で定義された160-bit内容SHA-1アルゴリズムチェック値              | String | いいえ   |
| PartNumber    | パートの番号                                                   | String | はい   |
| UploadId      | アップロードタスク番号                                                 | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名 | パラメータ説明                                                     | タイプ   |
| ------ | ------------------------------------------------------------ | ------ |
| err    | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data   | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| ETag   | パートのETag値、sha1チェック値です                               | String |

### Complete Multipart Upload

##### 機能説明

Complete Multipart Uploadは、全体のマルチパートアップロードを完了するために使用されます。Upload Partsを使用してすべてのパートをアップロードした後、このAPIでアップロードを完了できます。このAPIを使用するとき、パートの正確さを検証するために、ボディの各パートにPartNumberとETagを指定する必要があります。

#### 操作方法プロトタイプ

Complete Multipart Uploadの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Key : 'STRING_VALUE',							/* 必須 */
	UploadId : 'STRING_VALUE',						/* 必須 */
	Parts : [
		{
			PartNumber : 'STRING_VALUE',			/* 必須 */
			ETag : 'STRING_VALUE'					/* 必須 */
		},
		...
	]
};

cos.multipartComplete(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名     | パラメータ説明                                                     | タイプ   | 必須項目 |
| ---------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket     | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String | はい   |
| Region     | バケットが所在している地域。列挙値については、[バケット地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key        | オブジェクト鍵（オブジェクト の名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String | はい   |
| UploadId   | アップロードタスク番号                                                 | String | はい   |
| Parts      | パートのETag情報                                              | Array  | はい   |
| PartNumber | パートの番号                                                   | String | はい   |
| ETag       | パートのETag値は、sha1チェック値であり、チェック値の前後に二重引用符を追加する必要があります。例えば"3a0f1fd698c235af9cf098cb74aa25bc" | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名   | パラメータ説明                                                     | タイプ   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data     | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Location | 作成されたブジェクトのパブリックネットワークアクセスドメイン名                                 | String |
| Bucket   | マルチパートアップロードの目標バケット                                        | String |
| Key      | オブジェクトの名称                                                | String |
| ETag     | 組み合わせた後のファイルのMD5アルゴリズムチェック値                                  | String |

### List Parts

##### 機能説明

List Partsは、特定のマルチパートアップロードでアップロードされたパートを照合するために使用されます

#### 操作方法プロトタイプ

List Partsの呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Key : 'STRING_VALUE',							/* 必須 */
	UploadId : 'STRING_VALUE',						/* 必須 */
	EncodingType : 'STRING_VALUE',					/* 非必須 */
	MaxParts : 'STRING_VALUE',						/* 非必須 */
	PartNumberMarker : 'STRING_VALUE'				/* 非必須 */
};

cos.multipartListPart(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名           | パラメータ説明                                                     | タイプ   | 必須項目 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | Bucketの名前。命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String | はい   |
| Region           | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key              | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String | はい   |
| UploadId         | アップロードタスク番号                                                 | String | はい   |
| EncodingType     | 戻り値のエンコード方法を決めます                                         | String | いいえ   |
| MaxParts         | 一度に返された最大エントリ数。デフォルトでは1000です                             | String | いいえ   |
| PartNumberMarker | デフォルトではUTF-8のバイナリ順でエントリーを一覧表示します。すべての一覧表示されたエントリーはmarkerから開始します  | String | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名               | パラメータ説明                                                     | タイプ    |
| -------------------- | ------------------------------------------------------------ | ------ |
| err                  | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data                 | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Bucket               | マルチパートアップロードの目標バケット                                        | String |
| Encoding-type        | 戻り値のエンコーディング方式を規定します                                         | String |
| Key                  | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |
| UploadID             | 今回のマルチパートアップロードのIDを示します                                        | String |
| Initiator            | 今回のアップロードの発起者の情報を表すために使用され、サブノードはUIDを含みます                 | Object |
| UID                  | 開発者APPID                                                 | String |
| Owner                | これらのパートの所有者の情報を表すために使用され、サブノードはUIDを含みます                 | Object |
| UID                  | 所有者のqq                                                    | String |
| StorageClass         | これらのパートのストレージレベルを表すために使用されます。列挙値：Standard、Standard_IA    | String |
| PartNumberMarker     | デフォルトでは、エントリがUTF-8二進法の順でリストされ、すべてのリストされたエントリはmarkerから始まります  | String |
| NextPartNumberMarker | 仮に返されたエントリが遮断された場合、返されたNextMarkerは次のエントリの起点です   | String |
| MaxParts             | 一度に返されたエントリの最大数                                       | String |
| IsTruncated          | 返されたエントリが遮断されたかどうか、'true' または 'false'                     | String |
| Part                 | パート情報集合                                                 | Array  |
| PartNumber           | パートの番号                                                     | String |
| LastModified         | パートの最終変更時間                                               | String |
| Etag                 | パートのSHA-1アルゴリズムチェック値                                        | String |
| Size                 | パートのサイズ、単位 Byte                                            | String |

### Abort Multipart Upload

##### 機能説明

Abort Multipart Uploadは、1つのマルチパートアップロードを破棄し、アップロードされたパートを削除するために使用されます。このAbort Multipart Uploadを呼び出すとき、このUpload Partsを使用しているリクエストがあると、Upload Partsは失敗を返します。

#### 操作方法プロトタイプ

Abort Multipart Upload の呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Key : 'STRING_VALUE',							/* 必須 */
	UploadId : 'STRING_VALUE'						/* 必須 */
};

cos.multipartAbort(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名   | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket   | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String | はい   |
| Region   | Bucketの所在地域。列挙値については、[Bucket 地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Key      | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String | はい   |
| UploadId | アップロードタスク番号                                                 | String | はい   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名                | パラメータ説明                                                     | タイプ    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object  |
| data                  | リクエスト成功の時に返されたオブジェクト、リクエストエラーの時はブランクです                         | Object |
| MultipartAbortSuccess | Multipart Abort が成功したかどうか                                     | Boolean |

### List Multipart Uploads

##### 機能説明

List Multiparts Uploadsは、実行中のマルチパートアップロードを照合するために使用されます。単回リクエスト操作で、最大1000個の実行中のマルチパートアップロードがリストされます。

#### 操作方法プロトタイプ

List Multipart Uploads の呼び出し操作：

```js
var params = {
	Bucket : 'STRING_VALUE',						/* 必須 */
	Region : 'STRING_VALUE',						/* 必須 */
	Delimiter : 'STRING_VALUE',						/* 非必須 */
	EncodingType : 'STRING_VALUE',					/* 非必須 */
	Prefix : 'STRING_VALUE',						/* 非必須 */
	MaxUploads : 'STRING_VALUE',					/* 非必須 */
	KeyMarker : 'STRING_VALUE',						/* 非必須 */
	UploadIdMarker : 'STRING_VALUE'					/* 非必須 */
};

cos.multipartList(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名         | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket         | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String | はい   |
| Region         | バケットが位置する地域。列挙値については、[バケット地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String | はい   |
| Delimiter      | 区切り文字は記号であり、Prefixがある場合、Prefixからdelimiterまでの間にある同じパスが1つのタイプに分類され、Common Prefixとして定義し、その後、すべてのCommon Prefixをリストアウトします。Prefixがない場合、パスの始点から始まります | String | いいえ   |
| EncodingType   | 戻り値のエンコーディング方式を規定します                                         | String | いいえ   |
| Prefix         | プレフィックスマッチング、返されたオブジェクト鍵のプレフィックスアドレスを規定するために使用されます                       | String | いいえ   |
| MaxUploads     | 一回返された最大エントリ数。デフォルトでは1000です                             | String | いいえ   |
| KeyMarker      |upload-id-markerと共に使用され、<br><li>upload-id-markerが指定されていない場合、<br>ObjectNameがkey-markerの後ろ（アルファベット順）にあるエントリがリストされます。<br> <li>upload-id-markerが指定されている場合、<br>ObjectNameがkey-markerの後ろ（アルファベット順）にあるエントリがリストされます<br>ObjectNameがアルファベット順でkey-markerと同じ、同時にUploadIDがupload-id-markerの後ろ（アルファベット順）にあるエントリがリストされます。 | String | いいえ   |
| UploadIdMarker | key-markerと共に使用され、<br><li>key-markerが指定されていない場合、<br>upload-id-markerが無視されます。<br><li>key-markerが指定されている場合、<br>ObjectNameがkey-markerの後ろ（アルファベット順）にあるエントリがリストされます。<br>ObjectNameがアルファベット順でkey-markerと同じ、同時にUploadIDがupload-id-markerの後ろ（アルファベット順）にあるエントリがリストされます。 | String | いいえ   |

</li>

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名             | パラメータ説明                                                     | タイプ   |
| ------------------ | ------------------------------------------------------------ | ------ |
| err                | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data               | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Bucket             | マルチパートアップロードの目標バケット                                        | String |
| Encoding-type      | 戻り値のエンコーディング方式を規定します                                         | String |
| KeyMarker          | リストされたエントリはこのkey値から始まります                                      | String |
| UploadIdMarker     | リストされたエントリはこのUploadId値から始まります                                 | String |
| NextKeyMarker      | 仮に返されたエントリが遮断された場合、返されたNextKeyMarkerは次のエントリの起点です     | String |
| NextUploadIdMarker | 仮に返されたエントリが遮断された場合、返されたUploadIdは次のエントリの起点です     | String |
| IsTruncated        | 仮に返されたエントリが遮断されたかどうか、'true' または 'false'                     | String |
| Delimiter          | 区切り文字は記号であり、プレフィックスがある場合、プレフィックスからデリミターまでの間にある同じパスが1つのタイプに分類され、Common Prefixとして定義し、その後、すべてのCommon Prefixをリストアウトされます。プレフィックスがない場合、パスの先頭から開始します | String |
| CommonPrefixes | プレフィックスからデリミターの間にある同じパスが1つのタイプに分類され、Common Prefixとして定義されます | Array    |
| Prefix             | プレフィックスマッチング、返されたオブジェクト鍵のプレフィックスアドレスを規定するために使用されます                       | String   |
| Upload             | Uploadの情報集合                                            | Array  |
| Key                | オブジェクト鍵（オブジェクトの名称）、バケットにあるオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String   |
| UploadID           | 今回のマルチパートアップロードのIDを示します                                        | String |
| StorageClass       | パートのストレージレベルを表すために使用されます。列挙値：Standard、Standard_IA        | String |
| Initiator          | 今回のアップロードの発起者の情報を表すために使用され、サブノードはUIDを含みます                 | Object |
| UID                | 開発者APPID                                                 | String |
| Owner              | これらのパートの所有者の情報を表すために使用され、サブノードはUIDを含みます                 | Object |
| UID                | 所有者のqq                                                    | String |
| Initiated          | マルチパートアップロードの開始時間                                           | String |

### Slice Upload File

##### 機能説明

Slice Upload Fileは、ファイルのマルチパートアップロードを実現するために使用されます。

#### 操作方法プロトタイプ

Slice Upload Fileの呼び出し操作：

```js
var params = {
	Bucket: 'STRING_VALUE',	/* 必須 */
	Region: 'STRING_VALUE',	/* 必須 */
	Key: 'STRING_VALUE',	/* 必須 */
	FilePath: 'STRING_VALUE',	/* 必須 */
	SliceSize: 'STRING_VALUE',	/* 非必須 */
	AsyncLimit: 'NUMBER_VALUE',	/* 非必須 */
    onHashProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    },
    onProgress: function (progressData) {
        console.log(JSON.stringify(progressData));
    },
};

cos.sliceUploadFile(params, function(err, data) {
	if(err) {
		console.log(err);
	} else {
		console.log(data);
	}
});

```

#### 操作パラメータ説明

| パラメータ名         | パラメータ説明                                                     | タイプ     | 必須項目 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket         | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String | はい   |
| Region         | バケットが所在している地域。列挙値については、[バケット地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String   | はい   |
| Key            | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください  String   | はい   |
| FilePath       | ローカルファイルパス                                                 | String   | はい   |
| SliceSize      | パートのサイズ                                                     | String   | いいえ   |
| AsyncLimit     | パートの同時実行量                                                 | String   | いいえ   |
| onHashProgress | ファイルのsha1値を計算する進行コールバック関数。コールバックはオブジェクトであり、進行情報を含みます | Function | いいえ   |
| onProgress     | 進行コールバック関数。コールバックはオブジェクトであり、進行情報を含みます                   | Function | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名   | パラメータ説明                                                     | タイプ   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data     | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Location | 作成されたブジェクトのパブリックネットワークアクセスドメイン名                                 | String |
| Bucket   | マルチパートアップロードの目標バケット                                        | String |
| Key      | オブジェクトの名称                                                | String |
| ETag     | 組み合わせた後のファイルのSHA-1アルゴリズムチェック値                                | String |

#### 進行コールバックパラメータ

| パラメータ名     | パラメータ説明           | タイプ   |
| ---------- | ------------------ | ------ |
| SliceSize  | パートのサイズ           | String |
| PartNumber | アップロードに成功したパートの番号 | Number |
| FileSize   | ファイルの総サイズ         | Number |

### Slice Copy File

##### 機能説明

Slice Copy File は、ソースパスから目標パスへのファイルのコピーを実現するために使用することができます。ファイルのメタ属性とACLはコピー中に変更できます。ユーザーはこのAPIによりファイルの移動、ファイル名の変更、ファイル属性の変更、およびコピーの作成を実現できます。

#### 操作方法プロトタイプ

Slice Copy Fileを呼び出して操作します：

```js
cos.sliceCopyFile({
    Bucket: 'STRING_VALUE',                               /* 必須 */
    Region: 'STRING_VALUE',                               /* 必須 */
    Key: 'STRING_VALUE',                                  /* 必須 */
    CopySource: 'STRING_VALUE', 			  /* 必須 */
    SliceSize: 'NUMBER_VALUE',                            /* 非必須 */
    onProgress:function (progressData) {                  /* 非必須 */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});

```

#### 操作パラメータ説明

| パラメータ名     | パラメータ説明                                                     | タイプ     | 必須項目 |
| ---------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket     | バケットの名称。命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String | はい   |
| Region     | バケットが所在している地域。列挙値については、[バケット地域情報](https://cloud.tencent.com/document/product/436/6224)を参照してください | String   | はい   |
| Key        | オブジェクト鍵（オブジェクトの名称）、バケット内のオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください  String   | はい   |
| CopySource | ソースファイルURLパス。versionidサブリソースにより履歴バージョンを指定できます       | String   | はい   |
| ChunkSize  | シャードコピー時の各シャードのサイズのバイト数。デフォルト値1048576（1MB）           | Number   | いいえ   |
| SliceSize  | シャードコピー時のファイルのサイズ。デフォルト値5G                            | Number   | いいえ   |
| onProgress | 進行コールバック関数。コールバックはオブジェクトであり、進行情報を含みます                   | Function | いいえ   |

####コールバック関数の説明

```js
function(err, data) { ... }
```

#### コールバックパラメータの説明

| パラメータ名   | パラメータ説明                                                     | タイプ   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | ネットワークエラーとビジネスエラーを含むリクエストエラーが発生したときに返されたオブジェクト。対処方法については、[エラーコードドキュメント](https://cloud.tencent.com/document/product/436/7730)を参照してください。リクエスト成功の時はブランクです | Object |
| data     | リクエスト成功の時に返されたオブジェクト。リクエストエラーの時はブランクです                         | Object |
| Location | 作成されたブジェクトのパブリックネットワークアクセスドメイン名                                 | String |
| Bucket   | マルチパートアップロードの目標バケット                                        | String |
| Key      | オブジェクト鍵（オブジェクトの名称）、バケットにあるオブジェクトの唯一の識別子であり、詳細については、[オブジェクト鍵の説明](https://cloud.tencent.com/document/product/436/13324)を参照してください | String   |
| ETag     | 組み合わせた後のファイルのMD5アルゴリズムチェック値                                  | String |

