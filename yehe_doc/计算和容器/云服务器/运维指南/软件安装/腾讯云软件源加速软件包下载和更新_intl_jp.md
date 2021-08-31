## 操作シナリオ

ソフトウェアの依存関係をインストールするとき、公式ソースへのアクセスが遅いという問題を解決するために、Tencent Cloudは一部のソフトウェアにキャッシュサービスをセットアップしました。Tencent Cloudのソフトウェアリポジトリを使用して、依存関係のインストール速度を改善することができます。ユーザーがサービスアーキテクチャを自由に構築できるように、Tencent Cloudソフトウェアリポジトリは、現在パブリックネットワークアクセスとプライベートネットワークアクセスをサポートしています。
- パブリックネットワークアクセスアドレス：`http://mirrors.cloud.tencent.com/`
- プライベートネットワークアクセスアドレス：`http://mirrors.tencentyun.com/`

> 
> - 本ドキュメントは、Tencent Cloudソフトウェアリポジトリのパブリックネットワークアクセスアドレスを例として、CVMでTencent Cloudソフトウェアリポジトリのソフトウェアソースを利用する方法について説明します。プライベートネットワークを使用してリポジトリにアクセスする場合は、パブリックネットワークアクセスアドレスを**プライベートネットワークアクセスアドレス**に置き換えてください。
> - 本ドキュメントに関わったTencent Cloudソフトウェアリポジトリのアドレスは、ご参考のみとして提供しております。**Tencent Cloudソフトウェアリポジトリ**から最新のアドレスを取得してください。
>

## 注意事項

Tencent Cloudソフトウェアリポジトリは、各ソフトウェアソースの公式Webサイトからソフトウェアソースを1日に1回同期にしています。

## 前提条件

CVMにログインしました。

## 操作手順

### Tencent Cloudイメージソースを利用してpipを加速
> Tencent Cloudイメージソースを利用する前に、CVMにPythonがインストールされていることを確認してください。
>
#### 一時的にソフトウェアソースのパスを利用
Tencent Could PyPIソフトウェアソースを利用してpipをインストールするには、次のコマンドを実行します。
```
pip install -i  PyPIソフトウェアソースが配置されているディレクトリ
```
例えば、利用するPyPIソフトウェアソースが`http://mirrors.cloud.tencent.com/pypi/simple` ディレクトリ下にある場合は、次のコマンドを実行します。
```
pip install 17monip -i http://mirrors.cloud.tencent.com/pypi/simple --trusted-host mirrors.cloud.tencent.com 
```

#### デフォルトのソフトウェアソースパスを設定
下記のコマンドを実行して、 `~/.pip/pip.conf` ファイルの ` index-url`パラメータをTencent Cloudソフトウェアリポジトリのソースパスに変更します。

```
[global]
index-url = PyPIソフトウェアソースが配置されているディレクトリ
trusted-host = パブリック/プライベートネットワークアクセスアドレス
```
例えば、利用するPyPIソフトウェアソースが`http://mirrors.cloud.tencent.com/pypi/simple` ディレクトリ下にある場合は、次のコマンドを実行します。
```
[global]
index-url = http://mirrors.cloud.tencent.com/pypi/simple
trusted-host = mirrors.cloud.tencent.com
```

### Tencent Cloudイメージソースを利用してMavenを加速
> Tencent Cloudイメージソースを利用する前に、CVMにJDKとMavenがインストールされていることを確認してください。
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

### Tencent Cloudイメージソースを利用してNPMを加速
> Tencent Cloudイメージソースを利用する前に、CVMにNode.jsとNPMがインストールされていることを確認してください。
>
下記のコマンドを実行して、Tencent Cloud NPMソフトウェアソースを利用してNPMをインストールします。
```
npm config set registry http://mirrors.cloud.tencent.com/npm/
```

### Tencent Cloudイメージソースを利用してDockerを加速

#### TKEクラスターでTencent Cloud Dockerソフトウェアソースを利用

手動で設定する必要はありません。Tencent Kubernetes Engine（TKE）クラスターのCVMがノードを作成すると、自動的にDockerサービスをインストールし、またTencent Cloudプライベートネットワークイメージを設定します。

#### CVMでTencent Cloud Dockerソフトウェアソースを利用

> Tencent Cloud Dockerソフトウェアソースを利用する前に、CVMにDockerがインストールされていることを確認してください。
> Docker 1.3.2以降のバージョンのみ、Docker Hub Mirror機能をサポートします。Docker 1.3.2以降のバージョンをインストールしていない場合、またはインストールされているバージョンが古すぎる場合は、インストールまたはアップグレードしてから利用してください。
> 
CVMのOSの種類により、最適な操作手順を選んでください。
- 次の手順は、Ubuntu 14.04、Debian、CentOS 6 、Fedora、またはopenSUSEなどのOSに適用します。他のバージョンのOSの操作手順はわずかに異なります。
 1. 下記のコマンドを実行して、 設定ファイル`/etc/default/docker` を開きます。
```
vim /etc/default/docker
```
 2. **i**キーを押して編集モードに切り替え、次の内容を入力して保存します。
```
DOCKER_OPTS="--registry-mirror=https://mirror.ccs.tencentyun.com"
```
- Centos 7の場合：
 1．以下のコマンドを実行し、設定ファイル`/etc/docker/daemon.json`を開きます。
```
vim/etc/docker/daemon.json
```
 2. **i**キーを押して編集モードに切り替え、次の内容を入力して保存します。 
```
{
   ″registry-mirrors″:[
       ″https://mirror.ccs.tencentyun.com″
  ]
}
```
- Boot2DockerがインストールされているWindowsの場合：
 1. Boot2Docker Start Shellにアクセスし、次のコマンドを実行します。
```
sudo su echo "EXTRA_ARGS=\"–registry-mirror=https://mirror.ccs.tencentyun.com\"" >> /var/lib/boot2docker/profile  exit 
```
 2. Boot2Dockerを再起動します。

### Tencent Cloudイメージを利用してMariaDBを加速
> 以下の操作手順は、CentOS 7を例として説明します。具体的な手順はOSによって異なります。
>
1. 下記のコマンドを実行して、 `/etc/yum.repos.d/` の下に `MariaDB.repo` ファイルを作成します。
```
vi /etc/yum.repos.d/MariaDB.repo
```
2. **i**キーを押して編集モードに切り替え、次の内容を入力して保存します。
```
# MariaDB 10.2 CentOS7-amd64
[mariadb]  
name = MariaDB  
baseurl = http://mirrors.cloud.tencent.com/mariadb/yum/10.2/centos7-amd64/
gpgkey = http://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1  
```
3. 下記のコマンドを実行して、yumキャッシュをクリアします。
```
yum clean all
```
4. 下記のコマンドを実行して、MariaDBをインストールします。
```
yum install MariaDB-client MariaDB-server
```

### Tencent Cloudイメージを利用してMongoDBを加速
> 以下の操作手順は、MongoDB 4.0バージョンのインストールを例として説明します。その他のバージョンをインストールする必要がある場合は、mirrorパス内のバージョン番号を変更してください。
>
#### CentOS及びRedhatシステムのCVMでTencent Cloud MongoDBソフトウェアソースを利用

1. 下記のコマンドを実行して、`/etc/yum.repos.d/mongodb.repo` ファイルを作成します。
```
vi /etc/yum.repos.d/mongodb.repo
```
2. **i**キーを押して編集モードに切り替え、次の内容を入力して保存します。
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

#### DebianシステムのCVMでTencent Cloud MongoDBソフトウェアソースを利用

1. Debianのバージョンにより、下記の該当のコマンドを実行して、MongoDB GPGの公開鍵をインポートします。
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
3. 下記のコマンドを実行して、ソフトウェアパッケージリストを更新します。
```
sudo apt-get update
```
4. 下記のコマンドを実行して、MongoDBをインストールします。
```
sudo apt-get install -y mongodb-org
```

#### UbuntuシステムのCVMでTencent Cloud MongoDBソフトウェアソースを利用

1. 下記のコマンドを実行して、MongoDB GPGの公開鍵をインポートします。
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
3. 下記のコマンドを実行して、ソフトウェアパッケージリストを更新します。
```
sudo apt-get update
```
4. 下記のコマンドを実行して、MongoDBをインストールします。
```
sudo apt-get install -y mongodb-org
```

### Tencent Cloudイメージソースを利用してRubygemsを加速
> Tencent Cloudイメージソースを利用する前に、CVMにRubyがインストールされていることを確認してください。
>
下記のコマンドを実行して、Rubygemsのソースアドレスを修正します。
```
gem source -r https://rubygems.org/
gem source -a http://mirrors.cloud.tencent.com/rubygems/
```
