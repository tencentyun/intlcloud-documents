## 機能の説明

COS FTP Serverは、FTPプロトコルによるCloud Object Storage（COS）内のオブジェクトやディレクトリの直接操作をサポートしています。これにはファイルのアップロード、ダウンロード、削除、フォルダ作成などが含まれます。FTP ServerツールはPythonで実装されており、インストールがより簡単です。

## 機能説明

**アップロードメカニズム**：ストリーミングアップロードはローカルディスクに記録されることなく、標準的なFTPプロトコルに従って作業ディレクトリを設定するだけで、実際のディスクストレージ容量を占有することはありません。
**ダウンロードメカニズム**：ダイレクトストリーミングでクライアントへ戻ります。
**ディレクトリメカニズム**：bucketはFTP Server全体のルートディレクトリであり、bucketの下に複数のサブディレクトリを作成することができます。
**複数bucketのバインド**：複数のbucketの同時バインドをサポートします。
>? 複数bucketのバインド：異なるFTP Serverの作業パス(home_dir)を介して実装されるため、異なるbucketとユーザー情報を指定する場合は、home_dirが異なることを確認する必要があります。
>
**削除操作の制限**：新しいFTP Serverでは、各ftpユーザーに対しdelete_enableオプションを設定して、そのFTPユーザーがファイルの削除を許可されているかどうかを識別できるようになっています。
**サポートされているFTPコマンド：**put、mput、get、rename、delete、mkdir、ls、cd、bye、quite、size。
**サポートされていないFTPコマンド：**append、mget（ネイティブのmgetコマンドはサポートされていませんが、FileZillaクライアントなど一部のWindowsクライアントでは、引き続き一括ダウンロードが可能です）

>? FTP Serverツールは現在、中断からの再開機能をサポートしていません。
>

## 使用の開始

#### システム環境

- オペレーティングシステム：Linux。Tencent CentOSシリーズ[CVM](https://www.tencentcloud.com/document/product/213)を推奨します。現時点ではWindowsシステムはサポートしていません。
- psutilが依存するLinuxシステムパッケージ：python-devel（またはpython-dev。Linuxディストリビューションによって名前が異なります）。`yum install python-devel`や`aptitude install python-dev`などのLinuxのパッケージ管理ツールによって追加されます。
- Pythonインタープリターバージョン：Python 2.7、インストールと設定は、[Pythonのインストールと設定](https://intl.cloud.tencent.com/document/product/436/10866)を参照して行ってください。
>? FTP Serverツールは、Python 3をサポートしていません。
>
- 依存パッケージ：
 - [cos-python-sdk-v5](https://pypi.org/project/cos-python-sdk-v5/) （≥1.6.5）
 - [pyftpdlib](https://pypi.org/project/pyftpdlib/) （≥1.5.2）
 - [psutil](https://pypi.org/project/psutil/)(>=5.6.1)


#### 使用制限

COS XMLバージョンに適用します。

#### インストールと実行

FTP Serverツールのダウンロードアドレスは、[cos-ftp-server](https://github.com/tencentyun/cos-ftp-server-V5)です。インストール手順は次のとおりです。

1. FTP Serverのディレクトリに移動してsetup.pyを実行し、FTP Serverとそれに関連する依存ライブラリをインストールします（インターネットへのアクセスが必要です）。
```bash
python setup.py install   # ここでは、お客様のアカウントのsudoまたはroot権限が必要な場合があります。
```
2. サンプル設定ファイル`conf/vsftpd.conf.example`をコピーし、`conf/vsftpd.conf`というファイル名にします。本ドキュメントの[設定ファイル](#conf)の項を参照し、bucketやユーザー情報を適切に設定します。
3. ftp_server.pyを実行して、FTP Serverを起動します。
```bash
python ftp_server.py
```
また、FTP Serverの起動方法には、次の2通りがあります。
 - nohupコマンドを使用して、バックグラウンドプロセスとして起動します。
```bash
nohup python ftp_server.py >> /dev/null 2>&1 &
```
 - screenコマンドを使用して、バックグラウンドで実行します（screenツールをインストールする必要があります)。
```bash
screen -dmS ftp
screen -r ftp
python ftp_server.py
#ショートカットキーCtrl+A+Dを使用して、メインscreenに戻ります。
```

#### 実行の停止

- FTP Serverを直接起動する場合、またはFTP Serverをバックグラウンドでscreenモードで実行する場合は、ショートカットキー`Ctrl+C`を使用すると、FTP Serverの実行を停止することができます。 
- nohupコマンドで起動した場合は、以下のように停止させることができます。
```bash
ps -ef | grep python | grep ftp_server.py | grep -v grep | awk '{print $2}' | xargs -I{} kill {}
```


<a id="conf"></a>
## 設定ファイル

FTP Serverツールのサンプル設定ファイルは、`conf/vsftpd.conf.example`ですので、これをコピーしてvsftpd.confという名前を付け、次の設定項目に従って設定してください。
```conf
[COS_ACCOUNT_0]
cos_secretid = COS_SECRETID    # お客様のSECRETIDに置き換えてください
cos_secretkey = COS_SECRETKEY  # お客様のSECRETKEYに置き換えてください
cos_bucket = examplebucket-1250000000
cos_region = region   # お客様のバケットリージョンに置き換えてください
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user0      # FTPをマウントしたいローカルパスに置き換えてください（マシン上に実際に存在するパスに設定する必要があります。ソフトリンクはサポートしていません）
ftp_login_user_name=user0   # ユーザー定義のアカウントに置き換えてください
ftp_login_user_password=pass0   # ユーザー定義のパスワードに置き換えてください
authority=RW                # このユーザーの読み書き権限を設定します。Rは読み込み、Wは書き込み、RWは読み書き両方の権限を意味します
delete_enable=true		 # このftpユーザーの削除を許可する場合はtrue（デフォルト）、禁止する場合はfalseとします

[COS_ACCOUNT_1]
cos_secretid = COS_SECRETID    # お客様のSECRETIDに置き換えてください
cos_secretkey = COS_SECRETKEY  # お客様のSECRETKEYに置き換えてください
cos_bucket = examplebucket-1250000000
cos_region = region   # お客様のバケットリージョンに置き換えてください
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user1      # FTPをマウントしたいローカルパスに置き換えてください（マシン上に実際に存在するパスに設定する必要があります。ソフトリンクはサポートしていません）
ftp_login_user_name=user1  # ユーザー定義のアカウントに置き換えてください
ftp_login_user_password=pass1   #ユーザー定義のパスワードに置き換えてください
authority=RW               # このユーザーの読み書き権限を設定します。Rは読み込み、Wは書き込み、RWは読み書き両方の権限を意味します
delete_enable=false		 # このftpユーザーの削除を許可する場合はtrue（デフォルト）、禁止する場合はfalseとします

[NETWORK]
# FTP ServerがゲートウェイまたはNATの背後にある場合は、この設定項目を使用してゲートウェイのIPアドレスまたはドメイン名をFTPに割り当てることができます
masquerade_address = XXX.XXX.XXX.XXX
# FTP Serverのリスニングポート、デフォルトは2121です。ファイアウォールがこのポートを開放する必要があるので、ご注意ください（例えば、FTP ServerツールをTencent Cloud CVMにデプロイする場合は、CVMセキュリティグループでこのポートを開放する必要があります）
listen_port = 2121			
# passive_portは、passiveモードでポートの選択範囲を設定できます。デフォルトでは、[60000, 65535]の範囲で選択されます。ファイアウォール（CVMセキュリティグループなど）は、この範囲のポートを開放する必要があるので、ご注意ください
passive_port = 60000,65535      


[FILE_OPTION]
# デフォルトの単一ファイルサイズは最大200Gをサポートしますが、大きすぎるサイズを設定することはお勧めしません
single_file_max_size = 21474836480

[OPTIONAL]
# 以下の設定は、特に必要がなければdefaultのままにしておくことをお勧めします。設定する必要がある場合は、適切な整数を入力してください
min_part_size       = default
upload_thread_num   = default
max_connection_num  = 512
max_list_file       = 10000                # lsコマンドでリストアップできるファイルの最大数で、大きすぎない値に設定することをお勧めします。大きすぎる場合、lsコマンドの遅延が長くなります
log_level           = INFO                 # ログ出力レベルを設定します
log_dir             = log                  # ログをストレージするディレクトリを設定します。デフォルトは、FTP Serverディレクトリの下のログディレクトリです
```


>?
>- 各ユーザーを異なるbucketにバインドする場合は、[COS_ACCOUNT_X]のsectionを追加するだけで可能です。
それぞれのCOS_ACCOUNT_Xのsectionには、次のような説明があります
 - 各ACCOUNTのユーザー名(ftp_login_user_name)とユーザーのホームディレクトリ(home_dir)は、それぞれ異なっていなければなりません。また、ホームディレクトリは、システム上の実際のディレクトリである必要があります。
 - 各COS FTP Serverに同時にログインできるユーザー数は100以下とします。
 - endpointとregionは同時に有効になりません。パブリッククラウドCOSサービスを使用するには、regionフィールドを正しく入力するだけで可能です。endpointは一般的に、プライベートなデプロイ環境で使用されます。regionとendpointの両方が入力された場合、endpointが優先して有効になります。
>- 設定ファイルのOPTIONALオプションは、上級ユーザーがアップロード性能を調整するためのオプションです。マシンの性能に応じてアップロードスライスのサイズと同時アップロードするスレッド数を適度に調整することによって、アップロード速度を高めることができます。通常、ユーザーはこれを調整する必要はなく、デフォルト値のままで問題ありません。
また、最大接続数を制限するオプションも提供しています。最大接続数を制限したくない場合は、ここに0を入力します。0は、最大接続数が制限されていないことを意味します（ただし、マシンの性能に応じて合理的に評価する必要があります）。
>- 通常は、設定ファイルのmasquerade_address設定項目において、クライアントがCOS FTP Serverに接続するために使用するIPアドレスを指定することをお勧めします。この点に関してご質問がある場合は、[FTP Serverツール](https://intl.cloud.tencent.com/document/product/436/30588)のよくあるご質問のドキュメントをご参照ください。
 - FTP Serverに複数のIPアドレスがある場合、ifconfigコマンドを実行すると、パブリックネットワークにマッピングされたネットワークカードIPは10.xxx.xxx.xxxとなり、マッピングしたパブリックネットワークIPは119.xxx.xxx.xxxとみなされます。この際、FTP Serverが明示的にmasquerade_addressをパブリックネットワークIP(119.xxx.xxx.xxx)として設定しない場合、FTP ServerはPassiveモードでプライベートネットワークアドレス(10.xxx.xxx.xxx)を使用してクライアントにパケットを返すことがあります。この場合、クライアントはFTP Serverに接続できますが、クライアントにパケットを正しく返すことができません。したがって通常は、クライアントがServerに接続する際に使用するIPアドレスをmasquerade_addressに設定することをお勧めします。
>- 設定ファイルのlisten_port設定項目は、COS FTP Serverのリスニングポートであり、デフォルトは2121です。passive_port設定項目は、COS FTP Serverのデータチャネルリスニングポート範囲であり、デフォルトでは[60000, 65535]の範囲で選択されています。クライアントがCOS FTP Serverに接続するときは、ファイアウォールがlisten_portとpassive_portに設定されたポートを開放していることを確認する必要があります。

## クイックプラクティス

### Linuxftpコマンドを使用したCOS FTP Serverへのアクセス

1. Linux ftpクライアントをインストールします。
```sh
yum install -y ftp
```
2. Linuxコマンドラインでコマンド`ftp [ipアドレス] [ポート番号]`を使用して、COS FTP Serverに接続します。例えば、次のコマンドです。
```sh
ftp 192.xxx.xx.103 2121
```
 - ftpコマンドでは、IP設定はサンプル設定ファイル`conf/vsftpd.conf.example`の **masquerade_address**設定項目に対応しています。この例では、IPは192.xxx.xx.103に設定されています。
 - ftpコマンドでは、ポート設定はサンプル設定ファイル`conf/vsftpd.conf.example`の**listen_port**設定項目に対応しています。この例では、2121に設定されています。
3. 上記のコマンドを実行すると、**Name**と**Password**という入力すべき項目が表示されますので、COS FTP Serverの設定項目ftp_login_user_nameとftp_login_user_passwordに設定した内容を入力すると、接続が完了します。
 - **Name**：サンプル設定ファイル`conf/vsftpd.conf.example`の **ftp_login_user_name**設定項目に対応しています（設定が必要です）。
 - **Password**：サンプル設定ファイル`conf/vsftpd.conf.example`の **ftp_login_user_password**設定項目に対応しています（設定が必要です）。

### FileZillaコマンドを使用したCOS FTP Serverへのアクセス

1. [FileZillaクライアント](https://filezilla-project.org/)をダウンロードしてインストールします。
2. FileZillaクライアントでCOS FTP Serverのアクセス情報を設定した後、**クイック接続**をクリックします。
 - ホスト(H)：サンプル設定ファイル`conf/vsftpd.conf.example`の **masquerade_address**設定項目に対応しています。この例では、IPは192.xxx.xx.103に設定されています。
>! COS FTP ServerがゲートウェイまたはNATの背後にある場合は、この設定項目を使用してゲートウェイのIPアドレスまたはドメイン名をCOS FTP Serverに割り当てることができます。
 - **ユーザー名(U)：**サンプル設定ファイル`conf/vsftpd.conf.example`の **ftp_login_user_name**設定項目に対応しています（設定が必要です）。
 - **パスワード(W)：**サンプル設定ファイル`conf/vsftpd.conf.example`の **ftp_login_user_password**設定項目に対応しています（設定が必要です）。
 - **ポート(P)：**サンプル設定ファイル`conf/vsftpd.conf.example`の**listen_port**設定項目に対応しています。この例では、2121に設定されています。



## よくあるご質問

FTP Serverツールの使用時にエラーが発生した場合やアップロードの制限についてご質問がある場合は、[FTP Serverツール](https://intl.cloud.tencent.com/document/product/436/30588)のよくあるご質問をご参照ください。
