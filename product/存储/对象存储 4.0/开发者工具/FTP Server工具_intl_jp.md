COS FTP Serverは、FTPプロトコルでCOSのオブジェクトとディレクトリ（ファイルのアップロード、ダウンロード、削除とフォルダの作成などを含む）を直接的に操作することをサポートします。FTP Serverツールは、Pythonにより実現され、インストールがさらに簡単になりました。

## 使用開始

### システム環境

OS：Linux。Tencent CentOSシリーズ[CVM](https://cloud.tencent.com/document/product/213)をおすすめします。現時点でWindowsシステムをサポートしません。

Pythonインタプリタバージョン：Python 2.7。[Pythonのインストールと構成](https://cloud.tencent.com/document/product/436/10866)を参照してインストールと構成を行ってください。

依存パッケージ：
- cos-python-sdk-v5 （>=1.6.5）
- pyftpdlib （>=1.5.2）


### 使用制限

COS XMLバージョンに適します。

### インストールと実行

リンク取得：[cos-ftp-server](https://github.com/tencentyun/cos-ftp-server-V5)

1. setup.pyを実行し、FTP Serverおよび関連の依存ライブラリ（インターネット接続が必要）をインストールします。
```bash
python setup.py install  # ここであなたのアカウントsudoまたはroot権限が必要となることがあります。
```
2. 構成例ファイルconf/vsftpd.conf.exampleをコピーして、conf/vsftpd.confに名前変更します。[構成ファイル](#conf)章節を参考し、Bucketとユーザー情報を正しく構成してください。
3. ftp_server.pyを実行し、FTP Serverを起動します。
```bash
python ftp_server.py
```
さらに、以下の2つのFTP Server起動方法があります。
 - nohupコマンドを使って、アプリケーションサーバープロセス方式で起動します。
```bash
nohup python ftp_server.py >> /dev/null 2>&1 &
```
 - screenコマンドを使って、バックグラウンドで実行されます（screenツールをインストールする必要がある)。
```bash
screen -dmS ftp
screen -r ftp
python ftp_server.py
#ショートカットキーを使って、主screenに切り替えます。
Ctrl+A+D 
```

### 停止

- FTP Serverが直接的に実行される場合、またはscreen方式でバックグラウンドで実行される場合、ショートカットキー`Ctrl+C`を使って、FTP Serverの実行を停止できます。 

- nohupコマンドで起動する場合、次の方法で停止できます。
```bash
ps -ef | grep python | grep ftp_server.py | grep -v grep | awk '{print $2}' | xargs -I{} kill {}
```


## 機能説明

**アップロードメカニズム**：ストリーミングアップロードで、ローカルのディスクに書き込むことはしません。標準のFTPプロトコルで動作ディレクトリを構成するだけで十分です。実際のディスクストレージ空間を使用しません。
**ダウンロードメカニズム**：直接的にストリーミングでクライアントに返します
**ディレクトリメカニズム**：bucketをFTP Server全体のルートディレクトリとして使用します。bucket配下で複数のサブディレクトリを作成できます。
**複数のbucketバインディング**：同時に複数のbucketのバインディングをサポートします。
**削除操作の制限**：新しいFTP Serveでftpユーザーごとに`delete_enable`オプションを構成できます。このftpユーザーがファイルを削除できるかどうかを表します。

>?複数のbucketのバインディング：異なるFTP Serverの動作パス（`home_dir`）で実現されます。異なるBucketとユーザー情報を指定するときにそれぞれ違う`home_dir`を確保しなければなりません。


### サポートするFTPコマンド

- put
- mput
- get
- rename
- delete
- mkdir
- ls
- cd
- bye
- quite
- size

### FTPコマンドをサポートしません

- append
- mget（ネイティブmgetコマンドをサポートしませんが、一部のWindowsクライアントで、一括ダウンロードができます。例えば、FileZillaクライアント。）

>?FTP Serveツールは現時点で一時停止/再開機能をサポートしません。

<a id="conf"></a>
## 構成ファイル

 Ftp Serverツールの構成例ファイルは、conf/vsftpd.conf.exampleです。コピーしてvsftpd.confに名前付け、以下の構成項目のように構成してください。
```conf
[COS_ACCOUNT_0]
cos_secretid = XXXXXX
cos_secretkey = XXXXXX
cos_bucket = {bucket name}-123
cos_region = ap-xxx
cos_protocol = https
#cos_endpoint = ap-xxx.myqcloud.com
home_dir = /home/user0
ftp_login_user_name=user0
ftp_login_user_password=pass0
authority=RW
delete_enable=true					# trueは、このftpユーザーが削除操作（デフォルト）を行えることを表し、falseは、このユーザーが削除操作を行えないことを表します

[COS_ACCOUNT_1]
cos_secretid = XXXX
cos_secretkey = XXXXX
cos_bucket = {bucket name}-123
cos_region = ap-xxx
cos_protocol = https
#cos_endpoint = ap-xxx.myqcloud.com
home_dir = /home/user1
ftp_login_user_name=user1
ftp_login_user_password=pass1
authority=RW
delete_enable=false

[NETWORK]
masquerade_address = XXX.XXX.XXX.XXX       # FTP SERVERがあるゲートウェイまたはNATの背後にある場合、この構成項目によりゲートウェイのIPアドレスまたはドメイン名をFTPに指定できます
listen_port = 2121					   # Ftp Serverのリスニングポート。デフォルトは2121です。ファイアウォールはこのポートを開放する必要があります。

passive_port = 60000,65535             # passive_portは、passiveモードでのポートの選択範囲を設定できます。デフォルトで（60000, 65535）区間から選択します。

[FILE_OPTION]
# デフォルトで単一ファイルは最大200Gまでです。大きく設定することをおすすめしません
single_file_max_size = 21474836480

[OPTIONAL]
# 以下の設定について、特別な需要がなければ、default設定を保留することをおすすめします。設定する場合、適切に整数を入力してください
min_part_size       = default
upload_thread_num   = default
max_connection_num  = 512
max_list_file       = 10000               # lsコマンドでリストする可能な最大ファイル数。大きく設定することをおすすめしません。さもなければlsコマンドの遅延が高いです
log_level           = INFO                 # ログ出力のレベルを設定します
log_dir             = log                 # ログの格納ディレクトリを設定します。デフォルトでftp serverディレクトリ配下のlogディレクトリにあります
```

各ユーザーを異なるBucketにバインディングする場合、`[COS_ACCOUNT_X]`のsectionを追加するだけでよい。

それぞれの`COS_ACCOUNT_X`のsectionについて次のように説明します。

1. 各ACCOUNT下のユーザー名（`ftp_login_user_name`）とユーザーのホームディレクトリ（`home_dir`）はそれぞれ違う必要があります。また、ホームディレクトリは、システムの実際的に存在するディレクトリである必要があります。
2. 各COS FTP Serverでは、同時にログインするユーザー数が100を超えてはいません。
3. `endpoint`と`region`が同時に有効になることはできません。パブリッククラウドCOSサービスを使用するには、正しく`region`フィールドを入力するだけでよい。`endpoint`は一般的にプライベートな配置環境に使用されます。同時に`region`と`endpoint`を入力した場合、`endpoint`は優先して有効になります。

構成ファイルのOPTIONALオプションは、上級ユーザーがアップロード性能を調整するための選択可能項目です。マシンの性能に応じて適切にアップロードシャードの大きさと並行アップロードのスレッド数を調整すると、より高いアップロード速度を取得できます。一般的にはユーザーが調整する必要がなく、デフォルト値を保持するだけでよい。
また、最大接続数の制限オプションを提供します。最大接続数を制限したくない場合、0（最大接続数目を制限しない）を入力できます。ただし、マシンの性能に応じて適切に評価する必要があります。


## FAQ
FTP Serverツールを使用するときにエラーが発生した場合、またはアップロード制限について質問がありましたら、[FTP Serverツールについてのよくある質問](https://cloud.tencent.com/document/product/436/30742)を参照してください。

