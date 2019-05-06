## 機能説明
COSCMD ツールを使って、ユーザーが簡単なコマンドラインでオブジェクト（Object）の一括アップロード、ダウンロード、削除などを実現できます。

## 使用環境

### システム環境

Windows、Linux、macOSシステムをサポートします。

>?
- ローカルの文字フォーマットをUTF-8にしてください。さもなければ中国語ファイルを操作するときに異常が発生します。
- ローカル時間と国際標準時間が一致するように確保してください。誤差が大きければ、正常に使用できません。

### ソフトウェア依存

- Python 2.7/3.5/3.6。
- 最新バージョンのpip。

#### インストールと構成

環境インストールと構成の詳細操作については、[Pythonのインストールと構成](https://cloud.tencent.com/document/product/436/10866)を参照してください。

## ダウンロードおよびインストール
pipのインストール方式は以下のとおりです。

- **pipのインストール**
  `pip`コマンドを実行してインストールします。
```sh
pip install coscmd
```

 インストールした後、ユーザーが`-v`または`--version`コマンドで現在のバージョン情報を確認できます。
- **pipアップデート**
  `pip`コマンドを実行してアップデートします。
```sh
pip install coscmd -U
```
>! pipバージョンが10.0.0以降の場合、依存ライブラリをアップグレード、インストールするときに失敗する場合があります。pipバージョン9.x（pip install pip==9.0.0）をおすすめします。

- **ソースコードのインストール（非推奨）**
  ダウンロードURL：[GitHub URL](https://github.com/tencentyun/coscmd.git)。
```shell
git clone https://github.com/tencentyun/coscmd.git
cd coscmd
python setup.py install
```
>!Pythonバージョンが2.6の場合、pipの依存ライブラリをインストールするときに失敗する可能性が高い。この方法でインストールすることをおすすめします。

- **オフラインインストール**
```sh
# パブリックネットワークに接続するマシンで下記のコマンドを実行します
mkdir coscmd-packages
pip download coscmd -d coscmd-packages
tar -czvf coscmd-packages.tar.gz coscmd-packages
```
>! 2つの機器のPythonバージョンが一致するようにしてください。さもなければインストール失敗が発生します。
>```sh
># インストールパッケージをパブリックネットワークに接続されていない機器にコピーした後に以下のコマンドを実行します
>tar -xzvf coscmd-packages.tar.gz
>pip install coscmd --no-index -f coscmd-packages
```

## 使用方法

### help表示

ユーザーが`-h`または`--help`コマンドでツールのhelp情報を表示します。
```shell
coscmd -h  //現在バージョン情報を表示する
```

help情報を次に示します。
```shell
usage: cos_cmd.py [-h] [-d] [-b BUCKET] [-r REGION] [-c CONFIG_PATH]
                  [-l LOG_PATH] [-v]
                  {config,upload,download,delete,copy,list,info,mget,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl}
                  ...

an easy-to-use but powerful command-line tool. try 'coscmd -h' to get more
informations. try 'coscmd sub-command -h' to learn all command usage, likes
'coscmd upload -h'

positional arguments:
  {config,upload,download,delete,copy,list,info,mget,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl}
    config              config your information at first.
    upload              upload file or directory to COS.
    download            download file from COS to local.
    delete              delete file or files on COS
    copy                copy file from COS to COS.
    list                list files on COS
    info                get the information of file on COS
    mget                download file from COS to local.
    restore             restore
    signurl             get download url
    createbucket        create bucket
    deletebucket        delete bucket
    putobjectacl        set object acl
    getobjectacl        get object acl
    putbucketacl        set bucket acl
    getbucketacl        get bucket acl

optional arguments:
  -h, --help            show this help message and exit
  -d, --debug           debug mode
  -b BUCKET, --bucket BUCKET
                        set bucket
  -r REGION, --region REGION
                        set region
  -c CONFIG_PATH, --config_path CONFIG_PATH
                        set config_path
  -l LOG_PATH, --log_path LOG_PATH
                        set log_path
  -v, --version         show program's version number and exit
```

それ以外、ユーザーが各コマンドの後（パラメータなし）に`-h`を入力して、このコマンドの具体的な使い方を表示します。例えば：
```shell
coscmd upload -h  //uploadコマンドの使い方を表示する
```

### 構成パラメータ

COSCMDツールが使用前にパラメータ構成が必要です。ユーザーが以下のコマンドで構成を行うことができます。
```shell
coscmd  config [-h] -a <SECRET_ID> -s <SECRET_KEY> -b <BUCKET>
                         (-r <REGION> | -e <ENDPOINT>) [-m <MAX_THREAD>]
                         [-p <PART_SIZE>] [-u <APPID>] [--do-not-use-ssl]
                         [--anonymous <ANONYMOUS>]      
```
上例で、"<>"のフィールドは選択必須パラメータです。"[]"のフィールドは選択可能パラメータです。そのうち：

| 名前       | 記述                                                         | 有効値 |
| :--------- | :----------------------------------------------------------- | :----- |
| SECRET_ID  | 選択必須パラメータ。APPIDに対応する暗号鍵IDをCOSコンソール左側欄【暗号鍵管理】または[クラウドAPI暗号鍵コンソール]( https://console.cloud.tencent.com/cam/capi)から取得できます | 文字列 |
| SECRET_KEY | 選択必須パラメータ。APPIDに対応する暗号鍵KeyをCOSコンソール左側欄【暗号鍵管理】または[クラウドAPI暗号鍵コンソール]( https://console.cloud.tencent.com/cam/capi)から取得できます | 文字列 |
| BUCKET     | 選択必須パラメータ。指定したバケット名。Bucketの命名規則は`<BucketName-APPID>`です。[バケット概要](https://cloud.tencent.com/document/product/436/13312)を参照してください | 文字列 |
| REGION     | 選択必須パラメータ。バケット所在地域です。[可能な地域](https://cloud.tencent.com/doc/product/436/6224)を参照してください | 文字列 |
| MAX_THREAD | 選択可能パラメータ。マルチスレッドでアップロードするときの最大スレッド数（デフォルトは5、範囲は1～10）               | 数字   |
| PART_SIZE  | 選択可能パラメータ。マルチパートアップロードのパートの大きさ（単位MB、デフォルトは1MB、範囲は1～100）        | 数字   |


>!
- `~/.cos.conf`ファイル（Windows環境で、このファイルは**マイドキュメント**の非表示ファイル）を直接編集できます。このファイルは初期ときに存在しません。`coscmd config`コマンドで生成するか、ユーザーが手動で作成することもできます。
  構成完了後の`.cos.conf`ファイル内容例を次に示します。
```shell
 [common]
secret_id = AChT4ThiXAbpBDE
secret_key = WE54wreefvds34
bucket = examplebucket-1250000000
region = ap-guangzhou
max_thread = 5
part_size = 1
schema = https
```
- 構成ファイルに`schema`項目を追加して、`http/https`を選択できます。デフォルトは`https`。
- `anonymous`項目から`True/False`を選択して、匿名モードを使用できます。すなわち署名を空にします。
- Bucketの命名規則は`<BucketName-APPID>`。


### Bucketのコマンドを指定する
-  `-b<BucketName-APPID>でBucketを指定する`で特定のBucketを指定できます。
-  Bucketの命名規則は`<BucketName-APPID>`です。ここに入力するバケット名はこのフォーマットでなければなりません。
```sh
#コマンドフォーマット
coscmd -b <BucketName-APPID> method ...
#操作例-ファイルをアップロードする
coscmd -b examplebucket-1250000000 upload a.txt b.txt
#操作例-Bucketを作成する
coscmd -b examplebucket-1250000000 createbucket
```

### バケットの作成
-  `-b<BucketName-APPID>でBucketを指定する`に合わせて使用することをおすすめします。
```sh
#コマンドフォーマット
coscmd -b <BucketName-APPID> createbucket
#操作例
coscmd createbucket
coscmd -b examplebucket-1250000000 createbucket
```

### バケットの削除
-  `-b<BucketName-APPID>でBucketを指定する`に合わせて使用することをおすすめします。
```sh
#コマンドフォーマット
coscmd -b <BucketName-APPID> deletebucket
#操作例
coscmd deletebucket
coscmd -b examplebucket-1250000000 deletebucket
coscmd -b examplebucket-1250000000 deletebucket -f
```

-  -fパラメータを使うと、強制的にこのBucket（すべてのファイル、バージョンコントロールを有効にした後の過去フォルダ、アップロードにより生成される断片を含む）を削除します。

### ファイルまたはフォルダのアップロード
- ファイルアップロードコマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd upload <localpath> <cospath>
#操作例
#ローカルの/home/folder1/text.txtファイルをCOSのfolder2/text.txtパスにアップロードします
coscmd upload /home/folder1/text.txt folder2/text.txt
coscmd upload /home/folder1/text.txt folder2/
```

- フォルダアップロードコマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd upload -r <localpath> <cospath>
#操作例
coscmd upload -r /home/folder1/ folder2/folder1
coscmd upload -r /home/folder1/ folder2/
#この操作はfolder2/ディレクトリでfolder1/フォルダを作成します
coscmd upload -r /home/folder1  folder2/
#Bucketルートディレクトリにアップロードします
coscmd upload -r /home/folder1/ /
#同期アップロードし、md5が同じのファイルをスキップします
coscmd upload -rs /home/folder1/ /home/folder1
#.txtと.docのファイルを無視します
coscmd upload -rs /home/folder1/ /home/folder1 --ignore *.txt,*.doc
```

 "<>"のパラメータをアップロードするローカルファイルパス（localpath）、およびCOSに保存するパス（cospath）に変更してください。
 
 >!
 >  - ファイルをアップロードするときにCOSのパスとファイル（フォルダ）の名前を補足する（例を参考する）必要があります。
 >  - COSCMDは、大容量ファイルの一時的停止/再開アップロード機能をサポートします。大容量ファイルのマルチパートアップロードに失敗した場合、このファイルを再アップロードするとき最初からでなく、失敗したパートのみをアップロードします。（再アップロードするファイルのディレクトリおよび内容をアップロード先ディレクトリと一致するようにしてください）
 >  - COSCMDでマルチパートアップロードするとき、パートごとにMD5検証を行います。
 >  - COSCMDでアップロードするとき、デフォルトは`x-cos-meta-md5`のヘッダーを含みます。値はこのファイルの`md5`値です。
 >  - -sパラメータを使うと同期アップロードができます。md5が一致するファイルのアップロードをスキップします（COSの元ファイルが1.8.3.2以降のCOSCMDによってアップロードされる必要があります。デフォルトはx-cos-meta-md5のheaderを含みます）。
 >  - -Hパラメータを使ってHTTP headerを設定するとき、jsonフォーマットを確保してください。例：`coscmd upload -H '{"Cache-Control":"max-age=31536000","Content-Language":"ja-JP"}’ <localpath> <cospath>`。
 >  - フォルダをアップロードするとき、--ignoreパラメータを使用すると特定の種類のファイルを無視できます。shellのワイルドカード規則と複数の規則をサポートします。カンマ`,`で区切ります。特定のサフィックスを無視するとき、末尾に`,`を入力するか、`""`をつける必要があります。
 >  - 現時点で最大40TBの単一ファイルのみのアップロードをサポートします。

### ファイルまたはフォルダをダウンロードします
- ファイルのダウンロードコマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd download <cospath> <localpath>
#操作例
coscmd download folder2/text.txt /home/folder1/text.txt
coscmd download folder2/text.txt /home/folder1/
```
- フォルダのダウンロードコマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd download -r <cospath> <localpath>
#操作例
coscmd download -r /home/folder1/ folder2/folder1
coscmd download -r /home/folder1/ folder2/
#現在のbucketルートディレクトリのすべてのファイルをダウンロードし、ローカルファイルを上書きします
coscmd download -rf / folder2/folder1
#現在のbucketルートディレクトリのすべてのファイルを同期ダウンロードし、md5検証が同じのファイルをスキップします
coscmd download -rs / folder2/folder1
#.txtと.docのファイルを無視します
coscmd download -rs / folder2/folder1 --ignore *.txt,*.doc 
```
"<>"の中のパラメータを、ダウンロードするCOSのファイルのパス（cospath）、およびローカルストレージパス（localpath）に変更してください。
>!
> - ローカルに同名ファイルが存在した場合、ダウンロードに失敗します。`-f`パラメータでローカルファイルを上書きします。
> - `download`APIはパートダウンロードを採用します。旧バージョンの`mget`APIはすでに廃止されました。`download`APIを使ってください。
> - `-s`または`--sync`パラメータを使うと、フォルダをダウンロードするときにローカルに存在している同じファイル（前提としてフォルダのダウンロードは`COSCMD`の`upload`APIによりアップロードされたものであり、ファイルには`x-cos-meta-md5`のヘッダーが含まれる）をスキップします。
> - フォルダをダウンロードするとき、--ignoreパラメータを使用すると特定の種類のファイルを無視します。shellのワイルドカード規則と複数の規則をサポートします。カンマ`,`で区切ります。特定のサフィックスを無視するとき、末尾に`,`を入力するか、`""`をつける必要があります。

### ファイルまたはフォルダを削除します
- ファイル削除コマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd delete <cospath>
#操作例
coscmd delete folder2/text.txt
```
- フォルダ削除コマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd delete -r <cospath>
#操作例
coscmd delete -r folder2/
coscmd delete -r /
```

 "<>"の中のパラメータを、削除するCOSのファイルのパス（cospath）に変更してください。ツールは、ユーザーに削除確認を提示します。

 >!一括削除にはOKを入力する必要があります。`-f`パラメータでOK入力をスキップします。

### アップロードするファイルフラグメンテーションをクリアします
- コマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd abort
#操作例
coscmd abort
```

### ファイルまたはフォルダのレプリケーション
- ファイルのレプリケーションコマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd copy <sourcepath> <cospath> 
#操作例
coscmd copy bucket-appid.cos.ap-guangzhou.myqcloud.com/a.txt folder1/text.txt
```
- フォルダのレプリケーションコマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd copy -r <sourcepath> <cospath>
#操作例
coscmd copy -r bucket-appid.cos.ap-guangzhou.myqcloud.com/coscmd/ folder1
coscmd copy -r bucket-appid.cos.ap-guangzhou.myqcloud.com/coscmd/ folder1/
```

 "<>"の中のパラメータを、レプリケーションするCOSのファイルのパス（sourcepath）、COSにレプリケーションするファイルのパス（cospath）に変更してください

 >!sourcepathの仕様は以下のとおりです。```<bucketname>-<appid>.cos.<region>.myqcloud.com/<cospath>```。

### ファイルリストのプリント
プリントコマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd list <cospath>

#操作例
coscmd list -a
coscmd list folder2/text.txt  -r -n 10
```
"<>"の中のパラメータを、ファイルリストをプリントする必要があるCOSのファイルのパス（cospath）に変更してください。
 - `-a`を使って、すべてのファイルをプリントします。
 - `-r`を使って、プリントを渡し、リストするファイルの数量と大きさの和を末尾に返します。
 - `-n num`を使って、プリント数量の最大値を設定します。

>!`<cospath>`が空である場合、デフォルトで現在のBucketルートディレクトリをプリントします。

### ファイル情報の表示
コマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd info <cospath> 

#操作例
coscmd info folder2/text.txt
```
"<>"の中のパラメータを、表示するCOSのファイルのパス（cospath）に変更してください。

### 署名付きダウンロードURLを取得します
コマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd signurl <cospath>

#操作例
coscmd signurl folder2/text.txt
coscmd signurl folder2/text.txt -t 100
```

"<>"の中のパラメータを、ダウンロードURLの取得が必要なCOSのファイルのパス（cospath）に変更してください
`-t time`を使って、署名をプリントする有効時間（単位は秒）を設定します

### アクセス制御（ACL）の設定
下記のコマンドを使って、Bucketのアクセス制御を設定します。
```sh
#コマンドフォーマット
coscmd putbucketacl --grant-read <root_uin> --grant-write <root_uin> --grant-full-control <root_uin>/<sub_uin>

#操作例 
coscmd putbucketacl --grant-read 100000000001,100000000001/100000000002 --grant-write anyone --grant-full-control 100000000001/100000000003
```

下記のコマンドを使って、Objectのアクセス制御を設定します。
```sh
#コマンドフォーマット
coscmd putobjectacl --grant-read <root_uin>,<root_uin>/<sub_uin> --grant-write <root_uin> --grant-full-control <root_uin>/<sub_uin> <cospath> 

#操作例
coscmd putobjectacl  --grant-read 100000000001,100000000001/100000000002 --grant-write anyone --grant-full-control 100000000001/100000000003 folder1/text.txt
```

#### ACL設定の案内

- --grant-readは、読取権限を表します。
- --grant-writeは、書込権限を表します。
- --grant-full-controlは、読み書き権限を表します。
- ルートアカウントに権限を付与する場合、`<root_uin>`の形式を使用します。例えば100000000001。
- サブアカウントに権限を付与する場合、`<root_uin>/<sub_uin>`の形式を使用します。例えば100000000001/100000000002。
- すべての人に権限を付与する場合、anyoneの形式を使用します。
- 同時に権限を付与する複数のアカウントは英語カンマ`,`で区切ります。
- パラメータを、ACLを設定するファイルのCOSパス（cospath）に変更してください。

### アクセス制御（ACL）の取得
- 下記のコマンドを使って、Bucketのアクセス制御を設定します。
```sh
#コマンドフォーマット
coscmd getbucketacl 
#操作例
coscmd getbucketacl
```

- 下記のコマンドを使って、Objectのアクセス制御を設定します。
```sh
#コマンドフォーマット
coscmd putbucketacl <cospath> 
#操作例
coscmd getobjectacl folder1/text.txt 
```

### バージョン制御の有効・無効
コマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd putbucketversioning <status>

#バージョン制御を有効にする
coscmd putbucketversioning Enabled

#バージョン制御を無効にする
coscmd putbucketversioning Suspended
```

"<>"の中のパラメータを、バージョンコントロールのステータス（status）に変更してください。
>!バージョン制御の有効化は不可逆プロセスです。今後このbucketは、JSON API（すべてのJSON SDKを含む）を使用できなくなりますので、よくご確認のうえ選択してください。

### アーカイブファイルの回復
- アーカイブファイルの復元コマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd restore <cospath>
#操作例
coscmd restore -d 3 -t Expedited a.txt 
```
- アーカイブファイルの一括復元コマンドは以下のとおりです。
```sh
#コマンドフォーマット
coscmd restore -r <cospath>
#操作例
coscmd restore -r -d 3 -t Bulk folder/
```

 "<>"の中のパラメータを、ファイルリストをプリントする必要があるCOSのファイルのパス（cospath）に変更してください。
 - `-d day`を使って、一時コピーの期限切れ時間を設定します。デフォルト値：7。
 - `-t tier`を使って、復元プロセスタイプを設定します。列挙値：Expedited、Standard、Bulk。デフォルト値：Standard。

### Debugモードの実行コマンド
各コマンドの前に`-d`または`-debug`を追加します。以下のようにコマンド実行中に詳細な操作情報を表示します。
```sh
#uploadの詳細操作情報を表示します。コマンドフォーマット：
coscmd -d upload <localpath> <cospath>

#操作例
coscmd -d upload /home/folder1/text.txt folder2/text.txt  
```

## FAQ
COSCMDツールを使用するときに何らかの質問がありましたら、[COSCMDツールについてのよくある質問](https://cloud.tencent.com/document/product/436/30744)を参照してください。

