## ユースケース

ソフトウェアの依存関係をインストールするときに公式ソースへのアクセスが遅いという問題を解決するために、Tencent Cloudは一部のソフトウェアにキャッシュ機能を設定しました。Tencent Cloudのリポジトリを使用して、依存パッケージのインストール速度を改善することができます。ユーザーがサービスアーキテクチャを自由に構築できるように、Tencent Cloudのリポジトリはパブリックネットワークアクセスとプライベートネットワークアクセスをサポートしています。
- パブリックネットワークアクセスのURL：`http://mirrors.tencent.com`です
- プライベートネットワークアクセスのURL：`http://mirrors.tencentyun.com/`です

<dx-alert infotype="explain" title="">
- 本ドキュメントは、Tencent Cloudのリポジトリのパブリックネットワークアクセスアドレスを例として、CVMでリポジトリを利用する方法をご紹介します。プライベートネットワーク方式でTencent Cloudのリポジトリにアクセスしたい場合、パブリックネットワークのURLを**プライベートネットワークのURLに変更してください**。
- 本ドキュメントに関わったTencent CloudのリポジトリURLは、ご参考のみであり、**Tencent Cloudのリポジトリ**から最新のURLを取得してください。
</dx-alert>


## 注意事項

Tencent Cloudのリポジトリは、毎日公式リポジトリから各ソフトウェアを一回同期させます。

##  前提条件

CVMにログインしました。

## 操作手順

### Tencent Cloudのイメージソースを利用してpipを加速する


<dx-alert infotype="notice" title="">
利用する前に、お客様のCVMにPythonがインストールされたことを確認してください。
</dx-alert>


#### 一時的にリポジトリのパスを利用する
下記のコマンドを実行して、Tencent CloudのPyPIリポジトリを利用してpipをインストールします。
```shell
pip install pip -i  PyPI リポジトリのディレクトリ
```
例えば、17monipをインストールし、利用するPyPIリポジトリは`http://mirrors.tencent.com/pypi/simple` ディレクトリ配下にあるようにしたら、下記のコマンドを実行してください：
```shell
pip install 17monip -i http://mirrors.tencent.com/pypi/simple --trusted-host mirrors.tencent.com 
```

#### デフォルトリポジトリのパスを設定する
下記のコマンドを実行して、 `~/.pip/pip.conf` ファイルの ` index-url`パラメータをTencent Cloud上のリポジトリのパスに変更します。

```shell
[global]
index-url = PyPIリポジトリのディレクトリ
trusted-host = パブリック/プライベートネットワークのURL
```
下記の例のように、利用するPyPIリポジトリは`http://mirrors.tencent.com/pypi/simple` ディレクトリ配下にあります。下記のコマンドを実行してください：
```shell
[global]
index-url = http://mirrors.tencent.com/pypi/simple
trusted-host = mirrors.tencent.com
```

### Tencent Cloudのイメージソースを利用してMavenを加速する


<dx-alert infotype="notice" title="">
利用する前に、お客様のCVMにJDKとMavenがインストールされたことを確認してください。
</dx-alert>


1. Mavenの設定ファイル `settings.xml` を開きます。
2. `<mirrors>...</mirrors>` のコードブロックを見つけて、以下の内容を`<mirrors>...</mirrors>`コードブロックに設定します。
```xml
    <mirror>
        <id>nexus-tencentyun</id>
        <mirrorOf>*</mirrorOf>
        <name>Nexus tencentyun</name>
        <url>http://mirrors.tencent.com/nexus/repository/maven-public/</url>
    </mirror> 
```

### Tencent Cloudのイメージソースを利用してNPMを加速する


<dx-alert infotype="notice" title="">
利用する前に、お客様のCVMにNode.jsとNPMがインストールされたことを確認してください。
</dx-alert>


下記のコマンドを実行して、Tencent CloudのNPMリポジトリでNPMをインストールします。
```shell
npm config set registry http://mirrors.tencent.com/npm/
```

### Tencent Cloudのイメージソースを利用してDockerを加速する

#### TKEクラスターにTencent Cloud上のDockerリポジトリを利用する

手動で設定する必要はありません。Tencent Kubernetes Engine(TKE)クラスターに、CVMのホストはノードを作成するとき、自動的にDockerサービスをインストールし、またTencent Cloudプライベートネットワークイメージを作成します。

#### CVMでTencent CloudのDockerリポジトリを利用する



<dx-alert infotype="notice" title="">
利用する前に、お客様のCVMにDockerがインストールされたことを確認してください。
Docker Hub Mirror機能はDocker 1.3.2以降が必要です。1.3.2以降のDockerがインストールされていない場合、またはバージョンが古い場合、インストールまたはアップデートしてから利用してください。
</dx-alert>


CVMのOS種類により、最適な操作手順を選んでください。
- Ubuntu 14.04、Debian、CentOS 6 、Fedora、openSUSEなどのOSに適用します。他のバージョンのOSの操作手順は若干異なります。
 1. 下記のコマンドを実行して、 設定ファイル`/etc/default/docker` を開きます。
```shell
vim /etc/default/docker
```
 2. **i**キーを押すと編集モードに切り替えます。下記の内容を追加して、保存してください。 
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- Centos 7 OSに適用する：
 1. 下記のコマンドを実行して、 設定ファイル`/etc/docker/daemon.json`を開きます。
```shell
vim /etc/docker/daemon.json
```
 2. **i**キーを押すと編集モードに切り替えます。下記の内容を追加して、保存してください。 
```json
{
   "registry-mirrors": [
       "https://mirror.ccs.tencentyun.com"
  ]
}
```
- 既に Boot2DockerをインストールしたWindows OSに適用する：
 1. Boot2Docker Start Shellに入り、下記のコマンドを実行してください：
```shell
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile  exit 
```
 2. Boot2Dockerをリスタートします。

### Tencent Cloudのイメージを利用してMariaDBを加速する


<dx-alert infotype="explain" title="">
以下の操作手順は、CentOS 7を例として説明します。OSにより若干異なる操作手順があります。
</dx-alert>


1. 下記のコマンドを実行して、 `/etc/yum.repos.d/` の下に `MariaDB.repo` ファイルを作成します。
```shell
vi /etc/yum.repos.d/MariaDB.repo
```
2. **i**キーを押すと編集モードに切り替えます。下記の内容を書き込み、保存してください。
```shell
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. 下記のコマンドを実行して、yumのキャッシュをクレンジングします。
```shell
yum clean all
```
4. 下記のコマンドを実行して、MariaDBをインストールします。
```shell
yum install MariaDB-client MariaDB-server
```

### Tencent Cloudのイメージを利用してMongoDBを加速する


<dx-alert infotype="explain" title="">
以下の操作手順は、MongoDB 4.0のインストールを例として説明します。その他のバージョンをインストールする際に、mirrorパス内のバージョン番号を変更してください。
</dx-alert>


#### CentOS及びRedhatシステムのCVMは、Tencent CloudのMongoDBリポジトリを利用する。

1. 下記のコマンドを実行して、`/etc/yum.repos.d/mongodb.repo` ファイルを作成します。
```shell
vi /etc/yum.repos.d/mongodb.repo
```
2. **i**キーを押すと編集モードに切り替えます。下記の内容を書き込み、保存してください。
```shell
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=http://mirrors.tencent.com/mongodb/yum/el7-4.0
gpgcheck=0
enabled=1
```
2. 下記のコマンドを実行して、MongoDBをインストールします。
```shell
yum install -y mongodb-org
```

#### DebianシステムのCVMは、Tencent CloudのMongoDBリポジトリを利用する

1. Debianのバージョンにより、下記の該当のコマンドを実行して、MongoDB GPGのパブリックキーをインポートします。
```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 下記のコマンドを実行して、mirrorのパスを設定します。
```
#Debian 8
echo "deb http://mirrors.tencent.com/mongodb/apt/debian jessie/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Debian 9
echo "deb http://mirrors.tencent.com/mongodb/apt/debian stretch/mongodb-org/4.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 下記のコマンドを実行して、キャッシュをクレンジングします。
```shell
sudo apt-get clean all
```
4. 次のコマンドを実行して、ソフトウェアパッケージリストを更新します。
```shell
sudo apt-get update
```
5. 下記のコマンドを実行して、MongoDBをインストールします。
```shell
sudo apt-get install -y mongodb-org
```

#### UbuntuシステムのCVMは、Tencent CloudのMongoDBリポジトリを利用する

1. 下記のコマンドを実行して、MongoDB GPGのパブリックキーをインポートします。
```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4
```
2. 下記のコマンドを実行して、mirrorのパスを設定します。
```
#Ubuntu 14.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu trusty/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 16.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
#Ubuntu 18.04
echo "deb [ arch=amd64 ] http://mirrors.tencent.com/mongodb/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
```
3. 下記のコマンドを実行して、キャッシュをクレンジングします。
```shell
sudo apt-get clean all
```
4. 次のコマンドを実行して、ソフトウェアパッケージリストを更新します。
```shell
sudo apt-get update
```
5. 下記のコマンドを実行して、MongoDBをインストールします。
```shell
sudo apt-get install -y mongodb-org
```

### Tencent Cloudのイメージソースを利用してRubygemsを加速する


<dx-alert infotype="notice" title="">
利用する前に、お客様のCVMにRubyがインストールされたことを確認してください。
</dx-alert>


下記のコマンドを実行して、Rubygemsのソースアドレスを変更します。
```shell
gem source -r https://rubygems.org/
gem source -a http://mirrors.tencent.com/rubygems/
```
