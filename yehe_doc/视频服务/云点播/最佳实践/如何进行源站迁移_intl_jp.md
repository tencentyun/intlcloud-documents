## 概要

VOD Migrate Toolは、データマイグレーション機能を集約化した一体型ツールです。シンプルな設定ファイルを編集することで、ユーザーはソースアドレスのメディアファイルをVODに迅速にマイグレーションできます。

## サポートするデータソース
* [x] ローカルフォルダ
* [x] URLリスト
* [x] Tencent Cloud COS
* [x] AWS S3
* [x] Alibaba Cloud OSS
* [x] Qiniu Kodo

## 使用環境

#### システム環境

Windows、Linux 、macOSシステムをサポートします。

#### ソフトウェア依存

- Python 2.7/3.4+。
- 最新バージョンのpip。
  
## インストール

###  Pipによるインストール（推奨）
SDKをpipによってプロジェクトにインストールすることができます。プロジェクト環境にまだpipをインストールしていない場合は、pip公式サイトを参照してインストールしてください。

```
pip install vodmigrate
```


### ソースコードパッケージによるインストール
ソースコードダウンロードアドレス：[ここをクリック](https://github.com/tencentyun/vod-migrate.git)。
最新コードをダウンロードして解凍後：

```shell
git clone https://github.com/tencentyun/vod-migrate.git
cd vod-migrate
python setup.py install
```

## ユースケース
コマンドの実行：
```
vodmigrate config.toml
```
> ?マイグレーションが完了すると、結果は設定項目"migrateResultOutputPath"に対応するディレクトリに出力されます。ファイル名：vod_migrate_result.txt。

## 設定ファイルの説明
設定ファイルは、toml形式（参考：[config_template.toml](https://github.com/tencentyun/vod-migrate/blob/master/test/config_template.toml)を採用しています。ファイルがUTF-8でエンコードされていること確認してください）。ファイルの内容は以下のいくつかの部分に分けられます。

### 1. マイグレーションの種類の設定

typeはマイグレーションのニーズに応じて入力するマイグレーションのタイプを表します。例えば、ローカルデータをVODにマイグレーションする場合は、`[migrateType]`の設定内容は`type=migrateLocal`になります。
```
[migrateType]
type="migrateLocal"
```
現在サポートするマイグレーションの種類は以下のとおりです。

| migrateType  |           説明           |
| :----------- | :----------------------: |
| migrateLocal |     ローカルからVODにマイグレーション     |
| migrateUrl   |   ダウンロードURLからVODにマイグレーション   |
| migrateCos   | Tencent Cloud COSからVODにマイグレーション|
| migrateAws   |    AWS S3からVODにマイグレーション   |
| migrateAli   | Alibaba Cloud OSSからVODにマイグレーション |
| migrateQiniu |  Qiniu KodoからVODにマイグレーション |

### 2. マイグレーションタスクの設定

ユーザーは実際のマイグレーションのニーズに従って関連設定を行います。主にVOD設定とタスク設定の情報関連のマイグレーションになります。

``` 
#マイグレーションツールの標準設定
[common]
secretId = "SECRETID"
secretKey = "SECRETKEY"
region = 'REGION'
subAppId = 0
concurrency = 5
supportMediaClassification = [ 'video', 'audio', 'image' ]
excludeMediaType = [  ]
migrateDbStoragePath = ''
migrateResultOutputPath = ''
``` 

| 名称                       |                                                                                        説明                                                                                        |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| secretId                   |              SecretIdはユーザーキーです。`SECRETID`を実際のキー情報に置換してください。 [CAMコンソール](https://console.cloud.tencent.com/cam/capi) のTencent Cloud API キー画面に進んで取得することができます。             |
| secretKey                   |             SecretKeyはユーザーキーです。`SECRETKEY`を実際のキー情報に置換してください。 [CAMコンソール](https://console.cloud.tencent.com/cam/capi) のTencent Cloud API キー画面に進んで取得することができます。             |
| region                     | アクセスポイントリージョンとは、VODサーバーをリクエストするリージョンのことで、ストレージリージョンとは異なります。詳細はサポートする[リージョンリスト](https://intl.cloud.tencent.com/document/product/266/34113) をご参照ください。|
| subAppId                   |                 VODの[サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987) IDです。ファイルをサブアプリケーションにマイグレーションする場合は、このフィールドにサブアプリケーションIDを入力します。マイグレーションの必要がない場合、入力する必要はありません。             |
| concurrency                |                                                                            同時にマイグレーションされるファイルの数量。最大値50                                                                            |
| supportMediaClassification |                                                        マイグレーションでサポートされるメディアタイプのリスト。有効値：video（ビデオ）、audio（オーディオ）、image（画像）                                                         |
| excludeMediaType           |                                                                               排除するファイルタイプのリスト                                                                               |
| migrateDbStoragePath       |                                                                           マイグレーションされたdbの保存パス。空欄の場合は、現在のディレクトリを意味します。                                                                           |
| migrateResultOutputPath    |                                                      マイグレーション結果の保存パス（1個のマイグレーションレコードは、1行のjson形式の文字列に対応）。空欄の場合は、現在のディレクトリを意味します。                                                      |

ファイルタイプの説明：
- ビデオ：MP4、TS、FLV、WMV、ASF、RM、RMVB、MPG、MPEG、3GP、MOV、WEBM、MKV、AVI、** HLS、DASHはサポートしない**
- オーディオ：MP3、M4A、FLAC、OGG、WAV
- 画像：JPG、JPEG、PNG、GIF、BMP、TIFF、AI、CDR、EPS

### 3. データソース情報の設定
[migrateType] のマイグレーションタイプに従って、対応するセクションを設定します。例えば、 [migrateType] の設定内容がtype=migrateLocalであれば、ユーザーは [migrateLocal] セクションを設定するだけです。

#### 3.1 ローカルのデータソースmigrateLocalの設定

ローカルからVODにマイグレーションする場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。

``` 
# ローカルからVODへのマイグレーションの設定セクション
[migrateLocal]
localPath = ''
excludes = [ ]
``` 

| 設定項目    |                                 説明                                  |
| :-------- | :-------------------------------------------------------------------: |
| localPath |                     ローカルパスは、絶対パスの形式である必要があります                      |
| excludes  | 排除するディレクトリの絶対パス。localPathのディレクトリにあるファイルはマイグレーションされないことを示します。 |

#### 3.2 URLリストのデータソースmigrateUrlの設定
指定したURLリストからVODにマイグレーションする場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
```
# URLリストのダウンロードからVODにマイグレーションするための設定セクション
[migrateUrl]
urllistPath = 'D:\folder\urllist.txt'
```

| 設定項目      |                                    説明                                    |
| :---------- | :------------------------------------------------------------------------: |
| urllistPath | URLリストを保存しているファイルの絶対パス。ファイルの内容は1行に1個の元のURLアドレスを含むURLテキストです。|

>?ローカルの大型ファイルをVODにマイグレーションする必要がある場合は、 [pullUpload](https://intl.cloud.tencent.com/document/product/266/34118) インターフェースを使用してプルすることをお勧めします。
#### 3.3 COSデータソースmigrateCosの設定

Tencent CloudのCOSからVODにマイグレーションする場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
``` 
# Tencent CloudのCOSからVODへのマイグレーションの設定セクション
[migrateCos]
region = 'ap-shanghai'
bucket = 'examplebucket-1250000000'
secretId = 'COS_SECRETID'
secretKey = 'COS_SECRETKEY'
prefix = ''
``` 

| 設定項目    |                                                    説明                                                     |
| :-------- | :---------------------------------------------------------------------------------------------------------: |
| region    |        BucketのRegion情報については[アベイラビリティリージョン](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください        |
| bucket    |`<BucketName-APPID>`形式のBucket名。 Bucket名はAPPIDを必ず含める必要があります。例：examplebucket-1250000000 |
| secretId  |   Bucketが属するユーザーキーのsecretId。[Tencent Cloud APIキー](https://console.cloud.tencent.com/cam/capi) で表示することができます。  |
| secretKey |  Bucketが属するユーザーキーのsecretKey。 [Tencent Cloud APIキー](https://console.cloud.tencent.com/cam/capi) で表示することができます。  |
| prefix    |                     マイグレーションするパスのプレフィックス。Bucketの全データをマイグレーションする場合は、prefixを空欄にします。                      |

#### 3.4 AWSデータソースmigrateAwsの設定
AWSからVODにマイグレーションする場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
```
# AWSからVODへのマイグレーションの設定セクション
[migrateAws]
region = 'ap-northeast-2'
bucket = 'bucket-aws'
accessKeyId = 'AccessKeyId'
accessKeySecret = 'AccessKeySecret'
prefix = ''
```

| 設定項目          |                                説明                                |
| :-------------- | :----------------------------------------------------------------: |
| region          |                        AWS COS Region                         |
| bucket          |                      AWS COS Bucket名                      |
| accessKeyId     |                   AccessKeyIdをユーザーキーに置換                   |
| accessKeySecret |                 AccessKeySecretをユーザーキーに置換                 |
| prefix    |                    マイグレーションするパスのプレフィックス。 Bucketの全データをマイグレーションする場合は、prefixを空欄にします。                      |

#### 3.5 Alibaba OSSデータソースmigrateAliの設定
Alibaba Cloud OSSからVODにマイグレーションする場合は、この部分の設定を行います。具体的な設定項目及び説明は以下のとおりです。

```
# Alibaba OSSからVODへのマイグレーションの設定セクション
[migrateAli]
bucket = 'bucket-aliyun'
accessKeyId = 'yourAccessKeyId'
accessKeySecret = 'yourAccessKeySecret'
endPoint = 'oss-cn-hangzhou.aliyuncs.com'
prefix = ''
```

| 設定項目          |                                説明                                |
| :-------------- | :----------------------------------------------------------------: |
| bucket          |                       Alibaba Cloud OSS Bucket名                       |
| accessKeyId     |                 yourAccessKeyIdをユーザーキーに置換                 |
| accessKeySecret |               yourAccessKeySecretをユーザーキーに置換              |
| endPoint        |                        Alibaba Cloud endpointアドレス                        |
| prefix    |                     マイグレーションするパスのプレフィックス。Bucketの全データをマイグレーションする場合は、prefixを空欄にします                      |

#### 3.6 QiniuデータソースmigrateQiniuの設定
QiniuからVODにマイグレーションする場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
```
# QiniuからVODへのマイグレーションの設定セクション
[migrateQiniu]
bucket = 'bucket-qiniu'
accessKeyId = 'AccessKey'
accessKeySecret = 'SecretKey'
endPoint = 'www.bkt.clouddn.com'
prefix = ''
```

| 設定項目          |                                説明                                |
| :-------------- | :----------------------------------------------------------------: |
| bucket          |                      Qiniu Kodo Bucket名                      |
| accessKeyId     |                    AccessKeyをユーザーキーに置換                    |
| accessKeySecret |                    SecretKeyをユーザーキーに置換                    |
| endPoint        |                 QiniuダウンロードアドレスはdownloadDomainに対応                  |
| prefix          | マイグレーションするパスのプレフィックス。Bucketの全データをマイグレーションする場合、prefixを空欄にします |

## 制限事項
- このツールは1回限りのマイグレーションツールとして設計されています。マイグレーションは**オリジンサーバーのファイルスキャン**、**マイグレーション中**、**マイグレーションの完了**の3段階に分かれます。ファイルスキャンの完了後は、設定変更が必要な場合は、md5ファイルのチェックでエラーが発生しないように、dbファイルをクリアする必要があります（migrate.dbの削除またはdbストレージパスの修正）。
- マイグレーションするファイルは接尾辞を付けて表示する必要があります。
- HLS/DASHのマイグレーションは現在サポートしていません。
- マイグレーション後は、元のビデオ間のディレクトリ関係は維持できず、各ビデオには独立したFileIdがあり、相互には関連していません。

## マイグレーションフローの概要
1. 設定ファイルが読み取られ、セクションがマイグレーションtypeに従って読み取られ、パラメータがチェックされます。
2. オリジンサーバーはマイグレーションタイプに従ってスキャンされ、マイグレーションタスクが生成されます。
3. スキャンが完了すると、マイグレーションが実行され、各タスクの結果および全体の進捗が出力されます。
4. マイグレーションが完了すると、詳細情報が結果ファイルに出力されます。
![](https://main.qcloudimg.com/raw/66946618fe7e54ea19f7a8a78890078b.png)

