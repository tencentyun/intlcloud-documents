
## 機能説明

ユーザーはCOSCMDツールを使用すれば、簡単なコマンドラインによって、オブジェクト(Object)の一括アップロード・ダウンロード・削除などの操作が行えます。


## 使用環境

#### システム環境

Windows、Linux 、macOSシステムをサポートします。

> ?
> - ローカル文字形式がUTF-8であることを確認してください。UTF-8でない場合、中国語版のファイルを操作すると、異常が発生します。
> - 本機の時刻が協定世界時で修正されていることを確認してください。誤差が大きすぎると、正常に使用できなくなります。

#### ソフトウェア依存

- Python 2.7/3.5/3.6/3.9。
- 最新バージョンのpip。
>?pipが統合された最新版のPython（例：バージョン3.9.0）を直接インストールすることをお勧めします。

#### インストールおよび設定

- 環境のインストールと設定操作の詳細については、[Pythonのインストールと設定](https://intl.cloud.tencent.com/document/product/436/10866)をご参照ください。
- pip環境のインストールと設定操作の詳細については、[公式サイトpipのインストールの説明](https://pip.pypa.io/en/stable/installation/)をご参照ください。


### ダウンロードとインストール

ユーザーがCOSCMDをインストールする方法として、以下の3つの方法が提供されています。

#### 1.1 pipによるインストール 

`pip`コマンドを実行してインストールします。
```plaintext
pip install coscmd
```
インストールの成功後、ユーザーは`-v`または`--version`コマンドを使用して、現在のバージョン情報を確認することができます。
>! Windowsでインストールした場合は、環境変数に`C:\python_install_dir;`と`C:\python_install_dir\Scripts`という2つのパスを追加する必要があります。 

#### 1.2 pipの更新

インストールが完了したら、次のコマンドを実行して更新します。
```plaintext
pip install coscmd -U
```

#### 2. ソースコードのインストール（非推奨）

ソースコードダウンロードアドレス：[ここをクリック](https://github.com/tencentyun/coscmd.git)。

```plaintext
git clone https://github.com/tencentyun/coscmd.git
cd coscmd
python setup.py install
```

>! Pythonバージョンが2.6で、pipの依存ライブラリへのインストールが失敗しやすい場合は、この方法でインストールすることをお勧めします。 

#### 3. オフラインインストール

>! 2台のマシンのPythonのバージョンが同じであることを確認してください。同じでない場合、インストールは失敗してしまいます。

```sh
# パブリックネットワークを備えたマシンで次のコマンドを実行します
mkdir coscmd-packages
pip download coscmd -d coscmd-packages
tar -czvf coscmd-packages.tar.gz coscmd-packages



# インストールパッケージをパブリックネットワークのないマシンにコピーしてから、次のコマンドを実行します
tar -xzvf coscmd-packages.tar.gz
pip install coscmd --no-index -f coscmd-packages
```

## パラメータの設定

### helpオプションの確認

ユーザーは、`-h`または`--help`コマンドを使用して、ツールのhelp情報や使用方法を確認することができます。
```plaintext
coscmd -h  
```
help情報は次のとおりです。
```plaintext
usage: coscmd [-h] [-d] [-s] [-b BUCKET] [-r REGION] [-c CONFIG_PATH]
              [-l LOG_PATH] [--log_size LOG_SIZE]
              [--log_backup_count LOG_BACKUP_COUNT] [-v]
              {config,upload,download,delete,abort,copy,move,list,listparts,info,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl,putbucketversioning,getbucketversioning,probe}
              ...

an easy-to-use but powerful command-line tool. try 'coscmd -h' to get more
informations. try 'coscmd sub-command -h' to learn all command usage, likes
'coscmd upload -h'

positional arguments:
  {config,upload,download,delete,abort,copy,move,list,listparts,info,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl,putbucketversioning,getbucketversioning,probe}
    config              Config your information at first
    upload              Upload file or directory to COS
    download            Download file from COS to local
    delete              Delete file or files on COS
    abort               Aborts upload parts on COS
    copy                Copy file from COS to COS
    move                move file from COS to COS
    list                List files on COS
    listparts           List upload parts
    info                Get the information of file on COS
    restore             Restore
    signurl             Get download url
    createbucket        Create bucket
    deletebucket        Delete bucket
    putobjectacl        Set object acl
    getobjectacl        Get object acl
    putbucketacl        Set bucket acl
    getbucketacl        Get bucket acl
    putbucketversioning
                        Set the versioning state
    getbucketversioning
                        Get the versioning state
    probe               Connection test

optional arguments:
  -h, --help            show this help message and exit
  -d, --debug           Debug mode
  -s, --silence         Silence mode
  -b BUCKET, --bucket BUCKET
                        Specify bucket
  -r REGION, --region REGION
                        Specify region
  -c CONFIG_PATH, --config_path CONFIG_PATH
                        Specify config_path
  -l LOG_PATH, --log_path LOG_PATH
                        Specify log_path
  --log_size LOG_SIZE   specify max log size in MB (default 1MB)
  --log_backup_count LOG_BACKUP_COUNT
                        specify log backup num
  -v, --version         show program's version number and exit
```
これに加えて、ユーザーは各コマンドの後に（パラメータなしで）`-h`を入力すると、そのコマンドの具体的な使用法を確認することができます。次に例を示します。
```plaintext
coscmd upload -h  //コマンドの使用方法を確認します
```

### 設定ファイルの発行

COSCMDツールは、実行前にまず実行時に必要な情報を設定ファイルから読み込みます。COSCMDは、デフォルトでは`~/.cos.conf`から設定項目を読み込みます。

>? 設定する前に、COSコンソールでパラメータ設定用のバケットを作成し（例：configure-bucket-1250000000）、キー情報を作成する必要があります。

設定ファイルの例を次に示します。
```plaintext
[common]
secret_id = AKIDA6wUmImTMzvXZNbGLCgtusZ2E8mG****
secret_key = TghWBCyf5LIyTcXCoBdw1oRpytWk****
bucket = configure-bucket-1250000000
region = ap-chengdu
max_thread = 5
part_size = 1
retry = 5
timeout = 60
schema = https
verify = md5
anonymous = False
```

>?
>- 設定ファイルの`schema`項目で、オプション値はhttp、https、デフォルトはhttpsです。
>- 設定ファイルの`anonymous`項目で、オプション値はTrue、False、匿名モードを使用するかどうか、つまり署名を空にするかどうかを示します。
>- パラメータ設定の詳細については、コマンド`coscmd config -h`を使用して確認してください。
>

### configコマンドを使用して設定ファイルを発行



>!
>- ユーザーには[一時キーを使用](https://intl.cloud.tencent.com/document/product/436/14048)してSDKを呼び出し、一時権限承認方式によってSDK使用の安全性をさらに向上させることをお勧めします。一時キーを申請する際は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従い、ターゲットバケットまたはオブジェクト以外のリソースが漏洩しないようにしてください。
>- どうしてもパーマネントキーを使用したい場合は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従って、パーマネントキーの権限範囲を限定することをお勧めします。



configコマンドは、`~/.cos.conf`に設定ファイルを自動的に発行します。コマンド形式は次のとおりです。
```plaintext
coscmd config [OPTION]...<FILE>...
			  [-h] --help
			  [-a] <SECRET_ID>
			  [-s] <SECRET_KEY>
			  [-t] <TOKEN>
			  [-b] <BucketName-APPID>
              [-r] <REGION> | [-e] <ENDPOINT>
              [-m] <MAX_THREAD>
              [-p] <PART_SIZE>
              [--do-not-use-ssl]
              [--anonymous]   
```

>? ここで「[]」内のフィールドはオプション、「<>」内のフィールドは入力が必要なパラメータです。
>

パラメータ設定の説明は次のとおりです。

| オプション             | パラメータ説明                                                     | 有効値 | 入力必須かどうか |
| ---------------- | ------------------------------------------------------------ | ------ | -------- |
| -a               | キーIDは[APIキーコンソール](https://console.cloud.tencent.com/cam/capi)に移動して取得してください | 文字列 | はい       |
| -s               | Keyは[APIキーコンソール](https://console.cloud.tencent.com/cam/capi)に移動して取得します | 文字列 | はい       |
| -t               | 一時キーtokenは、一時キーを使用するときに設定が必要で、x-cos-security-tokenヘッダーを設定します | 文字列 | いいえ       |
| -b               | 指定されたバケット名。バケットの命名形式はBucketName-APPIDです。[命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください。初回設定時に使用する場合、COSコンソールでバケットを作成し、設定ツールとして用いる必要があります | 文字列 | はい       |
| -r               | バケットの所在リージョンです。[リージョンとアクセスドメイン名](https://www.tencentcloud.com/document/product/436/6224)をご参照ください。| 文字列 | はい       |
| -e               | リクエストのENDPOINTを設定します。ENDPOINTパラメータを設定すると、REGIONパラメータは無効になります。デフォルトのドメイン名を使用している場合、ここでの設定形式は、`cos.<region>.myqcloud.com`となります。グローバルアクセラレーションドメイン名を使用する場合、設定は`cos.accelerate.myqcloud.com`となります | 文字列 | いいえ       |
| -m               | マルチスレッド操作の最大スレッド数（デフォルトは5、範囲は1～30）             | 数値｜いいえ       |
| -p               | チャンク操作の1チャンクサイズ（MB単位、デフォルトは1MB、範囲は1～1000）     | 数値   | いいえ       |
| --do-not-use-ssl | HTTPSではなく、HTTPプロトコルを使用します                              | 文字列 | いいえ       |
| --anonymous      | 匿名操作（署名なし）                                       | 文字列 | いいえ       |

configコマンドの使用例は次のとおりです。

```shell
coscmd config -a AChT4ThiXAbpBDEFGhT4ThiXAbp**** -s WE54wreefvds3462refgwewe**** -b configure-bucket-1250000000 -r ap-chengdu
```

## 一般的なコマンド

### BucketとRegionのコマンドを指定

ユーザーがコマンドを実行するバケット名と所属リージョンを指定しない場合、パラメータの設定時に入力されたバケットがデフォルトで有効になります。異なるバケットで操作を実行する必要がある場合は、バケット名と所属リージョンを指定する必要があります。

>?
> - `-b <BucketName-APPID>`パラメータでバケット名を指定します。バケットの命名形式はBucketName-APPIDです。ここに入力するバケット名は、必ずこの形式である必要があります。
> - `-r <region>`でRegionを指定すると、バケットの所属リージョンを指定することができます。 

- コマンド形式
```plaintext
coscmd -b <BucketName-APPID> -r <region> <action> ...
```
- 操作事例 - バケット名がexamplebucket、所属リージョンが北京のバケットを作成します
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
```
- 操作事例 - Dドライブのファイルpicture.jpgを examplebucketという名前のバケットにアップロードします
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing upload D:/picture.jpg /
```

### 設定ファイルとログファイルパスを指定するコマンド

ユーザーが設定ファイルのパスを指定しない場合、デフォルトの設定ファイルパス`~/.cos.conf`が使用されます。ログファイルパスが指定されない場合、デフォルトのログファイルパス`~/.cos.log`が使用されます。

>?
> - `-c <conf_path>`パラメータで設定ファイルパスを指定すると、COSCMDは実行時にこのパスから設定情報を読み込むようになります。
> - `-l <log_conf>`パラメータでログパスを指定すると、COSCMDは実行中に生成されたログをこのパスのログファイルに出力します。
>

- コマンド形式
```plaintext
coscmd -c <conf_path> -l <log_conf> <action> ...
```
- 操作事例 - 設定ファイルパスを/data/home/cos_conf 、ログ出力パスを/data/home/cos_logと指定し、バケット名がexamplebucket、所属リージョンが北京のバケットを作成します
```plaintext
coscmd -c /data/home/cos_conf -l /data/home/cos_log -b examplebucket-1250000000 -r ap-beijing createbucket
```


### Debugモード実行コマンド

各コマンドの前に`-d`または`--debug`を追加すると、コマンドの実行中に詳細な操作情報が表示されます。次に例を示します。

- コマンド形式
```plaintext
coscmd -d upload <localpath> <cospath>
```

- 操作事例 - アップロード時に詳細情報を出力します
```plaintext
coscmd -d upload -rs D:/folder/ /
```

### Silenceモード実行コマンド

各コマンドの前に`-s`または`--silence`を追加すると、コマンドの実行中にいかなる情報も出力されなくなります。

>?このコマンドは、最小バージョン1.8.6.24を満たす必要があります。

- コマンド形式
```plaintext
coscmd -s upload <localpath> <cospath>
```
- 操作事例
```plaintext
coscmd -s upload D:/picture.jpg /
```

## 一般的なバケットコマンド

### バケットの作成

>? バケットを作成するコマンドを実行するときは、バケット名を指定するパラメータ`-b <BucketName-APPID>と所属リージョンを指定するパラメータ`-r <Region>`を付けてください。coscmd createbucketを直接実行した場合、バケット名と所属リージョンを指定しないと、既存のバケット（パラメータ設定時に入力したバケット）を作成したのと同じことになるため、エラーが発生します。

- コマンド形式
```plaintext
coscmd -b <BucketName-APPID> createbucket
```
- 操作事例-バケット名がexamplebucket、所属リージョンが北京のバケットを作成します
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
```

### バケットの削除

>? `coscmd deletebucket`の使用法は、パラメータを設定する際にストレージバケットに対してのみ有効です。`-b <BucketName-APPID>`でBucketを指定し、`-r <region>`でRegionを指定することをお勧めします。

- コマンド形式
```plaintext
coscmd -b <BucketName-APPID> deletebucket
```
- 操作事例 - 空のバケットを削除します
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket
```
- 操作事例 - 空ではないバケットを強制的に削除します
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket -f
```
>! `-f`パラメータを使用すると、すべてのファイルやバージョン管理を有効にした後の履歴フォルダ、アップロードによって生成されたフラグメントを含むバケットが強制的に削除されますので、操作は慎重に行ってください。

## 一般的なオブジェクトコマンド

### ファイルのアップロード

- ファイルアップロードのコマンド形式
```plaintext
coscmd upload <localpath> <cospath>
```
>! 「<>」のパラメータ を、アップロードする必要のあるローカルファイルパス(localpath)とCOSのストレージパス(cospath)に置き換えてください。
>
- 操作事例 - Dドライブのpicture.jpgファイルをCOSのdocディレクトリにアップロードします
```plaintext
coscmd upload D:/picture.jpg doc/
```
- 操作事例 - Dドライブのdocフォルダからpicture.jpgファイルをCOSのdocディレクトリにアップロードします
```plaintext
coscmd upload D:/doc/picture.jpg doc/
```
- 操作事例 - オブジェクトタイプを指定し、アーカイブタイプのファイルをCOSのdocディレクトリにアップロードします
```plaintext
coscmd upload D:/picture.jpg doc/ -H "{'x-cos-storage-class':'Archive'}"
```
>! -Hパラメータを使用してHTTP headerを設定する場合は、形式がJSONであることを必ず確認してください。例：`coscmd upload -H "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`。その他のヘッダーについては、[PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)のドキュメントをご参照ください。
>
- 操作事例 - metaメタ属性を設定し、COSのdocディレクトリにファイルをアップロードします
```plaintext
coscmd upload D:/picture.jpg doc/ -H "{'x-cos-meta-example':'example'}"
```


### フォルダのアップロード

- フォルダアップロードのコマンド形式
```plaintext
coscmd upload -r <localpath> <cospath>
```
>! Windowsユーザーは、システムに標準搭載されているcmdツールやPowerShellでCOSCMDのuploadコマンドを使用することをお勧めします。その他のツール（git bashなど）は、コマンドパスの解析ポリシーがPowerShellと異なるため、ユーザーのファイルが誤ったパスにアップロードされる可能性があります。
>
- 操作事例 - DドライブのdocフォルダとそのファイルをCOSのルートパスにアップロードします
```plaintext
coscmd upload -r D:/doc /
```
- 操作事例 - DドライブのdocフォルダとそのファイルをCOSのdocパスにアップロードします
```plaintext
coscmd upload -r D:/doc doc
```
- 操作事例 - 同時アップロード、md5と同名・同サイズのファイルをスキップします
```plaintext
coscmd upload -rs D:/doc doc
```
>! -sパラメータを使用すれば、同時アップロードによってmd5と一致するファイルのアップロードをスキップできます（COSの元のファイルは、必ずバージョン1.8.3.2以降のCOSCMDによってアップロードされている必要があります。デフォルトではx-cos-meta-md5のheaderが使用されます）。
>
- 操作事例 - 同時アップロード、同名・同サイズのファイルをスキップします
```plaintext
coscmd upload -rs --skipmd5 D:/doc doc
```
>! -sパラメータを使用すれば、同時アップロードを使用することができます。また、--skipmd5パラメータを使用すると、同名ファイルのサイズのみが比較され、同じサイズであればアップロードがスキップされます。
>
- 操作事例 - 同時アップロードを行い、「Dドライブのdocフォルダにある削除されたファイル」を削除します
```plaintext
coscmd upload -rs --delete D:/doc /
```
- 操作事例 - Dドライブのdocフォルダにある.txtおよび.doc拡張子を持つファイルのアップロードを無視することを選択します
```plaintext
coscmd upload -rs D:/doc / --ignore *.txt,*.doc
```
- 操作事例 - Dドライブのdocフォルダにある.txt拡張子を持つファイルのアップロードを無視することを選択します
```plaintext
coscmd upload -rs D:/doc / --ignore "*.txt"
```
>! 
> - フォルダをアップロードするときに、`--ignore`パラメータを使用すると、いずれかのタイプのファイルを無視することができます。`--include`パラメータを使用すると、いずれかのタイプのファイルをフィルタリングすることができます。shellワイルドカードルールや複数のルールをサポートし、カンマ`,`で区切ります。いずれかの種類の拡張子を無視する場合は、最後に`,`を入力するか、`""`を追加する必要があります。`""`の中に複数のカンマ区切りルールが含まれる場合は、最初のルールに準じます。
> - `--ignore`を使用して特定のフォルダ内のすべてのファイルをフィルタリングしたい場合は、絶対パスを使用し、パスの前後に`""`を追加する必要があります。例えば、`coscmd upload -rs D:/doc / --ignore "D:/doc/ignore_folder/*"`などとします。
>
- 操作事例 - Dドライブのdocフォルダにある.txtと.docという拡張子を持つファイルをアップロードします
```plaintext
coscmd upload -rs D:/doc / --include *.txt,*.doc
```
- 操作事例 - Dドライブのdocフォルダにある.txt拡張子を持つファイルをアップロードします
```plaintext
coscmd upload -rs D:/doc / --include "*.txt"
```

> !
> - 10MB以上のファイルをアップロードする場合、COSCMDはマルチパートアップロード方式を採用します。コマンドの使用法は単純なアップロードと同じで、`coscmd upload <localpath> <cospath>`です。
> - COSCMDは、大きなファイルのブレークポイントアップロード機能をサポートしています。大きなファイルのマルチパートアップロードが失敗した場合、このファイルの再アップロードでは失敗したチャンクのみがアップロードされ、最初からやり直すことはありません（再アップロードしたファイルのディレクトリとコンテンツがアップロードしたディレクトリと同じであることを確認してください）。
> - COSCMDのマルチパートアップロードのときは、チャンクごとにMD5チェックが行われます。
> - COSCMDのアップロードはデフォルトで`x-cos-meta-md5`というヘッダーが付きます。これはこのファイルのmd5値となりますが、--skipmd5パラメータがある場合、 このヘッダーは付きません。


### ファイルリストの照会

照会コマンドは次のとおりです。
- コマンド形式
```plaintext
coscmd list <cospath>
```
- 操作事例 - このバケット内のdoc/というプレフィックスを持つすべてのファイルリストを再帰的に照会します
```plaintext
coscmd list doc/
```
- 操作事例 - このバケット内のすべてのファイルリスト、ファイル数およびファイルサイズを再帰的に照会します
```plaintext
coscmd list -ar
```
- 操作事例 - examplefolderというプレフィックスを持つすべてのファイルリストを再帰的に照会します
```plaintext
coscmd list examplefolder/ -ar
```
- 操作事例 - このバケット内のすべてのファイル履歴を再帰的に照会します
```plaintext
coscmd list -v
```

>?
> - 「<>」内のパラメータを、ファイルリストを照会する必要のあるCOS上のファイルのパス(cospath)に置き換えてください。`<cospath>`が空の場合は、デフォルトで現在のバケットルートディレクトリを照会します。
> - `-a`を使用してすべてのファイルを照会します。
> - `-r`を使用して再帰的に照会すると、リストアップされたファイルの数とサイズの合計が末尾に返されます。
> - `-n num`を使用して、照会の最大値を設定します。

### ファイル情報の確認

コマンドは次のとおりです。

- コマンド形式
```plaintext
coscmd info <cospath> 
```
- 操作事例 - doc/picture.jpgのメタ情報を確認します
```plaintext
coscmd info doc/picture.jpg
```

> - 「<>」内のパラメータを、表示させる必要のあるCOS上のファイルのパス(cospath)に置き換えてください。


### ファイルまたはフォルダのダウンロード


#### ファイルダウンロードのコマンド形式
```plaintext
coscmd download <cospath> <localpath>
```
>! 「<>」のパラメータ を、ダウンロードする必要のあるCOS上のファイルのパス(cospath)とローカルストレージパス(localpath)に置き換えてください。
>
- 操作事例 - COS上のdoc/picture.jpgをD:/picture.jpgにダウンロードします
```plaintext
coscmd download doc/picture.jpg D:/picture.jpg
```
- 操作事例 - COS上のdoc/picture.jpgをDドライブにダウンロードします
```plaintext
coscmd download doc/picture.jpg D:/
```
- 操作事例 - バージョンID付きのpicture.jpgファイルをDドライブにダウンロードします
```plaintext
coscmd download picture.jpg --versionId MTg0NDUxMzc2OTM4NTExNTg7Tjg D:/
```

#### フォルダダウンロードのコマンド形式
```plaintext
coscmd download -r <cospath> <localpath>
```
- 操作事例 - docディレクトリをD:/folder/docにダウンロードします
```plaintext
coscmd download -r doc D:/folder/
```
- 操作事例 - ルートディレクトリファイルをダウンロードしますが、ルートディレクトリ下のdocディレクトリはスキップします
```plaintext
coscmd download -r / D:/ --ignore "doc/*"
```
- 操作事例 - 現在のバケットのルートディレクトリにあるすべてのファイルを上書きしてダウンロードします
```plaintext
coscmd download -rf / D:/examplefolder/
```
>! ローカルに同名ファイルがある場合、ダウンロードは失敗しますので、`-f`パラメータを使用してローカルファイルを上書きする必要があります。
>
- 操作事例 - 現在のbucketのルートディレクトリにあるすべてのファイルを同時にダウンロードし、同名ファイルのmd5チェックはスキップします
```plaintext
coscmd download -rs / D:/examplefolder
```
>! パラメータ`-s`または`--sync`を使用すると、フォルダをダウンロードする際に、すでにローカルに存在する同一ファイルをスキップすることができます（ただし、ダウンロードするファイルがCOSCMDのuploadインターフェース経由でアップロードされたもので、そのファイルに`x-cos-meta-md5`ヘッダーがふくまれることが前提条件です）。
>
- 操作事例 - 現在のbucketのルートディレクトリにあるすべてのファイルを同時にダウンロードし、同サイズ・同名のファイルをスキップします
```plaintext
coscmd download -rs --skipmd5 / D:/examplefolder
```
- 操作事例 - 現在のバケットのルートディレクトリにあるすべてのファイルを同時にダウンロードし、「クラウドでは削除されたがローカルでは削除されていないファイル」を同時に削除します
```plaintext
coscmd download -rs --delete / D:/examplefolder
```
- 操作事例 - .txtと.docという拡張子を持つファイルを無視します
```plaintext
coscmd download -rs / D:/examplefolder --ignore *.txt,*.doc
```
- 操作事例 - .txt拡張子を持つファイルを無視します
```plaintext
coscmd download -rs / D:/examplefolder --ignore "*.txt"
```
>! 
> - フォルダをアップロードするときに、`--ignore`パラメータを使用すると、いずれかのタイプのファイルを無視することができます。`--include`パラメータを使用すると、いずれかのタイプのファイルをフィルタリングすることができます。shellワイルドカードルールや複数のルールをサポートし、カンマ`,`で区切ります。いずれかの種類の拡張子を無視する場合は、最後に`,`を入力するか、`""`を追加する必要があります。`""`の中に複数のカンマ区切りルールが含まれる場合は、最初のルールに準じます。
> - `--ignore`を使用して特定のディレクトリ内のすべてのファイルをフィルタリングしたい場合は、絶対パスを使用し、パスの前後に`""`を追加する必要があります。例えば、`coscmd upload -rs D:/doc / --ignore "D:/doc/ignore_folder/*"`などとします。
>
- 操作事例 - .txtと.docという拡張子を持つファイルをフィルタリングします
```plaintext
coscmd download -rs / D:/examplefolder --include *.txt,*.doc
```
- 操作事例 - .txt拡張子を持つファイルをフィルタリングします
```plaintext
coscmd download -rs / D:/examplefolder --include "*.txt"
```
>! 古いバージョンのmgetインターフェースは廃止されました。downloadインターフェースはチャンク化されたダウンロードを使いますので、downloadインターフェースを使用してください。


### 署名入りダウンロードURLの取得

- コマンド形式
```plaintext
coscmd signurl <cospath>
```
- 操作事例 - doc/picture.jpgパスの署名付きURLを発行します
```plaintext
coscmd signurl doc/picture.jpg
```
- 操作事例 - doc/picture.jpgパスの100s署名付きURLを発行します
```plaintext
coscmd signurl doc/picture.jpg -t 100
```

>?
> - 「<>」のパラメータを、ダウンロードURLを取得する必要のあるCOS上のファイルのパス(cospath)に置き換えてください。
> - `-t time`を使用して、このURLの署名の有効期間（単位は秒）を設定します。デフォルトは10000sです。


### ファイルまたはフォルダの削除

#### ファイル削除のコマンド形式
```plaintext
coscmd delete <cospath>
```
> - 「<>」内のパラメータを、削除する必要のあるCOS上のファイルのパス(cospath)に置き換えてください。ツールは、削除操作を確認するようユーザーに促します。

- 操作事例 - doc/exampleobject.txtを削除します
```plaintext
coscmd delete doc/exampleobject.txt
```
- 操作事例 - バージョンID付きのファイルを削除します
```plaintext
coscmd delete doc/exampleobject.txt --versionId MTg0NDUxMzc4ODA3NTgyMTErEWN
```

#### フォルダ削除のコマンド形式
```plaintext
coscmd delete -r <cospath>
```
- 操作事例 - docディレクトリを削除します
```plaintext
coscmd delete -r doc
```
- 操作事例 - folder/docディレクトリを削除します
```plaintext
coscmd delete -r folder/doc
```
- 操作事例 - docフォルダ下のすべてのバージョン管理ファイルを削除します
```plaintext
coscmd delete -r doc/ --versions
```
>?
>- 一括削除では`y`を入力して確定する必要がありますが、`-f`パラメータを使用すると確認をスキップして直接削除することができます。
>- フォルダを削除するコマンドを実行すると、現在のフォルダとそのファイルが削除されますのでご注意ください。ただし、バージョン管理されたファイルを削除する場合は、バージョンIDを指定して削除する必要があります。

### マルチパートアップロードファイルのフラグメントの照会

- コマンド形式
```plaintext
coscmd listparts <cospath>
```
- 操作事例 - doc/プレフィックス付きファイルフラグメントを照会します
```plaintext
coscmd listparts doc/
```

### マルチパートアップロードファイルのフラグメントをクリア

- コマンド形式
```plaintext
coscmd abort
```
- 操作事例 - アップロードされたすべてのファイルフラグメントを削除します
```plaintext
coscmd abort
```

### ファイルまたはフォルダのコピー

#### ファイルコピーのコマンド形式
```plaintext
coscmd copy <sourcepath> <cospath>
```
- 操作事例 - 同じバケット内でコピーする場合、examplebucket-1250000000バケット内のpicture.jpgファイルをdocフォルダにコピーします
```plaintext
coscmd -b examplebucket-1250000000 -r ap-chengdu copy examplebucket-1250000000.ap-chengdu.myqcloud.com/picture.jpg doc/
```
- 操作事例 - 異なるバケット内でコピーする場合、examplebucket2-1250000000バケットのdoc/picture.jpgオブジェクトをexamplebucket1-1250000000バケットのdoc/examplefolder/にコピーします
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/
```
- ストレージタイプを変更し、ファイルタイプを低頻度ストレージに変更します
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/ -H "{'x-cos-storage-class':'STANDARD_IA'}"
```
- ストレージタイプを変更し、ファイルタイプをCASに変更して、photo.jpgとリネームします
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/photo.jpg -H "{'x-cos-storage-class':'Archive'}"
```

#### フォルダコピーのコマンド形式
```plaintext
coscmd copy -r <sourcepath> <cospath>
```
- 操作事例 - examplebucket2-1250000000バケット内のexamplefolderディレクトリをexamplebucket1-1250000000バケットのdocディレクトリにコピーします
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder doc/
```

> ?
> - 「<>」内のパラメータを、コピーする必要のあるCOS上のファイルのパス(sourcepath)と、COS上にコピーする必要のあるファイルのパス(cospath)に置き換えてください。
> - sourcepathの形式は、`<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`です。
> - -dパラメータを使用して`x-cos-metadata-directive`パラメータを設定します。オプション値はCopyとReplacedで、デフォルトはCopyです。
> - -Hパラメータを使用してHTTP headerを設定する場合は、形式がJSONであることを確認してください。例：`coscmd copy -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`。その他のヘッダーについては、[PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)のドキュメントをご参照ください。

### ファイルまたはフォルダの移動
>! 移動コマンドの<sourcepath>`は`<cospath>`と同一にすることはできません。同一にした場合はファイルが削除されます。moveコマンドは先にコピーを行ってから削除するため、`<sourcepath>`パスのファイルが最終的に削除されることが原因です。
#### ファイル移動のコマンド形式
```plaintext
coscmd move <sourcepath> <cospath> 
```
- 操作事例 - 同じバケット内で移動する場合、examplebucket-1250000000バケット内のpicture.jpgファイルをdocフォルダに移動します 
```plaintext
coscmd -b examplebucket-1250000000 -r ap-chengdu move examplebucket-1250000000.ap-chengdu.myqcloud.com/picture.jpg doc/
```
- 操作事例 - 異なるバケット内で移動する場合、examplebucket2-1250000000バケット内のdoc/picture.jpgオブジェクトをexamplebucket1-1250000000バケットのdoc/folder/に移動します
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/picture.jpg doc/folder/
```
- 操作事例 - ストレージタイプを変更し、ファイルタイプを低頻度ストレージに変更します
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/picture.jpg doc/folder/ -H "{'x-cos-storage-class':'STANDARD_IA'}"
```
- 操作事例 - ストレージタイプを変更し、ファイルタイプをCASに変更します
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'Archive'}"
```

#### フォルダ移動のコマンド形式
```plaintext
coscmd move -r <sourcepath> <cospath>
```
- 操作事例 - examplebucket2-1250000000バケット内のexamplefolderディレクトリをexamplebucket1-1250000000バケットのdocディレクトリに移動します
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder doc/
```

> ?
> - 「<>」内のパラメータを、移動させる必要のあるCOS上のファイルのパス(sourcepath)と、COSに移動する必要のあるファイルのパス(cospath)に置き換えてください。
> - sourcepathの形式は、`<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`です。
> - -dパラメータを使用して`x-cos-metadata-directive`パラメータを設定します。オプション値はCopyとReplacedで、デフォルトはCopyです。
> - -Hパラメータを使用してHTTP headerを設定する場合は、形式がJSONであることを確認してください。例：`coscmd move -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`。その他のヘッダーについては、[PUT Object - copy](https://intl.cloud.tencent.com/document/product/436/10881)のドキュメントをご参照ください。

### オブジェクトのアクセス権限の設定

- コマンド形式
```plaintext
coscmd putobjectacl --grant-<permissions> <UIN> <cospath>
```
- 操作事例 - アカウント100000000001にpicture.jpgの読み込み権限を付与します
```plaintext
coscmd putobjectacl --grant-read 100000000001 picture.jpg
```
- 操作事例 - ファイルのアクセス権限を照会します
```plaintext
coscmd getobjectacl picture.jpg
```

### バージョン管理の有効化/一時停止

- コマンド形式
```plaintext
coscmd putbucketversioning <status>
```
- 操作事例 - バージョン管理を有効化します
```plaintext
coscmd putbucketversioning Enabled
```
- 操作事例 - バージョン管理を一時停止します
```plaintext
coscmd putbucketversioning Suspended
```
- 操作事例 - バージョン管理を照会します
```plaintext
coscmd getbucketversioning
```

> !
> - 「<>」のパラメータを、ご希望のバージョン管理ステータス(status)に置き換えてください。
>- 一度バージョン管理を有効にしたバケットは、バージョン管理を有効にしていない状態（初期ステータス）に戻すことはできません。ただし、このバケットのバージョン管理を一時停止することはでき、その後にアップロードされるオブジェクトでは複数のバージョンが生成されなくなります。

### アーカイブファイルのリカバリ

- アーカイブファイルリカバリのコマンド形式
```plaintext
coscmd restore <cospath>
```
- 操作事例 - 高速取得モードでpicture.jpgをリトリーブします。有効期間は3日間です
```plaintext
coscmd restore -d 3 -t Expedited picture.jpg
```
- アーカイブファイル一括リカバリのコマンド形式
```plaintext
coscmd restore -r <cospath>
```
- 操作事例 - 高速取得モードでexamplefolder/ディレクトリをリトリーブします。有効期間は3日間です
```plaintext
coscmd restore -r -d 3 -t Expedited examplefolder/
```

>?
> - 「<>」のパラメータを、ファイルリストを照会する必要のあるCOS上のファイルのパス(cospath)に置き換えてください。
> - `-d <day>`を使用して、一時コピーの有効期限を設定します。デフォルト値は7です。
> - `-t <tier>`を使用してリカバリモードを指定します。列挙値はExpedited （高速取得モード）、Standard （標準取得モード）、Bulk（一括取得モード）であり、デフォルト値はStandardです。

## よくあるご質問

COSCMDツールの使用に関するご質問は、[COSCMDツールに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/436/30586)をご参照ください。



