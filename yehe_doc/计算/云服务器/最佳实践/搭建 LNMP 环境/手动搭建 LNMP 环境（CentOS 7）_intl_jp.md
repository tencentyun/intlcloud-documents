## ユースケース
LNMP環境とは、LinuxでのNginx+MySQL/MariaDB+PHP構成のウェブサイトアーキテクチャです。本ドキュメントは、Tencent Cloud Cloud Virtual Machine(CVM)上でLNMP環境を手動で構築する方法を紹介します。

手動でLNMP 環境を構築するには、 Linux コマンド（例：[CentOS環境におけるYUMによるソフトウェアのインストール](https://cloud.tencent.com/document/product/213/2046)等の常用コマンドに詳しい必要があります。また、インストールするソフトウェアの利用及びバージョン間の互換性を把握することも必要です。

## ソフトウェアバージョンの例
LNMP環境を構築したソフトウェアのバージョンと説明は以下の通りです：
- Linux：Linux OS、本ドキュメントはCentOS 7.6を例とします。
- Nginx：Webサーバー、本ドキュメントはNginx 1.17.7を例とします。
- MariaDB：データベース、本ドキュメントはMariaDB 10.4.8を例とします。
- PHP：スクリプト言語、本ドキュメントはPHP 7.2.22を例とします。

## 操作手順

### ステップ1：Linuxインスタンスへのログイン
[標準のログイン方法を使用してLinuxインスタンスにログインする（推奨）](https://cloud.tencent.com/document/product/213/5436)。実際の操作習慣に応じて、他のログイン方式を選択できます。
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://cloud.tencent.com/document/product/213/35699)
- [SSHを使用してLinuxインスタンスにログインする](https://cloud.tencent.com/document/product/213/35700)

### ステップ2：Nginxのインストール
1. 下記のコマンドを実行して、 `/etc/yum.repos.d/` の下に `nginx.repo` ファイルを作成します。
```
vi /etc/yum.repos.d/nginx.repo
```
2. 「**i**」キーを押すと編集モードに切り替えます。下記の内容を入力してください。
```
[nginx] 
name = nginx repo 
baseurl = https://nginx.org/packages/mainline/centos/7/$basearch/ 
gpgcheck = 0 
enabled = 1
```
3.  「**Esc**」をクリックし、「**:wq**」を入力し、ファイルを保存してから戻ります。
4. 以下のコマンドを実行して、nginxをインストールします。
```
yum install -y nginx
```
5. 以下のコマンドを実行して、`nginx.conf` ファイルを開きます。
```
vim /etc/nginx/nginx.conf
```
6.「**i**」を押して、編集モードになり、`nginx.conf` ファイルを編集します。
7. `server{...}` を見つけて、`server` の{}の中に対応する設定情報を以下の内容に切り替えます。
IPv6アドレスへの監視を取り消し、同時にNginxを設定し、PHPとの連動を実現します。
> `Ctrl+F` でページ下方にスクロールしたり、`Ctrl+B`でページ上方にスクロールすることでファイルを確認します。`nginx.conf` ファイアに`server{...}` を見つけない場合は、`include /etc/nginx/conf.d/*conf;` の上方に以下の内容を追加してください。
>
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
7.  「**Esc**」をクリックし、「**:wq**」を入力し、ファイルを保存してから戻ります。
1. 以下のコマンドを実行して、Nginxを起動します。
```
systemctl start nginx
```
9. 以下のコマンドを実行して、Nginxを自動起動に設定します。
```
systemctl enable nginx 
```
10. ローカルブラウザで以下のアドレスにアクセスして、Nginxサービスは正常に実行されるかどうかを確認します。
```
http://CVMインスタンスのパブリックIP
```
下図に示すように、Nginxのインストール・設定が成功したことを表します。
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### ステップ3：データベースのインストール
1. 以下のコマンドを実行して、システム中にMariaDBをインストールしたかどうかを確認します。 
```
rpm -qa | grep -i mariadb
```
 - 戻した結果は以下の内容に類似した場合、MariaDBがインストールしていることを表します。
![](https://main.qcloudimg.com/raw/6fa7fb51de4a61f4da08eb036b6c3e85.png)
異なるインストールバージョンによる衝突を避けるため、以下のコマンドを実行してインストールされたMariaDBを削除します。
```
yum -y remove パッケージ名
```
 - 戻した結果は空である場合、事前にインストールされていないことで、次を実行します。
2. 下記のコマンドを実行して、 `/etc/yum.repos.d/` の下に `MariaDB.repo` ファイルを作成します。
```
vi /etc/yum.repos.d/MariaDB.repo
```
3. 「**i**」キーを押すと編集モードに切り替えます。下記の内容を入力し、MariaDBのソフトウェアリポジトリを追加してください。
> 異なるOSのMariaDBソフトウェアリポジトリが違うため、[MariaDB 公式サイト](https://downloads.mariadb.org) で、他のOSに対応するMariaDBのインストール情報を取得します。
>
```
# MariaDB 10.4 CentOS repository list - created 2019-11-05 11:56 UTC
# http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```
4.  「**Esc**」を押して、 「**:wq**」を入力し、ファイルを保存してから戻ります。
5. 下記のコマンドを実行して、MariaDBをインストールします。
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
8. 以下のコマンドを実行して、MariaDBのインストールに成功したかどうかを確認します。
```
mysql
```
以下のような結果が表示されたら、インストールに成功しました。
![](https://main.qcloudimg.com/raw/bfe9a604457f6de09933206c21fde13b.png)
9. 下記のコマンドを実行し、 MariaDBから退出します。
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
2. 以下のコマンドを実行して、PHP 7.2のパッケージをインストールします。
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
環境設定が完了した後、以下の手順でLNMP環境を成功に構築したことを検証します。
1. 以下のコマンドを実行して、テストファイルを作成します。
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. 以下のコマンドを実行して、Nginxサービスをリスタートします。
```
systemctl restart nginx
```
2. ローカルブラウザで以下のアドレスにアクセスして、環境設定に成功したかどうかを確認します。
```
http://CVMインスタンスのパブリックIP
```
以下のような結果が表示されたら、環境構築に成功しました。
![](https://main.qcloudimg.com/raw/640812413941a61efe29d7faa546ad80.png)


## 関連操作
LNMP環境を構築した後、[手動でWordPress 個人用サイトの構築](https://cloud.tencent.com/document/product/213/8044) を実践することを通じて、CVMに関する機能をより多く理解、把握できます。

## よくある質問
CVMの使用中に問題があれば、下記のドキュメンテーションを参照しながら実際状況に合わせ分析した上で問題を解決することが可能です。
- CVMのログインに関する問題は、 [パスワードとキー](https://cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://cloud.tencent.com/document/product/213/17278)をご参照ください。
- CVMネットワークに関する問題は、 [IPアドレス](https://cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://cloud.tencent.com/document/product/213/2502)をご参照ください。
 - CVMディスクに関する問題は、[システムディスクとデータディスク](https://cloud.tencent.com/document/product/213/17351)をご参照ください。




