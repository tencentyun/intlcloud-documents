## 機能についてのお問い合わせ

### 一時キーを使用してバケットをマウントするにはどうすればよいですか。

一時キー（STS）を使用してバケットをマウントするには、次の2つの手順を実行する必要があります。

手順1：一時キー設定ファイル（例：/tmp/passwd-sts）を作成し、COSFSコマンドオプション -opasswd-file=\[path\]の指定キー設定ファイルとして使用します。一時キーに関する概念については、[一時キーの生成および使用ガイド](https://intl.cloud.tencent.com/document/product/436/14048)のドキュメントを参照できます。一時キー設定ファイルの例を次に示します。
```shell
COSAccessKeyId=AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX  #以下は一時キーのId、KeyおよびTokenフィールドです
COSSecretKey=GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY
COSAccessToken=109dbb14ca0c30ef4b7e2fc9612f26788cadbfac3
COSAccessTokenExpire=2017-08-29T20:30:00  #一時tokenの有効期限はGMT時間です。形式は例と同じにする必要があります
```
このうち、COSFSはCOSAccessTokenExpireで設定した時間を基に、キーファイルから再度設定をロードする必要があるかどうかを判断します。

>!キーの漏洩防止のため、COSFSはキーファイルの権限を600に設定し、次のコマンドを実行するよう要求します。
><pre><code class="language-shell">chmod 600 /tmp/passwd-sts</code></pre>
>
手順2：COSFSコマンドを実行し、コマンドオプション-ocam_role=[role]を使用して、ロールをsts、-opasswd_file=[path]に指定し、キーファイルパスを指定します。例を次に示します。
```shell
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oallow_other -ocam_role=sts -opasswd_file=/tmp/passwd-sts
```

### COSFSの提供するマウントパラメータオプションおよびバージョン番号を確認するにはどうすればよいですか。

`cosfs --help`コマンドを使用すると、COSFSの提供するパラメータオプションを確認できます。`cosfs --version`コマンドを使用すると、COSFSのバージョン番号を確認できます。

### COSFSの生成したログを確認するにはどうすればよいですか。

CentOSでは、COSFSが生成するログは/var/log/messagesに保存されます。Ubuntuでは、COSFSログは/var/log/syslogに保存されます。使用中に問題が生じた場合は、対応する時間帯のログをこちらに送信してください。

### Bucket下のあるディレクトリをマウントするにはどうすればよいですか。

マウントコマンドを実行する際、Bucket下のあるディレクトリを指定し、コマンドを次のように入力します。
```shell
cosfs examplebucket-1250000000:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```
>! my-dirは`/`から開始する必要があります。
>
v1.0.5より前のバージョンを使用する場合、マウントコマンドは次のとおりとします。
```shell
cosfs 1250000000:examplebucket:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

### 非rootユーザーはどのようにCOSFSをマウントすればよいですか。

非rootユーザーには、個人のHomeディレクトリに.passwd-cosfs ファイルを作成し、権限を600に設定することをお勧めします。通常のコマンドでマウントするだけです。そのほかに、-opasswd_file=pathオプションでキーファイルのパスを指定し、権限を600に設定することもできます。

### COSFSはHTTPSでのマウントをサポートしていますか。

COSFSはHTTPSをサポートしています。HTTPとHTTPSの使用形式はそれぞれ次のとおりです。
```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
-ourl=https://cos.ap-guangzhou.myqcloud.com
```

libcurlの依存するNSSライブラリは3.12.3およびそれ以上のバージョンのシステムとします（`curl -V`コマンドを使用するとNSSのバージョンを確認できます）。HTTPS方式でBucketをマウントするには、次のコマンドを実行する必要があります。

```shell
echo "export NSS_STRICT_NOFORK=DISABLED" >> ~/.bashrc
source ~/.bashrc
```

### COSFSを起動すると自動的にマウントするように設定するにはどうすればよいですか。

最初にfuseパッケージをインストールする必要があります。
```shell
#CentOSシステム
#sudo yum install -y fuse

#Ubuntuシステム
#sudo apt-get install fuse
```

/etc/fstabファイルに次の内容を追加します。このうち、_netdevオプションはネットワークの準備ができてから現在のコマンドを実行できるようにするものです。

```shell
cosfs#examplebucket-1250000000 /mnt/cosfs fuse _netdev,allow_other,url=http://cos.ap-guangzhou.myqcloud.com,dbglevel=info
```

### どのようにマウントポイント下のファイルおよびディレクトリのユーザーとユーザーグループを設定しますか。

一部のケース（例えばnginxサーバー）では、マウントポイント下のファイルおよびディレクトリのユーザーとユーザーグループの設定が必要です。例えば、www ユーザー（uid=1002，gid=1002）は、次のマウントパラメータを追加してください。

```shell
-ouid=1002 -ogid=1002
```

### 複数のバケットをマウントするにはどうすればよいですか。

複数のBucketを同時にマウントしたい場合、/etc/passwd-cosfs 設定ファイルで、マウントしたいBucketごとに1行書き込むことができます。各行の内容の形式は、単一のBucketのマウント情報と同じです。例えば次のようになります。

```shell
echo examplebucket-1250000000:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
echo log-1250000000:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
```

### マウント後、マシン上で、マウントされたディレクトリへの他アカウントからのアクセスを可能にするにはどうすればよいですか。

権限を開放したい場合は、マウントの際に`-oallow_other`を指定しておく必要があります。

### COSFSマウントディレクトリでは、作成するファイル名に何か制限はありますか。

COSFSマウントディレクトリでは、`/`以外の文字を名称とするファイルを作成することができます。Unix系のシステムでは、`/`はディレクトリの区切り文字であるため、COSFSマウントディレクトリでは`/`を含むファイルを作成することはできません。また、特殊文字を含むファイルを作成する場合は、shellに使用されている特殊文字も避ける必要があります。使用するとファイル作成に失敗する場合があります。

### COSFSはファイルが存在するかどうかをどのように判断しているのですか。

COSFSの内部ロジックでは、Headリクエストによって親ディレクトリとファイルが存在するかどうかを判断しています。


### COSFSで使用済みのストレージ容量を確認するにはどうすればよいですか。
COSFSは使用済みのストレージ容量を直接確認することはサポートしていません。COSバケットのストレージ量を集計したい場合、データ量が比較的小さいケースではCOSコンソールにログインして確認し、データ量が大きいケースでは[リスト](https://intl.cloud.tencent.com/document/product/436/30622)機能を使用してください。

### どのプロセスがマウントディレクトリにアクセスしているかを確認するにはどうすればよいですか。
次のコマンドを実行すると、どのプロセスがマウントディレクトリ（/mnt/cosfsなど）にアクセスしているかを確認できます。
```
lsof /mnt/cosfs 
```


## トラブルシューティング

### COSFSの使用中に、突然"unable to access MOUNTPOINT /path/to/mountpoint: Transport endpoint is not connected"と表示され、アクセスできなくなりました。

`ps ax|grep cosfs`コマンドを使用してCOSFSプロセスが存在するかどうかを確認できます。COSFSプロセスが誤操作によってオフになっている場合、次のコマンドを実行することで再マウントすることができます。

```shell
umount -l /path/to/mnt_dir
cosfs examplebucket-1250000000:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

COSFSプロセスが誤操作でオフになったのではない場合は、マシンのfuseのバージョンが2.9.4より低くないかをチェックしてください。libfuseがバージョン2.9.4より低い場合は、COSFSプロセスが異常終了することがあります。この場合は、[COSFSツール](https://intl.cloud.tencent.com/document/product/436/6883)のドキュメントを参照し、fuseのバージョンを更新するか、または最新バージョンのCOSFSをインストールすることをお勧めします。

### COSFSによってアップロードしたファイルのContent-Typeが「application/octet-stream」に変更されましたが、どうすればよいですか。

COSFSは/etc/mime.typesおよびアップロードファイルの拡張子に基づいて比較を行い、COSにアップロードするファイルのContent-Typeを自動的に設定します。Content-Typeの問題が発生した場合は、システム上にこの設定ファイルが存在するかどうかをチェックすることをお勧めします。Ubuntuの場合は、sudo apt-get install mime-supportによって追加できます。CentOSの場合は、sudo yum install mailcapによって追加できます。また、このファイルを手動で作成し、それぞれのファイル形式に次のような1行を追加することもできます。

```shell
image/jpeg                                      jpg jpeg
image/jpm                                       jpm jpgm
image/jpx                                       jpx jpf
```

### マウント時にBucket not existと表示されました。

パラメータ-ourlをチェックし、URLにBucketの一部が混入していないか確認してください。正しい形式は次のとおりです。

```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
```

### 以前は書き込みができていたファイルが突然書き込めなくなったのはなぜですか。

COS認証製品ポリシーの調整により、V1.0.0より前のバージョンのCOSFSツールを使用するとポリシーチェックで不合格となる場合があります。最新のCOSFSツールをインストールして再マウントすることができます。

### COSFSツールの使用中にInput/Output ERRORなどのエラーが発生しました。どのようにデバッグを行えばよいですか。

次の手順に従って順にチェックし、問題を確認してください。

1. マシンがCOSのドメイン名に正常にアクセスできるかどうかをチェックしてください。
2. アカウントの設定が正しいかどうかをチェックしてください。 
3. cpコマンドを使用してコピーを行い、かつ-pまたは-aパラメータが含まれている場合は、これらのパラメータを除去してからこのコマンドを実行することをお勧めします。

上記の設定が正しいことを確認してから、マシンの`/var/log/messages`ログファイルを開き、s3fs関連のログを見つけてください。問題の原因を特定する上でログが役立ちます。解決できない場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)いただき、問題解決のためのサポートをお求めください。

### /etc/fstabを使用して、COSFSを起動後に自動的にマウントするよう設定しましたが、mount -aを実行すると、"wrong fs type, bad option，bad superblock on cosfs"というエラーが発生します。
このエラーは通常、マシンにfuseライブラリがない場合に発生します。次のコマンドを実行してfuseライブラリをインストールすることをお勧めします。
- CentOS
```shell
sudo yum install fuse
```
- Ubuntu
```shell
sudo apt-get install fuse
```

### システムログ/var/log/messagesの中に大量の404エラーコードがありますが、正常ですか。
COSFSの内部ロジックで、Headリクエストによって親ディレクトリとファイルが存在するかどうかを判断しています。404はプログラムの実行エラーを意味するものではありません。

### COS上に表示されるファイルのサイズが0なのはなぜですか。
一般的な状況下では、COSFSにデータを書き込む際、先にCOS上にサイズが0のファイルを作成しておき、データをローカルキャッシュファイルに書き込みます。
書き込みの過程で、このマウントポイントのlsコマンドの結果はファイルサイズの変化を表します。ファイルを閉じた時点で、COSFSは ローカルキャッシュファイルに書き込んだデータをCOSにアップロードします。アップロードに失敗した場合、見ることができるのはサイズが0のファイルのみとなります。この場合は、失敗したファイルの再コピーを試すことができます。

### COSFSキャッシュディレクトリ内のファイルとCOS上のファイルは同じものですか。直接使用することはできますか。
直接使用することはできません。キャッシュディレクトリ内のファイルはCOSFS内部での読み取り/書き込みアクセラレーションに用いられ、COS上のファイルの一部分しか存在しない可能性があります。

### rsyncコマンドを使用してファイルをCOSFSにコピーする際、進捗は100%と表示されているのに、サーバー上には一時ファイルしか見当たらないのはなぜですか。
rsyncコマンドはマウントディレクトリ内に一時ファイルを作成する場合があり、進捗100%という表示は、この一時ファイルがローカルに100%書き込まれたということだけを意味します。一時ファイルの書き込み完了後、COSへのアップロードおよびリネームとコピー操作が行われます。
通常、COSFSマウントディレクトリへのデータコピーにrsyncコマンドを使用すると、cpコマンドを使用する場合に比べてさらに時間がかかります。

### COSFSの書き込みによってディスク容量がいっぱいになった場合はどのように対処すればよいですか。
COSFSのアップロード・ダウンロードはどちらもディスクファイルキャッシュを使用します。大容量ファイルをアップロード・ダウンロードする場合、-oensure_diskfree=[size]パラメータを指定しなければ、キャッシュファイルのあるディスクがいっぱいになるまで書き込みを行います。-oensure_diskfreeパラメータを指定することで、キャッシュファイルのあるディスクの空き容量が[size] MB未満になった時点で、COSFSは使用するディスク容量を可能な限り少なくします（単位：MB）。-ouse_cache=[path]パラメータを指定した場合、キャッシュファイルはpathディレクトリに入り、指定しなければ/tmpディレクトリに入ります。

例：ディスク空き容量が10GB未満となった時点で、COSFSの実行時に使用するディスク容量を少なくするよう指定するには、次のコマンドを使用します。
```shell
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oensure_diskfree=10240
```

### dockerを使用してCOSFSをマウントする際、fuse: failed to open /dev/fuse: Operation not permittedというエラーが表示されました。どのように対処すればよいですか。
dockerイメージを有効化する際は、パラメータ --privilegedを追加する必要があります。

### あるディレクトリを、複数のマウントポイントの共有キャッシュディレクトリとして使用することはできますか。
複数のマウントポイントの共有キャッシュディレクトリとすることはお勧めしません。キャッシュディレクトリにはCOSFSが使用するメタ情報が含まれており、共有によってCOSFSが使用するメタ情報が乱れる可能性があります。

### COSFSを使用したマウントの際に/bin/mount:unrecognized option --no-canonicalizeというエラーが発生しました。どのように対処すればよいですか。

比較的低いバージョンのmountは`--no-canonicalize`オプションをサポートしていないため、mountツールを更新し（バージョンv2.17を推奨します。[ダウンロードに進む](https://cdn.kernel.org/pub//linux/utils/util-linux/v2.17/)）、更新後に再マウントしてください。インストールコマンドは次のとおりです。

```shell
tar -jxvf util-linux-ng-2.17.tar.bz2
cd util-linux-ng-2.17
./configure --prefix=/usr/local/util-linux-ng
make && make install
mv /bin/mount{,.off}
ln -s /usr/local/util-linux-ng/bin/mount /bin
```

### マウントに失敗した場合はどうすればよいですか。

手順1：ログファイルおよびプロンプトメッセージから、マウントコマンド、キー設定ファイルの内容が正しいかどうか、COSサービスへのアクセスが可能なネットワーク状態かどうかをチェックします。

手順2：dateコマンドを使用し、マシン時刻が正確かどうかチェックします。正確でない場合はdateコマンドで時刻を修正した後、再マウントを行います。例：`date -s '2014-12-25 12:34:56'`。

### `ls -l --time-style=long-iso`コマンドを使用すると、マウントディレクトリの時刻が1970-01-01 08:00に変わりましたが、これは正常ですか。

マウントディレクトリの時刻が1970-01-01 08:00に変わることは正常です。マウントポイントをアンマウントすると、マウントディレクトリの時刻はマウント前の時刻に戻ります。

 ### マウントするディレクトリは空でなくてもよいですか。

`-ononempty`パラメータを使用すると、空ではないディレクトリにマウントすることができますが、空ではないディレクトリへのマウントはお勧めしません。マウントポイント内および元のディレクトリ内に同一のパスのファイルが存在する場合、問題が生じる可能性があります。

### COSFSのディレクトリ内でlsコマンドを使用すると、コマンドの戻り値が返るのに非常に時間がかかるのはなぜですか。
マウントディレクトリ内に多くのファイルがある場合、lsコマンドを実行するには、ディレクトリ内の各ファイルに対しHEAD操作を行う必要があるため、ディレクトリシステムを読み込んで呼び出し、戻り値を返すまでに長時間かかる場合があります。
>! IO hungを有効にすると、不必要な再起動が起こる場合があるため、有効にしないことをお勧めします。
>


### infoレベルのログを使用して生成したシステムログファイルが大量のストレージ容量を占有している場合は、どう対処すればよいですか。
生成されたシステムログファイルを定期的にクリアするか、あるいは例えば`-odbglevel=crit`を使用してマウントするなど、ログレベルを引き上げることができます。


### COSFSはどのようなケースに適していますか。読み取りおよび書き込みパフォーマンスはどうですか。
COSFSの読み取り/書き込みはどちらもディスクを経由しており、POSIXセマンティクスによるCOSアクセスが要求されるケースに適しています。例えば、データセットを共有する機械学習アルゴリズムで共有データを読みとる、簡単なログバックアップを取る場合などです。COSFSはマルチスレッドを使用したアップロード・ダウンロードの同時実行によるアクセラレーションが可能であり、同一リージョン内のプライベートネットワークを使用して6GBのファイルのシーケンシャルリードを行う場合、所要時間は80秒前後です。6GBのファイルのシーケンシャルライトを行う場合、所要時間は160秒前後です。通常、SDKおよびマルチスレッドなどの技術を用いることで、これ以上のパフォーマンスを実現できます。

>! ファイルの読み取り/書き込みによって発生する大量のシステム呼び出しは、大量のログを伴うため、COSFSの読み取り/書き込みパフォーマンスにある程度の影響を及ぼします。パフォーマンスに求められる条件が比較的高い場合は、 -odbglevel=warnまたはそれより高いログレベルを指定することができます。
>

### COSFS RPMパッケージをインストールすると、COSFSが見つかりませんと表示されましたが、どうすればよいですか。

cosfsのインストールパスは/usr/local/binであり、cosfsが見つからないと表示された場合は、このパスがPATH環境変数の中にない可能性があります。まず先に、`~/.bashrc`に設定を1行追加する必要があります。
```shell
export PATH=/usr/local/bin:$PATH
```
さらに次のコマンドを実行します。
```shell
source ~/.bashrc
```

### COSFS RPMパッケージをインストールする際、conflicts with file from package fuse-libs-\*と表示されましたが、どうすればよいですか。

COSFS RPMパッケージをインストールする際、`--force`オプションを追加します。
```shell
rpm -ivh cosfs-1.0.19-centos7.0.x86_64.rpm --force
```

###  COSFSに、あるディレクトリの読み取り専用の権限を承認した後、対応するディレクトリを単独でマウントする際、権限がないと表示されました。

COSFSにはルートディレクトリのGetBucket権限が必要です。そのため、ルートディレクトリのGetBucket権限および対応するディレクトリをの読み取り権限を追加する必要があります。これにより他のディレクトリをリストアップすることができますが、操作権限はありません。

### COSFSが毎日ある時間帯でのCPU使用率が高く、なおかつCOSに対し大量のHead、Listリクエストを送信し、大量のリクエスト回数と料金が発生しています。どのように対処すればよいですか。

これは通常、マシン上に定時スキャンディスクタスクが存在することが原因です。Linuxシステムの一般的なスキャンディスクプログラムはupdatedbです。COSFSのマウントポイントディレクトリをupdatedbの設定ファイル/etc/updatedb.confファイルのPRUNEPATHS設定項目に追加することで、このプログラムがスキャンディスク動作を行わないようにすることができます。また、Linuxツールのauditdを使用し、COSFSのマウントポイントにアクセスしているプログラムを探すこともできます。

操作手順は次のとおりです。

ステップ1：auditdをインストールする

Ubuntu:

```
ap-get install auditd -y
```

CentOS:

```
 yum install audit audit-libs
```

ステップ2：auditdサービスを起動する

```
systemctl start auditd
systemctl enable auditd
```

ステップ3：マウントディレクトリを監視する

>?`-w`は指定するCOSFSマウントディレクトリ、`-k`はauditログに出力されるkeyです。

```
auditctl -w /usr/local/service/mnt/ -k cosfs_mnt
```

ステップ4：ログに基づいてアクセスプログラムを確定する

auditのログディレクトリ： /var/log/audit。照会コマンドは次のとおりです。

```
ausearch -i|grep 'cosfs_mnt'
```

ステップ5：auditdサービスを停止する
auditdサービスを停止したい場合は、次のコマンドを使用することができます。

```
/sbin/service auditd stop
```

>!マウントポイントにアクセスしているプログラムが常時実行中の場合は、新たに起動したauditdによってそのプログラムのアクセス動作を監視することはできません。プログラム内でマウントディレクトリに関する複数回の呼び出しがあった場合は、1回目のみ記録されます。

### dfを実行するとCOSFSのSizeとAvailableが256Tと表示されるのはなぜですか。
COSバケットのスペースは無限大です。ここでAvailableが256Tというのは、dfの結果を表示しているだけであり、実際にCOSバケットがストレージ可能なデータ量は256Tよりはるかに大きいです。

### dfを実行するとCOSFSのUsedが0と表示されるのはなぜですか。
COSFSはローカルのストレージ容量を占有しません。dfなどのツールとの互換性のため、COSFSが表示するSize、Used、Availableは、いずれも真の値ではありません。

### df -iを実行するとInode/IUsed/IFreeがすべて0と表示されるのはなぜですか。
COSFSはハードディスクをベースとしたファイルシステムではないため、inodeは存在しません。

