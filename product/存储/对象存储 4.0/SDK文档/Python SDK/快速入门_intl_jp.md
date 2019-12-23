## 開発準備

### 関連するリソース
COSのXML Python SDKリソースのダウンロードアドレス：[XML Python SDK ](https://github.com/tencentyun/cos-python-sdk-v5)。
Demoのダウンロードアドレス：[XML Python Demo](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py)。

### 環境依存関係

COSのXML Python SDKは今の段階でPython　2.6、Python　2.7、およびPython　3.xが対応できます。
>?文章に記載されているSecretId、SecretKey、Bucketなどの名称の意味と取得方式については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

### SDKインストール

SDKをインストールする3つの方法：pipインストール、手動インストール、オフラインインストール。

####　pipインストール（推奨）
```sh
 pip install -U cos-python-sdk-v5
```

####　手動インストール
[XML Python SDK](https://github.com/tencentyun/cos-python-sdk-v5)からソースコードをダウンロードし、setupを使用して手動でインストールし、下記のコマンドを実行します。
```python
 python setup.py install
```
#### オフラインインストール
```python
# パブリックネットワークに接続するマシンで下記のコマンドを実行します
mkdir cos-python-sdk-packages
pip download cos-python-sdk-v5 -d cos-python-sdk-packages
tar -czvf cos-python-sdk-packages.tar.gz cos-python-sdk-packages

# インストールパッケージをパブリックネットワークに接続しないマシンにコピーした後、下記のコマンドを実行します
# 両方のマシンのpythonバージョンが一致していることを確認してください。そうでなければ、インストール失敗の可能性があります
tar -xzvf cos-python-sdk-packages.tar.gz
pip install cos-python-sdk-v5 --no-index -f cos-python-sdk-packages
```
 
## クイックスタート
下記のサンプルコードを参照してください。
```python
#appidは既に構成から削除されました。パラメータBucketにappidを付けてください。Bucketはbucketname-appidで構成されます。
# 1. ユーザー構成を設定する場合、secretId、secretKeyおよびRegionなどを設定する必要があります
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'xxxxxxxx'      # ユーザーのsecretIdに置き換え
secret_key = 'xxxxxxx'      # ユーザーのsecretKeyに置き換え
region = 'ap-beijing-1'    # ユーザーのRegionに置き換える
token = None                # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです
scheme = 'https'            # http/httpsプロトコルでCOSへアクセスする場合、デフォルトはhttpsです。入力しなくてもいいです
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. クライアントオブジェクトの取得
client = CosS3Client(config)
下記の説明、あるいはDemoプログラムを参照してください。詳細については、https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.pyをご覧ください。
```

一時暗号鍵の生成および使用方法については、[一時暗号鍵の生成と使用ガイド](https://cloud.tencent.com/document/product/436/14048)を参照してください。

## ファイルアップロード
### ファイルストリームの簡単なアップロード
```python
file_name = 'test.txt'
# 2進数モード（binary mode）でファイルを開くことを強くお勧めします。そうでなければ、エラーが発生する可能性があります
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='test04-123456789',
        Body=fp,
        Key=file_name,
        StorageClass='STANDARD',
        EnableMD5=False
    )
print(response['ETag'])
```
#### パラメータ説明
| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket| バケット名は、bucketname-appidからなります|String　| はい　| 
|  Body | アップロードするファイルの内容はファイルストリームまたはバイトストリームです|file/bytes|はい | 
|  Key  |  オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです |String|はい | 
|  StorageClass | ファイルのストレージタイプを設定します。STANDARD、STANDARD_IA、デフォルト値：STANDARD| String |いいえ| 
| EnableMD5 | SDKによるContent-MD5の計算が必要ですか。デフォルトはオフになっています。オンにすると、アップロードに多くの時間がかかります|Bool | いいえ| 

その他の選択可能なパラメーターについては、[Python SDK APIドキュメント](https://cloud.tencent.com/document/product/436/12270)を参照してください。

### バイトストリームの簡単なアップロード
```python
response = client.put_object(
    Bucket='test04-123456789',
    Body=b'abcdefg',
    Key=file_name,
    EnableMD5=False
)
print(response['ETag'])

```
### chunkの簡単なアップロード
```python
import requests
stream = requests.get('https://intl.cloud.tencent.com/document/product/436/7778')

# ネットワークフローはTransfer-Encoding:chunked方式でCOSに転送されます。
response = client.put_object(
    Bucket='test04-123456789',
    Body=stream,
    Key=file_name
)
print(response['ETag'])
```

### ローカルパスの簡単なアップロード
```python
response = client.put_object_from_local_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    EnableMD5=False
)
print(response['ETag'])
```

### HTTPヘッダー設定の簡単なアップロード
```python
response = client.put_object(
    Bucket='test04-123456789',
    Body=b'test',
    Key=file_name,
    ContentType='text/html; charset=utf-8',
    EnableMD5=False
)
print(response['ETag'])
```

### カスタムヘッダー設定の簡単なアップロード
```python
response = client.put_object(
    Bucket='test04-123456789',
    Body=b'test',
    Key=file_name,
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    EnableMD5=False
)
print(response['ETag'])
```

### ハイレベルのアップロードAPI（推奨）
ファイルサイズに応じて、簡単なアップロード、またはマルチパートアップロードを自動的に選択します。マルチパートアップロードには、継続送信機能があります。
```python
response = client.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10,
    EnableMD5=False
)
print(response['ETag'])
```

## ファイルのダウンロード
### ローカルへのファイル取得
```python
response = client.get_object(
    Bucket='test04-123456789',
    Key=file_name,
)
response['Body'].get_stream_to_file('output.txt')
```
#### パラメータ説明
| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|  Bucket |  バケット名称は、bucketname-appidからなります|String|はい |
| Key | オブジェクトキー(Key)は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String | はい |

その他の選択可能なパラメーターについては、[Python SDK APIドキュメント](https://cloud.tencent.com/document/product/436/12270)を参照してください。

### ファイルストリームの取得
```python
response = client.get_object(
    Bucket='test04-123456789',
    Key=file_name,
)
fp = response['Body'].get_raw_stream()
print(fp.read(2))
```

### Response HTTPヘッダーの設定
```python
response = client.get_object(
    Bucket='test04-123456789',
    Key=file_name,
    ResponseContentType='text/html; charset=utf-8'
)
print response['Content-Type']
fp = response['Body'].get_raw_stream()
print(fp.read(2))
```

### ダウンロード範囲の指定
```python
response = client.get_object(
    Bucket='test04-123456789',
    Key=file_name,
    Range='bytes=0-10'
)
fp = response['Body'].get_raw_stream()
print(fp.read())
```
## 異常タイプ
CosClientErrorとCosServiceErrorはそれぞれSDKクライアントエラーとCOSサーバーエラーに対応します。

### CosClientError
CosClientErrorは通常timeoutなどによるクライアントエラーを指します。ユーザーは取得した後、再試行またはその他の操作が選択できます。

### CosServiceError
CosServiceErrorはサーバーから返された具体的な情報を提供します。
```python
#except CosServiceError as e
e.get_origin_msg()  # 元のエラーメッセージを取得する場合、フォーマットはXMLです
e.get_digest_msg()  # 処理済みのエラー情報を取得する場合、フォーマットはdictです
e.get_status_code() # httpのエラーコードを取得する場合（例えば4XX,5XX)
e.get_error_code() # COSで定義されたエラーコードの取得
e.get_error_msg()  # COSエラーコードの具体的な説明の取得
e.get_trace_id()    # 要求のtrace_idの取得
e.get_request_id() # 要求のrequest_idの取得
e.get_resource_location() # URLアドレスの取得
```

