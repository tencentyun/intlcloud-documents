## 概要

データをクライアントとサーバー間で伝送する際にエラーが発生することがあります。COSはMD5検証の方式でアップロードしたデータの完全性を保証することができます。COSサーバーが受信したデータのMD5チェックサムとユーザーが設定したMD5チェックサムが一致した場合のみ、データのアップロードが成功します。

COS内の各オブジェクトには1つのETagが対応しています。ETagはオブジェクトが作成された時点でのオブジェクト内容の情報タグですが、ETagはオブジェクト内容のMD5チェックサムと必ずしも同じではありません。このため、ETagによってダウンロードしたオブジェクトと元のオブジェクトが同じかどうかを検証することはできませんが、 ユーザーはカスタムオブジェクトメタデータ（x-cos-meta-\*）を使用することで、ダウンロードしたオブジェクトと元のオブジェクトの整合性検証を実現することができます。

## データチェック検証方式

- アップロードオブジェクトの検証
COSにアップロードしたオブジェクトとローカルのオブジェクトが一致しているかを検証したい場合、ユーザーはアップロードの際にHTTPリクエストの[Content-MD5](https://intl.cloud.tencent.com/document/product/436/7728)フィールドを、Base64エンコードを経たオブジェクト内容のMD5チェックサムに設定することができます。このときCOSサーバーはユーザーがアップロードしたオブジェクトを検証し、COSサーバーが受信したオブジェクトのMD5チェックサムとユーザーが設定したContent-MD5が一致した場合のみ、オブジェクトを正常にアップロードします。
- ダウンロードオブジェクトの検証
ダウンロードしたオブジェクトと元のオブジェクトが一致しているかを検証したい場合、ユーザーはオブジェクトをアップロードする際に検証アルゴリズムを使用してオブジェクトのチェックサムを計算し、カスタムメタデータによってオブジェクトのチェックサムを設定し、オブジェクトのダウンロード後にオブジェクトのチェックサムを再計算し、カスタムメタデータとの比較によって検証することができます。この方式では、ユーザーはご自身で検証アルゴリズムを選択できますが、同一のオブジェクトについては、アップロードとダウンロードの際に使用する検証アルゴリズムは一致させる必要があります。   


## APIインターフェースの例

#### シンプルアップロードリクエスト

以下はユーザーがオブジェクトをアップロードする場合のリクエストの例です。オブジェクトをアップロードする際、Content-MD5を、Base64エンコードを経たオブジェクト内容のMD5チェックサムに設定します。こうすることで、COSサーバーが受信したオブジェクトのMD5チェックサムとユーザーが設定したContent-MD5が一致した場合のみ、オブジェクトのアップロードが正常に行われるようにし、かつカスタムメタデータx-cos-meta-md5をオブジェクトのチェックサムに設定します。
>?例で示したものはMD5検証アルゴリズムによって得られたオブジェクトのチェックサムです。ユーザーはご自身で他の検証アルゴリズムを選択することができます。  

```url
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:28 GMT
Content-Type: image/jpeg
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9
Connection: close

[Object Content]
```

#### マルチパートアップロードリクエスト

以下はマルチパートアップロードの初期化リクエストの例です。オブジェクトのパートをアップロードする際、ユーザーはマルチパートアップロードを初期化することによってオブジェクトのカスタムメタデータを設定できます。ここではカスタムメタデータx-cos-meta-md5をオブジェクトのチェックサムに設定します。   

```url
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:45:12 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9
```
>! マルチパートアップロードのファイルについて、COSは各パートのMD5値のみを検証し、合体後の完全なファイルのMD5値の計算は行いません。

#### オブジェクトダウンロードの応答

以下はユーザーがオブジェクトダウンロードリクエストを送信後に取得する応答の例です。ユーザーは応答の中からオブジェクトのカスタムメタデータx-cos-meta-md5を取得することができ、オブジェクトのチェックサムを再計算してそのカスタムメタデータとの比較を行うことで、ダウンロードしたオブジェクトと元のオブジェクトが一致しているかを検証できます。   

```url
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Content-Length: 13
Connection: close
Accept-Ranges: bytes
Cache-Control: max-age=86400
Content-Disposition: attachment; filename=example.jpg
Date: Thu, 04 Jul 2019 11:33:00 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Thu, 04 Jul 2019 11:32:55 GMT
Server: tencent-cos
x-cos-request-id: NWQxZGUzZWNfNjI4NWQ2NF9lMWYyXzk1NjFj****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9

[Object Content]
```

## SDKの例

次に、Python SDKを例に、オブジェクトの検証方法についてご説明します。完全なサンプルコードは次のとおりです。

>?コードはPython 2.7ベースです。Python SDKの詳細な使用方法については、Python SDKの[オブジェクトの操作](https://www.tencentcloud.com/document/product/436/43582)ドキュメントをご参照ください。

#### 1. 初期化設定

SecretId、SecretKey、Regionを含むユーザー属性を設定し、クライアントオブジェクトを作成します。

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError
import sys
import os
import logging
import hashlib

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# SecretId、SecretKey、Regionを含むユーザー属性の設定
# APPIDはすでに設定から削除されていますので、パラメータのBucketにAPPIDを含めてください。BucketはBucketName-APPIDで構成されます。
secret_id = os.environ['COS_SECRET_ID']     # ユーザーのSecretIdです。サブアカウントのキーを使用し、権限承認は最小権限ガイドに従って行い、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、https://cloud.tencent.com/document/product/598/37140をご参照ください
secret_key = os.environ['COS_SECRET_KEY']   # ユーザーのSecretKeyです。サブアカウントのキーを使用し、権限承認は最小権限ガイドに従って行い、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、https://cloud.tencent.com/document/product/598/37140をご参照ください
region = 'ap-beijing'      # ご自身のRegionに置き換えてください。ここでは北京とします
token = None               # 一時キーのToken。一時キーの生成および使用ガイドについてはhttps://cloud.tencent.com/document/product/436/14048をご参照ください
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # 設定を取得するオブジェクト
client = CosS3Client(config)
```

#### 2. シンプルアップロードオブジェクトの検証

#### （1）オブジェクトのチェックサムの計算

MD5検証アルゴリズムによってオブジェクトのチェックサムを取得します。ユーザーはご自身で他の検証アルゴリズムを選択することができます。

```python
object_body = 'hello cos'
#オブジェクトのmd5チェックサムを取得
md5 = hashlib.md5()
md5.update(object_body)
md5_str = md5.hexdigest()
```

#### （2）オブジェクトのシンプルアップロード

コード内にEnableMD5=Trueと表示されていればMD5検証が有効になっており、Python SDKがContent-MD5を計算します。有効にするとアップロードの消費時間が増加し、COSサーバーが受信したオブジェクトのMD5チェックサムとユーザーが設定したContent-MD5が一致した場合のみ、オブジェクトのアップロードが正常に行われます。
x-cos-meta-md5はユーザー定義のパラメータです（カスタムパラメータ名の形式はx-cos-meta-\*）。このパラメータはオブジェクトのMD5チェックサムを表します。

```python
#オブジェクトのシンプルアップロードを行い、MD5検証を有効化します
response = client.put_object(
    Bucket='examplebucket-1250000000',      #ご自身のBucket名に置き換えます。examplebucketはバケットの例、1250000000はAPPIDの例です。
    Body='hello cos',                 #アップロードするオブジェクトの内容
    Key='example-object-1',           #アップロードするオブジェクトのKey値に置き換えます 
    EnableMD5=True,                   #アップロードのMD5検証を有効化します
    Metadata={                        #カスタムパラメータを設定し、オブジェクトのMD5チェックサムをパラメータ値としてCOSサーバーに保存します
        'x-cos-meta-md5' : md5_str
    }
)
print 'ETag: ' + response['ETag']     # ObjectのEtag値
```

#### （3）オブジェクトのダウンロード

オブジェクトをダウンロードし、ユーザー定義のパラメータを取得します。

```python
#オブジェクトのダウンロード
response = client.get_object(
    Bucket='examplebucket-1250000000',      #ご自身のBucket名に置き換えます。examplebucketはバケットの例、1250000000はAPPIDの例です。
    Key='example-object-1'                  #ダウンロードしたオブジェクトのKey値
)
fp = response['Body'].get_raw_stream()
download_object = fp.read()                 #オブジェクトの内容を取得
print "get object body: " + download_object
print 'ETag: ' + response['ETag']               
print 'x-cos-meta-md5: ' + response['x-cos-meta-md5']   #ユーザー定義のパラメータx-cos-meta-md5を取得
```

#### （4） オブジェクトの検証

オブジェクトのダウンロードに成功後、ユーザーはオブジェクトのチェックサムを再計算し（検証アルゴリズムはオブジェクトのアップロード時のものと一致させます）、ユーザー定義のパラメータx-cos-meta-md5と比較し、ダウンロードしたオブジェクトとアップロードしたオブジェクトの内容が一致するかどうかを検証します。

```python
#ダウンロードオブジェクトのMD5チェックサムを計算
md5 = hashlib.md5()                 
md5.update(download_object)
md5_str = md5.hexdigest()
print 'download object md5: ' + md5_str

#ダウンロードオブジェクトのMD5チェックサムとアップロードオブジェクトのMD5チェックサムを比較し、オブジェクトの整合性を検証します
if md5_str == response['x-cos-meta-md5']:
    print 'MD5 check OK'
else:
    print 'MD5 check FAIL'
```

#### 3. マルチパートアップロードオブジェクトの検証

#### （1）オブジェクトのチェックサムの計算

オブジェクトの分割をシミュレートし、オブジェクト全体のチェックサムを計算します。以下ではMD5検証アルゴリズムによってオブジェクトのチェックサムを取得しますが、ユーザーはご自身で他の検証アルゴリズムを選択することができます。

```python
OBJECT_PART_SIZE = 1024 * 1024      #シミュレートした各パートのサイズ
OBJECT_TOTAL_SIZE = OBJECT_PART_SIZE * 1 + 123      #オブジェクト全体のサイズ
object_body = '1' * OBJECT_TOTAL_SIZE       #オブジェクトの内容

#オブジェクト内容全体のMD5チェックサムを計算
md5 = hashlib.md5()
md5.update(object_body)
md5_str = md5.hexdigest()
```

#### （2）マルチパートアップロードの初期化

マルチパートアップロードの初期化の際、カスタムパラメータx-cos-meta-md5を設定し、オブジェクト全体のMD5チェックサムをパラメータの内容とします。

```python
#マルチパートアップロードの初期化
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',  #ご自身のBucket名に置き換えます。examplebucketはバケットの例、1250000000はAPPIDの例です。
    Key='exampleobject-2',              #アップロードするオブジェクトのKey値に置き換えます 
    StorageClass='STANDARD',            #オブジェクトのストレージクラス
    Metadata={
        'x-cos-meta-md5' : md5_str      #カスタムパラメータの設定、MD5チェックサムに設定
    }
)
#マルチパートアップロードのUploadIdを取得
upload_id = response['UploadId']
```

#### （3）オブジェクトのマルチパートアップロード

オブジェクトのマルチパートアップロードは、オブジェクトを複数のパートに分割してアップロードを行うもので、最大10000パートの分割をサポートします。各パートのサイズは1MB～5GBで、最後のパートは1MB未満とすることができます。マルチパートアップロードの際は、各パートのPartNumber（番号）を設定する必要があります。パートの検証はEnableMD5=Trueで有効化でき、有効にするとアップロードの消費時間が増加します。このときPython SDKは各パートのContent-MD5を計算し、COSサーバーが受信したオブジェクトのMD5チェックサムとContent-MD5が一致した場合のみ、パートのアップロードを正常に行います。アップロードに成功すると、各パートのETagが返されます。     

```python
#マルチパートアップロードオブジェクト。各パートのサイズがOBJECT_PART_SIZEであり、最後のパートはOBJECT_PART_SIZE未満とすることができます
part_list = list()
position = 0
left_size = OBJECT_TOTAL_SIZE
part_number = 0
while left_size > 0:
    part_number += 1
    if left_size >= OBJECT_PART_SIZE:
        body = object_body[position:position+OBJECT_PART_SIZE]
    else:
        body = object_body[position:]
    position += OBJECT_PART_SIZE
    left_size -= OBJECT_PART_SIZE

    #パートアップロード
    response = client.upload_part(
        Bucket='examplebucket-1250000000',  #ご自身のBucket名に置き換えます。examplebucketはバケットの例、1250000000はAPPIDの例です。
        Key='exampleobject-2',              #オブジェクトのKey値 
        Body=body,
        PartNumber=part_number,
        UploadId=upload_id,
        EnableMD5=True       #パート検証を有効化します。COSサーバーが各パートに対しMD5検証を行います。
    )
    etag = response['ETag']     #ETagは各パートのMD5値を表します
    part_list.append({'ETag' : etag, 'PartNumber' : part_number})
    print etag + ', ' + str(part_number)
```

#### （4）マルチパートアップロードの完了

すべてのパートのアップロードが完了した後、マルチパートアップロード完了操作を行う必要があります。各パートのETagとPartNumberをそれぞれ対応させ、COSサーバーを使用してパートの正確性を検証します。マルチパートアップロードの完了後に返されるETagは合体後のオブジェクトの一意のタグ値を表すもので、オブジェクト内容全体のMD5チェックサムを表すものではありません。このためオブジェクトをダウンロードする際は、カスタムパラメータによって検証を行ってください。

```python
#マルチパートアップロードの完了
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',  #ご自身のBucket名に置き換えます。examplebucketはバケットの例、1250000000はAPPIDの例です。
    Key='exampleobject-2',              #オブジェクトのKey値 
    UploadId=upload_id,
    MultipartUpload={       #各パートのETagとPartNumberそれぞれの対応が必要
        'Part' : part_list    
    },
)

#ETagは合体後のオブジェクトの一意のタグ値を表すもので、この値はオブジェクトのMD5チェックサムではなく、オブジェクトの一意性のチェックのみに用いられます。
print "ETag: " + response['ETag']   
print "Location: " + response['Location']   #URLアドレス
print "Key: " + response['Key'] 
```

#### （5）オブジェクトのダウンロード

オブジェクトをダウンロードし、ユーザー定義のパラメータを取得します。

```python
# オブジェクトのダウンロード
response = client.get_object(
    Bucket='examplebucket-1250000000',  #ご自身のBucket名に置き換えます。examplebucketはバケットの例、1250000000はAPPIDの例です。
    Key='exampleobject-2'               #オブジェクトのKey値 
)
print 'ETag: ' + response['ETag']                        #オブジェクトのETagはオブジェクト内容のMD5チェックサムではありません
print 'x-cos-meta-md5: ' + response['x-cos-meta-md5']    #ユーザー定義のパラメータx-cos-meta-md5を取得
```

#### （6）オブジェクトの検証

オブジェクトのダウンロードに成功後、ユーザーはオブジェクトのMD5チェックサムを再計算し、ユーザー定義のパラメータx-cos-meta-md5と比較し、ダウンロードしたオブジェクトとアップロードしたオブジェクトの内容が一致するかどうかを検証します。

```python
#ダウンロードオブジェクトのMD5チェックサムを計算
fp = response['Body'].get_raw_stream()
DEFAULT_CHUNK_SIZE = 1024*1024
md5 = hashlib.md5()
chunk = fp.read(DEFAULT_CHUNK_SIZE)     
while chunk:
    md5.update(chunk)
    chunk = fp.read(DEFAULT_CHUNK_SIZE)
md5_str = md5.hexdigest()
print 'download object md5: ' + md5_str

#ダウンロードオブジェクトのMD5チェックサムとアップロードオブジェクトのMD5チェックサムを比較し、オブジェクトの整合性を検証します
if md5_str == response['x-cos-meta-md5']:
    print 'MD5 check OK'
else:
    print 'MD5 check FAIL'
```

