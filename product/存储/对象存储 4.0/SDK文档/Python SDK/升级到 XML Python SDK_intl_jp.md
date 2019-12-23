Python SDK V4とXML Python SDKのドキュメントを詳しく比較すると、単なる増分アップデートではないことがわかります。XML Python SDKはアーキテクチャ、可用性およびセキュリティが大幅に向上し、そして使いやすさ、ロバスト性、および伝送性能も大幅に向上しています。XML Python SDKにアップグレードする場合は、次のガイドラインを参照して、Python SDKのアップグレードを完了してください。

## 機能比較

下記のグラフに、JSON Python SDKとXML Python SDKの主な機能の比較を示しています。

| 機能       | XML Python SDK         | JSON Python SDK                         |
| -------- | :------------: | :------------------:    |
| ファイルのアップロード | ローカルファイル、バイトストリーム、入力ストリームのアップロードが可能<br>デフォルトでは、アップロードを上書きします<br>アップロードモードを知的に判断し、断続的なアップロード可能<br>簡単なアップロードは最大5GBをサポートします<br>マルチパートアップロードは最大48.82TB（50,000GB）をサポートします| ローカルファイルのアップロードのみサポートします<br>上書きかどうかが選択できます<br>簡単なアップロードかシャードアップロードかを手動で選択する必要があります<br>簡単なアップロードは最大20MBをサポートします<br>シャードアップロードは最大64GBをサポートします|
| バケット基本操作 | バケットの作成<br>バケットの取得<br>バケットの削除   | サポートしません |
| バケットACL操作 | バケットACLを設定します<br>バケットACLの設定を取得します<br>バケットACLの設定を削除します   | サポートしません |
| バケットライフサイクル | バケットライフサイクルを作成します<br>バケットライフサイクルを取得します<br>バケットライフサイクルを削除します | サポートしません |
| ディレクトリ操作 | APIを独立に提供しません   | ディレクトリを作成します<br>ディレクトリを照合します<br>ディレクトリを削除します |


## アップグレード手順
下記の4つの手順に従ってPython SDKをアップグレードしてください。 
**1. Python SDKのアップデート**

pipコマンドをを通して最新のXML Python SDKを簡単に取得できます。
```
 pip uninstall qcloud_cos_v4

 pip install -U cos-python-sdk-v5
```

また、Python SDK[クイックスタート](https://cloud.tencent.com/document/product/436/12269)を参照して、適切なインストール方法を選択してください。


**2. SDKの初期化の変更**

XML Python SDKにCosConfigオブジェクトが追加され、COSへのアクセス構成を管理できるようになりました。また、プロトコルHTTP/HTTPS、一時暗号鍵などの情報へのアクセスを簡単に設定できます。下記の例に従ってSDKを初期化してください。

JSON Python SDKの初期化方式は下記の通りです。

```
secret_id = u'COS_SECRETID'     # ユーザーのsecretIdに置き換える
secret_key = u'COS_SECRETKEY'     # ユーザーのsecretKeyに置き換える
region = 'sh'                # ユーザーのRegionに置き換える
appid = 100000              # ユーザーのappidに置き換える
cos_client = CosClient(appid, secret_id, secret_key, region=region)
```

XML Python SDKの初期化方式は下記の通りです。

```
#appidは既に構成から削除されました。パラメータBucketにappidを付けてください。Bucketはbucketname-appidで構成されます。
# 1. ユーザー構成を設定する場合、secretId、secretKeyおよびRegionなどを設定する必要があります
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'COS_SECRETID'     # ユーザーのsecretIdに置き換える
secret_key = 'COS_SECRETKEY'     # ユーザーのsecretKeyに置き換える
region = 'ap-shanghai'     # ユーザーのRegionに置き換える
token = None               # 一時暗号鍵を使用する場合、Tokenに渡す必要があります。デフォルトはブランクですから、入力しなくてもいいです。
scheme = 'https'           # http/httpsプロトコルでCOSへアクセスする場合、デフォルトはhttpsです。入力しなくてもいいです。
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. クライアントオブジェクトの取得
client = CosS3Client(config)
```


**3. バケット名称とAvailability Zoneの略称を変更します**

XML Python SDKのバケット名と可能な地域の略称はJSON Python SDKと異なる場合、ユーザーは対応して変更する必要があります。

**バケット**
XML Python SDKのバケット名はユーザーカスタマイズ文字列とAPPIDという2つの部分で構成されて、両者はハイフン「-」でつなぎます。
たとえば、`mybucket1-1250000000`の場合、その中`mybucket1`はユーザーカスタマイズ文字列で、`1250000000`はAPPIDです。
>?APPIDはTencent Cloudのアカウントタグの1つで、クラウドリソースの関連付けに用いられます。Tencent Cloudアカウントの登録ができたら、システムは自動でユーザーにAPPIDを発行します。[Tencent Cloudコンソール](https://console.cloud.tencent.com/) 【アカウント情報】を通じてAPPIDを確認できます。

バケットを設定する時、以下のサンプルコードを参照してください。
```
bucket = "examplebucket-1250000000"
file_name = "test.txt"
local_path = 'local.txt'
response = client.upload_file(
    Bucket=bucket,
    LocalFilePath=local_path,
    Key=file_name
)
```


**バケットのAvailability Zoneの略称Region**

XML Python SDKのバケット可能な地域の略称はが変更されました。初期化の時、バケットの領域の短縮名をCosConfigの中に設定します。下記の表には、異なる地域はJSON Python SDKとXML Python SDKでの対応関係を示しています。

| 地域       | XML Python SDK　地域略称         | JSON Python SDK　地域略称                         |
| -------- | ------------ | ---------------------------------------- |
| 北京1区（華北） | ap-beijing-1 | tj |
| 北京       | ap-beijing   | bj |
| 上海（華東）   | ap-shanghai  | sh |
| 広州（華南）   | ap-guangzhou | gz |
| 成都（西南）   | ap-chengdu   | cd |
| 重慶       | ap-chongqing | 無し |
| シンガポール      | ap-singapore | sgp |
| 香港       | ap-hongkong  | hk |
| トロント      | na-toronto   | ca |
| フランクフルト     | eu-frankfurt | ger |
| ムンバイ       | ap-mumbai    | 無し |
| ソウル       | ap-seoul     | 無し |
| シリコンバレー       | na-siliconvalley     | 無し |
| バージニア       | na-ashburn     | 無し |
| バンコク       | ap-bangkok     | 無し |
| モスクワ       | eu-moscow     | 無し |


**4. APIの変更
XML Python SDKにアップグレードした後、一部操作のAPIが変更されました。実際のニーズに合わせて変更してください。SDKを使いやすくするためにAPIをカプセル化しました。詳細については、例と[APIドキュメント](https://cloud.tencent.com/document/product/436/12270)を参照してください。
API変化は以下の4点があります。

**1）独立のディレクトリAPIがありません**

XML SDKでは、個別のディレクトリAPIは提供されなくなりました。COSにはフォルダとディレクトリの概念はありません。COSでは、オブジェクト`project/a.txt`のアップロードによってprojectフォルダは作成されません。ユーザーの使用習慣を満たすために、COSはコンソールやCOS browserなどのグラフィカルツールに「フォルダ」または「ディレクトリ」の表示方法をエミュレートします。具体的にはキー値が`project/`で、中身がブランクのオブジェクトを作成することで、従来のフォルダをエミュレートする表示方法で実現します。

たとえば、アップロードオブジェクト`project/doc/a.txt`、区切り記号`/`は「フォルダ」の表示方法をシミュレートし、コンソールに「フォルダ」projectとdocが表示されます。そのうち、docはprojectの下位レベルの「フォルダ」で、a.txtファイルが含まれています。

したがって、適用シナリオは単にファイルをアップロードするだけの場合は、最初にフォルダを作成せずに、直接アップロードすることができます。適用シナリオにフォルダの概念がある場合、フォルダの作成機能を提供する必要があります。パスは` / `で終わる0KBのファイルをアップロードすることができます。これにより、GetBucket　APIを呼び出すときに、このファイルをフォルダとして扱うことができます。



**2）ハイレベルのアップロードAPI**

XML SDKには、ハイレベルのアップロードAPIがカプセル化されています。このAPIはファイルサイズに応じて簡単なアップロードまたはマルチパートアップロードをインテリジェントに選択できます。マルチパートアップロードには断続的なアップロード機能があり、同時にスレッド数を設定することによってアップロード速度を制御することもできます。

ハイレベルのアップロードAPIを使用して、断続的にアップロードする時のサンプルコードは下記のとおりです。

```
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)
```

**3）署名アルゴリズムの変化**

通常は手動で署名を計算する必要がないが、SDKの署名をフロントエンドに返却して使用する場合、署名アルゴリズムの変化に注意してください。署名につき、単回と複数回署名の区別がなくなり、一方、署名の有効期の設定により安全性を確保するようになります。詳しいアルゴリズムについては、[XML署名のリクエスト](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください。

**4）新しいAPI**

XML Python SDKに新しいAPIが追加され、ニーズに応じて呼び出すことができます。以下を含みます：

*バケットの操作、たとえばcreate_bucket、delete_bucket、list_objectsなど。
*バケットACLの操作、たとえばput_bucket_acl、get_bucket_aclなど。
*バケットのライフサイクルの操作、たとえばput_bucket_lifecycle、get_bucket_lifecycleなど。

詳細については、Python SDK[APIドキュメント](https://cloud.tencent.com/document/product/436/12270)を参照してください。

