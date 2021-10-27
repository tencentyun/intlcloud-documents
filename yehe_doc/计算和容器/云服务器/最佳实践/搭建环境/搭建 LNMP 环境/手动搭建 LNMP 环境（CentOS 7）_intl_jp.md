## 概要
LNMP環境とは、LinuxでのNginx+MySQL/MariaDB+PHPで構成されるウェブサイトサーバーアーキテクチャです。本ドキュメントは、Tencent Cloud CVMでLNMP環境を手動で構築する方法について説明します。

手動でLNMP 環境を構築するには、 Linux コマンド（例：[CentOS環境でのYUMを使用してソフトウェアのインストール](https://intl.cloud.tencent.com/document/product/213/2046)）等の常用コマンドに精通している必要があります。また、インストールするソフトウェアの使用方法及びバージョン間の互換性を把握することも必要です。
>!Tencent Cloudでは、クラウドマーケットのイメージ環境を通じてLNMP環境をデプロイすることをお勧めしています。LNMP環境を手動で構築すると時間がかかる可能性があります。

## ソフトウェアのバージョン
この例では、LNMP環境の構築に使用されるソフトウェアのバージョンと説明は次のとおりです。
- Linux：Linux OS、本ドキュメントはCentOS 7.6を例として説明します。
- Nginx：Webサーバー、本ドキュメントはNginx 1.17.7を例として説明します。
- MariaDB：データベース、本ドキュメントはMariaDB 10.4.8を例として説明します。
- PHP：スクリプト言語、本ドキュメントはPHP 7.2.22を例とします。


## 前提条件
Linux CVMを購入済みであること。CVMを購入していない場合は、[Linux CVMのクイック設定](https://intl.cloud.tencent.com/zh/document/product/213/10517)をご参照ください。


## 操作手順

### ステップ1：Linuxインスタンスにログインする
[標準的な方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます：
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSHキーを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)

### ステップ2：Nginxをインストールする
1. 下記のコマンドを実行して、 `/etc/yum.repos.d/` の下に `nginx.repo` という名前のファイルを作成します。
```
vi /etc/yum.repos.d/nginx.repo
```
2. **i**キーを押して編集モードに切り替え、以下の内容を書き込みます。
```
[nginx] 
name = nginx repo 
baseurl = https://nginx.org/packages/mainline/centos/7/$basearch/ 
gpgcheck = 0 
enabled = 1
```
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. 以下のコマンドを実行して、nginxをインストールします。
```
yum install -y nginx
```
5. 以下のコマンドを実行し、`default.conf`ファイルを開きます。
```
vim /etc/nginx/conf.d/default.conf
```
6. **i**を押して編集モードに切り替え、`default.conf`ファイルを編集します。
7.`server{...}`を見つけて、 `server` 大括弧内の対応する設定情報を次の内容に置き換えます。 
```
server {
	listen       80;
	root   /usr/share/nginx/html;
	server_name  localhost;
	#charset koi8-r;
	#access_log  /var/log/nginx/log/host.access.log  main;
	#
	location / {
		  index index.php index.html index.htm;
	}
	#error_page  404              /404.html;
	#redirect server error pages to the static page /50x.html
	#
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
	  root   /usr/share/nginx/html;
	}
	#pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
	#
	location ~ .php$ {
	  fastcgi_pass   127.0.0.1:9000;
	  fastcgi_index  index.php;
	  fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
	  include        fastcgi_params;
	}
}
```
7.  **Esc**を押し、 **:wq**を入力し、ファイルを保存してから戻ります。
8.  以下のコマンドを実行して、Nginxを起動します。
```
systemctl start nginx
```
9. 以下のコマンドを実行して、Nginxを自動起動に設定します。
```
systemctl enable nginx 
```
10. ローカルブラウザで以下のアドレスにアクセスして、Nginxサービスは正常に実行されるかどうかを確認します。
```
http://CVMインスタンスのパブリックIPアドレス
```
下図に示すように、Nginxのインストール及び設定が成功したことを表します。
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### ステップ3：データベースのインストール
1. 以下のコマンドを実行して、システムにMariaDBをインストールしたかどうかを確認します。 
```
rpm -qa | grep -i mariadb
```
 - 次の結果が返された場合、MariaDBがインストールしていることを表します。
![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
異なるバージョン間での競合を回避するには、以下のコマンドを実行してインストールされたMariaDBを削除します。
```
yum -y remove パッケージ名
```
 - 返された結果が空の場合、MariaDBはインストールされていません。この場合は、次の手順に進んでください。
2. 下記のコマンドを実行して、 `/etc/yum.repos.d/` の下に `MariaDB.repo` ファイルを作成します。
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. **i**キーを押して編集モードに切り替え、以下の内容を書き込み、MariaDBソフトウェアライブラリを追加します。
>? 
>- 異なるOSのMariaDBソフトウェアライブラリが違うため、[MariaDB 公式サイト](https://downloads.mariadb.org) にアクセスして、他のOSに対応するMariaDBソフトウェアライブラリのインストール情報を取得できます。
>- CVMが[プライベートネットワークサービス](https://intl.cloud.tencent.com/document/product/213/5225)を使用する場合、`mirrors.cloud.tencent.com` をプライベートネットワークアドレス `mirrors.tencentyun.com`に変更します。このようにして、パブリックネットワークトラフィックは影響を受けず、アクセス速度が高速になります。 
>
```
# MariaDB 10.4 CentOS repository list - created 2019-11-05 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = https://mirrors.cloud.tencent.com/mariadb/yum/10.4/centos7-amd64
gpgkey=https://mirrors.cloud.tencent.com/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
4. ** Esc **を押して**：wq **を入力し、ファイルを保存して戻ります。
5. 以下のコマンドを実行して、MariaDBをインストールします。このプロセスには時間がかかります。インストールの進行状況に注意し、インストールが完了するまでお待ちください。
```
yum -y install MariaDB-client MariaDB-server
```
6. 以下のコマンドを実行して、MariaDBサービスを起動します。
```
systemctl start mariadb
```
7. 以下のコマンドを実行して、MariaDBを自動起動に設定します。
```
systemctl enable mariadb
```
8. 以下のコマンドを実行して、MariaDBが正常にインストールされていることを確認します。
```
mysql
```
以下のような結果が表示されたら、インストールが成功したことを意味します。
![](https://main.qcloudimg.com/raw/bfe9a604457f6de09933206c21fde13b.png)
9. 下記のコマンドを実行し、MariaDBを終了します。
```
\q
```


### ステップ4：PHPのインストールと設定
1. 順次に以下のコマンドを実行して、yumにあるPHPのソフトウェアソースを更新します。
```
rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-7.noarch.rpm
```
```
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```
2. 以下のコマンドを実行して、PHP 7.2に必要なパッケージをインストールします。
```
yum -y install mod_php72w.x86_64 php72w-cli.x86_64 php72w-common.x86_64 php72w-mysqlnd php72w-fpm.x86_64
```
3. 以下のコマンドを実行して、PHP-FPMサービスを起動します。
```
systemctl start php-fpm
```
4. 以下のコマンドを実行して、PHP-FPMサービスを自動起動に設定します。
```
systemctl enable php-fpm
```

## 環境設定の検証
環境設定が完了した後、以下の手順でLNMP環境が正常に構築されたことを確認します。
1. 以下のコマンドを実行して、テストファイルを作成します。
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. 以下のコマンドを実行して、Nginxサービスを再起動します。
```
systemctl restart nginx
```
3. ローカルブラウザに次のURLを入力して、環境設定が成功したかどうかを確認します。
```
http://CVMインスタンスのパブリックIPアドレス
```
以下のような結果が表示されたら、環境設定が成功したことを示します。
![](https://main.qcloudimg.com/raw/640812413941a61efe29d7faa546ad80.png)


## 関連する操作
LNMP環境を構築した後、CVMに関する機能をより多く理解と把握するために、[WordPress Webサイトを手動で構築](https://intl.cloud.tencent.com/document/product/213/8044)できます。

## よくあるご質問
CVMの使用中に問題が発生した場合は、下記のドキュメントを参照しながら実際状況に合わせ分析した上で問題を解決することが可能です。
- CVMのログインに関する問題は、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)ドキュメントをご参照ください。
- CVMのネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)ドキュメントをご参照ください。
- CVMのハードディスクに関する問題は、[システムディスクとデータディスク](https://intl.cloud.tencent.com/document/product/213/17351)ドキュメントをご参照ください。
