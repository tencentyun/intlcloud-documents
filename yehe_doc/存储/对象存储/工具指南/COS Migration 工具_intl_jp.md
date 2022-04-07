
## 機能説明
COS Migrationは、COSのデータ移行機能を統合したオールインワンツールです。簡単な設定操作により、ユーザーは元アドレスデータをCOSにすばやく移行することができ、以下のような特徴を持っています。
- 豊富なデータソース
   - ローカルデータ：ローカルに保存されているデータをCOSに移行します。
   - その他クラウドストレージ：現在、AWS S3、Alibaba Cloud OSS、Qiniu StorageからのCOSへの移行をサポートしており、今後も拡張していく予定です。
   - URLリスト：指定されたURLダウンロードリストに従ってダウンロードし、COSに移行します。
   - Bucket間相互コピー：COSのBucketデータは相互コピーされ、クロスアカウント、クロスリージョンのデータコピーをサポートします。
- 中断からの再開：ツールはアップロード時の中断からの再開をサポートしています。大容量ファイルについては、途中で終了した場合やサービスの障害があった場合、ツールを再実行して、アップロードが完了していないファイルのアップロードを再開することができます。
- マルチパートアップロード：COSにオブジェクトをチャンクでアップロードします。
- 並列アップロード：複数のオブジェクトの同時アップロードをサポートします。
- 移行チェック：オブジェクトの移行後のチェックです。

>!
>- COS Migrationのエンコード形式は、UTF-8形式のみをサポートします。
>- このツールを使って同名ファイルをアップロードすると、デフォルトでは古い方の同名ファイルが上書きされます。同名ファイルをスキップするには、追加の設定が必要です。

## 使用環境
#### システム環境
Windows、LinuxおよびmacOSシステム。

#### ソフトウェア依存
JDK 1.8 X64以降、JDKのインストールと設定の詳細については、[Javaのインストールと設定](https://intl.cloud.tencent.com/document/product/436/10865)をご参照ください。
- Linux環境ではIFUNCのサポートが必要です。環境のbinutilsのバージョンをチェックし、2.20以降のバージョンであることを確認します。

## 利用方法
### 1. ツールの取得
[COS Migrationツール](https://github.com/tencentyun/cos_migrate_tool_v5)に移動してダウンロードします。

### 2. 解凍ツールキット
####  Windows
解凍して、次のようにディレクトリに保存します。
```plaintext
C:\Users\Administrator\Downloads\cos_migrate
```

####  Linux
解凍して、いずれかのディレクトリに保存します。
```plaintext
unzip cos_migrate_tool_v5-master.zip && cd cos_migrate_tool_v5-master
```

#### マイグレーションツールの構造
COS Migrationツールを正しく解凍すると、次のようなディレクトリ構造になります。
```plaintext
COS_Migrate_tool
|——conf  #設定ファイルが配置されているディレクトリ
|   |——config.ini  #設定ファイルの移行
|——db    #移行に成功した記録を保存
|——dep   #プログラムのメインロジックコンパイルによって発行されたJARパッケージ
|——log   #ツールの実行中に発行されたログ
|——opbin #コンパイル用スクリプト
|——src   #ツールのソースコード
|——tmp   #一時ファイルストレージディレクトリ
|——pom.xml #プロジェクト設定ファイル
|——README  #説明ドキュメント
|——start_migrate.sh  #Linuxでの移行起動スクリプト
|——start_migrate.bat #Windowsでの移行起動スクリプト
```

>?
 - dbディレクトリには、主にツールの移行に成功したファイル識別子が記録されています。各移行タスクはdb内の記録に優先順位をつけ、現在のファイル識別子がすでに記録されている場合は現在のファイルをスキップし、それ以外の場合はファイルの移行を実行します。
 - ログディレクトリには、ツールの移行に伴うすべてのログが記録されています。移行中にエラーが発生した場合は、まずこのディレクトリ内のerror.logをご確認ください。

### 3. 設定ファイルconfig.iniの変更
移行起動スクリプトを実行する前に、設定ファイルconfig.iniを変更する必要があります（パス：`./conf/config.ini`）。config.iniの内容は、以下のセクションに分けられます。

#### 3.1 移行タイプの設定
typeは移行タイプを示し、ユーザーは移行要件に基づいて対応する識別子を入力します。例えば、ローカルデータをCOSに移行する必要がある場合、`[migrateType]`の設定内容は、`type=migrateLocal`となります。
```plaintext
[migrateType]
type=migrateLocal
```

現在サポートするマイグレーションの種類は以下のとおりです。

| migrateType  |           説明           |
| ------| ------ |
| migrateLocal| ローカルからCOSに移行 |
| migrateAws| AWS S3からCOSに移行 |
| migrateAli| Alibaba OSSからCOSに移行 |
| migrateQiniu| QiniuからCOSに移行 |
| migrateUrl| ダウンロードURLからCOSに移行 |
| migrateBucketCopy| ソースBucketからターゲットBucketにコピー|
|migrateUpyun  | UPYUNからCOSに移行 |

#### 3.2 移行タスクの設定
ユーザーは、主にターゲットCOS情報への移行の設定や移行タスク関連の設定など、実際の移行要件に基づいた設定を行います。
```plaintext
# マイグレーションツールのパブリック設定セクションには、ターゲットCOSに移行する必要のあるアカウント情報が含まれます。
[common]
secretId=COS_SECRETID
secretKey=COS_SECRETKEY
bucketName=examplebucket-1250000000
region=ap-guangzhou
storageClass=Standard
cosPath=/
https=off
tmpFolder=./tmp
smallFileThreshold=5242880
smallFileExecutorNum=64
bigFileExecutorNum=8
entireFileMd5Attached=on
daemonMode=off
daemonModeInterVal=60
executeTimeWindow=00:00,24:00
outputFinishedFileFolder=./result
resume=false
skipSamePath=false
```

| 名称 | 説明 |デフォルト値|
| ------| ------ |----- |
| secretId| ユーザーキーのSecretIdです。`COS_SECRETID`を実際のキー情報に置き換えてください。[CAMコンソール](https://console.cloud.tencent.com/cam/capi)のTencent Cloud APIキー画面に進むと取得できます |-|
| secretKey| ユーザーキーのSecretKeyです。`COS_SECRETKEY`を実際のキー情報に置き換えてください。[CAMコンソール](https://console.cloud.tencent.com/cam/capi)のTencent Cloud APIキー画面に進むと取得できます|-|
| bucketName| ターゲットBucketの名称で、命名形式は`<BucketName-APPID>`。Bucket名には必ずAPPIDを含める必要があります。例： examplebucket-1250000000 |  -  |
| region| ターゲットBucketのRegion情報です。COSのリージョンの略称については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください |-|
| storageClass|   データ移行後のストレージタイプです。オプション値はStandard（標準ストレージ）、Standard_IA（低頻度ストレージ）、Archive(アーカイブストレージ)、Maz_Standard（複数のAZを備えた標準ストレージ）、Maz_Standard_IA（複数のAZを備えた低頻度ストレージ）です。詳細については、[ストレージタイプの概要](https://intl.cloud.tencent.com/document/product/436/30925)をご参照ください    |Standard|
| cosPath|移行先のCOSパスです。`/`はBucketのルートパスへの移行、`/folder/doc/`はBucketの`/folder/doc/`への移行を表します。`/folder/doc/`が存在しない場合は、自動的にパスが作成されます|/|
| https| HTTPS通信を使用するかどうかです。onはオン、offはオフを表します。オンの場合は通信速度が遅くなり、セキュリティ要件の高いシナリオに適しています|off|
| tmpFolder|他のクラウドストレージからCOSへの移行中に一時ファイルを保存するために使用されたディレクトリは、移行が完了すると削除されます。形式は絶対パスである必要があります。<br>Linuxの場合、`/a/b/c`のようにシングルスラッシュで区切ります。<br>Windowsの場合、`E:\\a\\b\\c`のようにダブルバックスラッシュ区切ります。<br>デフォルトでは、ツールが配置されているパスのtmpディレクトリです|./tmp|
| smallFileThreshold| 小さなファイルの閾値のバイトです。この閾値以上であれば、マルチパートアップロードを使用します。それ以外の場合はシンプルアップロードを使用します。デフォルトは5MBです |5242880|
| smallFileExecutorNum|小さなファイル（smallFileThresholdより小さいファイル）の同時実行性で、シンプルアップロードを使用します。パブリックネットワーク経由でCOSに接続しており、帯域幅が小さい場合は、この同時実行性を低下させてください|64|
| bigFileExecutorNum| 大きなファイル（smallFileThreshold以上のファイル）の同時実行性で、マルチパートアップロードを使用します。パブリックネットワーク経由でCOSに接続しており、帯域幅が小さい場合は、この同時実行性を低下させてください|8|
| entireFileMd5Attached|マイグレーションツールがフルテキストのMD5を計算し、その後の検証のためにファイルのカスタムヘッダーx-cos-meta-md5に格納することを表します。COSのマルチパートアップロードされた大きなファイルのetagは、フルテキストのMD5ではないからです|on|
| daemonMode|daemonモードを有効にするかどうかです。onはオン、offはオフを表します。daemonは、プログラムがループで同期を実行し、各ラウンドの同期の間隔はdaemonModeInterValパラメータで設定されることを表します|off|
| daemonModeInterVal|各同期ラウンドの後、次の同期ラウンドがどの程度の時間で行われるかを表します。単位は秒です |60|
| executeTimeWindow|実行時間ウィンドウで、時間粒度は分です。このパラメータは、マイグレーションツールが毎日実行される時間帯を定義します。例えば、<br>パラメータが03:30,21:00の場合、早朝03:30から夜21:00の間にタスクを実行することを表します。それ以外の時間はスリープ状態になり、移行は一時停止となり、自動的に再開される次のタイムウィンドウまで進捗が保持されます|00:00,24:00|
| outputFinishedFileFolder  | このディレクトリには、移行に成功した結果が保存されます。結果のファイルは、例えば`./result/2021-05-27.out`のように日付に基づいて命名されます。ここで./resultは、作成済みのディレクトリです。ファイル内容の各行の形式は、絶対パス\tファイルサイズ\t最終更新時刻です。設定を空欄にすると、結果は出力されません。| ./result |
| resume | ソースファイルのリストを、最後に実行した結果までトラバーサル処理し続けるかどうかです。デフォルトは先頭からです。 | false |
| skipSamePath | COSにすでに同名ファイルがある場合に、そのままスキップするかどうかです。デフォルトではスキップされず、元のファイルが上書きされます。| false |

#### 3.3 データソース情報の設定
`[migrateType]`の移行タイプに従って、対応するセクションを設定します。例えば、`[migrateType]`の設定内容が`type=migrateLocal`であれば、ユーザーは`[migrateLocal]`セクションで設定可能です。

**3.3.1 ローカルのデータソースmigrateLocalの設定**

ローカルからCOSに移行する場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
```plaintext
# ローカルからCOSへの移行の設定セクション
[migrateLocal]
localPath=E:\\code\\java\\workspace\\cos_migrate_tool\\test_data
excludes=
ignoreModifiedTimeLessThanSeconds=
```

| 設定項目 | 説明 |
| ------| ------ |
|localPath|ローカルディレクトリ。形式は絶対パスである必要があります。<ul  style="margin: 0;"><li>Linuxの場合、`/a/b/c`のようにシングルスラッシュで区切ります。</li><li>Windowsの場合、`E:\\a\\b\\c`のようにダブルバックスラッシュで区切ります</li></ul>|
|excludes| 除外するディレクトリまたはファイルの絶対パスで、localPathより下のディレクトリまたはファイルは移行されないことを表します。複数の絶対パスはセミコロンで区切ります。空欄の場合、localPathより下のすべてが移行されることを表します|
|ignoreModifiedTimeLessThanSeconds| 更新時間が現在時刻から一定時間に満たないファイルを除外します。単位は秒で、デフォルトでは設定されていません。これは、lastmodified時刻に基づくフィルタリングを行わないことを表します。ファイルの更新と同時にマイグレーションツールを実行し、更新中のファイルがCOSに移行、アップロードされないようにしたいお客様向けです。例えば300に設定すると、更新から5分以上経過したファイルのみをアップロードします|

**3.3.2 Alibaba OSSデータソースmigrateAliの設定**

Alibaba Cloud OSSからCOSに移行する場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
```plaintext
# Alibaba OSSからCOSへの移行の設定セクション
[migrateAli]
bucket=bucket-aliyun
accessKeyId=yourAccessKeyId
accessKeySecret=yourAccessKeySecret
endPoint= oss-cn-hangzhou.aliyuncs.com
prefix=
proxyHost=
proxyPort=
```

| 設定項目 | 説明 |
| ------| ------ |
|bucket|Alibaba Cloud OSS Bucket名|
|accessKeyId|yourAccessKeyIdをユーザーキーに置換 |
|accessKeySecret| yourAccessKeySecretをユーザーキーに置換|
|endPoint|Alibaba Cloud endpointアドレス|
|prefix|移行するパスのプレフィックス。Bucket内の全データを移行する場合は、prefixを空欄にします|
|proxyHost|プロキシを使用してアクセスする場合は、プロキシのIPアドレスを入力します|
|proxyPort|プロキシポート|

**3.3.3 AWSデータソースmigrateAwsの設定**

AWSからCOSに移行する場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
```plaintext
# AWSからCOSへの移行の設定セクション
[migrateAws]
bucket=bucket-aws
accessKeyId=AccessKeyId
accessKeySecret=SecretAccessKey
endPoint=s3.us-east-1.amazonaws.com
prefix=
proxyHost=
proxyPort=
```

| 設定項目 | 説明 |
| ------| ------ |
|bucket| AWS COS Bucket名|
|accessKeyId|AccessKeyIdをユーザーキーに置換|
|accessKeySecret| AccessKeySecretをユーザーキーに置換|
|endPoint|AWSのendpointアドレス。必ずドメイン名を使用し、regionを使用しないでください|
|prefix|移行するパスのプレフィックス。Bucket内の全データを移行する場合は、prefixを空欄にします|
|proxyHost|プロキシを使用してアクセスする場合は、プロキシのIPアドレスを入力します|
|proxyPort|プロキシポート|

 
**3.3.4 QiniuデータソースmigrateQiniuの設定**

QiniuからCOSに移行する場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
```plaintext
# QiniuからCOSへの移行の設定セクション
[migrateQiniu]
bucket=bucket-qiniu
accessKeyId=AccessKey
accessKeySecret=SecretKey
endPoint=www.bkt.clouddn.com
prefix=
proxyHost=
proxyPort=
```

| 設定項目 | 説明 |
| ------| ------ |
|bucket|Qiniu COS Bucket名|
|accessKeyId|AccessKeyをユーザーキーに置換 |
|accessKeySecret| SecretKeyをユーザーキーに置換|
|endPoint|QiniuダウンロードアドレスはdownloadDomainに対応|
|prefix|移行するパスのプレフィックス。Bucket内の全データを移行する場合は、prefixを空欄にします|
|proxyHost|プロキシを使用してアクセスする場合は、プロキシのIPアドレスを入力します|
|proxyPort|プロキシポート|

 
**3.3.5 URLリストのデータソースmigrateUrlの設定**

指定したURLリストからCOSに移行する場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
```plaintext
# URLリストのダウンロードからCOSへの移行の設定セクション
[migrateUrl]
urllistPath=D:\\folder\\urllist.txt
```
     
| 設定項目 | 説明 |
| ------| ------ |
|urllistPath|URLリストのアドレス。内容はURLテキストで、1行に1つのURL オリジナルアドレスです（例えば、`http://aaa.bbb.com/yyy/zzz.txt`。二重引用符やその他いかなる記号の追加も不要です）。URLリストのアドレスは絶対パスである必要があります。<ul  style="margin: 0;"><li>LinuxLinuxの場合、`/a/b/c.txt`のようにシングルスラッシュで区切ります。</li><li>Windowsの場合、`E:\\a\\b\\c.txt`のようにダブルバックスラッシュで区切ります。<br>ディレクトリが入力された場合、そのディレクトリ内のすべてのファイルは、スキャン・移行のためのurllistファイルとみなされます</li></ul>|

 
**3.3.6 Bucket間相互コピーの設定 migrateBucketCopy**

指定したCOSのBucketから別のBucketに移行する場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。
>!移行を開始するアカウントは、移行元の読み取り権限と移行先の書き込み権限が必要です。

```plaintext
# ソースBucketからターゲットBucketへの移行設定セクション
[migrateBucketCopy]
srcRegion=ap-shanghai
srcBucketName=examplebucket-1250000000
srcSecretId=COS_SECRETID
srcSecretKey=COS_SECRETKEY
srcCosPath=/
```

| 設定項目 | 説明 |
| ------| ------ |
|srcRegion|ソースBucketのRegion情報については[アベイラビリティリージョン](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください|
|srcBucketName|ソースBucketの名称で、 命名形式は`<BucketName-APPID>`。Bucket名には必ずAPPIDを含める必要があります。例： examplebucket-1250000000|
|srcSecretId|ソースBucketが属するユーザーのキーSecretIdは、[Tencent Cloud APIキー](https://console.cloud.tencent.com/cam/capi)で確認できます。同じユーザーのデータである場合、srcSecretIdとcommonのSecretIdは同じとなり、そうでない場合、クロスアカウントのBucketコピーとなります|
|srcSecretKey|ソースBucketが属するユーザーのキーsecret_keyは、[Tencent Cloud APIキー](https://console.cloud.tencent.com/cam/capi)で確認できます。同じユーザーのデータである場合、srcSecretKeyとcommonのsecretKeyは同じとなり、そうでない場合、クロスアカウントのBucketコピーとなります|
|srcCosPath|移行先のCOSパスで、このパス内のファイルがターゲットBucketに移行されることを表します|

**3.3.7 UPYUNデータソースmigrateUpyunの設定**
UPYUNからCOSに移行する場合は、この部分の設定を行います。具体的な設定項目および説明は以下のとおりです。

```plaintext
[migrateUpyun]
# UPYUNからからの移行
bucket=xxx
#UPYUNオペレーターのID
accessKeyId=xxx
#UPYUNオペレーターのパスワード     
accessKeySecret=xxx       
prefix=

#UPYUN sdkの制限により、このproxyはグローバルのproxyとして設定されます
proxyHost=
proxyPort=
```

| 設定項目 | 説明 |
| ------| ------ |
|bucket|UPYUN USS Bucket名|
|accessKeyId|UPYUNオペレーターのIDに置換|
|accessKeySecret| UPYUNオペレーターのパスワードに置換|
|prefix|移行するパスのプレフィックス。Bucket内の全データを移行する場合は、prefixを空欄にします|
|proxyHost|プロキシを使用してアクセスする場合は、プロキシのIPアドレスを入力します|
|proxyPort|プロキシポート|

### 4. マイグレーションツールの実行
####  Windows
**start_migrate.bat**をダブルクリックして実行します。

####  Linux
1.設定ファイルconfig.iniから設定を読み込み、次のコマンドを実行します。
```plaintext
sh start_migrate.sh
```
2.一部のパラメータは、コマンドラインから設定を読み込み、次のコマンドを実行します。
```plaintext
sh start_migrate.sh -Dcommon.cosPath=/savepoint0403_10/
```

>?
> - ツールは、コマンドラインからの読み取りと設定ファイルからの読み取りという2種類の設定項目の読み取りをサポートしています。
> - コマンドラインは設定ファイルより優先されます。同じ設定オプションであれば、コマンドラインのパラメータが優先されるということです。
> - コマンドラインで設定項目を読み取る形式により、Bucket名、COSパス、移行するソースパスなど、2つのタスクの主要な設定項目が完全に同一でない場合、ユーザーは異なる移行タスクを同時に実行しやすくなります。さまざまな移行タスクを異なるdbディレクトリに書き込むことで、同時移行が確保されるからです。上記のツール構造のdb情報をご参照ください。
> - 設定項目の形式は、**-D{sectionName}.{sectionKey}={sectionValue}**です。ここで、sectionNameは設定ファイルのセクション名、sectionKeyはセクション内の設定項目名、sectionValueはセクション内の設定項目値を表します。移行先のCOSのパスを設定した場合、**-Dcommon.cosPath=/bbb/ddd**で表されます。
> 

## 移行のメカニズムとプロセス
### 移行メカニズムの原理

COSマイグレーションツールはステートフルであり、移行が成功するとdbディレクトリに記録され、KVの形式でleveldbファイルに保存されます。各移行の前に、移行するパスがdbに存在するかどうかをチェックします。存在しており、かつ属性がdbのものと同じであれば移行をスキップし、そうでない場合は移行を行います。ここでの属性は、移行タイプによって異なり、ローカル移行の場合、mtimeで判断します。その他のクラウドストレージの移行とBucketコピーでは、ソースファイルのetagと長さがdbと一致しているかどうかが判断されます。従ってCOSを探すのではなく、dbを参照して移行成功の記録があるかどうかを確認します。マイグレーションツールを迂回して別の方法（COSCMDやコンソールなど）でファイルを削除または変更した場合、マイグレーションツールを実行しても変更に気づかないため、再移行されません。

### 移行プロセスの手順

1. 設定ファイルが読み取られ、セクションがマイグレーションtypeに従って読み取られ、パラメータがチェックされます。
2. 指定された移行タイプに基づいて、db下で移行されるファイルの識別子をスキャンして比較し、アップロードが許可されているかどうかを判断します。
3. 移行の実行プロセス中に実行結果が出力されます。inprogressは移行中、skipはスキップ、failは失敗、okは成功、condition_not_matchは移行条件を満たさないためスキップされたファイル（lastmodifedやexcludesなど）を表します。失敗の詳細情報は、ログ内のerrorログで確認することができます。 実行プロセスは下図のとおりです。
 ![](https://main.qcloudimg.com/raw/7561d07ea315c9bacbb228b36d6ad6d6.png)
4. 移行全体の終了時に、累積した移行の成功数、失敗数、スキップ数、所要時間などの統計情報が出力されます。マイグレーションツールは成功したものをスキップして失敗したものを再移行するので、失敗した場合はerrorログを確認するか、再実行してください。実行完了結果の略図は以下のとおりです。
![](https://main.qcloudimg.com/raw/2534fd390218db29bb03f301ed2620c8.png)

## よくあるご質問
COS Migrationツールの使用中に移行失敗や実行エラーといった異常が発生した場合は、[COS Migrationツールに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/436/30585)をご参照ください。

