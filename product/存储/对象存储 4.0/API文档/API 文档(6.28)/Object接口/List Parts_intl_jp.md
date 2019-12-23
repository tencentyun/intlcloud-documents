## 機能説明
List Partsは、特定のマルチパートアップロードでアップロードされたパートを照合するために使用されます。つまり、指定されたUploadIdが属するすべてのアップロードに成功したパートをリストするために使用されます。

## リクエスト
### リクエスト例

```
GET /ObjectName?uploadId=UploadId HTTP/1.1
Host: <BucketName>-<APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

### リクエストヘッダー
#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。
#### 非共通のヘッダー
このリクエスト操作には、特別なリクエストヘッダー情報はありません。

#### リクエストパラメータ

名称|タイプ|必須項目|説明
---|---|---|---
UploadId|string|はい|今回マルチパートアップロードのIDを識別します。Initiate Multipart Upload APIを使ってマルチパートアップロードを初期化するとき、uploadIdが取得されます。このIDは、このパートデータを一意に識別するだけでなく、ファイル全体におけるこのパートデータの相対位置も識別します
encoding-type|string|いいえ|戻り値のエンコーディング方法を指定します
max-parts|string|いいえ|一度に返されるエントリの最大数、デフォルト値は1000です
part-number-marker|string|いいえ|デフォルトでは、エントリはUTF-8二進法の順でリストされ、すべてのエントリはマーカーから始まります

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。

### 応答ボディ
照合は成功しました。完成済みのパート情報を含む **application/xml** データを返します。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<ListPartsResult>
  <Bucket>string</Bucket>
  <Encoding-Type>string</Encoding-Type>
  <Key>string</Key>
  <UploadId>string</UploadId>
  <Initiator>
    <ID>string</ID>
    <DisplayName>string</DisplayName>
  </Initiator>
  <Owner>
    <ID>string</ID>
    <DisplayName>string</DisplayName>
  </Owner>
  <StorageClass>string</StorageClass>
  <PartNumberMarker>string</PartNumberMarker>
  <NextPartNumberMarker>string</NextPartNumberMarker>
  <MaxParts>string</MaxParts>
  <IsTruncated>true</IsTruncated>
  <Part>
    <PartNumber>string</PartNumber>
    <LastModified>string</LastModified>
    <ETag>string</ETag>
    <Size>string</Size>
  </Part>
</ListPartsResult>
```

具体的なデータ説明は以下のとおりです：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
ListPartsResult|無し|List Partsリクエスト結果のすべての情報を保存します|Container|はい

コンテナノードListPartsResult の内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
Bucket|ListPartsResult|マルチパートアップロードのターゲットバケット、バケットの名称、ユーザーがカスタマイズで生成された文字列とシステムで生成されたappid数値列をハイフンで接続します。例えば：mybucket-1250000000|string|はい
Encoding-Type|ListPartsResult|エンコーディングフォーマット|string|はい
Key|ListPartsResult|オブジェクトの名称|string|はい
UploadId|ListPartsResult|今回のマルチパートアップロードIDを識別します|string|はい
Initiator|ListPartsResult|これらのパート所有者の情報を表すために使用されます|Container|はい
Owner|ListPartsResult|これらのパート所有者の情報を表すために使用されます|Container|はい
StorageClass|ListPartsResult|これらのパートのストレージレベルを示すために使用されます。列挙値：STANDARD、STANDARD_IA、ARCHIVE|string|はい
PartNumberMarker|ListPartsResult|デフォルトでは、エントリはUTF-8二進法の順でリストされ、すべてのエントリはマーカーから始まります|string|はい
NextPartNumberMarker|ListPartsResult|返されたエントリが遮断された場合、返されたNextMarkerが次のエントリの起点です|string|はい
MaxParts|ListPartsResult|一度に返されるエントリの最大数|string|はい
IsTruncated|ListPartsResult|応答リクエストのエントリが遮断されたかどうか、ブール値：true、false|boolean|はい
Part|ListPartsResult|メタデータ情報|Container|はい
コンテナノードInitiatorの内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
ID|ListPartsResult.Initiator|作成者の一意な識別子|string|はい
DisplayName|ListPartsResult.Initiator|作成者のユーザー名の説明|string|はい
コンテナノードオーナーの内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
ID|ListPartsResult.Owner|作成者の一意な識別子|string|はい
DisplayName|ListPartsResult.Owner|作成者のユーザー名の説明|string|はい
コンテナノードPartの内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
PartNumber|ListPartsResult.Part|パートの番号|string|はい
LastModified|ListPartsResult.Part|パートの最後の変更時間を説明します|string|はい
ETag|ListPartsResult.Part|パートのMD-5アルゴリズムチェック値|string|はい
Size|ListPartsResult.Part|パートサイズを説明します。単位はByteです|string|はい

## 実際のケース

### リクエスト

```
GET /coss3/test10M_2?uploadId=14846420620b1f381e5d7b057692e131dd8d72dfa28f2633cfbbe4d0a9e8bd0719933545b0&max-parts=1 HTTP/1.1
Host:burning-1251668577.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3MqQCn&q-sign-time=1484643123;1484646723&q-key-time=1484643123;1484646723&q-header-list=host&q-url-param-list=max-parts;uploadId&q-signature=b8b4055724e64c9ad848190a2f7625fd3f9d3e87
```

### 応答

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 661
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
x-cos-request-id: NTg3ZGRiMzhfMmM4OGY3XzdhY2NfYw==

<ListPartsResult>
    <Bucket>burning-123456789</Bucket>
    <Encoding-type/>
    <Key>test10M_2</Key>
    <UploadId>14846420620b1f381e5d7b057692e131dd8d72dfa28f2633cfbbe4d0a9e8bd0719933545b0</UploadId>
    <Initiator>
        <ID>123456789</ID>
        <DisplyName>123456789</DisplyName>
    </Initiator>
    <Owner>
        <ID>qcs::cam::uin/156545789:uin/156545789</ID>
        <DisplyName>156545789</DisplyName>
    </Owner>
    <PartNumberMarker>0</PartNumberMarker>
    <Part>
        <PartNumber>1</PartNumber>
        <LastModified>Tue Jan 17 16:43:37 2017</LastModified>
        <ETag>"a1f8e5e4d63ac6970a0062a6277e191fe09a1382"</ETag>
        <Size>5242880</Size>
    </Part>
    <NextPartNumberMarker>1</NextPartNumberMarker>
    <StorageClass>STANDARD</StorageClass>
    <MaxParts>1</MaxParts>
    <IsTruncated>true</IsTruncated>
</ListPartsResult>
```



