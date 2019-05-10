COS XML Android SDK操作は成功した場合、各APIに対応するタイプを返します。失敗した場合、CosXmlClientExceptionとCosXmlServiceExceptionをスローします。その中でCosXmlClientExceptionは、クライアント異常を指します。例えば、パラメータの空白、ネットワーク接続の失敗など；CosXmlServiceExceptionは、サーバーが要件を満たさないクライアントリクエストを処理するときに返されたエラーを指します。例えば、存在しないファイルへのアクセス、ファイルへのアクセス許可がないなど。詳細については、[SDK異常情報説明](#sdk_exception)を参照してください。

SDKでは、各APIリクエストのために同期と非同期という2つのリクエスト方法を提供します。

## Bucket API説明

## Put Bucket

このAPIを呼び出すと、指定されたアカウントの下に1つのバケットを作成します。具体的な手順は次のとおりです：

1. **PutBucketRequest(String)**構造メソッドを呼び出して、PutBucketRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのputBucketメソッドを呼び出して、PutBucketRequestを渡して、PutBucketResultオブジェクトを返します。
   （または、putBucketAsyncメソッドを呼び出して、PutBucketRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```c
PutBucketResult putBucket(PutBucketRequest request) throws CosXmlClientException, CosXmlServiceException;
void putBucketAsync(PutBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのbucketのフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

PutBucketResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```
String bucket = "bucket";
PutBucketRequest putBucketRequest = new PutBucketRequest(bucket);

//オブジェクトのACL属性を定義します。有効値：private、public-read-write、public-read；デフォルト値：private
putBucketRequest.setXCOSACL("private");

//権限が付与された者に読み取り権限を付与します
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(readACLS);

//権限が付与された者に書き込み権限を付与します
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(writeACLS);

//権限が付与された者に読み書き権限を付与します
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(writeandReadACLS);

//同期メソッドを使用します
try {
    PutBucketResult putBucketResult = cosXmlService.putBucket(putBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.putBucketAsync(putBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`putBucketRequst.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Delete Bucket 

このAPIを呼び出して、指定されたアカウント下にバケットを削除できます。削除する前は、バケット内の内容がブランクである必要があります。バケット内のすべてのオブジェクトを削除する限り、バケット自体を削除できます。具体的な手順は次のとおりです：

1. **DeleteBucketRequest(String)**構造メソッドを呼び出して、DeleteBucketRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのdeleteBucketメソッドを呼び出して、DeleteBucketRequestを渡して、DeleteBucketResultオブジェクトを返します。
   （または、deleteBucketAsyncメソッドを呼び出して、DeleteBucketRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
DeleteBucketResult deleteBucket(DeleteBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketAsync(DeleteBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

DeleteBucketResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
DeleteBucketRequest deleteBucketRequest = new DeleteBucketRequest(bucket);

// 同期メソッドを使用します
try {
    DeleteBucketResult deleteBucketResult = cosXmlService.deleteBucket(deleteBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.deleteBucketAsync(deleteBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`deleteBucketRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Head Bucket

このAPIを呼び出すと、指定されたバケットが存在しているかどうかを確認します。具体的な手順は次のとおりです：

1. HeadBucketRequest（String）構造メソッドを呼び出して、HeadBucketRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのheadBucketメソッドを呼び出して、HeadBucketRequestを渡して、HeadBucketResultオブジェクトを返します。
   （または、headBucketAsyncメソッドを呼び出して、HeadBucketRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
HeadBucketResult headBucket(HeadBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void headBucketAsync(HeadBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

PutBucketResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
HeadBucketRequest headBucketRequest = new HeadBucketRequest(bucket);

//同期メソッドを使用します
try {
    HeadBucketResult headBucketResult = cosXmlService.headBucket(headBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.headBucketAsync(headBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Head Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Head Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`headBucketRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Get Bucket Location

このAPIは、バケットが所在する地域情報を取得するために使用されます。具体的な手順は次のとおりです：

1. **GetBucketLocationRequest(String)**構造メソッドを呼び出して、GetBucketLocationRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのgetBucketLocationメソッドを呼び出して、GetBucketLocationRequestを渡して、GetBucketLocationResultオブジェクトを返します。
   （または、getBucketLocationAsyncメソッドを呼び出して、GetBucketLocationRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetBucketLocationResult getBucketLocation(GetBucketLocationRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketLocationAsync(GetBucketLocationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

GetBucketLocationResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称       | 変数説明                              | タイプ               |
| ------------------ | ------------------------------------- | ------------------ |
| locationConstraint | バケットが所在する地域                       | LocationConstraint |
| httpCode           | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int                |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
GetBucketLocationRequest getBucketLocationRequest = new GetBucketLocationRequest(bucket);

//同期メソッドを使用します
try {
    GetBucketLocationResult getBucketLocationResult = cosXmlService.getBucketLocation(getBucketLocationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.getBucketLocationAsync(getBucketLocationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket Location
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Location failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getBucketLocationRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Get Bucket（すべてのオブジェクトをリストします）

このAPIを呼び出すと、該当バケットの下にあるオブジェクトの一部または全部がリストされます。具体的な手順は次のとおりです：

1. **GetBucketRequest(String)**構造メソッドを呼び出して、GetBucketRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのgetBucketメソッドを呼び出して、GetBucketRequestを渡して、GetBucketResultオブジェクトを返します。
   （または、getBucketAsyncメソッドを呼び出して、GetBucketRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetBucketResult getBucket(GetBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketAsync(GetBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのbucketのフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

GetBucketResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ       |
| ------------ | ------------------------------------- | ---------- |
| listBucket   | Get Bucketリクエスト結果のすべての情報を保存します    | ListBucket |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int        |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";  
GetBucketRequest getBucketRequest = new GetBucketRequest(bucket);

//プレフィックスマッチ、返されるファイルプレフィックスアドレスを指定するために使用されます
getBucketRequest.setPrefix("prefix");

//一度に返されるエントリーの最大数、デフォルト値は1000です
getBucketRequest.setMaxKeys(100);

//区切りは記号の1つです。Prefixがあれば、
//プレフィックスとデリミターの間の同じパスが1つのタイプに分類され、Common Prefixとして定義されます。
//それから、すべてのCommon Prefixをリストします。プレフィックスがなければ、パスの開始点から始めます
getBucketRequest.setDelimiter('/');

// 同期メソッドを使用します
try {
    GetBucketResult getBucketResult = cosXmlService.getBucket(getBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getBucketRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Put Bucket ACL

このAPIを呼び出すと、バケットのアクセス制御権限を指定することができます。具体的な手順は次のとおりです：

1. **PutBucketACLRequest(String)**構造メソッドを呼び出して、PutBucketACLRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのputBucketACLメソッドを呼び出して、PutBucketACLRequestを渡して、PutBucketACLResultオブジェクトを返します。
   （または、putBucketACLAsyncメソッドを呼び出して、PutBucketACLRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
PutBucketACLResult putBucketACL(PutBucketACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketACLAsync(PutBucketACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| xcosACL                   | バケットのアクセス権限を設定します。有効値：private、public-read-write、public-read；デフォルト値：private | String               | いいえ   |
| xcosGrantRead             | 権限が付与された者の読み取り権限                                         | ACLAccount           | いいえ   |
| xcosGrantWrite            | 権限が付与された者の書き込み権限                                         | ACLAccount           | いいえ   |
| xcosGrantRead             | 権限が付与された者の読み取り権限                                       | ACLAccount           | いいえ   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

PutBucketACLResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
PutBucketACLRequest putBucketACLRequest = new PutBucketACLRequest(bucket);

//バケットアクセス権限を設定します
putBucketACLRequest.setXCOSACL("public-read");

//権限が付与された者に読み取り権限を付与します
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(readACLS);

//権限が付与された者に書き込み権限を付与します
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(writeACLS);

//権限が付与された者に読み書き権限を付与します
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(writeandReadACLS);

// 同期メソッドを使用します
try {
    PutBucketACLResult putBucketACLResult = cosXmlService.putBucketACL(putBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期コールバックリクエストを使用します
cosXmlService.putBucketACLAsync(putBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket ACL success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`putBucketACLRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。

## Get Bucket ACL

このAPIは、バケットのACLを取得するために使用されます。具体的な手順は次のとおりです：

1. **GetBucketACLRequest(String)**構造メソッドを呼び出して、GetBucketACLRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのgetBucketACLメソッドを呼び出して、GetBucketACLRequestを渡して、GetBucketACLResultオブジェクトを返します。
   （または、getBucketACLAsyncメソッドを呼び出して、GetBucketACLRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetBucketACLResult getBucketACL(GetBucketACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketACLAsync(GetBucketACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

GetBucketACLResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称        | 変数説明                                                     | タイプ                |
| ------------------- | ------------------------------------------------------------ | ------------------- |
| accessControlPolicy | [権限が付与された者の情報と権限情報](https://cloud.tencent.com/document/product/436/7733) | AccessControlPolicy |
| httpCode            | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗                        | Int                 |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
GetBucketACLRequest getBucketACLRequest = new GetBucketACLRequest(bucket);

// 同期メソッドを使用します
try {
    GetBucketACLResult getBucketACLResult = cosXmlService.getBucketACL(getBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期コールバックリクエストを使用します
cosXmlService.getBucketACLAsync(getBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket ACL success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getBucketACLRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


### Put Bucket CORS

このAPIを呼び出すと、指定されたバケットのクロスオリジンアクセス構成情報を設定します。具体的な手順は次のとおりです：

1. **PutBucketCORSRequest（String）**構造メソッドを呼び出して、PutBucketCORSRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのputBucketCORSメソッドを呼び出して、PutBucketCORSRequestを渡して、PutBucketCORSResultオブジェクトを返します。
   （または、putBucketCORSAsyncメソッドを呼び出して、PutBucketCORSRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
 PutBucketCORSResult putBucketCORS(PutBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketCORSAsync(PutBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                       | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String                     | はい   |
| cORSRule                  | クロスオリジンアクセス構成情報                                             | CORSConfiguration.CORSRule | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                       | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>             | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>             | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener       | いいえ   |

#### 戻り結果の説明

PutBucketCORSResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
PutBucketCORSRequest putBucketCORSRequest = new PutBucketCORSRequest(bucket);
    
/**
 * CORSConfiguration.cORSRule：クロスオリジンアクセス構成情報
 * corsRule.id：規則のIDを構成します
 * corsRule.allowedOrigin：許可されたアクセスソース、ワイルドカード * をサポートします。フォーマット：プロトコル://ドメイン[:ポート]、例えば：http://www.qq.com
 * corsRule.maxAgeSeconds：オプションリクエストが取得される結果の有効期間を設定します
 * corsRule.allowedMethod：許可されたHTTP操作、例えば：GET、PUT、HEAD、POST、DELETE
 * corsRule.allowedHeader：オプションリクエストを送信するときに、後続のリクエストがどのカスタムHTTPリクエストヘッダーを使用できるかをサーバーに通知します。ワイルドカード *をサポートします
 * corsRule.exposeHeader：ブラウザが受信できるサーバーからのカスタムヘッダー情報を設定します
 */
CORSConfiguration.CORSRule corsRule = new CORSConfiguration.CORSRule();

corsRule.id = "123";
corsRule.allowedOrigin = "https://cloud.tencent.com";
corsRule.maxAgeSeconds = 5000;

List<String> methods = new LinkedList<>();
methods.add("PUT");
methods.add("POST");
methods.add("GET");
corsRule.allowedMethod = methods;

List<String> headers = new LinkedList<>();
headers.add("host");
headers.add("content-type");
corsRule.allowedHeader = headers;

List<String> exposeHeaders = new LinkedList<>();
headers.add("x-cos-metha-1");
corsRule.exposeHeader = headers;

//クロスオリジンアクセス構成情報を設定します
putBucketCORSRequest.addCORSRule(corsRule);

// 同期メソッドを使用します
try {
    PutBucketCORSResult putBucketCORSResult = cosXmlService.putBucketCORS(putBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.putBucketCORSAsync(putBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket Replication success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`putBucketCORSRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Get Bucket CORS

このAPIを呼び出すと、指定されたバケットのクロスオリジンアクセス構成情報を取得します。具体的な手順は次のとおりです：

1. **GetBucketCORSRequest(String)**構造メソッドを呼び出して、GetBucketCORSRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのgetBucketCORSメソッドを呼び出して、GetBucketCORSRequestを渡して、GetBucketCORSResultオブジェクトを返します。
   （または、getBucketCORSAsyncメソッドを呼び出して、GetBucketCORSRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetBucketCORSResult getBucketCORS(GetBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketCORSAsync(GetBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

GetBucketCORSResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称      | タイプ                                                         | 変数説明          |
| ----------------- | ------------------------------------------------------------ | ----------------- |
| cORSConfiguration | [クロスオリジンリソース共有構成のすべての情報](https://cloud.tencent.com/document/product/436/8274) | CORSConfiguration |
| httpCode          | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗                        | Int               |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
GetBucketCORSRequest getBucketCORSRequest = new GetBucketCORSRequest(bucket);

//同期メソッドを使用します
try {
    GetBucketCORSResult getBucketCORSResult = cosXmlService.getBucketCORS(getBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.getBucketCORSAsync(getBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket CORS success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getBucketCORSRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Delete Bucket CORS

このAPIを呼び出すと、指定されたバケットのクロスオリジンアクセス構成情報を削除します。具体的な手順は次のとおりです：

1. **DeleteBucketCORSRequest(String)**構造メソッドを呼び出して、DeleteBucketCORSRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのdeleteBucketCORSメソッドを呼び出して、DeleteBucketCORSRequestを渡して、DeleteBucketCORSResultオブジェクトを返します 
   （または、deleteBucketCORSAsyncメソッドを呼び出して、DeleteBucketCORSRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
DeleteBucketCORSResult deleteBucketCORS(DeleteBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketCORSAsync(DeleteBucketCORSRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

DeleteBucketCORSResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
DeleteBucketCORSRequest deleteBucketCORSRequest = new DeleteBucketCORSRequest(bucket);

// 同期メソッドを使用します
try {
    DeleteBucketCORSResult deleteBucketCORSResult = cosXmlService.deleteBucketCORS(deleteBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.deleteBucketCORSAsync(deleteBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket CORS success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`deleteBucketCORSRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Put Bucket Versioning

このAPIは、バケットのマルチバージョン制御機能を設定するために使用されます。具体的な手順は次のとおりです：
1. PutBucketVersioningRequest構造メソッドの呼び出しを通して、PutBucketVersioningRequestオブジェクトをインスタンス化します；
2.CosXmlServiceのputBucketVersioning（PutBucketVersioningRequest）同期メソッドの呼び出しを通して、PutBucketVersioningRequestを渡して、PutBucketVersioningResultオブジェクトを返します。（または、putBucketVersionAsyncメソッドを呼び出して、PutBucketVersioningRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
PutBucketVersioningResult putBucketVersioning(PutBucketVersioningRequest request)throws CosXmlClientException, CosXmlServiceException;

void putBucketVersionAsync(PutBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| isEnable                  | マルチバージョン制御機能を有効にするかどうか、true：有効にする；そうではなければ、false              | boolean              | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

PutBucketVersioningResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
PutBucketVersioningRequest putBucketVersioningRequest = new PutBucketVersioningRequest(bucket);
request.setEnableVersion(true);//有効化

// 同期リクエストを使用します
try {
    PutBucketVersioningResult putBucketVersioningResult = cosXmlService.putBucketVersioning(putBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.putBucketVersionAsync(putBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Object success
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`putBucketVersioningRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Get Bucket Versioning

このAPIを呼び出すと、指定されたバケットのマルチバージョン構成情報を取得します。具体的な手順は次のとおりです：

1. GetBucketVersioningRequest構造メソッドの呼び出しを通して、GetBucketVersioningRequestオブジェクトをインスタンス化します；
2. CosXmlServiceのgetBucketVersioning（GetBucketVersioningRequest）同期メソッドの呼び出しを通して、GetBucketVersioningRequestを渡して、GetBucketVersioningResultオブジェクトを返します。（または、getBucketVersioningAsyncメソッドを呼び出して、GetBucketVersioningRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetBucketVersioningResult getBucketVersioning(GetBucketVersioningRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketVersioningAsync(GetBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

GetBucketVersioningResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称            | 変数説明                              | タイプ                    |
| ----------------------- | ------------------------------------- | ----------------------- |
| versioningConfiguration | マルチバージョン構成情報                        | VersioningConfiguration |
| httpCode                | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int                     |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
GetBucketVersioningRequest getBucketVersioningRequest = new GetBucketVersioningRequest(bucket);
    
// 同期リクエストを使用します
try {
    GetBucketVersioningResult getBucketVersioningResult = cosXmlService.getBucketVersioning(getBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期コールバックリクエストを使用します
cosXmlService.getBucketVersioningAsync(getBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Bucket Versioning success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Versioning failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getBucketVersioningRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


#### Put Bucket Replication

このAPIを呼び出すと、異なる地域のバケットの間で非同期コピー機能の実行を構成します。具体的な手順は次のとおりです：

1. PutBucketReplicationRequest構造メソッドの呼び出しを通して、PutBucketReplicationRequestオブジェクトをインスタンス化します；
2.CosXmlServiceのputBucketReplication（PutBucketReplicationRequest）同期メソッドの呼び出しを通して、PutBucketReplicationRequestを渡して、PutBucketReplicationResultオブジェクトを返します。（または、putBucketReplicationAsyncメソッドを呼び出して、PutBucketReplicationRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
PutBucketReplicationResult putBucketReplication(PutBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;

void putBucketReplicationAsync(PutBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| ownerUin                  | replicationを設定する送信者の身元標識Owner Uin                    | String               | はい   |
| subUin                    | replicationを設定する送信者の身元標識sub Uin                     | String               | はい   |
| ruleStruct                | ドメイン間構成情報、最大1000をサポートします。すべてのポリシーは1つのターゲットバケットのみを指すことができます | RuleStruct           | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

PutBucketReplicationResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
PutBucketReplicationRequest putBucketReplicationRequest = new PutBucketReplicationRequest(bucket);
PutBucketReplicationRequest.RuleStruct ruleStruct = new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_id";
ruleStruct.isEnable = true;
ruleStruct.appid = "1253960454";
ruleStruct.bucket = "replicationtest";
ruleStruct.region = "ap-beijing";
putBucketReplicationRequest.setReplicationConfigurationWithRule(ruleStruct);
putBucketReplicationRequest.setReplicationConfigurationWithRole("ownerUin", "subUin");

// 同期リクエストを使用します    
try {
    PutBucketReplicationResult result = cosXmlService.putBucketReplication(putBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期リクエストを使用します    
cosXmlService.putBucketReplicationAsync(putBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Put Bucket Replication success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket Replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`putBucketReplicationRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Get Bucket Replication

このAPIを呼び出すと、指定されたバケットのドメイン間構成情報を取得します。具体的な手順は次のとおりです：

1. GetBucketReplicationRequest構造メソッドの呼び出しを通して、GetBucketReplicationRequestオブジェクトをインスタンス化します；
2. CosXmlServiceのgetBucketReplication（GetBucketReplicationRequest）同期メソッドの呼び出しを通して、GetBucketReplicationRequestを渡して、GetBucketReplicationResultオブジェクトを返します。（または、getBucketReplicationAsyncメソッドを呼び出して、GetBucketReplicationRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetBucketReplicationResult getBucketReplication(GetBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;

void getBucketReplicationAsync(GetBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

GetBucketReplicationResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称             | 変数説明                              | タイプ                     |
| ------------------------ | ------------------------------------- | ------------------------ |
| replicationConfiguration | ドメイン間構成情報                        | ReplicationConfiguration |
| httpCode                 | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int                      |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
GetBucketReplicationRequest getBucketReplicationRequest = new GetBucketReplicationRequest(bucket);

// 同期リクエストを使用します    
try {
    GetBucketReplicationResult getBucketReplicationResult = cosXmlService.getBucketReplication(getBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期リクエストを使用します    
cosXmlService.getBucketReplicationAsync(getBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Bucket Replication success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getBucketReplicationRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。 


## Delete Bucket Replication

このAPIを呼び出すと、指定されたバケットのドメイン間構成情報を削除します。具体的な手順は次のとおりです：

1. DeleteBucketReplicationRequest構造メソッドの呼び出しを通して、DeleteBucketReplicationRequestオブジェクトをインスタンス化します。
2.CosXmlServiceのdeleteBucketReplication（DeleteBucketReplicationRequest）同期メソッドの呼び出しを通して、DeleteBucketReplicationRequestを渡して、DeleteBucketReplicationResultオブジェクトを返します。（または、deleteBucketReplicationAsyncメソッドを呼び出して、DeleteBucketReplicationRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
DeleteBucketReplicationResult deleteBucketReplication(DeleteBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;

void deleteBucketReplicationAsync(DeleteBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

DeleteBucketReplicationResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
DeleteBucketReplicationRequest deleteBucketReplicationRequest = new DeleteBucketReplicationRequest(bucket);
    
// 同期リクエストを使用します
try {
    DeleteBucketReplicationResult result = cosXmlService.deleteBucketReplication(deleteBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期リクエストを使用します
cosXmlService.deleteBucketReplicationAsync(deleteBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Delete Bucket Replication success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket Replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`deleteBucketReplicationRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Put Bucket Lifecycle

このAPIは、バケットのライフサイクル情報を設定するために使用されます。具体的な手順は以下のとおりです：

1. `PutBucketLifecycleRequest(String)`構造メソッドを呼び出して、PutBucketLifecycleRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのputBucketLifecycleメソッドを呼び出して、PutBucketLifecycleRequestを渡して、PutBucketLifecycleResultオブジェクトを返します。
   （または、putBucketLifecycleAsyncメソッドを呼び出して、PutBucketLifecycleRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
PutBucketLifecycleResult putBucketLifecycle(PutBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketLifecycleAsync(PutBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称       | 説明                                       | タイプ                        | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String                      | はい   |
| rule                      | ライフサイクル構成規則                                             | LifecycleConfiguration.Rule | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                        | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>              | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>              | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener         | いいえ   |

#### 戻り結果の説明

PutBucketLifecycleResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
PutBucketLifecycleRequest putBucketLifecycleRequest = new PutBucketLifecycleRequest(bucket);

// サイクル構成規則情報を宣言します
LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
rule.id = "Lifecycle ID";
LifecycleConfiguration.Filter filter = new LifecycleConfiguration.Filter();
filter.prefix = "prefix/";
rule.filter = filter;
rule.status = "Enabled or Disabled";
LifecycleConfiguration.Transition transition = new LifecycleConfiguration.Transition();
transition.days = 100;
transition.storageClass = COSStorageClass.STANDARD.getStorageClass();
putBucketLifecycleRequest.setRuleList(rule);

// 同期メソッドを使用します
try {
    PutBucketLifecycleResult putBucketLifecycleResult = cosXmlService.putBucketLifecycle(putBucketLifecycleRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.putBucketLifecycleAsync(putBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket Lifecycle success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`putBucketLifecycleRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Get Bucket Lifecycle

このAPIは、バケットのライフサイクル情報を取得するために使用されます。具体的な手順は以下のとおりです：

1. **GetBucketLifecycleRequest(String)**構造メソッドを呼び出して、GetBucketLifecycleRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのgetBucketLifecycleメソッドを呼び出して、GetBucketLifecycleRequestを渡して、GetBucketLifecycleResultオブジェクトを返します。
   （または、getBucketLifecycleAsyncメソッドを呼び出して、GetBucketLifecycleRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetBucketLifecycleResult getBucketLifecycle(GetBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketLifecycleAsync(GetBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

getBucketLifecycleオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称           | 変数説明                              | タイプ                   |
| ---------------------- | ------------------------------------- | ---------------------- |
| lifecycleConfiguration | ライフサイクル構成                      | LifecycleConfiguration |
| httpCode               | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int                    |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
GetBucketLifecycleRequest getBucketLifecycleRequest = new GetBucketLifecycleRequest(bucket);

// 同期メソッドを使用します
try {
    GetBucketLifecycleResult getBucketLifecycleResult = cosXmlService.getBucketLifecycle(getBucketLifecycleRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.getBucketLifecycleAsync(getBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket Lifecycle success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getBucketLifecycleRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Delete Bucket Lifecycle

このAPIは、バケットのライフサイクル情報を削除するために使用されます。具体的な手順は以下のとおりです：

1. **DeleteBucketLifecycleRequest(String)**構造メソッドを呼び出して、DeleteBucketLifecycleRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのdeleteBucketLifecycleメソッドを呼び出して、DeleteBucketLifecycleRequestを渡して、DeleteBucketLifecycleResultオブジェクトを返します。
   （または、deleteBucketLifecycleAsyncメソッドを呼び出して、DeleteBucketLifecycleRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
DeleteBucketLifecycleResult deleteBucketLifecycle(DeleteBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketLifecycleAsync(DeleteBucketLifecycleRequest request,CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

DeleteBucketLifecycleResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
DeleteBucketLifecycleRequest deleteBucketLifecycleRequest = new DeleteBucketLifecycleRequest(bucket);

//同期メソッドを使用します
try {
    DeleteBucketLifecycleResult deleteBucketCORSResult = cosXmlService.deleteBucketLifecycle(deleteBucketLifecycleRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.deleteBucketLifecycleAsync(deleteBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket Lifecycle success
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`deleteBucketLifecycleRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## List Multipart Uploads

このAPIは、バケットで実行中のマルチパートアップロードを取得するために使用されます。単回リクエスト操作で、最大1000個の実行中のマルチパートアップロードがリストされます。具体的な手順は以下のとおりです：

1. **ListMultiUploadsRequest(String)**構造メソッドを呼び出して、ListMultiUploadsRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのlistMultiUploadsメソッドを呼び出して、ListMultiUploadsRequestを渡して、ListMultiUploadsResultオブジェクトを返します。
   （または、listMultiUploadsAsyncメソッドを呼び出して、ListMultiUploadsRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
ListMultiUploadsResult listMultiUploads(ListMultiUploadsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listMultiUploadsAsync(ListMultiUploadsRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

ListMultiUploadsResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称         | 変数説明                              | タイプ                 |
| -------------------- | ------------------------------------- | -------------------- |
| listMultipartUploads | すべてのマルチパートアップロード情報                    | ListMultipartUploads |
| httpCode             | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int                  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";   
ListMultiUploadsRequest listMultiUploadsRequest = new ListMultiUploadsRequest(bucket);

// 同期メソッドを使用します
try {
    ListMultiUploadsResult listMultiUploadsResult = cosXmlService.listMultiUploads(listMultiUploadsRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期メソッドを使用します
cosXmlService.listMultiUploadsAsync(listMultiUploadsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo List Multi Uploads success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo List Multi Uploads failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`listMultiUploadsRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Object API説明

## Put Object

ローカルファイルをCOSにアップロードします。画像のような小さいファイル（20M未満）のアップロードに適し、最大5GB（5GBを含む）をサポートし、5GB以上の場合は、[COSXMLUploadTaskアップロード](#upload_task)またはマルチパートアップロードを使用する必要があります。オブジェクトがCOSにすでに存在する場合は、それが上書きされます。簡単なアップロードAPIは一時停止して再開することはできません。アップロード中に異常が発生して失敗した場合、再度アップロードする必要があります。
具体的な手順は以下のとおりです：

1. `（String, String, String）`構造メソッドを呼び出して、PutObjectRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのputObjectメソッドを呼び出して、PutObjectRequestを渡して、PutObjectResultオブジェクトを返します。
   （または、putObjectAsyncメソッドを呼び出して、PutObjectRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
PutObjectResult putObject(PutObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectAsync(PutObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称       | 説明                                       | タイプ                   | 必須項目   |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String                 | はい   |
| cosPath                   | [オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String                 | はい   |
| srcPath                   | ローカルファイルの絶対パス                                           | String                 | はい   ||
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                   | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>         | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>         | いいえ   |
| qCloudProgressListener    | アップロード進捗のコールバック                                                 | CosXmlProgressListener | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener   | いいえ   |

#### 戻り結果の説明

PutObjectResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ   |
| ------------ | ------------------------------------- | ------ |
| accessUrl    | リクエストが成功する場合、アクセスファイルのアドレスを返します        | String |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int    |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "バケット名称"; // COS XML APIのバケットフォーマットは：`<BucketName-APPID>`です。例えば、examplebucket-1250000000
String cosPath = "オブジェクト鍵"; //すなわち、 //cosPath = "test.txt"のフォーマットでCOSに格納されているファイルの絶対パス；
String srcPath = "ローカルファイルの絶対パス"; //例えば、srcPath = Environment.getExternalStorageDirectory().getPath() + "/test.txt";

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);

putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

// 同期メソッドを使用してアップロードします
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックを使用してアップロードします
cosXmlService.putObjectAsync(putObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Put object success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put object failed because of CosXmlClientException or CosXmlServiceException...
    }
});


//バイト配列をアップロードします
String bucket = "バケット名称"; // COS XML APIのバケットフォーマットは：`<BucketName-APPID>`です。例えば、examplebucket-1250000000
String cosPath = "オブジェクト鍵"; //すなわち、 //cosPath = "test.txt"のフォーマットでCOSに格納されているファイルの絶対パス；
byte[] data = "this is a test".getBytes(Charset.forName("UTF-8"));
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}


//バイトストリームをアップロードします
String bucket = "バケット名称"; // COS XML APIのバケットフォーマットは：`<BucketName-APPID>`です。例えば、examplebucket-1250000000
String cosPath = "オブジェクト鍵"; //すなわち、 //cosPath = "test.txt"のフォーマットでCOSに格納されているファイルの絶対パス；
InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, inputStream);
putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`putObjectRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## マルチパートアップロード

### <span id = "InitMultipartUploadRequest">Initiate Multipart Upload</span>

このAPIを呼び出してマルチパートアップロードを初期化し、このリクエストが正常に実行された後、それ以降のUpload Partリクエスト用のUploadIdを返します。具体的な手順は以下のとおりです：

1. **InitMultipartUploadRequest（String, String）**構造メソッドを呼び出して、InitMultipartUploadRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのinitMultipartUploadメソッドを呼び出して、InitMultipartUploadRequestを渡して、InitMultipartUploadResultオブジェクトを返します。
   （または、initMultipartUploadAsyncメソッドを呼び出して、InitMultipartUploadRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
InitMultipartUploadResult initMultipartUpload(InitMultipartUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void initMultipartUploadAsync(InitMultipartUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| cosPath                   | [オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

InitMultipartUploadResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称        | 変数説明                                                     | タイプ                |
| ------------------- | ------------------------------------------------------------ | ------------------- |
| initMultipartUpload | [リクエスト成功の戻り結果](https://cloud.tencent.com/document/product/436/7746) | InitMultipartUpload |
| httpCode            | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗                        | Int                 |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";

InitMultipartUploadRequest initMultipartUploadRequest = new InitMultipartUploadRequest(bucket, cosPath);

// 同期メソッドを使用してリクエストします
try {
    InitMultipartUploadResult initMultipartUploadResult = cosXmlService.initMultipartUpload(initMultipartUploadRequest);
    String uploadId =initMultipartUploadResult.initMultipartUpload.uploadId;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期メソッドを使用してリクエストします
cosXmlService.initMultipartUploadAsync(initMultipartUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        String uploadId = ((InitMultipartUploadResult)cosXmlResult).initMultipartUpload.uploadId;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Init Multipart Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`initMultipartUploadRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


### Upload Part

このAPIを呼び出して、マルチパートアップロードを実現します。サポートされているパート数は1 - 10000で、パートサイズは1MB - 5GBです。具体的な手順は次のとおりです：

1. **UploadPartRequest（String, String, int, String, String）**構造メソッドを呼び出して、UploadPartRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのuploadPartメソッドを呼び出して、UploadPartRequestを渡して、UploadPartResultオブジェクトを返します。
   （または、uploadPartAsyncメソッドを呼び出して、UploadPartRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
UploadPartResult uploadPart(UploadPartRequest request) throws CosXmlClientException, CosXmlServiceException;

void uploadPartAsync(UploadPartRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称       | 説明                                       | タイプ                   | 必須項目   |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String                 | はい   |
| cosPath                   | [オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String                 | はい   |
| uploadId                  | マルチパートアップロードを初期化します。uploadIdを返します                              | String                 | はい   |
| partNumber                | 1から始まるパートの番号                                    | Int                    | はい   |
| srcPath                   | ローカルファイルの絶対パス                                           | String                 | はい   |
| fileOffset                | このパートはファイルでの開始位置                                     | Long                   | いいえ   |
| contentLength             | このパートのサイズ                                             | Long                   | いいえ   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                   | いいえ   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>         | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>         | いいえ   |
| qCloudProgressListener    | アップロード進捗のコールバック                                                 | CosXmlProgressListener | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener   | いいえ   |

#### 戻り結果の説明

UploadPartResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | タイプ                                              | 変数説明 |
| ------------ | ------------------------------------------------- | -------- |
| eTag         | リクエスト成功、最終のパートを完成するために、パートファイルのMD5値を返します | String   |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗             | Int      |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
String uploadId = "パートが初期化されたときuploadIdが返される";
int partNumber = 1;//今回のアップロードパートの番号は1から始まります
String srcPath = "ローカルファイルの絶対パス";

UploadPartRequest uploadPartRequest = new UploadPartRequest(bucket, cosPath, partNumber, srcPath, uploadId);

uploadPartRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        float result = (float) (progress * 100.0/max);
        Log.w("TEST","progress =" + (long)result + "%");
    }
});

//同期メソッドを使用してアップロードします
try {
    UploadPartResult uploadPartResult = cosXmlService.uploadPart(uploadPartRequest);
    String eTag = uploadPartResult.eTag; // パートファイルのeTagを取得します
    
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

    
// 非同期コールバックリクエストを使用します
cosXmlService.uploadPartAsync(uploadPartRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        String eTag =((UploadPartResult)cosXmlResult).eTag;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Upload Part failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`uploadPartRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


### <span id = "CompleteMultiUploadRequest">Complete Multipart Upload</span>

すべてのパートをアップロードしたら、このAPIを呼び出してパート全体のアップロードを完了する必要があります。具体的な手順は次のとおりです：

1. **CompleteMultiUploadRequest（String, String, String, Map<Integer, String>）**構造メソッドを呼び出して、CompleteMultiUploadRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのcompleteMultiUploadメソッドを呼び出して、CompleteMultiUploadRequestを渡して、CompleteMultiUploadResultオブジェクトを返します。
   （または、completeMultiUploadAsyncメソッドを呼び出して、CompleteMultiUploadRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
CompleteMultiUploadResult completeMultiUpload(CompleteMultiUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void completeMultiUploadAsync(CompleteMultiUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称       | 説明                                       | タイプ                   | 必須項目   |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String                 | はい   |
| cosPath                   | [オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String                 | はい   |
| uploadId                  | マルチパートアップロードを初期化します。uploadIdを返します                              | String                 | はい   |
| partNumberAndETag         | パート番号と対応するパートMD5値                                 | Map&lt;Integer,String> | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                   | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>         | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>         | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener   | いいえ   |

#### 戻り結果の説明

CompleteMultiUploadResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称            | 変数説明                                                     | タイプ                    |
| ----------------------- | ------------------------------------------------------------ | ----------------------- |
| completeMultipartUpload | [リクエスト成功の戻り結果](https://cloud.tencent.com/document/product/436/7742) | CompleteMultipartResult |
| accessUrl               | リクエストが成功する場合、アクセスファイルのアドレスを返します                               | String                  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
String uploadId = "パートが初期化されたときuploadIdが返される";
int partNumber = 1;
String etag = "番号はpartNumberで、マルチパートアップロードが完了した後に返されたetagに対応します ";
Map<Integer, String> partNumberAndETag = new HashMap<>();
partNumberAndETag.put(partNumber, etag);

CompleteMultiUploadRequest completeMultiUploadRequest = new CompleteMultiUploadRequest(bucket, cosPath, uploadId, partNumberAndETag);

// 同期メソッドを使用してリクエストします
try {
    CompleteMultiUploadResult completeMultiUploadResult = cosXmlService.completeMultiUpload(completeMultiUploadRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.completeMultiUploadAsync(completeMultiUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Complete Multi Upload success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Complete Multi Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`completeMultiUploadRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


### List Parts

このAPIを呼び出して、特定のマルチパートアップロードでアップロードされたパートを照合するために使用されます。つまり、指定されたUploadIdが属するすべてのアップロードに成功したパートをリストするために使用されます。

1. **ListPartsRequest（String, String, String）**構造メソッドを呼び出して、ListPartsRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのlistPartsメソッドを呼び出して、ListPartsRequestを渡して、ListPartsResultオブジェクトを返します。
   （または、listPartsAsyncメソッドを呼び出して、ListPartsRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
ListPartsResult listParts(ListPartsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listPartsAsync(ListPartsRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| cosPath                   | [オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String               | はい   |
| uploadId                  | マルチパートアップロードを初期化します。uploadIdを返します                              | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

ListPartsResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                                                     | タイプ      |
| ------------ | ------------------------------------------------------------ | --------- |
| listParts    | [リクエスト成功の戻り結果](https://cloud.tencent.com/document/product/436/7747) | ListParts |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗                        | Int       |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
String uploadId = "パートが初期化されたときuploadIdが返される";

ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, cosPath, uploadId);

// 同期メソッドを使用してリクエストします
try {
    ListPartsResult listPartsResult = cosXmlService.listParts(listPartsRequest);
    ListParts listParts = listPartsResult.listParts;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します 
cosXmlService.listPartsAsync(listPartsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        ListParts listParts = ((ListPartsResult)cosXmlResult).listParts;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo List Part failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`listPartsRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


### Abort Multipart Upload

このAPIは、マルチパートアップロードの破棄を実現し、アップロードされたパートを削除するために使用されます。

1. **AbortMultiUploadRequest（String, String, String）**構造メソッドを呼び出して、AbortMultiUploadRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのabortMultiUploadメソッドを呼び出して、AbortMultiUploadRequestを渡して、AbortMultiUploadResultオブジェクトを返します。
   （または、abortMultiUploadAsyncメソッドを呼び出して、AbortMultiUploadRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
AbortMultiUploadResult abortMultiUpload(AbortMultiUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void abortMultiUploadAsync(AbortMultiUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| cosPath                   | [オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String               | はい   |
| uploadId                  | マルチパートアップロードを初期化します。uploadIdを返します                              | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

AbortMultiUploadResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、具体的には、この文章の冒頭にある[SDK異常情報の説明](#sdk_exception)を参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
String uploadId = "パートが初期化されたときuploadIdが返される";

AbortMultiUploadRequest abortMultiUploadRequest = new AbortMultiUploadRequest(bucket, cosPath, uploadId);

// 同期メソッドを使用してリクエストします
try {
    AbortMultiUploadResult abortMultiUploadResult = cosXmlService.abortMultiUpload(abortMultiUploadRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期コールバックリクエストを使用します
cosXmlService.abortMultiUploadAsync(abortMultiUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Abort Multi Upload success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Abort Multi Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`abortMultiUploadRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## ファイルの削除

### Delete Object

このAPIを呼び出して、指定されたバケットで1つのファイルを削除することができます。具体的な手順は以下のとおりです：

1. **DeleteObjectRequest（String, String)**構造メソッドを呼び出して、DeleteObjectRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのcompleteMultiUploadメソッドを呼び出して、DeleteObjectRequestを渡して、DeleteObjectResultオブジェクトを返します。
   （または、deleteObjectAsyncメソッドを呼び出して、DeleteObjectRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
DeleteObjectResult deleteObject(DeleteObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteObjectAsync(DeleteObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| cosPath                   | [オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

DeleteObjectResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket, cosPath);

// 同期メソッドを使用して削除します
try {
    DeleteObjectResult deleteObjectResult = cosXmlService.deleteObject(deleteObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します 
cosXmlService.deleteObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Delete Object success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`deleteObjectRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


### Delete Multi Objects

このAPIを呼び出すと、指定されたバケット内のファイルを一括削除することができます。1回のリクエストで最大1000ファイルを一括削除できます。具体的な手順は次のとおりです：

1. DeleteMultiObjectRequest（String, List&lt;String>）構造メソッドを呼び出して、DeleteMultiObjectRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのdeleteMultiObjectメソッドを呼び出して、DeleteMultiObjectRequestを渡して、DeleteMultiObjectResultオブジェクトを返します。
   （または、deleteMultiObjectAsyncメソッドを呼び出して、DeleteMultiObjectRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
DeleteMultiObjectResult deleteMultiObject(DeleteMultiObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteMultiObjectAsync(DeleteMultiObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| quiet                     | true：削除エラーが発生するファイル情報のみを返す；false：各ファイルの削除結果を返します | Boolean              | はい   |
| objectList                | 削除する[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)リスト | List&lt;String>      | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

DeleteMultiObjectResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
List<String> objectList = new ArrayList<String>();
objectList.add("/2/test.txt");

DeleteMultiObjectRequest deleteMultiObjectRequest = new DeleteMultiObjectRequest(bucket, objectList);
deleteMultiObjectRequest.setQuiet(true);

// 同期メソッドを使用して削除します
try {
    DeleteMultiObjectResult deleteMultiObjectResult =cosXmlService.deleteMultiObject(deleteMultiObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.deleteMultiObjectAsync(deleteMultiObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // Delete Multi Object success...
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        //  Delete Multi Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`deleteMultiObjectRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。 


## Get Object

このAPIを呼び出すと、指定されたバケットの一つのファイルをローカルにダウンロードします。具体的な手順は次のとおりです：

1. **GetObjectRequest（String, String, String）**構造メソッドを呼び出して、GetObjectRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのgetObjectメソッドを呼び出して、GetObjectRequestを渡して、GetObjectResultオブジェクトを返します。
   （または、getObjectAsyncメソッドを呼び出して、GetObjectRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetObjectResult getObject(GetObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectAsync(GetObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称       | 説明                                       | タイプ                   | 必須項目   |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String                 | はい   |
| cosPath                   | [オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String                 | はい   |
| savaPath                  | ローカルフォルダにダウンロードするファイルの絶対パス                               | String                 | はい   |
| start                     | リクエストファイルの開始位置                                           | Long                   | いいえ   |
| end                       | リクエストファイルの終了位置                                           | Long                   | いいえ   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                   | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>         | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>         | いいえ   |
| qCloudProgressListener    | ダウンロード進捗のコールバック                                                 | CosXmlProgressListener | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener   | いいえ   |

#### 戻り結果の説明

GetObjectResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
String savePath = "savePath";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePath);
getObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

//同期メソッドを使用してダウンロードします
try {
    GetObjectResult getObjectResult =cosXmlService.getObject(getObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.getObjectAsync(getObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Object success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getObjectRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。 


## オブジェクトのコピー

### Copy Object

このAPIを呼び出すと、ソースパスからターゲットパスにファイルをコピーすることを実現します。ファイルサイズは1M - 5Gで、5Gを超えるファイルは、Upload - Copyマルチパートアップロードを使用してください。具体的な手順は次のとおりです：

1. **CopyObjectRequest（String，String, CopySourceStruct）**構造メソッドを呼び出して、CopyObjectRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのcopyObject メソッドを呼び出して、CopyObjectRequestを渡して、CopyObjectResultオブジェクトを返します。
   （または、copyObjectAsyncメソッドを呼び出して、CopyObjectRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
CopyObjectResult copyObject(CopyObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(CopyObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| cosPath                   | ターゲット[オブジェクト鍵](https://cloud.tencent.com/document/product/436/13324)、すなわち、COSに格納されているファイルの絶対パス | String               | はい   |
| copySourceStruct          | ソースパス構造体                                                 | CopySourceStruct     | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

CopyObjectResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ       |
| ------------ | ------------------------------------- | ---------- |
| copyObject   | コピー結果情報を返します                      | CopyObject |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int        |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct("ソースファイルのappid",
        "ソースファイルのbucket", "ソースファイルregion", "ソースファイルのcosPath");

CopyObjectRequest copyObjectRequest = null;
try {
    copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}

// 同期メソッドを使用します
try {
    CopyObjectResult copyObjectResult = cosXmlService.copyObject(copyObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Copy Object success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Copy Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`copyObjectRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。 


### パートコピー

具体的な手順：

1. cosXmlService.initMultipartUpload(InitMultipartUploadRequest)を呼び出して、パートを初期化します。[InitMultipartUploadRequest初期化パート](#InitMultipartUploadRequest)を参照してください。
2. cosXmlService.copyObject(UploadPartCopyRequest)を呼び出して、パートコピーを完成します。
3. cosXmlService.completeMultiUpload(CompleteMultiUploadRequest)を呼び出して、パートコピーを完成します。[CompleteMultiUploadRequestパートコピーの完成](#CompleteMultiUploadRequest)を参照してください。

### UploadPartCopyRequest説明

```java
UploadPartCopyResult copyObject(UploadPartCopyRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(UploadPartCopyRequest request,final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称       | 説明                                       | タイプ                   | 必須項目   |
| ------------------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String                 | はい   |
| cosPath                   | オブジェクト鍵、すなわち、COSに格納されているファイルの絶対パス                            | String                 | はい   |
| uploadId                  | マルチパートアップロードを初期化します。uploadIdを返します                              | String                 | はい   |
| partNumber                | 1から始まるパートの番号                                      | Int                    | はい   |
| copySourceStruct          | ソースパス構造体                                                 | CopySourceStruct       | はい   |
| start                     | このパートはソースファイルでの開始位置                                   | Long                   | いいえ   |
| end                       | このパートはソースファイルでの終了位置                                   | Long                   | いいえ   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                   | いいえ   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set<String>            | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set<String>            | いいえ   |
| qCloudProgressListener    | アップロード進捗のコールバック                                                 | CosXmlProgressListener | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener   | いいえ   |

#### 戻り結果の説明

CopyObjectResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ       |
| ------------ | ------------------------------------- | ---------- |
| copyObject   | コピー結果情報を返します                      | CopyObject |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int        |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct("ソースファイルのappid",
        "ソースファイルのbucket", "ソースファイルのregion", "ソースファイルのcosPath");
String uploadId = "パートのuploadIdを初期化します";
int partNumber = 1; //パート番号
long start = 0;//ソースファイルの開始位置をコピーします
long end = 100; //ソースファイルの終了位置をコピーします
UploadPartCopyRequest uploadPartCopyRequest = null;
try {
    uploadPartCopyRequest = new UploadPartCopyRequest(bucket, cosPath, partNumber,  uploadId, copySourceStruct， start, end);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}

// 同期メソッドを使用します
try {
    UploadPartCopyResult uploadPartCopyResult = cosXmlService.copyObject(uploadPartCopyRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.copyObjectAsync(uploadPartCopyRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Copy Object success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Copy Object failed because of CosXmlClientException or CosXmlServiceException..
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`uploadPartCopyRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。 


## Head Object

このAPIを呼び出すと、指定されたバケットのオブジェクトが存在しているかどうかを確認します。具体的な手順は次のとおりです：

1. HeadObjectRequest（String, string）構造メソッドを呼び出して、HeadObjectRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのheadObjectメソッドを呼び出して、HeadObjectRequestを渡して、HeadObjectResultオブジェクトを返します。
   （または、headObjectAsyncメソッドを呼び出して、HeadObjectRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
HeadObjectResult headObject(HeadObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void headObjectAsync(HeadObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| cosPath                   | オブジェクト鍵、すなわち、COSに格納されているファイルの絶対パス                            | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

HeadObjectResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath"
HeadObjectRequest headObjectRequest = new HeadObjectRequest(bucket, cosPath);

//同期メソッドを使用します
try {
    HeadObjectResult headObjectResult = cosXmlService.headObject(headObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 非同期コールバックリクエストを使用します
cosXmlService.headObjectAsync(headObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Head Bucket success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Head Bucket failed because of CosXmlClientException or CosXmlServiceException..
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`headObjectRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。 


## Put Object ACL

このAPIを呼び出すと、バケットのオブジェクトのアクセス制御権限を指定することができます。具体的な手順は次のとおりです：

1. **PutObjectACLRequest(String, string)**構造メソッドを呼び出して、PutObjectACLRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのputObjectACLメソッドを呼び出して、PutObjectACLRequestを渡して、PutObjectACLResultオブジェクトを返します。
   （または、putObjectACLAsyncメソッドを呼び出して、PutObjectACLRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
PutObjectACLResult putObjectACL(PutObjectACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectACLAsync(PutObjectACLRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| cosPath                   | オブジェクト鍵、すなわち、COSに格納されているファイルの絶対パス                            | String               | はい   |
| xcosACL                   | バケットのアクセス権限を設定します。有効値：private、public-read-write、public-read；デフォルト値：private | String               | いいえ   |
| xcosGrantRead             | 権限が付与された者の読み取り権限                                         | ACLAccount           | いいえ   |
| xcosGrantWrite            | 権限が付与された者の書き込み権限                                         | ACLAccount           | いいえ   |
| xcosGrantRead             | 権限が付与された者の読み取り権限                                       | ACLAccount           | いいえ   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

PutObjectACLResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称 | 変数説明                              | タイプ |
| ------------ | ------------------------------------- | ---- |
| httpCode     | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗 | Int  |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
PutObjectACLRequest putObjectACLRequest = new PutObjectACLRequest(bucket, cosPath);

//バケットアクセス権限を設定します
putObjectACLRequest.setXCOSACL("public-read");

//権限が付与された者に読み取り権限を付与します
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "SubUin");
putObjectACLRequest.setXCOSGrantRead(readACLS);

//権限が付与された者に書き込み権限を付与します
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("OwnerUin", "SubUin");
putObjectACLRequest.setXCOSGrantRead(writeACLS);

//権限が付与された者に読み書き権限を付与します
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "SubUin");
putObjectACLRequest.setXCOSGrantRead(writeandReadACLS);

// 同期メソッドを使用します
try {
    PutObjectACLResult putObjectACLResult = cosXmlService.putObjectACL(putObjectACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期コールバックリクエストを使用します
cosXmlService.putObjectACLAsync(putObjectACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket ACL success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`putObjectACLRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## Get Object ACL

このAPIは、バケットの中で指定されたオブジェクトのACLを取得するために使用されます。具体的な手順は次のとおりです：

1. **GetObjectACLRequest(String, string)**構造メソッドを呼び出して、GetObjectACLRequestオブジェクトをインスタンス化します。
2. CosXmlServiceのgetObjectACLメソッドを呼び出して、GetObjectACLRequestを渡して、GetObjectACLResultオブジェクトを返します。
   （または、getObjectACLAsyncメソッドを呼び出して、GetObjectACLRequestとCosXmlResultListenerを渡して、非同期コールバック操作を行います）。

```java
GetObjectACLResult getObjectACL(GetObjectACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectACLAsync(GetObjectACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### パラメータ説明

| パラメータ名称                  | パラメータ説明                                                     | タイプ                 | 必須項目 |
| ------------------------- | ------------------------------------------------------------ | -------------------- | ---- |
| bucket                    | バケット名称（COS XML APIのバケットフォーマット：`<BucketName-APPID>`、例えば、examplebucket-1250000000） | String               | はい   |
| cosPath                   | オブジェクト鍵、すなわち、COSに格納されているファイルの絶対パス                            | String               | はい   |
| signDuration              | 署名の有効期間、単位は秒です                                       | Long                 | はい   |
| checkHeaderListForSign    | 署名で検証必要なリクエストヘッダー                                       | Set&lt;String>       | いいえ   |
| checkParameterListForSing | 署名で検証必要なリクエストパラメータ                                     | Set&lt;String>       | いいえ   |
| cosXmlResultListener      | アップロード結果のコールバック                                                 | CosXmlResultListener | いいえ   |

#### 戻り結果の説明

GetObjectACLResultオブジェクトのメンバー変数を通して、リクエスト結果を返します。

| メンバー変数名称        | 変数説明                                                     | タイプ                |
| ------------------- | ------------------------------------------------------------ | ------------------- |
| accessControlPolicy | [権限が付与された者の情報と権限情報](https://cloud.tencent.com/document/product/436/7733) | AccessControlPolicy |
| httpCode            | [200, 300)の間でリクエスト成功、そうではなければ、リクエスト失敗                        | Int                 |

> ?CosClientExceptionまたはCosServiceException異常をスローした場合、詳細については、この文章の[SDK異常情報の説明](#sdk_exception)セクションを参照してください。

#### 例

```java
String bucket = "bucket";
String cosPath = "cosPath";
GetObjectACLRequest getBucketACLRequest = new GetObjectACLRequest(bucket, cosPath);

// 同期メソッドを使用します
try {
    GetObjectACLResult getObjectACLResult = cosXmlService.getObjectACL(getBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// 非同期コールバックリクエストを使用します
cosXmlService.getObjectACLAsync(getBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket ACL success
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> ?リクエスト場合、計算された署名文字列を直接設定する必要がある場合は、`getBucketACLRequest.setSign("計算された署名文字列")`を呼び出して設定できます。デフォルトでは、sdkにより署名文字列を計算します。


## 高レベルAPI説明

## <span id = "upload_task">高レベルAPIによるファイルアップロード（推薦）</span>

**TransferManager**、**COSXMLUploadTask**は、簡単なアップロード、マルチパートアップロードAPIの非同期リクエストをカプセル化し、アップロードリクエストの一時停止、再開、キャンセル、および継続送信をサポートします。この方法でファイルをアップロードすることをお勧めします。サンプルコードは次のとおりです：

```java
//TransferConfigを初期化します
TransferConfig transferConfig = new TransferConfig.Builder().build();

/*特別な要件がある場合は、次のように初期化をカスタマイズできます。ファイル >= 2Mの場合、マルチパートアップロードを有効にして、且つマルチパートアップロードのパートサイズが1Mになります。ソースファイルが5Mより大きい場合、パートコピーを有効にして、且つパートコピーのサイズが5Mになります。*/
TransferConfig transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) //パートでコピーされたファイルの最小サイズを有効にするかどうか
        .setSliceSizeForCopy(5 * 1024 * 1024) //パートでコピーするときのパートサイズ
        .setDivisionForUpload(2 * 1024 * 1024) //マルチパートアップロードされたファイルの最小サイズを有効にするかどうか
        .setSliceSizeForCopy(1024 * 1024) //マルチパートアップロードするときのパートサイズ
        .build();


//TransferManagerを初期化します
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "バケット名称";
String cosPath = "オブジェクト鍵"; //すなわち、 //cosPath = "test.txt"のフォーマットでCOSに格納されているファイルの絶対パス"；
String srcPath = "ローカルファイルの絶対パス"; //例えば：srcPath=Environment.getExternalStorageDirectory().getPath() + "/test.txt";
String uploadId = null; //マルチパートアップロードを初期化するUploadIdが存在する場合、割り当て値に対応するuploadId値が継続送信に使用され、それ以外の場合、割り当て値はnullです。
//ファイルのアップロード
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);

/**
* バイト配列をアップロードする場合は、TransferManagerのupload（string、string、byte []）メソッドを呼び出して実現できます；
* byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
*/

/**
* バイトストリームをアップロードする場合は、TransferManagerのupload（String、String、InputStream）メソッドを呼び出して実現できます；
* InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, inputStream);
*/

//アップロード進捗のコールバックを設定します
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
//返し結果のコールバックを設定します
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//タスク状態のコールバックを設定することでタスクプロセスを確認できます。
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
特殊な要件があれば、次の操作ができます：
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region); //バケットが所在するキャンパスを設定します
 putObjectRequest.setNeedMD5(true); //Md5検証を有効にするかどうか
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

//アップロードをキャンセルします
cosxmlUploadTask.cancel();


//アップロードを中止します
cosxmlUploadTask.pause();

//アップロードを回復します
cosxmlUploadTask.resume();

```

## <span id = "download_task">高レベルAPIファイルダウンロード（推薦）</span>

**TransferManager**、**COSXMLDownloadTask**は、ダウンロードAPIの非同期リクエストをカプセル化し、ダウンロードリクエストの一時停止、再開、キャンセル、およびブレークポイントのダウンロードをサポートします。サンプルコードは次のとおりです。

```java
Context applicationContext = "applicationコンテキスト"； // getApplicationContext()
String bucket = "バケット名称"; //ファイルが所在するバケット
String cosPath = "オブジェクト鍵"; //すなわち、 //cosPath = "test.txt"のフォーマットでファイルをCOSに格納されている絶対パス；
String savedDirPath = "ファイルをローカルフォルダパスにダウンロードします"；
String savedFileName = "ローカルにダウンロードされたファイル名"；//入力しない場合（null）、cosのファイル名と同じ
//ファイルのダウンロード
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savedDirPath, savedFileName);
//ダウンロード進捗コールバックを設定します
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
//返し結果のコールバックを設定します
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//タスク状態のコールバックを設定することでタスクプロセスを確認できます。
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
特殊な要件があれば、次の操作ができます：
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, localDir, localFileName);
getObjectRequest.setRegion(region); //バケットが所在するキャンパスを設定します
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(context, getObjectRequest);
*/

//ダウンロードをキャンセルします
cosxmlDownloadTask.cancel();

//ダウンロードを中止します
cosxmlDownloadTask.pause();

//ダウンロードを回復します
cosxmlDownloadTask.resume();

```

## <span id = "copy_task">高レベルAPIファイルコピー（推薦）</span>

**TransferManager**、**COSXMLCopyTask**は、簡単なコピー、パートコピーAPIの非同期リクエストをカプセル化し、コピーリクエストの一時停止、再開、キャンセルをサポートします。サンプルコードは次のとおりです。

```java
String bucket = "バケット名称"; //ターゲットファイルのバケット
String cosPath = "オブジェクト鍵"; //すなわち、 //cosPath = "test.txt"のフォーマットでターゲットファイルをCOSに格納されている絶対パス；
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(
                "ソースファイルバケットが所在するappid", "ソースファイルバケット", "ソースファイルバケットが所在するキャンパス", "ソースファイルのオブジェクト鍵");//ソースファイルが所在するcosの位置説明
//ファイルのコピー
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath, copySourceStruct);
//返し結果のコールバックを設定します
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                Log.d("TEST",  "Success: " + result.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
//タスク状態のコールバックを設定することでタスクプロセスを確認できます。
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });
/**
特殊な要件があれば、次の操作ができます：
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
copyObjectRequest.setRegion(region); //バケットが所在するキャンパスを設定します
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(copyObjectRequest);
*/

//コピーをキャンセルします
cosxmlCopyTask.cancel();


//コピーを中止します
cosxmlCopyTask.pause();

//コピーを再開します
cosxmlCopyTask.resume();
```

## 事前署名リンクを生成します

CosXmlServiceのgetPresignedURL(CosXmlRequest)メソッドを呼び出して、対応するリクエストの事前署名リンクを取得します

String getPresignedURL(CosXmlRequest cosXmlRequest) throws CosXmlClientException

```java
try{
String urlWithSign = cosXml.getPresignedURL(putObjectRequest);
}catch(Exception ex){
Log.d("TEST", ex.getMessage());
}
```

## <span id = "sdk_exception">SDK異常情報説明</span>

SDKの中で、APIを呼び出してCOSオブジェクトの操作に失敗した場合、CosXmlClientExceptionまたはCosXmlServiceException異常をスローします。

### CosXmlClientException

クライアント異常、クライアントの原因でサーバーとの正常な対話を完了できないことによる失敗（例えば、クライアントがサーバーに接続できず、サーバーから返されたデータを解析できず、ローカルファイルの読み取りにIO異常が発生した）を指すために使用されます。CosXmlClientExceptionは、Exceptionから統合されました。使用方法はExceptionと同じで、同時に、以下のようなメンバーerrorCodeをもう1つ追加します。

| メンバー      | 説明                                  | タイプ |
| --------- | ------------------------------------- | ---- |
| errorCode | クライアントエラーコード、例えば、10000はパラメータ検証失敗と示します | int  |

### CosXmlServiceException

CosXmlServiceExceptionサービス異常は、対話は正常に完了したが、操作が失敗したシナリオを指すために使用されます。例えば、クライアントが存在しないバケットにアクセスし、存在しないファイルを削除し、ある操作を実行する権限を有さず、サーバー故障異常などです。CosXmlServiceExceptionには、サーバーから返されたステータスコード、requesttid、エラーの詳細などが含まれています。異常をキャプチャした後、必要なトラブルシューティング要因を含む異常全体を印刷することをお勧めします。以下は、異常メンバー変数の説明です：

| メンバー         | 説明                                                         | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| requestId    | リクエストIDであり、リクエストを表すために使用され、トラブルシューティングに非常に重要です。            | String |
| statusCode   | 応答のステータスコードであり、4xxはクライアントによるリクエストの失敗を指し、5xxはサーバー異常による失敗です。[COSエラー情報](https://cloud.tencent.com/document/product/436/7730)を参照してください。 | String |
| errorCode    | リクエストが失敗した時にボディにより返されたError Codeについて、[COSエラー情報](https://cloud.tencent.com/document/product/436/7730)を参照してください。 | String |
| errorMessage | リクエストが失敗した時にボディにより返されたError Messageについて、[COSエラー情報](https://cloud.tencent.com/document/product/436/7730)を参照してください。 | String |

