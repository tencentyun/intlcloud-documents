## ネームスペース統一機能の概要

GooseFSのネームスペース（NameSpace）統一機能は、透明性の高い命名メカニズムによって、さまざまな基盤ストレージシステムのアクセスセマンティクスを融合し、統一されたデータ管理インタラクションビューをユーザーに提供することができる機能です。

GooseFSはネームスペース統一機能によって、ローカルファイルシステム、Cloud Object Storage（COS）、Tencent Cloud HDFS（CHDFS）などの異なる基盤ストレージシステムを連携させ、これらの基盤ストレージシステムと通信を行い、上層の業務に対し統一されたアクセスインターフェースおよびファイルプロトコルを提供します。業務側はGooseFSのアクセスインターフェースを使用するだけで、異なる基盤ストレージシステム内のデータにアクセスすることが可能です。

![](https://main.qcloudimg.com/raw/6ef8e2899bbd704f7c05c7d0526624b1.png)

上の図は統一ネームスペースの動作原理を表したものです。GooseFSのネームスペース作成コマンドcreate nsによって、COS とCloud HDFSの指定のファイルディレクトリをGooseFSにマウントした後、gfs://という統一schemaによってデータにアクセスします。詳細な説明は次のとおりです。

- COSにはbucket-1、bucket-2、bucket-3という3つのバケットがあります。このうちbucket-1にはBU_AとBU_Bという2つのディレクトリがあり、bucket-1とbucket-2はどちらもGooseFSにマウントされています。
- Cloud HDFSにはBU_E、BU_F、BU_G、BU_Hという4つのディレクトリがあり、このうちBU_H以外のディレクトリはすべてGooseFS上にマウントされています。
- GooseFSでのファイル操作において、gfs://という統一schemaによってBU_AとBU_Eという2つのディレクトリにアクセスした場合、どちらも正常にアクセスでき、かつファイルはGooseFSのローカルファイルシステム内にキャッシュされます。
- 基盤ファイルシステム（COS、Cloud HDFS）内に保存されているBU_AとBU_Eの2つのディレクトリはすでにGooseFSにマウントされているため、ファイルがGooseFSにキャッシュされていれば、gfs://という統一schemaによってアクセスできます（例：hadoop fs ls gfs://BU_A）。また、各リモートファイルシステムのネームスペースによってアクセスすることもできます（例：hadoop fs ls cosn://bucket-1/BU_A）。
- ファイルがGooseFSにキャッシュされていない場合、gfs://という形式によるアクセスは失敗します。これはファイルがローカルファイルシステムにキャッシュされていないためです。ただし基盤ストレージシステムのネームスペースによるアクセスは可能です。

## ネームスペース統一機能の使用

ns操作によってGooseFSにネームスペースを作成し、基盤ストレージシステムをGooseFSにマップすることができます。現在サポートしている基盤ストレージシステムにはCOS、Cloud HDFS、ローカルHDFSなどがあります。ネームスペースの作成操作はLinuxファイルシステムでの論理ボリュームのマウントに似ています。ネームスペースを作成すると、GooseFSはクライアントに対し、統一のアクセスセマンティクスを有するファイルシステムを提供できるようになります。現在のGooseFSネームスペースの操作命令セットは次のとおりです。

```plaintext
$ goosefs ns
Usage: goosefs ns [generic options]
         [create <namespace> <CosN/Chdfs path> <--wPolicy <1-6>> <--rPolicy <1-5>> [--readonly] [--shared] [--secret fs.cosn.userinfo.secretId=<AKIDxxxxxxx>] [--secret fs.cosn.userinfo.secretKey=<xxxxxxxxxx>] [--attribute fs.ofs.userinfo.appid=1200000000][--attribute fs.cosn.bucket.region=<ap-xxx>/fs.cosn.bucket.endpoint_suffix=<cos.ap-xxx.myqcloud.com>]]
         [delete <namespace>]                                      
         [help [<command>]]                                        
         [ls [-r|--sort=option|--timestamp=option]]                
         [setPolicy [--wPolicy <1-6>] [--rPolicy <1-5>] <namespace>]
         [setTtl [--action delete|free] <namespace> <time to live>]
         [stat <namespace>]                                        
         [unsetPolicy <namespace>]                                 
         [unsetTtl <namespace>] 
```
>!
>- 設定の際にパーマネントキーはできるだけ使用しないことをお勧めします。サブアカウントキーまたは一時キー方式を用いると業務の安全性が向上します。サブアカウントへの権限承認の際は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従い、データが意図せず漏洩しないようにしてください。
>- どうしてもパーマネントキーを使用したい場合は、パーマネントキーの権限範囲を限定することをお勧めします。[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)を参照し、パーマネントキーで実行できるアクション、リソースの範囲および条件（アクセスIPなど）を限定することで、使用上の安全性を向上させることができます。

上記の命令セットの各コマンドの機能を簡単にご説明します。

| コマンド        | 説明                                                         |
| ----------- | ------------------------------------------------------------ |
| create      | ネームスペースを作成し、リモートストレージシステム（UFS）をネームスペースにマップするために使用します。ネームスペースの作成時に読み取り書き込みキャッシュポリシーを設定することができます。権限を有するキー情報（secretId、secretKey）を渡す必要があります。 |
| delete      | 指定したネームスペースの削除に使用します。                                       |
| ls          | 指定したネームスペースの詳細情報（マウントポイント、UFSパス、作成時間、キャッシュポリシー、TTL情報など）のリストアップに使用します。 |
| setPolicy   | 指定したネームスペースのキャッシュポリシーの設定に使用します。                             |
| setTtl      | 指定したネームスペースのTTLの設定に使用します。                             |
| stat        | 指定したネームスペースの記述的情報（マウントポイント、UFSパス、作成時間、キャッシュポリシー、TTL情報、永続化の状態、ユーザーグループ、ACL、最終アクセス時刻、変更時刻など）の提供に使用します。 |
| unsetPolicy | 指定したネームスペースのキャッシュポリシーのリセットに使用します。                             |
| unsetTtl    | 指定したネームスペースのTTLのリセットに使用します。                             |

### ネームスペースの作成と削除
GooseFSのネームスペース作成操作によって、頻繁にアクセスするホットデータをリモートストレージシステムからローカルのハイパフォーマンスストレージノードにキャッシュし、ローカルでのコンピューティング業務の際に高いパフォーマンスでデータにアクセスできるようにすることが可能です。次のコマンドは、COS内のバケットexample-bucket、バケット内のexample-prefixディレクトリおよびCloud HDFSファイルシステムをそれぞれtest_cos、test_cos_prefix、test_chdfsなどのネームスペースにマップする場合を表したものです。

```plaintext
# COSバケットexample-bucketをtest_cosネームスペースにマッピング
$ goosefs ns create test_cos cosn://example-bucket-1250000000/ --wPolicy 1 --rPolicy 1 --secret fs.cosn.userinfo.secretId=AKIDxxxxxxx --secret fs.cosn.userinfo.secretKey=xxxxxxxxxx --attribute fs.cosn.bucket.region=ap-guangzhou --attribute fs.cosn.bucket.endpoint_suffix=cos.ap-guangzhou.myqcloud.com 

# COSバケットexample-bucketのexample-prefixディレクトリをtest_cos_prefixネームスペースにマッピング
$ goosefs ns create test_cos_prefix cosn://example-bucket-1250000000/example-prefix/ --wPolicy 1 --rPolicy 1 --secret fs.cosn.userinfo.secretId=AKIDxxxxxxx --secret fs.cosn.userinfo.secretKey=xxxxxxxxxx --attribute fs.cosn.bucket.region=ap-guangzhou --attribute fs.cosn.bucket.endpoint_suffix=cos.ap-guangzhou.myqcloud.com

# Cloud HDFSファイルシステムf4ma0l3qabc-Xy3をtest_chdfsネームスペースにマッピング
$ goosefs ns create test_chdfs ofs://f4ma0l3qabc-Xy3/ --wPolicy 1 --rPolicy 1 --attribute fs.ofs.userinfo.appid=1250000000
```

作成に成功すると、goosefs fs lsコマンドによってディレクトリの詳細を確認できます。
```plaintext
$ goosefs fs ls /test_cos
```

不要なネームスペースはdeleteコマンドで削除できます。

```plaintext
$ goosefs ns delete test_cos
Delete the namespace: test_cos
```

### キャッシュポリシーの設定
ユーザーはsetPolicyおよびunsetPolicyによって指定したネームスペースのキャッシュポリシーを設定できます。キャッシュポリシー設定の命令セットは次のとおりです。
```plaintext
$goosefs ns setPolicy [--wPolicy <1-6>] [--rPolicy <1-5>] <namespace>
```
これらの各パラメータの意味は次のとおりです。
- wPolicy：書き込みキャッシュポリシーです。6種類の書き込みキャッシュポリシーをサポートしています。
- rPolicy：読み取りキャッシュポリシーです。5種類の読み取りキャッシュポリシーをサポートしています。
- namespace：指定のネームスペースです。

GooseFSが現在サポートしている読み取り書き込みキャッシュポリシーはそれぞれ次のとおりです。

**書き込みキャッシュポリシー**

| ポリシー名      | アクション                                                         | 対応するWrite_Type | データの安全性 | 書き込み効率 |
| :------------ | :---------------------------------- | :--------- | :-----  | :-----  |
| MUST_CACHE（1） | データをGooseFSのみに保存し、リモートストレージシステムには書き込みません。 | MUST_CACHE | 信頼性が低い     | 高い     |
| TRY_CACHE（2） | キャッシュにスペースがある場合はGooseFSに書き込み、スペースがない場合は基盤ストレージに直接書き込みます。 | TRY_CACHE | 信頼性が低い | 中程度 |
| CACHE_THROUGH（3） | データを可能な限りキャッシュし、同時にリモートストレージシステムに同期的に書き込みます。                    | CACHE_THROUGH | 信頼性が高い       | 低い    |
| THROUGH（4）       | データをGooseFSに保存せず、リモートストレージシステムに直接書き込みます。                   | THROUGH | 信頼性が高い       | 中程度     |
| ASYNC_THROUGH（5） | データをGooseFSに書き込み、リモートストレージシステムに非同期的にキャッシュします。                 | ASYNC_THROUGH | 信頼性がやや低い     | 高い     |

>? Write_Type：ユーザーがSDKまたはAPIを呼び出してGooseFSにデータを書き込む際に指定するファイルキャッシュポリシーを指します。単一のファイルに対して有効です。
> 

**読み取りキャッシュポリシー**

| ポリシー名                      | アクション                                                         | メタデータ同期 | 対応するRead_Type | データ整合性 | 読み取り効率                  | データをキャッシュするか |
| :---------------------------- | :----------------------------------------------------------- | :--------- | ------------- | :--------- | :---------------------- | :----------- |
| NO_CACHE（1）                 | データをキャッシュせず、リモートストレージシステムから直接データを読み取ります。                     | NO         | NO_CACHE      | 強い整合性     | 低い                      | いいえ           |
| CACHE（2）                    | <li>メタデータアクセスアクション：キャッシュにヒットした場合、メタデータはMaster内のものに準じ、能動的に基盤からメタデータを同期することはありません。</li><li>データフローアクセスアクション：データフローのReadTypeはCACHEポリシーを使用します。</li> | Once       | CACHE         | 弱い整合性     | ヒットした場合：高い<br/>ヒットしない場合：低い | はい           |
| CACHE_PROMOTE（3）            | <li>メタデータアクセスアクション：CACHEモードと同様です。</li><li>データフローアクセスアクション：データフローのReadTypeはCACHE_PROMOTEポリシーを使用します。</li> | Once       | CACHE_PROMOTE | 弱い整合性     | ヒットした場合：高い<br/>ヒットしない場合：低い | はい           |
| CACHE_CONSISTENT_PROMOTE（4） | <li>メタデータアクセスアクション：毎回の読み取り操作前にリモートストレージシステムUFS上のメタデータを同期し、UFS内に存在しない場合はエラーNot Existsをスローします。</li><li>データフローアクセスアクション：データフローのReadTypeはCACHE_PROMOTEポリシーを使用し、ヒットした後は最もホットなメディア内にキャッシュします。</li> | Always     | CACHE         | 強い整合性     | ヒットした場合：中程度<br/>ヒットしない場合：低い | はい           |
| CACHE_CONSISTENT（5）         | <li>メタデータアクション：CACHE_CONSISTENT_PROMOTEモードと同様です。</li><li>データフローアクセスアクション：データフローのReadTypeはCACHEポリシーを使用します。すなわちCACHEがヒットした場合は他のメディア層へのデータ移動を行いません。</li> | Always     | CACHE_PROMOTE | 強い整合性     | ヒットした場合：中程度<br/>ヒットしない場合：低い | はい           |

>? Read_Type：ユーザーがSDKまたはAPIを呼び出してGooseFSからデータを読み取る際に指定するファイルキャッシュポリシーを指します。単一のファイルに対して有効です。
>  

現在のビッグデータ業務での実践を踏まえて、主に次のような読み取り書き込みキャッシュポリシーの組み合わせを推奨しています。

| 書き込みキャッシュポリシー                      | 読み取りキャッシュポリシー                                                         | ポリシー組み合わせの効果 |
| :---------------------------- | :----------------------------------------------------------- | :--------- |
|CACHE_THROUGH（3）|CACHE_CONSISTENT（5）|キャッシュとリモートストレージシステムのデータは強い整合性を有します。|
|CACHE_THROUGH（3）|CACHE（2）|書き込みは強い整合性を、読み取りは最終的な整合性を有します。|
|ASYNC_THROUGH（5）|CACHE_CONSISTENT（5）|書き込みは最終的な整合性を、読み取りは強い整合性を有します。|
|ASYNC_THROUGH（5）|CACHE（2）|読み取りと書き込みは最終的な整合性を有します。|
|MUST_CACHE（1）|CACHE（2）|キャッシュ内からのみデータを読み取ります。|

以下は、指定したネームスペースtest_cosの読み取り書き込みキャッシュポリシーをそれぞれCACHE_THROUGHとCACHE_CONSISTENTに設定した場合の例です。
```plaintext
$ goosefs ns setPolicy --wPolicy 3 --rPolicy 5 test_cos
```

>!ユーザーはネームスペースの作成時にキャッシュポリシーを設定するほか、ファイルの読み取りと書き込みの際に、指定したファイルに対してReadTypeまたはWrite_Typeを設定することや、properties設定ファイルによってキャッシュポリシーをグローバルに設定することもできます。複数のポリシーが同時に存在する場合、優先順位は、ユーザー定義の優先順位> Namespaceの読み取り書き込みポリシー>設定ファイルのグローバルキャッシュポリシー設定の順となります。このうち、読み取りポリシーにユーザー定義のReadTypeおよびNamespaceのDirReadPolicyを用いる組み合わせが発効した場合、データフローの読み取りポリシーにはユーザー定義のReadType、メタデータにはNamespaceのポリシーが用いられます。 
>
> 例えば、GooseFS内にCOSNネームスペースが存在し、読み取りポリシーがCACHE_CONSISTENTであり、このネームスペースに1つのtest.txtファイルが存在するとします。クライアントはtest.txtを読み取る際、ReadTypeをCACHE_PROMOTEに指定しています。この場合、読み取りアクション全体がメタデータを同期し、かつCACHE_PROMOTEとなります。
> 

読み取り書き込みポリシーをリセットしたい場合はunsetPolicyで実現できます。以下のポリシーはtest_cosネームスペースの読み取り書き込みキャッシュポリシーをリセットする場合を表しています。
```plaintext
$ goosefs ns unsetPolicy test_cos
```


### TTLの設定

TTLはGooseFSのローカルノードにキャッシュしたデータの管理に使用します。TTLパラメータを設定することで、キャッシュしたデータに、指定した時刻の後にdeleteやfree操作などの指定した操作を行わせることができます。現在のTTL設定操作コマンドは次のとおりです。

```plaintext
$ goosefs ns setTtl [--action delete|free] <namespace> <time to live>
```

これらの各パラメータの意味は次のとおりです。
- action：キャッシュ時間の有効期限後に実行する操作です。現在はdeleteとfreeの2種類の操作をサポートしています。delete操作はキャッシュとUFS上のデータを削除します。free操作はキャッシュ上のデータのみを削除します。
- namespace：指定のネームスペースです。
- time to live：データのキャッシュ時間です。単位はミリ秒です。

以下は、指定したネームスペースtest_cosのポリシーを、60秒後に削除するよう設定する場合の例です。

```plaintext
$ goosefs ns setTtl --action free test_cos 60000
```

## メタデータ情報の管理

このセクションでは、メタデータの同期、更新などの内容を含めたGooseFSでのメタデータの管理方法についてご説明します。GooseFSはネームスペース統一機能を提供しており、ユーザーは基盤ストレージシステムのパスを指定するだけで、gfs://という統一パスによって他の基盤ストレージシステム上のファイルにアクセスすることができます。メタデータ情報の整合性を保障するため、GooseFSを統一のデータアクセス層として、常にGooseFSからデータの読み取りと書き込みを行うことを推奨します。

### メタデータ同期の概要

conf/goosefs-site.properties設定ファイル内でメタデータの同期サイクルを変更し、メタデータの同期サイクルを管理することができます。設定パラメータは次のとおりです。

```plaintext
goosefs.user.file.metadata.sync.interval=<INTERVAL>
```

同期サイクルでは次の3種類の入力パラメータをサポートしています。

- 入力パラメータの値が-1：メタデータをGooseFSに最初にロードして以降、更新を行わないことを表します。
- 入力パラメータの値が0：GooseFSが毎回の読み取り書き込み操作後にメタデータの更新を行うことを表します。
- 入力パラメータの値が正の整数：GooseFSが指定の時間間隔で定期的にメタデータの更新を行うことを表します。

ノード数、GooseFSクラスターおよび基盤ストレージのI/Oの距離、基盤ストレージタイプなどの要素を総合的に考慮し、適切な同期サイクルを選択することができます。通常は次のようになります。

- GooseFSのクラスターノード数が多いほど、メタデータの同期遅延が大きくなります。
- GooseFSのクラスターが存在するデータセンターと基盤ストレージの物理的距離が遠いほど、メタデータの同期遅延が大きくなります。
- 基盤ストレージシステムのメタデータ同期遅延への影響は主にシステムのリクエストQPS負荷によって決まります。QPS負荷が高いほど、同期遅延は相対的に低くなります。

### メタデータ同期管理方法

#### 設定方法

1. コマンドラインによる設定
コマンドライン方式でメタデータ情報の同期サイクルを設定できます。
```plaintext
goosefs fs ls -R -Dgoosefs.user.file.metadata.sync.interval=0 <path to sync>
```
2. 設定ファイルによる設定
大規模なGoosefsクラスターの場合、goosefs-site.properties設定ファイルによって、クラスター内のMasterノードのメタデータ情報同期サイクルを一括設定することができます。他のノードの同期サイクルにはデフォルトでこのサイクル値が適用されます。
```plaintext
goosefs.user.file.metadata.sync.interval=1m
```

>! 多くの業務ではディレクトリによってデータの用途を区別する方法を選択しており、データへのアクセス頻度はディレクトリごとにそれぞれ異なります。メタデータの同期サイクルはディレクトリごとに異なるサイクル値を設定することができ、常に変化するディレクトリではメタデータの同期サイクルを短め（5分など）に設定し、変化が極めて少ないディレクトリや変化しないディレクトリでは同期サイクルを-1に設定することで、GooseFSがこのディレクトリのメタデータを自動的に同期しないようにすることができます。
>

#### 推奨設定

業務アクセスモードの違いに応じて、異なるメタデータの同期サイクルを設定できます。

<table>
   <tr>
      <td colspan=2>アクセスモード</td>
      <td>メタデータ同期サイクル</td>
      <td>説明</td>
   </tr>
   <tr>
      <td colspan=2>すべてのファイルリクエストがGooseFSを経由する場合</td>
      <td>-1</td>
      <td>-</td>
   </tr>
   <tr>
      <td rowspan=2>大部分のファイルリクエストがGooseFSを経由する場合</td>
      <td>HDFSをUFSとして使用</td>
      <td>ホットアップデートの使用またはパスによる更新を推奨</td>
      <td>HDFSの更新が特に頻繁な場合は更新サイクルを-1に設定し、更新を無効にすることを推奨します</td>
   </tr>
   <tr>
      <td>COSをUFSとして使用</td>
      <td>パスによる更新サイクルの設定を推奨</td>
      <td rowspan=3>ディレクトリごとに異なる更新サイクルを設定すると、メタデータ同期の負荷を軽減できます</td>
   </tr>
   <tr>
      <td rowspan=2>ファイルアップロードリクエストが通常GooseFSを経由しない場合</td>
      <td>HDFSをUFSとして使用</td>
      <td>パスによる更新サイクルの設定を推奨</td>
   </tr>
   <tr>
      <td>COSをUFSとして使用</td>
      <td>パスによる更新サイクルの設定を推奨</td>
   </tr>
</table>
