### コンテナ内にbash がないときはどうしたらいいですか。

bashがないときは、コマンドラインで実行したいコマンドを入力すると、スクリーンにコマンドの実行結果が表示されます。コマンドラインはオートコンプリート自動補完などの機能を持たない簡易的なbash とみなしてよいです。bashのコマンドを先にインストールして、後続操作を実行することを推奨します。 

### apt-get のインストールが遅いのはなぜですか。
`Apt-get` のインストールが遅い原因として、サーバーが海外ソフトウエアのソースにアクセスするのが遅いことが挙げられます。コンテナのOSによって、速度向上の案を提供しています。実際の状況に応じて下記の操作をしてください。

#### 注意事項
エラーを防ぐため、コンテナのOSをご確認の上、速度向上の解決方法を選択してください。確認方法は次の通りです。
 - Ubuntu： `cat /etc/lsb-release` を実行し、`/etc/lsb-release` が存在するかを確認。
 - CentOS： `cat /etc/redhat-release` を実行し、 `/etc/redhat-release` が存在するかを確認。
 - Debian： `cat /etc/debian_version` を実行し、 `/etc/debian_version` が存在するかを確認。

#### 解決方法<span id="solve"></span>

##### Ubuntu 16.04
OSがUbuntu 16.04 のコンテナは、端末で次のコマンドを実行し、apt のソースにTencent Cloud のソースサーバーを設定してください。
```shell
cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
ENDOF
```

##### CentOS 7

OSがCentOS 7 のコンテナは、端末で次の操作を実行し、ソースアドレスを直接変更することで、インストール速度を改善できます。
１．以下のコードをコンテナ内にコピーして実行します。
```shell
cat << ENDOF > /etc/yum.repos.d/CentOS-Base.repo
[os]
name=Qcloud centos os - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/os/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
[updates]
name=Qcloud centos updates - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/updates/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[centosplus]
#name=Qcloud centosplus - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/centosplus/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[cloud]
#name=Qcloud centos contrib - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/cloud/$basearch/openstack-kilo/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[cr]
#name=Qcloud centos cr - \$basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/cr/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
[extras]
name=Qcloud centos extras - \$basearch
baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/extras/\$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
#[fasttrack]
#name=Qcloud centos fasttrack - \basearch
#baseurl=http://mirrors.tencentyun.com/centos1/\$releasever/fasttrack/\$basearch/
#enabled=1
#gpgcheck=1
#gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
ENDOF
```
2. YUMキャッシュをクリアして再作成するために、下記のコマンドを実行してください。
```
yum clean all && yum clean metadata && yum clean dbcache && yum makecache
```

##### Debian 

OSがDebian のコンテナは、端末で次のコマンドを実行し、apt のソースにTencent Cloudのソースサーバーを設定してください。
```shell
cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/debian stretch main contrib non-free
deb http://mirrors.tencentyun.com/debian stretch-updates main contrib non-free
deb http://mirrors.tencentyun.com/debian-security stretch/updates main

deb-src http://mirrors.tencentyun.com/debian stretch main contrib non-free
deb-src http://mirrors.tencentyun.com/debian stretch-updates main contrib non-free
deb-src http://mirrors.tencentyun.com/debian-security stretch/updates main
ENDOF
```

#### まとめ

コンテナ内でソースアドレスを直接変更するのは臨時的な解決方法であり、コンテナがスケジューリングされた場合、その変更は無効になります。イメージ作成の時点でトラブルを解決することを推奨します。具体的な手順は次の通りです。

作成したコンテナイメージの Dockerfile を修正し、Dockerfile の RUN フィールドに [解决方法](#solve) に従って、対応するOSの情報を追加して、ソースアドレスを変更します。。たとえば、 Ubuntuベースのイメージの Dockerfileに次の内容を追加してください。
```shell
RUN cat << ENDOF > /etc/apt/sources.list
deb http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
#deb http://mirrors.tencentyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
#deb http://mirrors.tencentyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-updates main restricted universe multiverse
#deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
#deb-src http://mirrors.tencentyun.com/ubuntu/ xenial-backports main restricted universe multiverse
ENDOF
```



### コンテナにログイン後、vim、netstatなどのツールがないと気づいたらどうしたらいいですか。

apt-get install vim、 net-toolsなどのコマンドを実行し、必要なツールをインストールできます（CentOS の場合、 yum install vimを実行）。

### apt-get install を実行したが、ツールが見つからないときはどうしたらいいですか。

以下の操作を実施してインストールしてください。
1. 次のコマンドを実行して、ソフトウエアリストをアップデートします。
```
apt-get update
```
2. 次のコマンドを実行して、ソフトウエアをインストールします（CentOS の場合、 yum updateinfoを実行）。
```
apt-get install
```

### コンテナ内で自作のツールを使用するには、どうしたらいいですか。

リモートターミナルにアクセスし、右下のドキュメントアシスタントをクリックすることで、アップロードとダウンロードが可能になります。

### 分析のため、dumpやログなどのライブファイルをローカルにコピーする方法は？

リモートターミナルにアクセスし、右下のドキュメントアシスタントをクリックすることで、アップロードとダウンロードが可能になります。

### ドキュメントをコンテナにアップロード、またはローカルシステムにダウンロードできないのはなぜ？

原因として、コンテナイメージに tar プログラムがインストールされていないことが挙げられます。 apt-get install vim、net-toolsなどのコマンド（CentOS の場合 yum install vim）を実行し、tar プログラムをインストールしてから再試行してください。

### 以前インストールしたツールが消えてしまいました。

原因として、Kubernetes がコンテナを再スケジューリングする時、新しいコンテナを生成するためにイメージを取得することが挙げられます。イメージの中に以前インストールしたツールが含まれていなければ、新しいコンテナにもそれらのツールは含まれません。イメージ作成時に、よく使われるトラブルシューティングツールをインストールすることを推奨します。

### コンソール上の文字をコピーするには？

コピーしたい文字列を選択すると、選択された文字列はコピーされます。

### コピーした文字をペーストするには？

Shift + Insert でペーストできます。

### コネクションが切れたのはなぜですか。

原因として、Tencent Cloud の他のページで行ったコンテナやCloud Virtual Machine（CVM）に対する操作により、コンテナが変更されたか、長時間（３分間）操作をしなかったことにより、サーバーが接続を切断したことが挙げられます。

### top コマンド等の実行で TERM environment variable not set のエラーが発生した場合、どうしたらいいですか。

export TERM linux コマンドを実行してください。

### 絶対パスが長いディレクトリにアクセスすると、bash プロンプトが 「<」 と一部のパスのみを表示するのはなぜですか。

デフォルトの bash プロンプトが「ユーザー名@ホスト名　カレントディレクトリ」の表示に設定されているためです。現在のディレクトリパスが一定の長さを超えた場合、bash は「<」 及びパスの末尾部分のみをデフォルトで表示します。

