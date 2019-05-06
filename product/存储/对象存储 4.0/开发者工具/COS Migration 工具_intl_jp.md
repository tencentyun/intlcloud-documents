## 機能説明
COS Migrationは、COSデータ移行機能を統合する一体化ツールです。簡単な構成操作により、ユーザーがソースアドレスデータを迅速的にCOSに移行することができます。以下の特徴があります。
- 豊富なデータソース：
   - ローカルデータ：ローカルにストレージされるデータをCOSに移行します。
   - その他のCloud Redis：現時点でAWS S3、Alibaba Cloud OSS、QiNiuストレージをCOSに移行することをサポートします。今後適用対象を拡張します。
   - URLリスト：指定したURLダウンロードリストによりダウンロードし、COSに移行します。
   - Bucketの相互コピー：COSのBucketデータ相互コピーであり、アカウント間地域間のデータコピーをサポートします。
- ブレイクポイントからの再開：ツールは、アップロードときにブレイクポイントからの再開をサポートします。大容量ファイルであれば、途中で終了するか、サービス故障が発生した場合、ツールを再起動すると、アップロード未完了のファイルをアップロードし続けます。
- マルチパートアップロード：オブジェクトをパートにしてCOSにアップロードします。
- 並列アップロード：複数オブジェクトの同時アップロードをサポートします。
- 移行検証：オブジェクト移行後の検証。

## 使用環境
### システム環境
Windows、Linux、macOSシステム。

### ソフトウェア依存
- JDK1.7 X64以降。JDKのインストールと構成については、[Javaのインストールと構成](https://cloud.tencent.com/document/product/436/10865)を参照してください。

## 使用方法
### 1. ツール取得
[COS Migrationツール](https://github.com/tencentyun/cos_migrate_tool_v5)にアクセスしてダウンロードします。

### 2. ツールキット解凍
#### Windows
 解凍し特定のディレクトリに保存します。例えば
<pre>
C:\Users\Administrator\Downloads\cos_migrate
</pre>

#### Linux
解凍し特定のディレクトリに保存します。
<pre>
unzip cos_migrate_tool_v5-master.zip && cd cos_migrate_tool_v5-master
</pre>

#### 移行ツールの構造
正しく解凍後のCOS Migrationツールのディレクトリ構造を次に示します。
<pre>
COS_Migrate_tool
|——conf  #構成ファイルの所在ディレクトリ
|   |——config.ini  #移行構成ファイル
|——db    #ストレージ移行成功のレコード
|——dep   #プログラムメインロジックのコンパイルにより生成されるJARパッケージ
|——log   #ツール実行中に生成されるログ
|——opbin #コンパイルに使用されるスクリプト
|——src   #ツールのソースコード
|——tmp   #一時ファイルストレージディレクトリ
|——pom.xml #プロジェクト構成ファイル
|——README  #説明ドキュメント
|——start_migrate.sh  #Linuxでの起動スクリプトの移行
|——start_migrate.bat #Windowsでの起動スクリプトの移行
</pre>

>?
 - dbディレクトリはツール移行成功のファイルタグを記録します。毎回の移行タスクは、dbのレコードを優先して比較します。現在のファイルタグが記録されると、現在のファイルをスキップします。さもなければファイル移行を行います。
 - logディレクトリはツール移行ときのすべてのログを記録します。移行中にエラーが発生した場合、まずこのディレクトリのerror.logを確認してください。

### 3. config.ini構成ファイルの変更
起動スクリプトを移行する前、config.ini構成ファイル（パス：`./conf/config.ini`）を変更する必要があります。config.ini内容は以下を含みます。

#### 3.1 移行タイプの構成
typeは、移行タイプを示します。ユーザーが移行需要に応じてタグを入力します。例えば、ローカルデータをCOSに移行するには、`[migrateType]`の構成内容を`type=migrateLocal`にします。
<pre>[migrateType]
type=migrateLocal
</pre>

現時点で下記の移行タイプをサポートします。

| migrateType | 説明 |
| ------| ------ |
| migrateLocal| ローカルからCOSに移行します |
| migrateAws| AWS S3ローカルからCOSに移行します |
| migrateAli| Alibaba OSSからCOSに移行します |
| migrateQiniu| QiNiuからCOSに移行します |
| migrateUrl| ダウンロード用URLからCOSに移行します |
| migrateBucketCopy| ソースBucketから目標Bucketにコピーします|

#### 3.2 移行タスクの構成
ユーザーが実際の移行需要に応じて関連構成（目標COSへの移行の情報構成および移行タスクに関する構成を含む）を行います。
<pre>
# 移行ツールの公共構成セクション（移行先COSのアカウント情報を含む） 
[common]
secretId="COS_SECRETID"
secretKey="COS_SECRETKEY"
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
damonMode=off
damonModeInterVal=60
executeTimeWindow=00:00,24:00
</pre>

| 名前 | 説明 |デフォルト値|
| ------| ------ |----- |
| secretId| ユーザー暗号鍵SecretId。[クラウドAPI暗号鍵コンソール](https://console.cloud.tencent.com/cam/capi)で表示されます |-|
| secretKey| ユーザー暗号鍵SecretKey。[クラウドAPI暗号鍵コンソール]( https://console.cloud.tencent.com/cam/capi)で表示されます|-|
| bucketName| 目標Bucket名。 命名フォーマットは`<BucketName-APPID>`、すなわちBucket名はAPPIDを含む必要があります。例えば examplebucket-1250000000 |-|
| region| 目標BucketのRegion情報。COSの地域略称については、[可能な地域](https://cloud.tencent.com/document/product/436/6224)を参照してください |-|
| storageClass|ストレージタイプ：Standard - 標準ストレージ、Standard_IA - 低頻度ストレージ |Standard|
| cosPath|移行先COSパス。`/`はBucketのルートパスに移行することを表し、`/aaa/bbb/`はBucketの` /aaa/bbb/`に移行することを表します。`/aaa/bbb/`は存在しない場合、自動的にパスを作成します|/|
| https| がHTTPS伝送を使用するかどうか。onは有効を表し、offは無効を表します。伝送を有効にすると速度が遅い。伝送のセキュリティ要求が高いシナリオに適します|off|
| tmpFolder|その他のクラウドストレージからCOSに移行するとき、一時ファイルをストレージするためのディレクトリであり、移行完了後に削除します。フォーマットは絶対パス：<br>Linuxの区切り記号は1つのスラッシュ（例えば` /a/b/c`）です。<br>Windowsの区切り記号は二重バックスラッシュ（例えば`E:\\a\\b\\c`）です。<br>デフォルトはツールの所在パスのtmpディレクトリです|./tmp|
| smallFileThreshold| 小容量ファイルしきい値のバイト数。しきい値以上の場合マルチパートアップロードを使用します。さもなければ簡単なアップロードを使用します。デフォルトは5MB |5242880|
| smallFileExecutorNum|小容量ファイル（ファイルがsmallFileThreshold未満）の同時実行性で簡単なアップロードを使用します。パブリックネットワークによりCOSに接続し、帯域幅が小さい場合、この同時実行性を減らしてください|64|
| bigFileExecutorNum| 大容量ファイル（ファイルがsmallFileThreshold以上）の同時実行性でマルチパートアップロードを使用します。パブリックネットワークによりCOSに接続し、帯域幅が小さい場合、この同時実行性を減らしてください|8|
| entireFileMd5Attached|移行ツールでテキスト全体のMD5を計算した後、ファイルのカスタムヘッダーx-cos-meta-md5に保存し今後の検証に使用します。COSのマルチパートアップロードする大容量ファイルのetagがテキスト全体のMD5ではないからです|on|
| damonMode|damonモードを使用するかどうか。onは有効を表し、offは無効を表します。damonはプログラムが周期的に同期を実行し、サイクルの間隔はdamonModeInterValパラメータにより設定されます|off|
| damonModeInterVal|1サイクルの同期が終了した時点から次のサイクルの同期に入るまでの時間。単位は秒 |60|
| executeTimeWindow|実行時間ウィンドウ。時間粒度は分です。このパラメータは移行ツールが毎日実行する時間帯を定義します。例えば：<br>パラメータ03:30,21:00は、早朝03:30から夜21:00の間にタスクを実行し、その他の時間帯で休止状態に入り、休止状態のときに移行を一時的に停止し、次の時間ウィンドウが自動的に実行するまで移行進捗を保留します|00:00,24:00|

#### 3.3 データソース情報の構成
`[migrateType]`の移行タイプにより適切なセクションを構成します。例えば`[migrateType]`の構成内容は`type=migrateLocal`であれば、ユーザーが`[migrateLocal]`セクションを構成するだけでよい。

**3.3.1 ローカルのデータソースmigrateLocalの構成**

ローカルからCOSに移行した場合、この部分の構成を行います。具体的な構成項目と説明は以下のとおりです。
<pre>
# ローカルからCOSの構成セクションに移行します
[migrateLocal]
localPath=E:\\code\\java\\workspace\\cos_migrate_tool\\test_data
exeludes=
ignoreModifiedTimeLessThanSeconds=
</pre>

| 構成項目 | 説明 |
| ------| ------ |
|localPath|ローカルパス。フォーマットは絶対パスです。<br>Linuxの区切り記号は1つのスラッシュ（例えば`/a/b/c`）で、<br>Windowsの区切り記号は二重バックスラッシュ（例えば`E:\\a\\b\\c`）です。|
|excludes| 除去するディレクトリまたはファイルの絶対パス。localPath配下のディレクトリまたはファイルを移行しないことを表します。複数の絶対パスの前にセミコロンで区切り、未入力はlocalPath配下のすべてを移行することを表します|
|ignoreModifiedTimeLessThanSeconds| アップデート時間と現在の時間の差が一定の時間帯以内のファイルを排除します。単位は秒、デフォルトは設定されません。選別にはlastmodified時間によらないことを表します。顧客がファイルをアップデートすると同時にツール移行を実行し、アップデート中のファイルをCOSにアップロードしないときに使用されます。例えば、300に設定すると、5分钟以上アップデートしたファイルのみをアップロードすることを表します|

**3.3.2 Alibaba OSSデータソースmigrateAliの構成**

Alibaba Cloud OSSからCOSに移行した場合、この部分の構成を行います。具体的な構成項目と説明は以下のとおりです。
<pre># Alibaba OSSからCOSの構成セクションに移行します
[migrateAli]
bucket=bucket-aliyun
accessKeyId="<yourAccessKeyId>"
accessKeySecret="<yourAccessKeySecret>"
endPoint= oss-cn-hangzhou.aliyuncs.com
prefix=
proxyHost=
proxyPort=
</pre>

| 構成項目 | 説明 |
| ------| ------ |
|bucket|Alibaba Cloud OSS Bucket名|
|accessKeyId|ユーザーの暗号鍵accessKeyId |
|accessKeySecret| ユーザーの暗号鍵accessKeySecret|
|endPoint|Alibaba Cloud endpointアドレス|
|prefix|移行するパスのプレフィックス。Bucketのすべてのデータを移行する場合、prefixはブランクです|
|proxyHost|プロキシアクセスの場合、プロキシIPアドレスを入力します|
|proxyPort|プロキシのポート|

**3.3.3 AWSデータソースmigrateAwsの構成**

AWSからCOSに移行した場合、この部分の構成を行います。具体的な構成項目および説明は以下のとおりです。
<pre># AWSからCOSの構成セクションに移行します
[migrateAws]
bucket=bucket-aws
accessKeyId="AccessKeyId"
accessKeySecret="SecretAccessKey"
endPoint=s3.us-east-1.amazonaws.com
prefix=
proxyHost=
proxyPort=
</pre>

| 構成項目 | 説明 |
| ------| ------ |
|bucket| AWS COS Bucket 名|
|accessKeyId|ユーザーの暗号鍵accessKeyId |
|accessKeySecret| ユーザーの暗号鍵accessKeySecret|
|endPoint|AWSのendpointアドレス。regionでなく、ドメイン名を使用します。|
|prefix|移行するパスのプレフィックス。Bucketのすべてのデータを移行する場合、prefixはブランクです|
|proxyHost|プロキシアクセスの場合、プロキシIPアドレスを入力します|
|proxyPort|プロキシのポート|

 
**3.3.4 QiNiuデータソースmigrateQiniuの構成**

QiNiuからCOSに移行した場合、この部分の構成を行います。具体的な構成項目および説明は以下のとおりです。
<pre># QiNiuからCOSの構成セクションに移行します
[migrateQiniu]
bucket=bucket-qiniu
accessKeyId=”AccessKey”
accessKeySecret=”SecretKey”
endPoint=www.bkt.clouddn.com
prefix=
proxyHost=
proxyPort=
</pre>

| 構成項目 | 説明 |
| ------| ------ |
|bucket|QiNiu COS Bucket名|
|accessKeyId|ユーザーの暗号鍵accessKeyId |
|accessKeySecret| ユーザーの暗号鍵accessKeySecret|
|endPoint|QiNiuダウンロードアドレス。downloadDomainに対応します|
|prefix|移行するパスのプレフィックス。Bucketのすべてのデータを移行する場合、prefixはブランクです|
|proxyHost|プロキシアクセスの場合、プロキシIPアドレスを入力します|
|proxyPort|プロキシのポート|

 
**3.3.5 URLリストデータソースmigrateUrlの構成**

指定したURLリストからCOSに移行した場合、この部分の構成を行います。具体的な構成項目および説明は以下のとおりです。
<pre>
# ダウンロード用URLリストからCOSの構成セクションに移行します
[migrateUrl]
urllistPath=D:\\folder\\urllist.txt
</pre>
     
| 構成項目 | 説明 |
| ------| ------ |
|urllistPath|URLリストのアドレス。内容はURLテキスト、1行ごとに1個URLの元アドレス（例えば `http://aaa.bbb.com/yyy/zzz.txt`、ダブルコーテーションまたはその他の記号を含まない）を入れます。URLリストのアドレスは絶対パスを使用します。<br>Linuxの区切り記号は1つのスラッシュ（例えば`/a/b/c.txt`）で、<br>Windowsの区切り記号は二重バックスラッシュ（例えば`E:\\a\\b\\c.txt`）です。<br>ディレクトリを入力した場合、このディレクトリ下のすべてのファイルをurllistファイルとしてスキャンし移行します|

 
**3.3.6 Bucket相互コピーmigrateBucketCopyの構成**

COSの指定したBucketから別のBucketに移行した場合、この部分の構成を行います。具体的な構成項目および説明は以下のとおりです。
<pre>
# ソースBucketから目標Bucketの構成セクションに移行します
[migrateBucketCopy]
srcRegion=ap-shanghai
srcBucketName=examplebucket-1250000000
srcSecretId="COS_SECRETID"
srcSecretKey="COS_SECRETKEY"
srcCosPath=/
</pre>

| 構成項目 | 説明 |
| ------| ------ |
|srcRegion|ソースBucketのRegion情報については、[可能な地域](https://cloud.tencent.com/document/product/436/6224)を参照してください|
|srcBucketName|ソースBucket名。命名フォーマットは`<BucketName-APPID>`、すなわちBucket名はAPPIDを含む必要があります。例えば examplebucket-1250000000|
|srcSecretId|ソースBucket所属のユーザーの暗号鍵SecretId。[クラウドAPI暗号鍵](https://console.cloud.tencent.com/cam/capi)に表示されます。同一ユーザーのデータの場合、srcSecretIdとcommonのSecretIdが同じ、さもなければアカウント間のBucketコピーです|
|srcSecretKey|ソースBucket所属のユーザーの暗号鍵secret_key。[クラウドAPI暗号鍵](https://console.cloud.tencent.com/cam/capi)に表示されます。同一ユーザーのデータの場合、srcSecretIdとcommonのsecretIdが同じ、さもなければアカウント間のBucketコピーです|
|srcCosPath|移行するCOSパス。このパスのファイルが目標Bucketに移行することを表します|


### 4. 移行ツールの実行
#### Windows
**start_migrate.bat**をダブルクリックすると実行します。

#### Linux
1.config.ini構成ファイルから構成を読み込みます。実行コマンドが次のとおりです：
<pre>
sh start_migrate.sh
</pre>
2.一部のパラメータがコマンドラインから構成を読み込みます。実行コマンドが次のとおりです：
<pre>
sh start_migrate.sh -Dcommon.cosPath=/savepoint0403_10/
</pre>

>?
> - ツールが、コマンドライン読取または構成ファイル読取を含む構成項目の読取方式をサポートします。
> - コマンドラインの優先順位が構成ファイルより高い。すなわち、同じ構成項目がコマンドラインのパラメータを優先して採用します。
> - コマンドラインの構成項目の読取形式は、ユーザーが同時にさまざまな移行タスクを実行することに有利です。前提として2つのタスクの重要構成項目が完全に同じではありません。例えば、Bucket名、COSパス、移行するソースパスなど。移行タスクによって書き込むdbディレクトリが異なりますので、並行移行を保証します。前文のツール構造のdb情報を参照してください。
> - 構成項目の形式は、**-D{sectionName}.{sectionKey}={sectionValue}** の形式です。そのうち、sectionNameは構成ファイルのセクション名、sectionKeyはセクションの構成項目名称、sectionValueはセクションの構成項目値です。移行先COSパスを設定するとき、**-Dcommon.cosPath=/bbb/ddd**で表されます。

## 移行メカニズムおよびプロセス
### 移行メカニズム原理
COS移行ツールはステータスがあります。移行が成功したものはdbディレクトリに記録され、KVの形式でleveldbファイルにストレージされます。移行前に移行先パスがdbに存在するかどうかを検索します。存在し、属性とdbのものが一致する場合、移行をスキップします。さもなければ移行します。ここの属性は、移行タイプによって異なります。ローカルの移行について、mtimeを判断します。その他のクラウドストレージ移行とBucketコピーについて、ソースファイルのetagと長さがdbに一致するかどうかを判断します。そのため、COSを検索することでなく、dbには移行成功レコードが存在するかどうかを照合します。移行ツールによらず、別の方式（例えばCOSCMDまたはコンソール）でファイルを削除、変更した場合、移行ツールを実行するときにそのような変化を検出できないため、再移行しません。

### 移行プロセスの手順
1. 構成ファイルを読取ります。移行typeによりレスポンスの構成セクションを読取り、パラメータのチェックを実行します。
2. 指定した移行タイプにより、dbの移行するファイルのタグをスキャンし比較し、アップロードが許可されるかどうかを判断します。
3. 移行実行中に実行結果をプリントします。そのうち、inprogressが移行中、skipがスキップ、failが失敗、okが成功、condition_not_matchが移行条件を満たさないためスキップされたファイル（例えば、lastmodifedとexcludes）。失敗の詳細情報がlogのerrorログで表示されます。実行イメージは下図に示されます。
 ![](https://main.qcloudimg.com/raw/7561d07ea315c9bacbb228b36d6ad6d6.png)
4. 移行全体が終了した後統計情報（累積された移行成功数、失敗数、スキップ数、時間消費を含む）をプリントします。失敗の場合、errorログを確認するか、再実行します。移行ツールが移行成功のものをスキップし、未成功のものをスキップします。実行完了結果イメージは下図に示されます。
![](https://main.qcloudimg.com/raw/2534fd390218db29bb03f301ed2620c8.png)

## FAQ
COS Migrationツールを使用するとき、移行に失敗し、実行エラーなどの異常が発生した場合、[COS Migrationツールなどのよくある質問](https://cloud.tencent.com/document/product/436/30745)を参照して解決策を見つけてください。

