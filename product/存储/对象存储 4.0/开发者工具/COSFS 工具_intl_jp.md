## 機能説明 
COSFSツールは、COSバケットをローカルにマウントし、ローカルのファイルシステムのように直接的にCOSのオブジェクトを使用できます。COSFSは以下の主な機能を提供します。
- POSIXファイルシステムのほとんどの機能（例えば、ファイル読み書き、ディレクトリ操作、リンク操作、権限管理、uid/gid管理などを含む）をサポートします。
- 大容量ファイルの分割伝送機能。
- MD5データの検証機能。
- ローカルデータをCOSにアップロードするには、[COS Migrationツール](https://cloud.tencent.com/document/product/436/15392)または[COSCMDツール](https://cloud.tencent.com/document/product/436/10976)の使用をおすすめします。

## 制限性
**COSFSは、マウント後にファイルを簡単管理することに適します。ローカルファイルシステムの一部の機能をサポートせず、パフォーマンスについてもCBSまたはCFSに取って代わることはできません。**以下の非適用シナリオに注意を払ってください。

- ファイルのランダム書込みまたは追加書込みは、ファイル全体の書込みになります。Bucketと同じ領域にあるCVMを使ってファイルのアップロード・ダウンロードを加速できます。
- 複数のクライアントが同一のCOSバケットをマウントするとき、ユーザーが自ら各クライアントを協調する行為に依存します。例えば、複数のクライアントが同一ファイルを書き込むことを避けるなど。
- ファイル/フォルダのrename操作はアトミック操作ではありません。
- メタデータ操作（例えばlist directory）のパフォーマンスが低い。リモートでCOSサーバにアクセスする必要がありますから。
- hard linkをサポートしません。高い同時並行読み/書きのシナリオに適していません。
- 同時に1つのマウントポイントにファイルをマウント、マウント解除してはいけません。cdコマンドを用いてその他のディレクトリに切り替えて、マウントポイントのマウント、マウント解除操作を行います。

## インストールと使用 
### 適用するOSバージョン 
主流のUbuntu、CentOS、macOSシステム。

### インストール手順

#### 1. ソースコードを取得します 
GitHubから[COSFSソースコード](https://github.com/tencentyun/cosfs)を指定ディレクトリにダウンロードします。以下、ディレクトリ`/usr/cosfs`を例として示します。
```shell
git clone https://github.com/tencentyun/cosfs /usr/cosfs
```

#### 2. 依存ソフトウェアのインストール 
COSFSのコンパイルインストールは、automake、git、libcurl-devel、libxml2-devel、fuse-devel、make、openssl-develなどのソフトウェアパッケージに依存します。Ubuntu、CentOSとmacOSの依存ソフトウェアのインストールは以下のとおりです。

- Ubuntuシステムで依存ソフトウェアをインストールします。

```shell
sudo apt-get install automake autotools-dev g++ git libcurl4-gnutls-dev libfuse-dev libssl-dev libxml2-dev make pkg-config fuse
```

- CentOSシステムで依存ソフトウェアをインストールします。

```shell
sudo yum install automake gcc-c++ git libcurl-devel libxml2-devel fuse-devel make openssl-devel fuse
```

- macOSシステムで依存ソフトウェアをインストールします。

```shell
brew install automake git curl libxml2 make pkg-config openssl 
brew cask install osxfuse
```
<a id="compile"> </a>
#### 3. COSFSのコンパイルとインストール 
インストールディレクトリに入り、以下のコマンドを実行してコンパイルとインストールを行います。
```sh
cd /usr/cosfs
./autogen.sh
./configure
make
sudo make install
cosfs --version  #cosfsバージョン番号を確認する
```

OSによって、configure操作を行うときに以下のメッセージが表示されます。
- CentOS 6.5以前のバージョンのOSでconfigure操作を行うとき、fuseバージョンが低いために下記のメッセージが表示される場合があります。
```shell
checking for common_lib_checking... configure: error: Package requirements (fuse >= 2.8.4 libcurl >= 7.0 libxml-2.0 >= 2.6) were not met:
  Requested 'fuse >= 2.8.4' but version of fuse is 2.8.3 
```
この場合、fuse 2.8.4以降のバージョンを手動インストールする必要があります。インストールコマンドは以下のとおりです。
```sh
yum -y remove fuse-devel
wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
./configure
make
make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse #fuseカーネルモジュールをマウントする
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig #ダイナミックリンクライブラリアップデート
pkg-config --modversion fuse #fuseバージョン番号を確認し、「2.9.4」が表示されるとき、fuse2.9.4のインストールが成功したことを示します 
```

- macOSでconfigure操作を行うとき、以下のメッセージが表示される場合があります。
```shell
configure: error: Package requirements (fuse >= 2.7.3 libcurl >= 7.0 libxml-2.0 >2.6 libcrypto >= 0.9) were not met
No package 'libcrypto' found
```
この場合、PKG_CONFIG_PATH変数を設定し、それによりpkg-configツールがopensslを見つけることができます。コマンドは以下のとおりです。
```shell
brew info openssl 
export PKG_CONFIG_PATH=/usr/local/opt/openssl/lib/pkgconfig#前コマンドの表示情報に基づき、このコマンドを変更することがあります
```

### COSFS使用方法

#### 1. 暗号鍵ファイルの構成
ファイル/etc/passwd-cosfsに、バケット名&lt;Name&gt;-&lt;Appid&gt;、およびこのバケットに対応する&lt;SecretId&gt;と&lt;SecretKey&gt;を記入します。3つの間に半角コロンで区切ります。暗号鍵の漏えいを防ぐため、COSFSでは、暗号鍵ファイルの権限を640に設定する必要があります。/etc/passwd-cosfs暗号鍵ファイルを構成するためのコマンドフォーマットは以下のとおりです。
```shell
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```
>!&lt;Name&gt;、&lt;Appid&gt;、&lt;SecretId&gt;と&lt;SecretKey&gt;をあなたの情報に変更する必要があります。
>Bucketの命名規則については、[バケット命名規則](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83)を参照してください。&lt;SecretId&gt;と&lt;SecretKey&gtについては、CAMコンソールの[クラウドAPI暗号鍵管理](https://console.cloud.tencent.com/cam/capi)から取得してください。また、暗号鍵をファイル$HOME/.passwd-cosfsに格納するか、-opasswd_file=[path]を使って暗号鍵ファイルパスを指定します。この場合、暗号鍵ファイル権限を600に設定する必要があります。

**例：**

```shell
echo examplebucket-1250000000:AKIDHTVVaVR6e3:PdkhT9e2rZCfy6 > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

#### 2. ツールを実行する
暗号鍵ファイルに構成された情報のバケットを指定したディレクトリにマウントします。以下のコマンドラインを使用できます。

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=<CosDomainName> -odbglevel=info
```
そのうち：
- &lt;MountPoint&gt;はローカルのマウントディレクトリ（例えば/mnt）です。
- &lt;CosDomainName&gt;は、バケットに対応するアクセスドメイン名です。形式：`http://cos.<Region>.myqcloud.com`（XML APIに適します。このパラメータにバケット名を渡しては行けません）。そのうち、&lt;Region&gt;は地域略語、例えば、ap-guangzhou、eu-frankfurtなど。その他の地域情報については、[可能な地域](https://cloud.tencent.com/document/product/436/6224)を参照してください。
- -odbglevelは、ログレベルを指定します。

**例：**

```shell
mkdir -p /mnt/cosfs
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -onoxattr
```

>!v1.0.5以前のバージョンのCOSFSのマウントコマンドは以下のとおりです。
```shell
cosfs <APPID>:<BucketName> <MountPoint> -ourl=<CosDomainName>
```
v1.0.5以前のバージョンのCOSFSの構成ファイルフォーマット：
```shell
<BucketName>:<SecretId>:<SecretKey>
```

#### 3. バケットのマウント解除

バケットのマウント解除例：

```shell
fusermount -u /mntまたは umount -l /mnt
```

## よく使われるマウントオプビョン

### -omultipart_size=[size]
マルチパートアップロードときの単一パートの大きさ（単位： MB）を指定します。デフォルトは10MB。マルチパートアップロードは単一ファイルパート数の最大値（10000パート）を制限するため、100GB（10MB\*10000）以上のファイルについて、場合によってこのパラメータを調整する必要があります。

### -oallow_other
その他のユーザーがマウントフォルダにアクセスすることを可能にしたい場合、COSFSを実行するときにこのパラメータを指定します。

### -odel_cache
デフォルトの場合、COSFSは、パフォーマンスを最適化するため、umount後にローカルのキャッシュデータをクリアすることはしません。COSFSが終了するとき、自動的にキャッシュをクリアする必要があれば、マウントするときにこのオプションを追加します。

###  -onoxattr
getattr/setxattr機能を無効にします。1.0.9以前のバージョンのCOSFSは拡張属性の設定と取得をサポートしません。マウントするときにuse_xattrオプションを使うと、Bucketにファイルをmvすることに失敗する場合があります。
 
### -ouse_cache=[path]
キャッシュディレクトリでファイルを一時的保存します。pathはローカルのキャッシュディレクトリパスです。このオプションは、ファイルを一時的に保存した後、ファイルの読み書き（非第1回の読み書き）を加速できます。ローカルキャッシュが必要なく、またはローカルディスク容量が限られた場合、このオプションを指定しなくてもかまいません。

### -opasswd_file=[path]
このオプションは、COSFS暗号鍵ファイルの所在パスを指定します。このオプションに設定される暗号鍵ファイルの権限を600に設定する必要があります。

### -odbglevel=[info|dbg]

COSFSログ記録レベルを設定します。info、dbgを選択できます。生産環境の場合、infoに設定し、デバッグの場合、dbgに設定することをおすすめします。

### -oumask=[perm]

このオプションは所定タイプのユーザーのマウントディレクトリ内のファイルに対する操作権限を削除できます。例えば、-oumask=007の場合、ファイル読み書きに対するその他のユーザーの実行権限を削除できます。

### -ouid=[uid]
このオプションは、ユーザーＩＤが[uid]のユーザーがマウントディレクトリのファイル権限の制限を受けず、マウントディレクトリ中のすべてのファイルにアクセスすることを可能にします。
ユーザーuidを取得するには、idコマンドを使用できます。フォーマット：`id -u username`。例えば、`id -u user_00`を実行すると、ユーザーuser_00のuidを取得できます。

## FAQ
COSFSツールを使用するときに何らかの質問がありましたら、[COSFSツールについてのよくある質問](https://cloud.tencent.com/document/product/436/30743)を参照してください。

