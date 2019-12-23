## 機能説明
GET BucketリクエストはList Objectリクエストに相当し、このバケットの下にあるオブジェクトの一部または全部をリストすることができます。このAPIのオペレータはバケットへの読み取りアクセス権限を持つ必要があります。

## リクエスト
### リクエスト例

```shell
GET / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。

### リクエストヘッダー
#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。
#### 非共通のヘッダー
このリクエスト操作には、特別なリクエストヘッダー情報はありません。

#### リクエストパラメータ

名称|タイプ|説明|必須項目
---|---|---|---
prefix|string|プレフィックスマッチング、返されるファイルプレフィックスアドレスを指定するために使用されます |いいえ
delimiter|string|区切りは記号の1つです。プレフィックスがある場合は、プレフィックスとデリミターの間の同じパスが1つのタイプに分類され、Common Prefixとして定義されてから、すべてのCommon Prefixがリストされます。プレフィックスがない場合は、パスの先頭から開始します|いいえ
encoding-type|string|戻り値のエンコーディング方法を指定します。選択できる値：url |いいえ
marker|string|デフォルトでは、エントリはUTF-8二進法の順でリストされ、すべてのエントリはマーカーから始まります|いいえ
max-keys|string|一度に返されるエントリの最大数、デフォルト値は1000、最大値は1000です|いいえ

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答
### 応答ヘッダー

#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。

### 応答ボディ
照合に成功、バケット内のオブジェクト情報を含むapplication/xmlデータを返します。

```shell
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
    <Name>examplebucket-1250000000</Name>
    <Encoding-Type>url</Encoding-Type>
    <Prefix>ela</Prefix>
    <Marker/>
    <MaxKeys>1000</MaxKeys>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <NextMarker>exampleobject.txt</NextMarker>
    <Contents>
        <Key>photo</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"79f2a852fac7e826c9f4dbe037f8a63b\"</ETag>
        <Size>10485760</Size>
        <Owner>
           <ID>1250000000</ID>
        </Owner>
        <StorageClass>STANDARD</StorageClass>
    </Contents>
    <CommonPrefixes>
      <Prefix>example</Prefix>
    </CommonPrefixes>
</ListBucketResult>
```

具体的なデータ説明は以下のとおりです：

ノード名称（キーワード）|親ノード|説明|タイプ
---|---|---|---
ListBucketResult|無し|Get Bucketリクエスト結果のすべての情報を保存します|Container

**コンテナノードListBucketResult内容：**

ノード名称（キーワード）|親ノード|説明|タイプ
---|---|---|---
Name|ListBucketResult|バケットの情報を説明します|string
Encoding-Type|ListBucketResult|エンコーディングフォーマット|string
Prefix|ListBucketResult|プレフィックスマッチング、応答リクエストから返されるファイルプレフィックスアドレスを指定するために使用されます|string
Marker|ListBucketResult|デフォルトでは、エントリはUTF-8二進法の順でリストされ、すべてのエントリはマーカーから始まります|string
MaxKeys|ListBucketResult|単回応答リクエスト内で返された結果エントリの最大数|string
Delimiter|ListBucketResult|区切りは記号の1つです。プレフィックスがある場合は、プレフィックスとデリミターの間の同じパスが1つのタイプに分類され、Common Prefixとして定義されてから、すべてのCommon Prefixがリストされます。プレフィックスがない場合は、パスの先頭から開始します|string
IsTruncated|ListBucketResult|応答リクエストのエントリが遮断されたかどうか、ブール値：true、false|boolean
NextMarker|ListBucketResult|仮に返されたエントリが遮断された場合、返されたNextMarkerが次のエントリの開始点です|string
Contents|ListBucketResult|メタデータ情報|Container
CommonPrefixes|ListBucketResult|プレフィックスとデリミターの間の同じパスが1つのタイプに分類され、Common Prefixとして定義されます|Container


**コンテナノード内容：**

ノード名称（キーワード）|親ノード|説明|タイプ
---|---|---|--
Key|ListBucketResult.Contents|オブジェクトのキー|string
LastModified|ListBucketResult.Contents|オブジェクトの最後の変更時間を説明します|string
ETag|ListBucketResult.Contents|ファイルのMD-5アルゴリズムチェック値|string
Size|ListBucketResult.Contents|ファイルサイズを説明します。単位はByteです|string
Owner|ListBucketResult.Contents|バケット所有者情報|Container
StorageClass|ListBucketResult.Contents|オブジェクトの格納レベル、列挙値：STANDARD、STANDARD_IA、ARCHIVE|string

**コンテナノードオーナー内容：**

ノード名称（キーワード）|親ノード|説明|タイプ
---|---|---|---
ID|ListBucketResult.Contents.Owner|バケットのAppID|string


**コンテナノードCommonPrefixes内容：**

ノード名称（キーワード）|親ノード|説明|タイプ
---|---|---|---
Prefix|ListBucketResult.CommonPrefixes|単一のCommonのプレフィックス|string


###　エラーコード
このリクエスト操作には、特別なエラーメッセージがありません。一般的なエラーメッセージについては、 [エラーコード](https://cloud.tencent.com/document/product/436/7730) ドキュメントを参照してください。

## 実際のケース

### リクエスト

```shell
GET / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213451;32557109451&q-key-time=1484213451;32557109451&q-header-list=host&q-url-param-list=&q-signature=0336a1fc8350c74b6c081d4dff8e7a2db9007dc
```

### 応答

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1132
Connection: keep-alive
Vary: Accept-Encoding
Date: Wed, 18 Oct 2014 22:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRjY2VfYmRjMzVfMTc5M182MmIyNg==

<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
    <Name>examplebucket-1250000000</Name>
    <Encoding-Type>url</Encoding-Type>
    <Prefix>ela</Prefix>
    <Marker/>
    <MaxKeys>1000</MaxKeys>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <NextMarker>exampleobject.txt</NextMarker>
    <Contents>
        <Key>photo</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"79f2a852fac7e826c9f4dbe037f8a63b\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000001</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>picture</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"3f9a5dbff88b25b769fa6304902b5d9d\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000002</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>file</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"39bfb88c11c65ed6424d2e1cd4db1826\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000003</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>world</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"fb31459ad10289ff49327fd91a3e1f6a\"</ETag>
        <Size>4</Size>
        <Owner>
            <ID>1250000004</ID>
        </Owner>
        <StorageClass>STANDARD</StorageClass>
    </Contents>
</ListBucketResult>
```



