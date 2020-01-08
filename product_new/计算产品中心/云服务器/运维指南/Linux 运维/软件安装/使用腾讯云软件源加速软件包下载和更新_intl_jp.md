## ユースケース

ソフトウェアの依存関係をインストールするとき、公式ソースへのアクセスが遅い問題を解決するために、Tencent Cloudは一部のソフトウェアにキャッシュ機能を設定しました。Tencent Cloudのリポジトリを使用して、依存パッケージのインストール速度を改善することができます。ユーザーがサービスアーキテクチャを自由に構築できるように、Tencent Cloudのリポジトリはパブリックネットワークアクセスとプライベートネットワークアクセスをサポートしています。
- パブリックネットワークアクセスのURL：`http://mirrors.cloud.tencent.com/`です
- プライベートネットワークアクセスのURL：`http://mirrors.tencentyun.com/`です

> 
> - 本ドキュメントは、Tencent Cloudのリポジトリのパブリックネットワークアクセスアドレスを例として、どのようにCVMでリポジトリを利用するのかをご紹介します。プライベートネットワーク方式でTencent Cloudのリポジトリにアクセスしたい場合、パブリックネットワークのURLを**プライベートネットワークのURLに変更してください**。
> - 本ドキュメントに関わったTencent CloudのリポジトリURLは、ご参考のみであり、**Tencent Cloudのリポジトリ**から最新のURLを取得してください。
>

## 注意事項

Tencent Cloudのリポジトリは、毎日公式リポジトリから各ソフトウェアを一回同期させます。

## 前提条件

CVMにログインしました。

## 操作手順

### Tencent Cloudのイメージソースを利用してpipを加速する
> 利用する前に、お客様のCVMにPythonがインストールされたことを確認してください。
>
#### 一時的にリポジトリのパスを利用する
下記のコマンドを実行して、Tencent CloudのPyPIリポジトリを利用してpipをインストールします。
```
pip install -i  PyPIリポジトリのディレクトリ
```
下記の例のように、利用するPyPIリポジトリは`http://mirrors.cloud.tencent.com/pypi/simple/17monip` ディレクトリ配下にあります。下記のコマンドを実行してください：
```
pip install -i http://mirrors.cloud.tencent.com/pypi/simple/17monip
```

#### デフォルトリポジトリのパスを設定する
下記のコマンドを実行して、 `~/.pip/pip.conf` ファイルの ` index-url`パラメータをTencent Cloud上のリポジトリのパスに変更します。

```
[global]
index-url = PyPIリポジトリのディレクトリ
trusted-host = パブリック/プライベートネットワークのURL
```
下記の例のように、利用するPyPIリポジトリは`http://mirrors.cloud.tencent.com/pypi/simple/17monip` ディレクトリ配下にあります。下記のコマンドを実行してください：
```
[global]
index-url = http://mirrors.cloud.tencent.com/pypi/simple/17monip
trusted-host = mirrors.cloud.tencent.com
```

### Tencent Cloudのイメージソースを利用してMavenを加速する
> 利用する前に、お客様のCVMにJDK、及びMavenがインストールされたことを確認してください。
>
1. Mavenの設定ファイル `settings.xml` を開きます。
2. `<mirrors>...</mirrors>` のコードブロックを見つけて、以下の内容を`<mirrors>...</mirrors>`コードブロックに設定します。
```
    <mirror>
        <id>nexus-tencentyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus tencentyun</name>
        <url>http://mirrors.cloud.tencent.com/nexus/repository/maven-public/</url>
    </mirror> 
```

### Tencent Cloudのイメージソースを利用してNPMを加速する
> 利用する前に、お客様のCVMにNode.js、及びNPMがインストールされたことを確認してください。
>
下記のコマンドを実行して、Tencent CloudのNPMリポジトリでNPMをインストールします。
```
npm config set registry http://mirrors.cloud.tencent.com/npm/
```

### Tencent Cloudのイメージソースを利用してDockerを加速する

#### TKEクラスターにTencent Cloud上のDockerリポジトリを利用する

手動で設定する必要はありません。Tencent Kubernetes Engine(TKE)クラスターに、CVMのホストはノードを作成するとき、自動的にDockerサービスをインストールし、またTencent Cloudプライベートネットワークイメージを作成します。

#### CVMでTencent CloudのDockerリポジトリを利用する

> 利用する前に、お客様のCVMにDockerがインストールされたことを確認してください。
> Docker 1.3.2以上のバージョンのみ、Docker Hub Mirror機能をサポートします。1.3.2以上のバージョンをインストールしていない、またはバージョンが古い時、インストールまたはアップデートしてから利用してください。
> 
CVMのOS種類により、最適な操作手順を選んでください。
- Ubuntu 14.04、Debian、CentOS 6 、Fedora、またはopenSUSEなどのOSに適用します。他のバージョンのOSの操作手順はわずかに異なります。
 1. 下記のコマンドを実行して、 設定ファイル`/etc/default/docker` を開きます。
```
vim /etc/default/docker
```
 2. **i**キーを押すと編集モードに切り替えます。下記の内容を追加して、保存してください。 
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- Centos 7 OSに適用する：
 1. 下記のコマンドを実行して、 設定ファイル`/etc/sysconfig/docker` を開きます。
```
vim /etc/sysconfig/docker
```
 2. **i**キーを押すと編集モードに切り替えます。下記の内容を追加して、保存してください。
```
OPTIONS='--registry-mirror=https://mirror.ccs.tencentyun.com'
```
- 既に Boot2DockerをインストールしたWindows OSに適用する：
 1. Boot2Docker Start Shellに入り、下記のコマンドを実行してください。
```
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile  exit 
```
 2. Boot2Dockerをリスタートします。

### Tencent Cloudのイメージを利用してMariaDBを加速する
> 以下の操作手順は、CentOS 7を例として説明します。OSにより少し異なる操作手順があります。
>
1. 下記のコマンドを実行して、 `/etc/yum.repos.d/` の下に `MariaDB.repo` ファイルを作成します。
```
vi /etc/yum.repos.d/MariaDB.repo
```
2. **i**キーを押すと編集モードに切り替えます。下記の内容を書き込み、保存してください。
```
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.cloud.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. 下記のコマンドを実行して、yumのキャッシュをクレンジングします。
```
yum clean all
```
4. 下記のコマンドを実行して、MariaDBをインストールします。
```
yum install MariaDB-client MariaDB-server
```

### Tencent Cloudのイメージを利用してMongoDBを加速する
> 以下の操作手順は、MongoDB 4.0バージョンのインストールを例として説明します。その他のバージョンをインストールする際に、mirrorパス内のバージョン番号を変更してください。
>
#### CentOS及びRedhatシステムのCVMは、Tencent CloudのMongoDBリポジトリを利用する。

1. 下記のコマンドを実行して、`/etc/yum.repos.d/mongodb.repo` ファイルを作成します。
```
vi /etc/yum.repos.d/mongodb.repo
```
2. **i**キーを押すと編集モードに切り替えます。下記の内容を書き込み、保存してください。
```
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=http://mirrors.cloud.tencent.com/mongodb/yum/el7-4.0
gpgcheck=0
enabled=1
```
2. 下記のコマンドを実行して、MongoDBをインストールします。
```
yum install -y mongodb-org
```

#### DebianシステムのCVMは、Tencent CloudのMongoDBリポジトリを利用する

1. Debianのバージョンにより、下記の該当のコマンドを実行して、MongoDB GPGのパブリックキーをインポートします。
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 下記のコマンドを実行して、mirrorのパスを設定します。
```
#Debian 8
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Debian 9
echo "deb http://mirrors.cloud.tencent.com/mongodb/apt/debian stretch/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 下記のコマンドを実行して、パッケージリストを更新します。
```
sudo apt-get update
```
4. 下記のコマンドを実行して、MongoDBをインストールします。
```
sudo apt-get install -y mongodb-org
```

#### UbuntuシステムのCVMは、Tencent CloudのMongoDBリポジトリを利用する

1. 下記のコマンドを実行して、MongoDB GPGのパブリックキーをインポートします。
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 下記のコマンドを実行して、mirrorのパスを設定します。
```
#Ubuntu 14.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu trusty/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 16.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 18.04
echo "deb [ arch=amd64 ] http://mirrors.cloud.tencent.com/mongodb/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 下記のコマンドを実行して、パッケージリストを更新します。
```
sudo apt-get update
```
4. 下記のコマンドを実行して、MongoDBをインストールします。
```
sudo apt-get install -y mongodb-org
```

### Tencent Cloudのイメージソースを利用してRubygemsを加速する
> 利用する前に、お客様のCVMにRubyがインストールされたことを確認してください。
>
下記のコマンドを実行して、Rubygemsのソースアドレスを変更します。
```
gem source -r https://rubygems.org/
gem source -a http://mirrors.cloud.tencent.com/rubygems/
```
