## 基本APIの説明
> 本書に記載されるSecretId、SecretKey、Bucketなどの名前の意味と取得方法について[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

### バケットリストの取得
#### 方法のプロトタイプ
```php
public Guzzle\Service\Resource\Model listBucket(array $args = array())
```

####　リクエスト例

```php
//バケットリストの取得
$result = $cosClient->listBuckets();
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/3210232098:uin/3210232098
                    [DisplayName] => 3210232098
                )

            [Buckets] => Array
                (
                    [0] => Array
                        (
                            [Name] => accesslog-10055004
                            [Location] => ap-shanghai
                            [CreationDate] => 2016-07-29T03:09:54Z
                        )

                    [1] => Array
                        (
                            [Name] => accesslogbj-10055004
                            [Location] => ap-beijing
                            [CreationDate] => 2017-08-02T04:00:24Z
                        )

                )

            [RequestId] => NWE3YzgxZmFfYWZhYzM1MGFfMzc3MF9iOGY5OQ==
        )

)
```
### Bucketの作成

#### 方法のプロトタイプ

```php
// バケットの作成
public Guzzle\Service\Resource\Model createBucket(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :---------: |    :-----------------: | :--------:   | :-------------: |
| Bucket   |      バケット名    |    string     |  はい              |
| ACL      |         ACL権限のコントロール         |    string     | いいえ           | 

####　リクエスト例

```php
//バケットの作成
//バケットの命名規則は{name}-{appid}です。ここに入力するバケット名はこのフォーマットでなければなりません
$result = $cosClient->createBucket(array('Bucket' => 'testbucket-125000000'));
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Location] => 
            [RequestId] => NWE3YzgzMTZfMTdiMjk0MGFfNTQ1OF8xNjEyYmE=
        )
)
```
### バケットの削除

#### 方法のプロトタイプ

```php
// バケットの削除
public Guzzle\Service\Resource\Model deleteBucket(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: |    :------------: |  :--------:   | :----------------------------------: |
| Bucket  |  バケット名        |     string         |         はい                     |

####　リクエスト例

```php
//バケットの削除
//バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません。
$result = $cosClient->deleteBucket(array('Bucket' => 'testbucket-125000000'));
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzgzMTZfMTdiMjk0MGFfNTQ2MF8xNjBjZTI=
        )
)
```
### 簡単なファイルアップロード

#### 方法のプロトタイプ

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  バケット名は数字、アルファベット小文字とハイフン「-」より構成されます | string |   はい |
 |  Body  | アップロードするファイルの内容はファイルストリームまたはバイトストリームです |  file/string |  はい |
 |  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String |  はい | 
 |  ACL  | ファイルのACLを設定します。例えば'private、public-read'、'public-read-write' | string |   いいえ | 
 |  GrantFullControl  |指定されたアカウントのファイルへの読み書き権限の付与 |  string |  いいえ | 
 |  GrantRead  |  指定されたアカウントのファイルへの読み取り権限の付与 | string |  いいえ |
 |  GrantWrite  |  指定されたアカウントのファイルへの書き込み権限の付与 | string |  いいえ |
 |  StorageClass  |  ファイルのストレージタイプ（STANDARD、STANDARD_IA）の設定。デフォルト値：STANDARD | String |   いいえ |
 |  Expires  | Content-Expiresの設定 | string|  いいえ | 
 |  CacheControl  |  キャッシュポリシー、Cache-Controlの設定 | string |   いいえ |
 |  ContentType  | 内容タイプ、Content-Typeの設定 |String |   いいえ |  
 |  ContentDisposition  |  ファイル名、Content-Dispositionの設定 | string |   いいえ |
 |  ContentEncoding  |  エンコードフォーマット、Content-Encodingの設定 | string |   いいえ |
 |  ContentLanguage  |  言語タイプ、Content-Languageの設定 | string |   いいえ |
 |  ContentLength  | 伝送長さの設定 | string |   いいえ | 
 |  ContentMD5  | 検証するためにアップロードされたファイルのMD5値の設定 | string |   いいえ | 
 |  Metadata | ユーザー設定のファイルのメタ情報 | array |   いいえ |
 |  ServerSideEncryption | サーバーの暗号化方式 | string |   いいえ |

####　リクエスト例
```php
# ファイルのアップロード
## putObject（アップロードAPI、最大5GBのファイルアップロードをサポートします）。
## 現在のアクセスポリシーエントリは1000に制限され、オブジェクトACL制御を行う必要がない場合、設定しないでください。デフォルトではバケット権限を継承します。
### メモリ内の文字列のアップロード。
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### ファイルストリームのアップロード
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => fopen($local_path, 'rb')));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### headerとmetaの設定
try {
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => fopen($local_path, 'rb'),
        'CacheControl' => 'string',
        'ContentDisposition' => 'string',
        'ContentEncoding' => 'string',
        'ContentLanguage' => 'string',
        'ContentLength' => integer,
        'ContentType' => 'string',
        'Expires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'GrantFullControl' => 'string',
        'GrantRead' => 'string',
        'GrantWrite' => 'string',
        'Metadata' => array(
            'string' => 'string',
        ),
        'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Expiration] => 
            [ETag] => "ed076287532e86365e841e92bfc50d8c"
            [ServerSideEncryption] => AES256
            [VersionId] => 
            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [RequestCharged] => 
            [RequestId] => NWE3Yzg0M2NfOTcyMjViNjRfYTE1YV8xNTQzYTY=
            [ObjectURL] => http://testbucket-1252448703.cos.cn-south.myqcloud.com/11%2F%2F32%2F%2F43
        )
)
```

### パートファイルのアップロード

パートファイルのアップロードは、ファイアを複数のパートに分割してアップロードし、複数のパートを同時にアップロードすることができ、最大40TBをサポートします。

パートファイルアップロード手順は以下のとおりです：

1. マルチパートアップロードを初期化し、uploadidを取得します、（createMultipartUpload）。
2. パートデータを（同時に）アップロードします、（uploadPart）。
3. マルチパートアップロードを完了します、（completeMultipartUpload）。

また、マルチパートアップロードの取得（listParts）、マルチパートアップロードの終了（abortMultipartUpload）も含まれます。

#### 方法のプロトタイプ

```php
// マルチパートアップロードを初期化します
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());

// データパートをアップロードします
public Guzzle\Service\Resource\Model uploadPart(array $args = array());
            
// マルチパートアップロードを完了します
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());

// アップロードされたパートをリストします
public Guzzle\Service\Resource\Model listParts(array $args = array());

// マルチパートアップロードを終了します
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```
### ファイルのアップロード
####　リクエスト例
```php
## Upload（ハイレベルのアップロードAPI、デフォルトではマルチパートアップロードは最大50TBをサポートします）
## 現在のアクセスポリシーエントリは1000に制限され、オブジェクトACL制御を行う必要がない場合、設定しないでください。デフォルトではバケット権限を継承します。
### メモリ内の文字列のアップロード
try {
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = 'Hello World!');
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### ファイルストリームのアップロード
try {
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = fopen($local_path, 'rb'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### headerとmetaの設定
try {
    $result = $cosClient->Upload(
        $bucket= $bucket,
        $key = $key,
        $body = fopen($local_path, 'rb'),
        $options = array(
            'CacheControl' => 'string',
            'ContentDisposition' => 'string',
            'ContentEncoding' => 'string',
            'ContentLanguage' => 'string',
            'ContentLength' => integer,
            'ContentType' => 'string',
            'Expires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
            'GrantFullControl' => 'string',
            'GrantRead' => 'string',
            'GrantWrite' => 'string',
            'Metadata' => array(
                'string' => 'string',
            ),
            'StorageClass' => 'string'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

```

>?単一ファイルが5M未満の場合、単一ファイルを使用してアップロードします。5M以上となれば、シャードアップロードを使用します。

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Location] => testbucket-1252448703.cos.cn-south.myqcloud.com/111.txt
            [Bucket] => testbucket
            [Key] => 111.txt
            [ETag] => "715691804ee474f2eb94adb2c5c01155-1"
            [Expiration] => 
            [ServerSideEncryption] => AES256
            [VersionId] => 
            [SSEKMSKeyId] => 
            [RequestCharged] => 
            [RequestId] => NWE3Yzg0YTRfOTUyMjViNjRfNWYyZF8xNTI5ZDQ=
        )
)
```
### ファイルのダウンロード

ファイルをローカルまたはメモリにダウンロードします。

#### 方法のプロトタイプ

```php
// ファイルのダウンロード
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: |    :------------:   | :--------:   | :----------------------------------: |
| Bucket   |      バケット名               |   string     | はい           |       
| Key      |   オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです         |    string      | はい           |       
| SaveAs   |   ローカルに保存するローカルファイルのパス                 |   string      | いいえ           |
| VersionId     |   オブジェクトのバージョン番号        |   string      | いいえ           |       

####　リクエスト例

```php
# ファイルのダウンロード
## getObject（ファイルのダウンロード）
### メモリにダウンロード
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key));
    echo($result['Body']);
} catch (\Exception $e) {
    echo "$e\n";
}

### ローカルにダウンロード
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

### ダウンロード範囲の指定
/*
 * Rangeフィールドのフォーマットは'bytes=a-b'です
 */
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}

### headerへ戻る設定
try {
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'ResponseCacheControl' => 'string',
        'ResponseContentDisposition' => 'string',
        'ResponseContentEncoding' => 'string',
        'ResponseContentLanguage' => 'string',
        'ResponseContentType' => 'string',
        'ResponseExpires' => 'mixed type: string (date format)|int (unix timestamp)|\DateTime',
        'SaveAs' => $local_path));
} catch (\Exception $e) {
    echo "$e\n";
}
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Body] =>
            [DeleteMarker] => 
            [AcceptRanges] => bytes
            [Expiration] => 
            [Restore] => 
            [LastModified] => Fri, 09 Feb 2018 01:10:56 GMT
            [ContentLength] => 5242880
            [ETag] => "715691804ee474f2eb94adb2c5c01155-1"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => private
            [ContentDisposition] => attachment; filename*="UTF-8''111.txt"
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentRange] => 
            [ContentType] => text/plain; charset=utf-8
            [Expires] => 
            [WebsiteRedirectLocation] => 
            [ServerSideEncryption] => AES256
            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWE3Yzg4ODlfMThiMjk0MGFfMmI3OV8xNWQxNDg=
        )
)
```

### ファイルの削除

COS上のオブジェクトを削除します。

#### 方法のプロトタイプ

```php
// ファイルを削除します
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   | 
| Bucket   |                バケット名               |   string     |  はい           | 
| Key      |         オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです         |    string      | はい           |   
| VersionId      |         オブジェクトのバージョン番号        |   string    | いいえ           |  

####　リクエスト例

```php
// COSオブジェクトを削除します
$result = $cosClient->deleteObject(array(
    //バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
    'Bucket' => 'testbucket-125000000',
    'Key' => 'hello.txt'));
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [DeleteMarker] => 
            [VersionId] => 
            [RequestCharged] => 
            [RequestId] => NWE3Yzg5MzJfY2FhMzNiMGFfNDVjOV8yY2QyMzg=
        )
)
```


### オブジェクトの属性を取得します

照合によりCOS上のオブジェクトの属性を取得します。

#### 方法のプロトタイプ

```php
// ファイル属性を取得します
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |    バケット名     |    string   | はい           |   
| Key      |         オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです         |    string      | はい           |    
| VersionId      |          オブジェクトのバージョン番号        |   string    | いいえ           | 

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [DeleteMarker] => 
            [AcceptRanges] => 
            [Expiration] => 
            [Restore] => 
            [LastModified] => Thu, 08 Feb 2018 17:34:53 GMT
            [ContentLength] => 12
            [ETag] => "ed076287532e86365e841e92bfc50d8c"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => 
            [ContentDisposition] => 
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentType] => application/octet-stream
            [Expires] => 
            [WebsiteRedirectLocation] => 
            [ServerSideEncryption] => AES256
            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWE3YzhhM2RfMWViZTk0MGFfNWMzMF8xNTFiZDg=
        )
)
```

####　リクエスト例

```php
// COSファイル属性を取得します
 //バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
$result $cosClient->headObject(array('Bucket' => 'testbucket-125000000', 'Key' => 'hello.txt'));
```

### バケットの存在を照合します

照合によりCOS上のバケットが存在するかどうかを取得します。

#### 方法のプロトタイプ

```php
// ファイル属性を取得します
public Guzzle\Service\Resource\Model headBucket(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |     オブジェクトのバージョン番号      |   string   | はい           |      



####　リクエスト例

```php
// COSファイル属性を取得します
 //バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
$result $cosClient->headBucket(array('Bucket' => 'testbucket-125000000'));
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzhhN2VfY2VhMzNiMGFfMmNmXzJjNzc3Zg==
        )
)
```

### ファイルリストの取得

照合によりCOS上のファイルリストを取得します

#### 方法のプロトタイプ


```php
// ファイルリストの取得
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |       バケット名               |    string     |はい           |     
| Delimiter      |      区切り記号         |    string     |  いいえ          |    
| Marker      |          タグ        |   string     |  いいえ          | 
| MaxKeys      |           最大オブジェクト数         |  int     |   いいえ          | 
| Prefix      |            プレフィックス         |string     |  いいえ           |  

####　リクエスト例

```php
// バケット内のメンバーを取得します。
//バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません。
$result = $cosClient->listObjects(array('Bucket' => 'testbucket-125000000'));
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Name] => testbucket-1252448703
            [Prefix] => 
            [Marker] => 
            [MaxKeys] => 1000
            [IsTruncated] => 
            [Contents] => Array
                (
                    [0] => Array
                        (
                            [Key] => 11/32/43
                            [LastModified] => 2018-02-08T17:09:16.000Z
                            [ETag] => "ed076287532e86365e841e92bfc50d8c"
                            [Size] => 12
                            [Owner] => Array
                                (
                                    [ID] => 1252448703
                                    [DisplayName] => 1252448703
                                )

                            [StorageClass] => STANDARD
                        )

                    [1] => Array
                        (
                            [Key] => 111
                            [LastModified] => 2018-02-08T17:41:11.000Z
                            [ETag] => "ed076287532e86365e841e92bfc50d8c"
                            [Size] => 12
                            [Owner] => Array
                                (
                                    [ID] => 1252448703
                                    [DisplayName] => 1252448703
                                )

                            [StorageClass] => STANDARD
                        )

                    [2] => Array
                        (
                            [Key] => 111.txt
                            [LastModified] => 2018-02-08T17:11:00.000Z
                            [ETag] => "715691804ee474f2eb94adb2c5c01155-1"
                            [Size] => 5242880
                            [Owner] => Array
                                (
                                    [ID] => 1252448703
                                    [DisplayName] => 1252448703
                                )

                            [StorageClass] => STANDARD
                        )

                )

            [RequestId] => NWE3YzhiYjdfMWJiMjk0MGFfMzA4M18xNjdiNDM=
        )
)
```

### putBucketACL

#### 方法のプロトタイプ

```php
// バケットの権限リストを設定します
public Guzzle\Service\Resource\Model putBucketAcl(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |              バケット名               |     string      | はい           | 
| ACL      |        ACL権限のコントロール         |   string       | いいえ           |   
| GrantRead |       権限が付与された者の読み取り権限。フォーマット：id=" ",id=" "；サブアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"。ルートアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"。例えば、'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |  string       | いいえ           |     
| GrantWrite  |      権限が付与された者の書き込み権限。フォーマット：id=" ",id=" "；サブアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"。ルートアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"。例えば、'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'       |     string        | いいえ          |      
| GrantFullControl |  権限が付与された者の読み書き権限。フォーマット：id=" ",id=" "；サブアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"。ルートアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"。例えば、'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |   string       | いいえ           |          


####　リクエスト例

```php
#putBucketACL
try {
    $result = $cosClient->putBucketAcl(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',
        'Grants' => array(
            array(
                'Grantee' => array(
                    'DisplayName' => 'qcs::cam::uin/327874225:uin/327874225',
                    'ID' => 'qcs::cam::uin/327874225:uin/327874225',
                    'Type' => 'CanonicalUser',
                ),
                'Permission' => 'FULL_CONTROL',
            ),
            // ... repeated
        ),
        'Owner' => array(
            'DisplayName' => 'qcs::cam::uin/3210232098:uin/3210232098',
            'ID' => 'qcs::cam::uin/3210232098:uin/3210232098',
        ),));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzhiZTZfZDRiMjk0MGFfODMwXzJjODllYw==
        )
)
```


### getBucketACL
#### 方法のプロトタイプ

```php
// バケットの権限リストを取得します
public Guzzle\Service\Resource\Model getBucketAcl(array $args = array());
```

#### リクエストパラメータ

| フィールド名   |       タイプ     | デフォルト値 | 必須項目 |                  説明                 |
| :------: |    :------------: | :--:   | :--------:   | :----------------------------------: |
| Bucket   |     string     |  なし    | はい           |               バケット名               |



####　リクエスト例
```php
#getBucketACL
try {
    $result = $cosClient->getBucketAcl(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/3210232098:uin/3210232098
                    [DisplayName] => qcs::cam::uin/3210232098:uin/3210232098
                )

            [Grants] => Array
                (
                    [0] => Array
                        (
                            [Grantee] => Array
                                (
                                    [ID] => qcs::cam::uin/327874225:uin/327874225
                                    [DisplayName] => qcs::cam::uin/327874225:uin/327874225
                                )

                            [Permission] => FULL_CONTROL
                        )

                )

            [RequestId] => NWE3YzhjMTRfYzdhMzNiMGFfYjdiOF8yYzZmMzU=
        )
)
```

### putObjectACL

現在のアクセスポリシーエントリは1000件までとします。オブジェクトACLのコントロールが必要とされない場合、設定しないでください。デフォルトでBucket権限が継承されます。

#### 方法のプロトタイプ

```php
// オブジェクトの権限リストを設定します
public Guzzle\Service\Resource\Model putObjectAcl(array $args = array());
```

#### リクエストパラメータ
| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |              バケット名               |     string      | はい           | 
 |  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String |  はい | 
| ACL      |        ACL権限のコントロール         |   string       | いいえ           |   
| GrantRead |       権限が付与された者の読み取り権限。フォーマット：id=" ",id=" "；サブアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"。ルートアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"。例えば、'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |  string       | いいえ           |     
| GrantWrite  |      権限が付与された者の書き込み権限。フォーマット：id=" ",id=" "；サブアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"。ルートアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"。例えば、'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'       |     string        | いいえ          |      
| GrantFullControl |  権限が付与された者の読み書き権限。フォーマット：id=" ",id=" "；サブアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"。ルートアカウントに権限を付与する時、id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"。例えば、'id="qcs::cam::uin/123:uin/123", id="qcs::cam::uin/123:uin/456"'         |   string       | いいえ           |          


####　リクエスト例
```php
#putObjectACL
try {
    $result = $cosClient->putObjectAcl(array(
        'Bucket' => 'testbucket-1252448703',
        'Key' => '111.txt',
        'Grants' => array(
            array(
                'Grantee' => array(
                    'DisplayName' => 'qcs::cam::uin/327874225:uin/327874225',
                    'ID' => 'qcs::cam::uin/327874225:uin/327874225',
                    'Type' => 'CanonicalUser',
                ),
                'Permission' => 'FULL_CONTROL',
            ),
            // ... repeated
        ),
        'Owner' => array(
            'DisplayName' => 'qcs::cam::uin/3210232098:uin/3210232098',
            'ID' => 'qcs::cam::uin/3210232098:uin/3210232098',
        ),));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] => 
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### getObjectACL
#### 方法のプロトタイプ

```php
// オブジェクトの権限リストを取得します
public Guzzle\Service\Resource\Model getObjectAcl(array $args = array());
```

#### リクエストパラメータ

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |          バケット名               |   string     | はい           |        
| Key      |         オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです         |    string      | はい           |        

####　リクエスト例
```php
#getObjectACL
try {
    $result = $cosClient->getObjectAcl(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',
        'Key' => '11'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/3210232098:uin/3210232098
                    [DisplayName] => qcs::cam::uin/3210232098:uin/3210232098
                )

            [Grants] => Array
                (
                    [0] => Array
                        (
                            [Grantee] => Array
                                (
                                    [ID] => qcs::cam::uin/327874225:uin/327874225
                                    [DisplayName] => qcs::cam::uin/327874225:uin/327874225
                                )

                            [Permission] => FULL_CONTROL
                        )

                )

            [RequestCharged] => 
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjU5OF8yYzlkMmE=
        )
)
```

### putBucketCors
#### 方法のプロトタイプ

```php
// バケットのクロスオリジン構成を設定します
public Guzzle\Service\Resource\Model putBucketCors(array $args = array());
```
#### リクエストパラメータ

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |       バケット名               |    string        | はい           |         
| CORSRules |        CORS規則        |    array     | はい            | 
| AllowedMethods |        許可されたHTTP操作。列挙値：GET、PUT、HEAD、POST、DELETE        |    array   | いいえ           |  
| AllowedOrigins |           許可されたアクセスソース、ワイルドカード * をサポートします。フォーマット：プロトコル://ドメイン名[:ポート]、例えば：http://www.qq.com       |   array   | いいえ           |
| AllowedHeaders |        オプションリクエストを送信するときに、後続のリクエストがどのカスタムHTTPリクエストヘッダーを使用できるかをサーバーに通知します。ワイルドカードの使用をサポートします　        |   array    | いいえ           |    
| ExposeHeaders |       ブラウザが受信できるサーバーからのカスタムヘッダー情報を設定します       |    array    | いいえ           |   
| MaxAgeSeconds |    オプションリクエストが取得される結果の有効期間を設定します        |   string       | いいえ           |       
| ID |         規則のIDを構成します       | string   | いいえ           |    

####　リクエスト例
```php
###putBucketCors
try {
    $result = $cosClient->putBucketCors(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',
        // CORSRules is required
        'CORSRules' => array(
            array(
                'AllowedHeaders' => array('*',),
            // AllowedMethods is required
            'AllowedMethods' => array('Put', ),
            // AllowedOrigins is required
            'AllowedOrigins' => array('*', ),
            'ExposeHeaders' => array('*', ),
            'MaxAgeSeconds' => 1,
        ),
        // ... repeated
    ),
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] => 
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### getBucketCors
#### 方法のプロトタイプ

```php
// バケットのクロスオリジン構成を取得します
public Guzzle\Service\Resource\Model getBucketCors(array $args = array());
```
#### リクエストパラメータ



| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |       バケット名            |     string     | はい           | 


####　リクエスト例
```php
#getBucketCors
try {
    $result = $cosClient->getBucketCors(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [CORSRules] => Array
                (
                    [0] => Array
                        (
                            [ID] => 1234
                            [AllowedHeaders] => Array
                                (
                                    [0] => *
                                )

                            [AllowedMethods] => Array
                                (
                                    [0] => PUT
                                )

                            [AllowedOrigins] => Array
                                (
                                    [0] => http://www.qq.com
                                )

                        )

                )

            [RequestId] => NWE3YzhkMmRfMTdiMjk0MGFfNTQzZl8xNWUwMGU=
        )
)
```

### deleteBucketCors
#### 方法のプロトタイプ

```php
// バケットのクロスオリジン構成を削除します
public Guzzle\Service\Resource\Model deleteBucketCors(array $args = array());
```
#### リクエストパラメータ

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |       バケット名            |     string     | はい           | 


####　リクエスト例
```php
#deleteBucketCors
try {
    $result = $cosClient->deleteBucketCors(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] => 
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### putBucketReplication
#### 方法のプロトタイプ

```php
// バケットの地域間コピー構成を設定します
public Guzzle\Service\Resource\Model putBucketReplication(array $args = array());
```
#### リクエストパラメータ

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |       バケット名               |    string        | はい           |         
| Role |        発起者の身元タグ：qcs::cam::uin/<OwnerUin>:uin/<SubUin>        |    string     | はい            | 
| Rules |        具体的な構成情報、最大1000をサポートします       |    array   |  はい           |  
| ID |           具体的なRule名の表示に使用されます       |   string   | はい           |
| Status |        タグRuleが有効かどうかを標識します。列挙値: Enabled、Disabled       |   String    |   はい        |    
| Prefix |       プレフィックスのマッチングポリシーとして、重複できません。重複ならエラーを返します。プレフィックスマッチングのルートディレクトリがブランクです       |    string    | はい           |   
| Destination |   ターゲットバケット情報    |   array       |  はい          |       
| Bucket   |   リソース識別子：qcs::cos:[region]::[bucketname-AppId]    |   array       |  はい          |       
| StorageClass |   ストレージレベル、列挙値：STANDARD、STANDARD_IA、NEARLINE；デフォルト値：元のバケットレベル    |   array       |  いいえ          |      

####　リクエスト例
```php
###putBucketCors
try {
    $result = $cosClient->PutBucketReplication(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',
        'Role' => 'qcs::cam::uin/320000000:uin/320000000',
        'Rules'=>array(
            array(
                'Status' => 'Enabled',
                'ID' => 'string',
                'Prefix' => 'string',
                'Destination' => array(
                    'Bucket' => 'qcs::cos:ap-guangzhou::testbucket01-125000000',
                    'StorageClass' => 'standard',
                ),
                // ...repeated
            ),
        ),
    ));
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### getBucketReplication
#### 方法のプロトタイプ

```php
// バケットの地域間コピー構成を取得します
public Guzzle\Service\Resource\Model getBucketReplication(array $args = array());
```
#### リクエストパラメータ



| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |       バケット名            |     string     | はい           | 


####　リクエスト例
```php
#getBucketReplication
try {
    $result = $cosClient->GetBucketReplication(array(
        'Bucket' => 'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```

#### 返された結果の例
```php
Array
(
	[data:protected] => Array
	(
	    [Role] => qcs::cam::uin/320000000:uin/320000000
	    [Rules] => Array
	        (
	            [0] => Array
	                (
	                    [ID] => string
	                    [Status] => Enabled
	                    [Prefix] => string
	                    [Destination] => Array
	                        (
	                            [Bucket] => qcs::cos:ap-guangzhou::testbucket01-125000000
	                            [StorageClass] => Standard
	                        )

	                )

	        )

	    [RequestId] => NWI2YWFlN2NfMjNiMjM1MGFfNTQ0OF80NzMzNWY=
	)
)
```

### deleteBucketReplication
#### 方法のプロトタイプ

```php
// バケットの地域間コピー構成を削除します
public Guzzle\Service\Resource\Model deleteBucketReplication(array $args = array());
```
#### リクエストパラメータ

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |       バケット名            |     string     | はい           |  


####　リクエスト例
```php
#deleteBucketReplication
try {
    $result = $cosClient->deleteBucketReplication(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### オブジェクトのコピー
#### 方法のプロトタイプ

```php
// オブジェクトのコピー
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### リクエストパラメータ
| パラメータ名   | 説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|  Bucket  |  バケット名は数字、アルファベット小文字とハイフン「-」より構成されます | string |   はい |
|  CopySource  | ソースをコピーします     |  string |  はい |
|  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String |  はい | 
|  ACL  | ファイルのACLを設定します。例えば'private、public-read'、'public-read-write' | string |   いいえ | 
|  GrantFullControl  |指定されたアカウントのファイルへの読み書き権限の付与 |  string |  いいえ | 
|  GrantRead  |  指定されたアカウントのファイルへの読み取り権限の付与 | string |  いいえ |
|  GrantWrite  |  指定されたアカウントのファイルへの書き込み権限の付与 | string |  いいえ |
|  StorageClass  |  ファイルのストレージタイプ（STANDARD、STANDARD_IA）の設定。デフォルト値：STANDARD | String |   いいえ |
|  Expires  | Content-Expiresの設定 | string|  いいえ | 
|  CacheControl  |  キャッシュポリシー、Cache-Controlの設定 | string |   いいえ |
|  ContentType  | 内容タイプ、Content-Typeの設定 |String |   いいえ |  
|  ContentDisposition  |  ファイル名、Content-Dispositionの設定 | string |   いいえ |
|  ContentEncoding  |  エンコードフォーマット、Content-Encodingの設定 | string |   いいえ |
|  ContentLanguage  |  言語タイプ、Content-Languageの設定 | string |   いいえ |
|  ContentLength  | 伝送長さの設定 | string |   いいえ | 
|  ContentMD5  | 検証するためにアップロードされたファイルのMD5値の設定 | string |   いいえ | 
|  Metadata | ユーザー設定のファイルのメタ情報 | array |   いいえ |
|  ServerSideEncryption | サーバーの暗号化方式 | string |   いいえ |
| MetadataDirective | ソースファイルのヘッダーを使用するかどうか。選択可能な値はCopy、Replacedで、デフォルト値はCopyです。Copyはソースファイルのヘッダーを使用し、ReplacedはこのAPIのヘッダーを使用します |string | いいえ |

####　リクエスト例

```php
#copyobject
#　簡単なcopy API
try {
    $result = $cosClient->copyObject(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' => 'testbucket-125000000',
        // CopySource is required
        'CopySource' => 'lewzylu03-1252448703.cos.ap-guangzhou.myqcloud.com/tox.ini',
        // Key is required
        'Key' => 'string',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

#copy
#5Gを超える場合、自動的にパートcopyAPIを使用します。
try {
    $result = $cosClient->Copy($bucket = 'lewzylu01-1252448703',
        $key = 'string',
        $copysource = 'lewzylu02-1252448703.cos.ap-guangzhou.myqcloud.com/test1G',
        $options = array('VersionId'=>'MTg0NDY3NDI1NTk0MzUwNDQ1OTg'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### putBucketLifecycle
#### 方法のプロトタイプ

```php
// バケットのライフサイクルを構成します
public Guzzle\Service\Resource\Model putBucketLifecycle(array $args = array());
```
#### リクエストパラメータ
| パラメータ名   | 説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|  Bucket  |  バケット名は数字、アルファベット小文字とハイフン「-」より構成されます | string |   はい |
|  Rules  | 対応する規則を設定します。つまり、ID、Filter、Status、Expiration、Transition、NoncurrentVersionExpiration、NoncurrentVersionTransition、AbortIncompleteMultipartUpload       |  array |  はい |　
|  ID     |  規則のIDを構成します  | string |  いいえ | 
|  Filter  | 規則の影響を受けるオブジェクトのセットを説明するために使用されます | array |   はい | 
|  Status  |Ruleをオンにするかどうかを設定します。選択可能な値はEnabledまたはDisabled |  string |  はい | 
|  Expiration  |  オブジェクトの期限切れ規則は日付Daysまたは日付Dateを指定できます | array |  いいえ |
|  Transition  |  オブジェクト変換ストレージタイプの規則は日数Daysまたは日付Dateを指定できます。StorageClassはStandard_IAが選択可能です| array |  いいえ |


####　リクエスト例

```php
#putBucketLifecycle
try {
    $result = $cosClient->putBucketLifecycle(array(
    //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
    'Bucket' => 'testbucket-125000000',
    // Rules is required
    'Rules' => array(
        array(
            'Expiration' => array(
                'Days' => 1,
            ),
            'ID' => 'id1',
            'Filter' => array(
                'Prefix' => 'documents/'
            ),
            // Status is required
            'Status' => 'Enabled',
            'Transitions' => array(
                array(
                    'Days' => 200,
                    'StorageClass' => 'Standard_IA')),
            // ... repeated
        ),
    )));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] => 
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### getBucketLifecycle
#### 方法のプロトタイプ

```php
// バケットのライフサイクルを取得します
public Guzzle\Service\Resource\Model getBucketLifecycle(array $args = array());
```
#### リクエストパラメータ

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |              バケット名               |   string   | はい           |    


####　リクエスト例
```php
#getBucketLifecycle
try {
    $result = $cosClient->getBucketLifecycle(array(
        //バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
        'Bucket' =>'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Rules] => Array
                (
                    [0] => Array
                        (
                            [ID] => id1
                            [Filter] => Array
                                (
                                    [Prefix] => documents/
                                )

                            [Status] => Enabled
                            [Transition] => Array
                                (
                                    [Days] => 200
                                    [StorageClass] => Standard_IA
                                )

                            [Expiration] => Array
                                (
                                    [Days] => 1000
                                )

                        )

                )

            [RequestId] => NWE3YzhlZjNfY2FhMzNiMGFfNDVkNF8yZDIxODE=
        )
)
```

### deleteBucketLifecycle
#### 方法のプロトタイプ

```php
// バケットのライフサイクル構成を削除します
public Guzzle\Service\Resource\Model deleteBucketLifecycle(array $args = array());
```
#### リクエストパラメータ

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |            バケット名               |      string    | はい           |   

####　リクエスト例

```php
#deleteBucketLifecycle
try {
    $result = $cosClient->deleteBucketLifecycle(array(
        //バケットの命名規則は{name}-{appid}です。ここで入力するバケット名はこのフォーマットでなければなりません。
        'Bucket' =>'testbucket-125000000',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] => 
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### オブジェクトのダウンロードURLを取得します

オブジェクトの署名付きダウンロードURLを取得します。

####　リクエスト例

```php
//オブジェクトのダウンロードURLを取得します
//バケットの命名規則は{name}-{appid}です。ここに入力するバケット名はこのフォーマットでなければなりません
$bucket =  'testbucket-125000000';
$key = 'hello.txt';
$signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
```
### 一時暗号鍵の使用

```php
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => 'cn-south',
        'timeout' => ,
        'credentials'=> array(
            'appId' => '',
            'secretId'    => '',
            'secretKey' => '',
            'token' => '')));
```


### アーカイブファイルの回復

#### 方法のプロトタイプ

```php
//  アーカイブファイルの回復
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。


| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |                バケット名               |  string    | はい             |  
| Key      |         オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです         |    string      | はい           |      
| Days      |        保存時間        |   integer |  はい          |   
| Tier   |        回復タイプ        | string |   いいえ          |    

####　リクエスト例

```php
  try {
    $result = $cosClient->restoreObject(array(
        // Bucket is required
        'Bucket' => 'lewzylu02',
        // Objects is required
        'Key' => '11',
        'Days' => 7,
        'CASJobParameters' => array(
            'Tier' =>'Bulk'
        )
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```


### バージョン制御を有効にします

#### 方法のプロトタイプ

```php
// バージョン制御を有効にします
public Guzzle\Service\Resource\Model putBucketVersioning(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |           バケット名               |    string        | はい             |     
| Status   |          バージョン制御状態              |   string       | はい           |       

####　リクエスト例
```php
#putBucketVersioning
try {
    $result = $cosClient->putBucketVersioning(
    array('Bucket' => 'lewzylu02',
    'Status' => 'Enabled')
    );
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [RequestCharged] => 
            [RequestId] => NWE3YzhjZDdfY2JhMzNiMGFfNjVhOV8yZDJhNjY=
        )
)
```

### バケットバージョンの取得

#### 方法のプロトタイプ

```php
// バケットバージョンの取得
public Guzzle\Service\Resource\Model getBucketVersioning(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |        バケット名               |    string  | はい           |        

####　リクエスト例

```php
try {
    $result = $cosClient->getBucketVersioning(
        array('Bucket' => 'lewzylu02',)
    );
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

```

#### 返された結果の例
```php
Array
(
    [data:protected] => Array
        (
            [Status] => Enabled
            [RequestId] => NWE3YzhmZTVfNjIyNWI2NF80YzQ3XzJkNjU4NQ==
        )
)
```

### 各バージョンのファイルリストをプリントします

#### 方法のプロトタイプ

```php
// 各バージョンのファイルリストをプリントします
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```

#### リクエストパラメータ

$argsは下記のフィールドを含む関連配列です。

| パラメータ名称   | 説明   | タイプ | 必須項目 | 
| :------: | :------------: | :--:   | :--------:   |
| Bucket   |        バケット名               |  string      | はい           |          
| Delimiter      |     区切り記号         |   string      | いいえ          |      
| Marker      |     タグ        |   string       | いいえ          |      
| MaxKeys      |     最大オブジェクト数         |  int        | いいえ          |       
| Prefix      |          プレフィックス         |   string       | いいえ           | 

####　リクエスト例

```php
try {
    $result = $cosClient->listObjectVersions(
        array('Bucket' => 'lewzylu02',
            'Prefix'=>'test1G')
    );
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

```
#### 返された結果の例
```php
Array
(
   [data:protected] => Array
        (
            [Name] => lewzylu02-1252448703
            [Prefix] => test1G
            [KeyMarker] => 
            [VersionIdMarker] => 
            [MaxKeys] => 1000
            [IsTruncated] => 
            [Versions] => Array
                (
                    [0] => Array
                        (
                            [Key] => test1G
                            [VersionId] => MTg0NDY3NDI1NTg1ODc4Nzk3NjI
                            [IsLatest] => 1
                            [LastModified] => 2018-01-05T03:07:51.000Z
                            [ETag] => "202cb962ac59075b964b07152d234b70"
                            [Size] => 3
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1252448703
                                )

                        )

                    [1] => Array
                        (
                            [Key] => test1G
                            [VersionId] => MTg0NDY3NDI1NTk0MzI3NDU3NTk
                            [IsLatest] => 
                            [LastModified] => 2017-12-26T08:26:50.000Z
                            [ETag] => "13ddf6552868644926ba606cd287106b-1"
                            [Size] => 5242880
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1252448703
                                )

                        )

                    [2] => Array
                        (
                            [Key] => test1G
                            [VersionId] => MTg0NDY3NDI1NTk0MzI3ODAzODc
                            [IsLatest] => 
                            [LastModified] => 2017-12-26T08:26:16.000Z
                            [ETag] => "3c86b7371340b2174b875fa7bcc0bd9a-1"
                            [Size] => 5242880
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1252448703
                                )

                        )
                )

            [RequestId] => NWE3YzkwMGFfMTliYjk0MGFfMWUwOWRfMmJlZWIx
        )
)
```
### 事前署名リンク
####　リクエスト例
```
try {
    #ここは任意のAPIに置き換えることができます
    $command = $cosClient->getCommand('putObject', array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => '', //Bodyは無制限
    ));
    $signedUrl = $command->createPresignedUrl('+10 minutes');
    echo ($signedUrl);
} catch (\Exception $e) {
    echo($e);
}
```

