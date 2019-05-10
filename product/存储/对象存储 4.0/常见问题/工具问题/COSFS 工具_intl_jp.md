## 機能のお問い合わせ
### テンポラリキーでバケットをマウントしますか？

テンポラリキー（STS）でバケットをマウントするには、以下の2つのステップを実行します。

ステップ1：テンポラリキーの構成ファイルを作成します。例えば、/tmp/passwd-sts。COSFSコマンドオプション-opasswd-file=\[path\]で暗号鍵の構成ファイルを指定します。テンポラリキーに関する概念について[テンポラリキーの生成および使用ガイドライン](https://cloud.tencent.com/document/product/436/14048)ドキュメントを参照してください。テンポラリキー構成ファイルの例を次に示します。

```shell
COSAccessKeyId=AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX #以下はテンポラリキーのID、Key、およびTokenフィールドです
COSSecretKey=GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY
COSAccessToken=109dbb14ca0c30ef4b7e2fc9612f26788cadbfac3
COSAccessTokenExpire=2017-08-29T20:30:00  #一時的なtokenの有効期間はGMTを基準とし、表示形式が例と一致します
```
そのうち、COSFSは、COSAccessTokenExpireに設定される時間に基づいて、暗号鍵ファイルから構成を再ロードする必要があるかを判断します。

>!暗号鍵の漏えいを防ぐために、COSFSでは、暗号鍵ファイルの権限を600に設定する必要があります。次のコマンドを実行します。
>```shell
>chmod 600 /tmp/passwd-sts
>```

ステップ2：COSFSコマンドを実行し、コマンドオプション-ocam_role=[role]で役割をstsに指定し、-opasswd_file=[path]で暗号鍵ファイルパスを指定します。例を次に示します：

```shell
cosfs example-1253972369 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oallow_other -ocam_role=sts -opasswd_file=/tmp/passwd-sts
```

### COSFSによって提供されるマウントパラメータオプションとバージョン番号の確認方法は？

`cosfs --help`コマンドでCOSFSによって提供されるパラメータオプションを確認できます。`cosfs --version`コマンドでCOSFSバージョン番号を確認できます。

### COSFSによって生成されるログの確認方法は？

CentOSの場合、COSFSによって生成されるログは/var/log/messagesに保存されます。Ubuntuの場合、COSFSログは/var/log/syslogに保存されます。使用する時に問題がある場合、対応時間帯の当該ログを送信してください。

### Bucket配下のディレクトリをどうマウントしますか？

マウントコマンドを実行する時、Bucket配下のディレクトリを指定できます。コマンドを次に示します：

```shell
cosfs example-1253972369:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

>!my-dirは`/`で始まる必要があります。

v1.0.5前のバージョンを使用する場合、マウントコマンドを次に示します。

```shell
cosfs 1253972369:example:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

### 非rootユーザーは、COSFSをどうマウントしますか？

非rootユーザーの場合、個人のHomeディレクトリで.passwd-cosfsファイルを作成し、権限を600に設定し、通常コマンドでマウントすればよい。また、-opasswd_file=pathオプションで暗号鍵ファイルのパスを指定し、権限を600に設定します。

### COSFSはHTTPSによるマウントをサポートしますか？

COSFSはHTTPSをサポートします。HTTPとHTTPSの使用形式を次に示します。

```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
-ourl=https://cos.ap-guangzhou.myqcloud.com
```

libcurlの依存するNSSライブラリが3.12.3以降のバージョンのシステム（`curl -V`コマンドでNSSバージョンを確認する）である場合、HTTPS方式でBucketをマウントします。次のコマンドを実行します。

```shell
echo "export NSS_STRICT_NOFORK=DISABLED" >> ~/.bashrc
source ~/.bashrc
```

### COSFS起動後の自動マウントをどう設定しますか？

/etc/fstabファイルに次の内容を追加します。ここで、_netdevオプションによって、ネットワークの準備ができた後に現在のコマンドを実行するようにします。

```shell
cosfs#example-1253972369 /mnt/cosfs fuse _netdev,allow_other,url=http://cos.ap-guangzhou.myqcloud.com,dbglevel=info
```

### 複数のバケットをどうマウントしますか？

複数のBucketを同時にマウントするには、/etc/passwd-cosfs構成ファイルにマウントするBucketごとに次のような1行のコードを記入します。各行の内容形式が単一Bucketのマウント情報と同じです。例えば：

```shell
echo example-123456789:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
echo log-123456789:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
```

### マウント後、マシンの他のアカウントのマウントされたディレクトリにアクセスする方法は？

権限を開放するには、マウントする時に`-oallow_other`を指定する必要があります。

### COSFSのマウントディレクトリで、作成するファイル名の制限がありますか？

COSFSのマウントディレクトリで、`/`記号を含まないファイル名を作成できます。Unixシステムで、`/`記号はディレクトリの区切り記号ですので、COSFSのマウントディレクトリで`/`記号を含むファイルを作成できません。また、名前が特殊記号を含むファイルを作成する時、shellによって使用される特殊記号を避けてください。ファイル作成失敗の原因となります。


## トラブルシューティング

### COSFSを使用する時、「unable to access MOUNTPOINT /path/to/mountpoint: Transport endpoint is not connected」が突然表示され、二度とアクセスできません？

`ps ax|grep cosfs`コマンドでCOSFSプロセスが存在するかどうかを確認できます。COSFSプロセスが操作ミスでハングアップした場合、次のコマンドでもう一度マウントしてください。

```shell
umount -l /path/to/mnt_dir
cosfs example-1253972369:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

COSFSプロセスのハングアップした原因が操作ミスでない場合、マシンのfuseバージョンが2.9.4以下であるかをチェックしてください。libfuseが2.9.4以下のバージョンであれる場合、COSFSプロセスが異常終了する場合があります。この時、本文の[COSFSのコンパイルとインストール](https://cloud.tencent.com/document/product/436/6883#compile)を参照しながら、fuseバージョンを更新するか、最新バージョンのCOSFSをインストールすることをおすすめします。

### COSFSによりアップロードされるファイルのContent-Typeが「application/octet-stream」になる場合、どうすればいい？

COSFSは、/etc/mime.typesとアップロードファイルのサフィックスとを比較することによって、COSにアップロードするファイルのContent-Typeを自動的に設定します。Content-Type問題が発生した場合、システムにこの構成ファイルが存在するかどうかを確認してください。Ubuntuの場合、sudo apt-get install mime-supportで追加できます。CentOSの場合、sudo yum install mailcapで追加できます。このファイルを手動で作成できます。ファイル形式ごとに1行コードを追加します。例えば：

```shell
image/jpeg                                      jpg jpeg
image/jpm                                       jpm jpgm
image/jpx                                       jpx jpf
```

### マウントする時に「Bucket not exist」が表示されますか？

パラメータ-ourlを確認し、URLにBucketが含まれないように保証してください。正しい形式を次に示します。

```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
```

### 前に書込み可能なファイルが、なぜ書込み不可能になりますか？

COS認証製品ポリシーが調整されたので、V1.0.0以下のバージョンを使用するCOSFSツールは、ポリシー検証に合格できないことになっています。最新のCOSFSツールをインストールしてもう一度マウントしてください。

### COSFSツールを使用する時、Input/Output ERRORなどが発生した場合、どうデバッグしますか？

次のステップで不具合を順にチェックして問題を確認してください。

1. マシンが正常にCOSのドメイン名にアクセスできるかどうかを確認します。
2. アカウント構成が正しいかどうかを確認します。 

以上の構成が正しい場合、マシンの`/var/log/messages`ログファイルを開き、s3fsの関連ログを捜してください。ログによって、不具合の原因を特定できます。解決できない場合、[チケット提出](https://console.cloud.tencent.com/workorder/category)でTencent Cloudの技術サポートにお問い合わせください。

### /etc/fstabでCOSFS起動後の自動マウントを設定しますが、mount -aを実行すると、「wrong fs type, bad option，bad superblock on cosfs」というエラーメッセージが表示されます。
このエラーは、通常、マシンにfuseライブラリーがないから発生します。次のコマンドを実行し、fuseライブラリーをインストールしてください。
- CentOS
```shell
sudo yum install fuse
```
- Ubuntu
```shell
sudo apt-get install fuse
```

