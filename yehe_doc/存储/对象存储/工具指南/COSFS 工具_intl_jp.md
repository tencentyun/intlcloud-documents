## 機能説明 

COSFSツールは、Cloud Object Storage(COS)バケットのローカルへのマウントをサポートし、ローカルファイルシステムを使用する場合と同じように、Tencent Cloud COS内のオブジェクトを直接操作します。COSFSが提供する主な機能は、次のとおりです。
- ファイルの読み書き、ディレクトリ操作、リンク操作、権限管理、ユーザーID/gid管理機能など、POSIXファイルシステムのほとんどの機能をサポートしています。
- 大容量ファイルチャンク転送機能。
- MD5データチェック機能。
- ローカルデータをCOSにアップロードするには、[COS Migrationツール](https://intl.cloud.tencent.com/document/product/436/15392)または[COSCMDツール](https://intl.cloud.tencent.com/document/product/436/10976)の使用をお勧めします。

## 制限事項
**COSFSはS3FSをベースとして構築されており、読み取り書き込み操作はディスクを介して転送されます。マウント後のファイルの簡単な管理にのみ適していますが、ローカルファイルシステムの一部機能の使用方法はサポートされていないため、Tencent Cloud Storage Gatewayを使用してCOSにアクセスすることをお勧めします。Tencent CSGはCOSバケットを、ネットワークファイルシステムによって複数のサーバーにマウントすることができ、ユーザーはPOSIXファイルプロトコルを使用して、マウントポイントを通じてCOS上のオブジェクトの読み取りと書き込みを行うことができます。**COSFSツールを使用する場合、次のような適しないケースがあることに注意する必要があります。

- ファイルをランダムにまたは追加で書き込むと、ファイル全体がダウンロードおよび再アップロードされます。Bucketと同じリージョンのCVMを使用すれば、ファイルのアップロード・ダウンロードを高速化できます。
- 複数のクライアントが同じCOSバケットをマウントする場合、ユーザーに依存して各クライアントの動作の調整が行われます。例えば、複数のクライアントが同じファイルに書き込むことを避けるなどです。
- ファイル/フォルダのrename操作はアトミックではありません 。
- 例えば、list directoryなどのメタデータ操作は、COSサーバーにリモートアクセスする必要があるため、パフォーマンスが低下します。
- hard linkをサポートしていないため、同時読み書きのシナリオには適していません。
- マウントポイントでファイルのマウントとアンマウントを同時に行うことはできません。cdコマンドを使用して他のディレクトリに切り替えてから、マウントポイントのマウント・アンマウント操作を行うことができます。

## 使用環境
主要なUbuntu、CentOS、SUSE、macOSシステムをサポートしています。


## インストール方法
COSFSは、インストールパッケージによるインストールと、コンパイルされたソースコードによるインストールという、主に2つのインストール方法を提供しています。


### 方法1：インストールパッケージによるインストール
>? この方法は、主要なUbuntu、CentOSシステムをサポートしています。
>

#### Ubuntuシステム

1. システムのバージョンに応じて、対応するインストールパッケージを選択します。現在サポートしているUbuntuディストリビューションには、Ubuntu14.04、Ubuntu16.04、Ubuntu18.04、Ubuntu20.04があります。
Githubダウンロードアドレス：
```plaintext
#Ubuntu14.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu14.04_amd64.deb
#Ubuntu16.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu16.04_amd64.deb
#Ubuntu18.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu18.04_amd64.deb
#Ubuntu20.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu20.04_amd64.deb
```
CDNダウンロードアドレス：
[cosfs_1.0.20-ubuntu14.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu14.04_amd64.deb)
[cosfs_1.0.20-ubuntu16.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu16.04_amd64.deb)
[cosfs_1.0.20-ubuntu18.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu18.04_amd64.deb)
[cosfs_1.0.20-ubuntu20.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu20.04_amd64.deb)

2. インストール。Ubuntu16.04を例とします。
```shell
sudo dpkg -i cosfs_1.0.20-ubuntu16.04_amd64.deb
```

#### CentOSシステム

1. 依存のインストール
```plaintext
sudo yum install libxml2-devel libcurl-devel -y
```
2. システムのバージョンに応じて、対応するインストールパッケージを選択します。現在サポートしているCentOSディストリビューションには、CentOS6.5、CentOS7.0があります。
Githubダウンロードアドレス：
```plaintext
#CentOS6.5
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs-1.0.20-centos6.5.x86_64.rpm
#CentOS7.0
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs-1.0.20-centos7.0.x86_64.rpm
```
CDNダウンロードアドレス：
[cosfs-1.0.20-centos6.5.x86_64.rpm](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs-1.0.20-centos6.5.x86_64.rpm)
[cosfs-1.0.20-centos7.0.x86_64.rpm](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs-1.0.20-centos7.0.x86_64.rpm)
3. インストールします。CentOS7.0を例とします。
```shell
sudo rpm -ivh cosfs-1.0.20-centos7.0.x86_64.rpm
```
>? インストール中にエラーが報告された場合は、`conflicts with file from package fuse-libs-*`というプロンプトが表示されますので、`--force`パラメータを追加して再インストールします。
>

### 方法2：ソースコードのコンパイルによるインストール

>? この方法は、主要なUbuntu、CentOS、SUSE、macOSシステムをサポートしています。
>


#### 1. 依存ソフトウェアのインストール 
COSFSのコンパイルとインストールは、 automake、git、libcurl-devel、libxml2-devel、fuse-devel、make、openssl-develなどのソフトウェアパッケージに依存しています。Ubuntu 、CentOS、SUSE、macOSの依存ソフトウェアのインストール手順は次のとおりです。

- Ubuntuシステムに依存ソフトウェアをインストールします。
```shell
sudo apt-get install automake autotools-dev g++ git libcurl4-gnutls-dev libfuse-dev libssl-dev libxml2-dev make pkg-config fuse
```
- CentOSシステムに依存ソフトウェアをインストールします。
```shell
sudo yum install automake gcc-c++ git libcurl-devel libxml2-devel fuse-devel make openssl-devel fuse
```
- SUSEシステムに依存ソフトウェアをインストールします。
```shell
sudo zypper install gcc-c++ automake make libcurl-devel libxml2-devel openssl-devel pkg-config
```
- macOSシステムに依存ソフトウェアをインストールします。
```shell
brew install automake git curl libxml2 make pkg-config openssl 
brew install cask osxfuse
```

#### 2. ソースコードの取得 

[COSFSソースコード](https://github.com/tencentyun/cosfs)をGitHubから指定されたディレクトリにダウンロードする必要があります。以下では、ディレクトリ`/usr/cosfs`を例として取り上げます（実際の操作では、具体的な操作環境に応じてディレクトリを選択することをお勧めします）。
```shell
sudo git clone https://github.com/tencentyun/cosfs /usr/cosfs
```


#### 3. COSFSのコンパイルとインストール 
インストール先のディレクトリに移動し、以下のコマンドを実行して、コンパイルとインストールを行います。
```shell
cd /usr/cosfs
sudo ./autogen.sh
sudo ./configure
sudo make
sudo make install
cosfs --version  #cosfsバージョン番号の確認
```

#### 4. Configure操作に関する問題点への対処

configure操作時に表示されるプロンプトはOSによって異なります。fuseバージョンが2.8.4未満のOSでは、configure操作を行うときに、以下のようなエラーメッセージが表示されます。
```shell
checking for common_lib_checking... configure: error: Package requirements (fuse >= 2.8.4 libcurl >= 7.0 libxml-2.0 >= 2.6) were not met:
  Requested 'fuse >= 2.8.4' but version of fuse is 2.8.3 
```
この場合、fuse 2.8.4以降のバージョンを手動でインストールする必要があります。インストールコマンドの例は次のとおりです。
```shell
sudo yum -y remove fuse-devel
sudo wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
sudo ./configure
sudo make
sudo make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   #fuseカーネルモジュールをマウントします
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   #ダイナミックリンクライブラリを更新します
pkg-config --modversion fuse  #fuseのバージョン番号を確認します。「2.9.4」と表示されていれば、fuse 2.9.4のインストールは成功しています 
```
SUSEシステムの場合、fuse 2.8.4以降のバージョンを手動でインストールする必要があります。インストールコマンドの例は次のとおりです。
>! インストールするときは、`example/fusexmp.c`ファイルの222行目をコメントアウトしないと、makeがエラーを報告します。コメントの方法は、`/*content*/`です。
>
```shell
zypper remove fuse libfuse2
sudo wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
sudo ./configure
sudo make 
sudo make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   #fuseカーネルモジュールをマウントします
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   #ダイナミックリンクライブラリを更新します
pkg-config --modversion fuse  #fuseのバージョン番号を確認します。「2.9.4」と表示されていれば、fuse 2.9.4のインストールは成功しています 
```
- macOSでconfigure操作を行うときは、次のようなプロンプトが表示される場合があります。
```shell
configure: error: Package requirements (fuse >= 2.7.3 libcurl >= 7.0 libxml-2.0 >2.6 libcrypto >= 0.9) were not met
No package 'libcrypto' found
```
 この場合、PKG_CONFIG_PATH変数を設定して、pkg-configツールがopensslを見つけられるようにする必要があります。コマンドは次のとおりです。
```shell
brew info openssl 
export PKG_CONFIG_PATH=/usr/local/opt/openssl/lib/pkgconfig #前のコマンドのプロンプト情報に従って、このコマンドを変更する必要がある場合があります。
```


## 利用方法

### 1. キーファイルの設定
ファイル`/etc/passwd-cosfs`に、バケット名（形式はBucketName-APPID）と、そのバケットに対応する&lt;SecretId&gtと&lt;SecretKey&gtを半角のコロンで区切って書き込みます。キーの漏洩を防ぐため、COSFSではキーファイルの権限値を640に設定する必要があります。`/ etc / passwd-cosfs`キーファイルを設定するためのコマンド形式は次のとおりです。
```shell
sudo su  #をrootに切り替えて/etc/passwd-cosfsファイルを変更します。すでにrootユーザーである場合は、このコマンドを実行する必要はありません。
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>? &lt;&gtのパラメータをお客様の情報に置き換える必要があります。
> - &lt;BucketName-APPID&gt;はバケット名の形式です。バケットの命名ルールについては、[バケット命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください。
> - &lt;SecretId&gt; と &lt;SecretKey&gt;はキー情報です。サブアカウントキーを使用し、[最小権限ガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従うことで、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については[サブアカウントのアクセスキー管理](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。
> - ファイル$HOME/.passwd-cosfsでキーを設定するか、-opasswd_file=[path]でキーファイルパスを指定し、キーファイルの権限値を600に設定する必要があります。
> 

**事例：**

```shell
echo examplebucket-1250000000:AKIDHTVVaVR6e3****:PdkhT9e2rZCfy6**** > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>! V1.0.5以前のバージョンのCOSFSの場合、設定ファイルの形式は、&lt;BucketName>:&lt;SecretId>:&lt;SecretKey>となります。
>


### 2. 実行ツール
キーファイルで設定されたバケットを指定されたディレクトリにマウントするには、次のコマンドラインを使用することができます。

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=http://cos.<Region>.myqcloud.com -odbglevel=info -oallow_other
```
そのうち：
- &lt;MountPoint&gt;は、ローカルマウントディレクトリです（例：`/mnt`）。
- &lt;Region&gt;はリージョンの略称で、例としては、ap-guangzhou、eu-frankfurtなどです。リージョンの略称情報については、[アベイラビリティリージョン](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください。
- -odbglevel ログレベルを指定します。デフォルトはcrit、オプション値はcrit、error、warn、info、debugです。
- -oallow_other マウントされていないユーザーがマウントされたフォルダにアクセスすることを許可します。

**事例：**

```shell
mkdir -p /mnt/cosfs
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -onoxattr -oallow_other
```

>!
>- COSFSツールはパフォーマンスを向上させるために、デフォルトではシステムディスクを使用してアップロード・ダウンロードの一時キャッシュを保存し、ファイルが閉じられた後にスペースを解放します。同時に開くファイル数が多い場合や大きなファイルの読み書きが行われる場合、COSFSツールはパフォーマンスを向上させるために、ハードディスクを可能な限り使用します。デフォルトでは、他のプログラムのためにハードディスクの空き容量が100MBだけ確保されています。オプションoensure_diskfree=[size]を使用すれば、COSFSツールが確保する利用可能なディスク容量をMB単位で設定することができます。例えば、`-oensure_diskfree=1024`とした場合、COSFSツールは1024MBの空き領域を確保します。
>- V1.0.5以前のバージョンのCOSFSの場合、マウントコマンドは、cosfs &lt;APPID>:&lt;BucketName> &lt;MountPoint> -ourl=&lt;CosDomainName> -oallow_otherとなります。
>


### 3. バケットのアンマウント

バケットのアンマウント例：

```shell
方法1：fusermount -u /mnt。 fusermountコマンドはFUSEファイルシステムのアンマウント専用です 
方法2：umount -l /mnt。プログラムがファイルシステム内のファイルを参照するときにエラーを報告せずにアンマウントし、プログラムが参照しない場合にアンマウントが完了します
方法3：umount /mnt。プログラムがファイルシステム内のファイルを参照する場合、アンマウント時にエラーが報告されます
```

## 一般的なマウントオプション

#### -omultipart_size=[size]
マルチパートアップロード時の1チャンクのサイズ（単位：MB）を指定するために使用し、デフォルトは10MBです。マルチパートアップロード時の1ファイルのチャンク数には上限があるため（10000チャンク）、100GB(10MB\* 10000)を超えるサイズのファイルについては、このパラメータを具体的な状況に応じて調整する必要があります。

#### -oallow_other
他のユーザーがマウントされたフォルダにアクセスできるようにする場合は、COSFSの実行時にこのパラメータを指定することができます。

#### -odel_cache
デフォルトでは、COSFSツールはパフォーマンスを最適化するために、umount後にローカルキャッシュデータをクリアしません。COSFSの終了時にキャッシュを自動的にクリアする必要がある場合は、マウント時にこのオプションを追加することができます。

####  -onoxattr
getattr/setxattr機能を無効にします。1.0.9以前のバージョンのCOSFSは、拡張属性の設定と取得に対応していません。マウント時にuse_xattrオプションを使用すると、mvファイルのBucketへの送信が失敗する場合があります。

#### -opasswd_file=[path]
このオプションでは、COSFSキーファイルが配置されているパスを指定することができます。このオプションで設定するキーファイルは、権限を600に設定する必要があります。

#### -odbglevel=[dbg|info|warn|err|crit]

COSFSのログレベルをinfo、dbg、warn、errおよびcritに設定します。本番環境ではinfoに設定することをお勧めします。デバッグ時にはdbgに設定することができます。システムログが定期的にクリーンアップされておらず、アクセス量が多いために大量のログが生成される場合は、errまたはcritに設定することができます。

#### -oumask=[perm]

このオプションは、所定のタイプのユーザーに対して、マウントされたディレクトリのファイルに対する操作権限を削除することができます。例えば、-oumask=755の場合、対応するマウントディレクトリの権限は022になります。

#### -ouid=[uid]
このオプションは、ユーザーIDが[uid]のユーザーが、マウントされたディレクトリのファイルパーミッションビットに制限されることなく、マウントされたディレクトリのすべてのファイルにアクセスできるようにします。
ユーザーIDを取得する場合、` id -u username`の形式でIDコマンドを使用することができます。例えば、`id -u user_00`を実行すると、ユーザーuser_00のユーザーIDが取得できます。

#### -oensure_diskfree=[size]

COSFSツールはパフォーマンスを向上させるために、デフォルトではシステムディスクを使用してアップロード・ダウンロードの一時キャッシュを保存し、ファイルが閉じられた後にスペースを解放します。同時に開くファイル数が多い場合や大きなファイルの読み書きが行われる場合、COSFSツールはパフォーマンスを向上させるために、ハードディスクを可能な限り使用します。デフォルトでは、他のプログラムのためにハードディスクの空き容量が100MBだけ確保されています。オプションoensure_diskfree=[size]を使用すれば、COSFSツールが確保する利用可能なディスク容量をMB単位で設定することができます。例えば、`-oensure_diskfree=1024`とした場合、COSFSツールは1024MBの空き領域を確保します。


## よくあるご質問
COSFSツールの使用に関するご質問は、[COSFSツールに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/436/30587)をご参照ください。
