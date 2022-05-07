## 概要
ここでは、Tencent Cloud CVMでDockerを構築、使用する方法についてご説明します。Linux OSを熟知し、Tencent Cloud CVMを使い始めたばかりの開発者を対象にしています。Dockerの詳細については、[Docker公式ドキュメント](https://docs.docker.com/)をご参照ください。

<dx-alert infotype="explain" title="">
Windows OSのCVMでDockerを構築、使用する必要がある場合は、[WindowsへのDockerデスクトップのインストール](https://docs.docker.com/docker-for-windows/install/)をご参照ください。
</dx-alert>



## デモ用オペレーティングシステム
このドキュメントでは、CVMインスタンスのオペレーティングシステムの例としてCentOS 8.2および7.6をを使用します。
TencentOS Serverオペレーティングシステムを使用している場合は、実際の対応バージョンを使用してください：
  - TencentOS Server 2.4：イメージにはDockerが組み込まれたため、インストールする必要はありません。[Dockerの使用](#userDocker)を参照してそのまま使用してください。
  - TencentOS Server 3.1(TK4)：ドキュメントの手順を参照して構築してください。

##  前提条件
Linux CVMを購入済みであること。
<dx-alert infotype="explain" title="">
Dockerの構築には64ビットシステムを使用し、カーネルバージョンが3.10以上である必要があります。
</dx-alert>



## 操作手順

### Dockerのインストール

実際に使用しているOSのバージョンに応じて、次の手順で操作します：

<dx-tabs>
::: CentOS 8.2
1. [標準方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)します。
2. 次のコマンドを実行して、Dockerリポジトリを追加します。
```
dnf config-manager --add-repo=http://mirrors.tencent.com/docker-ce/linux/centos/docker-ce.repo
```
3. 次のコマンドを実行して、追加されたDockerリポジトリを確認します。
```
dnf list docker-ce
```
4. 次のコマンドを実行して、Dockerをインストールします。
```
dnf install -y docker-ce --nobest
```
5. 次のコマンドを実行して、Dockerを実行します。
```
systemctl start docker
```
6. 次のコマンドを実行して、インストール結果をチェックします。
```
docker info
```
次のような情報が返されれば、インストールが完了しています。
![](https://main.qcloudimg.com/raw/113b820e4efc6441d88410488441291f.png)
:::
::: CentOS 7.6
1. [標準方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)します。
2. 次のコマンドを順に実行して、YUMリポジトリを追加します。
```
yum update
```
```
yum install epel-release -y
```
```
yum clean all
```
```
yum list
```
3. 次のコマンドを実行して、Dockerをインストールします。
```
yum install docker-io -y
```
4. 次のコマンドを実行して、Dockerを実行します。
```
systemctl start docker
```
5. 次のコマンドを実行して、インストール結果を確認します。
```
docker info
```
次のような情報が返されれば、インストールに成功しています。
![](https://main.qcloudimg.com/raw/a848737e9d011f528f66dc54fca61c08.png)
:::
</dx-tabs>


### Docker[](id:userDocker)の使用
Dockerを使用するための基本的なコマンドは次のとおりです：
- Dockerデーモンを管理します。
 - Dockerデーモンを実行します：
```
systemctl start docker
```
 - Dockerデーモンを停止します：
```
systemctl stop docker
```
 - Dockerデーモンを再起動します：
```
systemctl restart docker
```
- イメージを管理します。ここではDocker HubのNginxイメージを例として取り上げます。
```
docker pull nginx 
```
 - タグの変更：イメージタグを変更して、違いを記憶させることができます。
```
docker tag docker.io/nginx:latest tencentyun/nginx:v1
```
 - 既存イメージを確認します：
```
docker images
```
 - イメージを強制的に削除します：
```
docker rmi -f tencentyun/nginx:v1
```
- コンテナを管理します。
 - コンテナにログインします：
```
docker run -it ImageId /bin/bash
```
そのうち、`ImageId`は`docker images`コマンドを実行することで取得できます。
 - コンテナからのログアウト：`exit`コマンドを実行し、現在のコンテナからログアウトします。
 - バックグラウンドで実行されているコンテナにログインします：
```
docker exec -itコンテナID /bin/bash
```
 - コンテナをイメージ化します：
```
docker commit <コンテナIDまたはコンテナ名> [<リポジトリ名>[:<タグ>]]
```
例：
```
docker commit 1c23456cd7**** tencentyun/nginx:v2
```

### イメージの作成

1. 次のコマンドを実行して、Dockerfileファイルを開きます。
```
vim Dockerfile
```
2. **i**を押して編集モードに切り替え、次の内容を追加します。
```
FROM tencentyun/nginx:v2  #ベースイメージのソースを宣言します。
MAINTAINER DTSTACK #イメージの所有者を宣言します。
RUN mkdir /dtstact # RUNの後ろには、コンテナを実行する前に実行する必要のあるコマンドが続きます。Dockerfileは127行を超えることはできないため、コマンドが多い場合は、スクリプトに記述して実行することをお勧めします。
ENTRYPOINT ping https://cloud.tencent.com/ #ブートコマンドです。ここでの最後のコマンドは、フォアグラウンドで継続的に実行できるコマンドである必要があります。そうでない場合、コンテナはバックグラウンドで実行され、コマンドの実行が終了した時点でログアウトします。
```
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. 次のコマンドを実行して、イメージを作成します。
```
docker build -t nginxos:v1 .  #.は、Dockerfileファイルのパスなので、無視することはできません。
```
5. 次のコマンドを実行して、イメージの作成が成功したかどうかを確認します。
```
docker images
```
6. 次のコマンドを順に実行して、コンテナの実行とコンテナの表示を行います。
```
docker run -d nginxos:v1         #コンテナをバックグラウンドで実行します。
docker ps                        #現在実行中のコンテナを確認します。
docker ps -a                     #実行されていないコンテナを含むすべてのコンテナを確認します。
docker logs CONTAINER ID/IMAGE   #先ほど実行したコンテナが表示されない場合は、コンテナIDまたはコンテナ名でブートログを確認し、トラブルシューティングを行います。
```
6. 次のコマンドを順に実行して、イメージを作成します。
```
docker commit fb2844b6**** nginxweb:v2 #commitパラメータの後に、コンテナID、作成する新しいイメージの名前とバージョン番号を追加します。
docker images                    #ローカル（ダウンロード済みおよびローカルで作成された）イメージを一覧表示します。
```
7. 次のコマンドを順に実行して、リモートリポジトリにイメージをプッシュします。
デフォルトでDockerHubにプッシュします。まずDockerにログインして、タグをイメージにバインドし、イメージに`Dockerユーザー名/イメージ名:タグの形式で名前を付け、最後にプッシュを完了する必要があります。
```
docker login #実行後、イメージリポジトリのユーザー名とパスワードを入力します
docker tag [イメージ名]:[タグ] [ユーザー名]:[タグ]
docker push [ユーザー名]:[タグ]
```
プッシュが完了したら、ブラウザを使用してDocker Hubの公式ウェブサイトにログインし、確認することができます。



