## 概要
LNMP環境とは、LinuxでのNginx+MySQL/MariaDB+PHPで構成されるウェブサイトサーバーアーキテクチャです。本ドキュメントは、Tencent Cloud CVMでLNMP環境を手動で構築する方法について説明します。

手動でLNMP 環境を構築するには、 Linux コマンド（例：[CentOS環境でのYUMを使用してソフトウェアのインストール](https://intl.cloud.tencent.com/document/product/213/2046)）等の常用コマンドに精通している必要があります。また、インストールするソフトウェアの使用方法及びバージョン間の互換性を把握することも必要です。

>!Tencent Cloudでは、クラウドマーケットのイメージ環境を通じてLNMP環境をデプロイすることをお勧めしています。LNMP環境を手動で構築すると時間がかかる可能性があります。


## ソフトウェアのバージョン
この例では、LNMP環境の構築に使用されるソフトウェアのバージョンと説明は次のとおりです。
Linux：Linux OS。ここではCentOS 6.9を例として説明します。
Nginx：Webサーバー。ここではNginx 1.17.5を例として説明します。
MySQL：データベース。ここではMySQL 5.1.73を例として説明します。
PHP：スクリプト言語。ここでは PHP 7.1.32を例として説明します。

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
name=nginx repo
baseurl=https://nginx.org/packages/mainline/centos/6/$basearch/
gpgcheck=0
enabled=1
```
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. 以下のコマンドを実行して、Nginxをインストールします。
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
8. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
9. 以下のコマンドを実行し、Nginxを起動します。
```
service nginx start
```
10. 以下のコマンドを順に実行し、コンピュータの起動時にNginxが自動的に起動するように設定します。
```bash
chkconfig --add nginx
```
```
chkconfig  nginx on
```
11. ローカルブラウザで以下のアドレスにアクセスして、Nginxサービスは正常に実行されるかどうかを確認します。
```
http://CVMインスタンスのパブリックIPアドレス
```
次の結果が表示されれば、Nginxのインストールと設定は成功です。
![](https://main.qcloudimg.com/raw/fdc40877928729679d392eb304a3f12c.png)


### ステップ3：データベースのインストール
1. 以下のコマンドを実行して、システムにMySQLがインストールされているかどうかを確認します。
```
rpm -qa | grep -i mysql
```
 - 返された結果が次のようになっていれば、MySQLがすでに存在することを示しています。
![](https://main.qcloudimg.com/raw/74e544638637d39209cc1e474083d11d.png)
インストールされたバージョンの違いによる競合を避けるため、次のコマンドを実行して、インストールされているMySQLを削除してください。
```
yum remove -y パッケージ名
```
 - 返された結果が空の場合、MariaDBはインストールされていません。この場合は、次の手順に進んでください。
2. 以下のコマンドを実行し、MySQLをインストールします。
```
yum install -y mysql-devel.x86_64 mysql-server.x86_64 mysql-libs.x86_64
```
3. 以下のコマンドを実行し、MySQLを起動します。
```
service mysqld start 
```
4. 以下のコマンドを順に実行し、コンピュータの起動時にMySQLが自動的に起動するように設定します。
```bash
chkconfig --add mysqld
```
```
chkconfig mysqld  on 
```
5. 以下のコマンドを実行し、MySQLのインストールに成功したかどうかを確認します。
```
mysql
```
以下のような結果が表示されたら、インストールが成功したことを意味します。
![](https://main.qcloudimg.com/raw/9c9347ad0264ddad5e98c8dd48adcc6a.png)
6. 以下のコマンドを実行して、MySQLを終了します。
```
\q
```

### ステップ4：PHPのインストールと設定
1. 順次に以下のコマンドを実行して、yumにあるPHPのソフトウェアソースを更新します。
```
rpm -Uvh https://mirrors.cloud.tencent.com/epel/epel-release-latest-6.noarch.rpm
```
```
rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
```
2. 以下のコマンドを実行して、PHP 7.1.32に必要なパッケージをインストールします。
```
yum -y install mod_php71w.x86_64 php71w-cli.x86_64 php71w-common.x86_64 php71w-mysqlnd php71w-fpm.x86_64
```
3. 以下のコマンドを実行して、PHP-FPMサービスを起動します。
```
service php-fpm start
```
3. 以下のコマンドを順に実行し、コンピュータの起動時にPHP-FPMが自動的に起動するように設定します。
```bash
chkconfig --add php-fpm  
```
```
chkconfig php-fpm on
```


## 環境設定の検証
1. 以下のコマンドを実行して、テストファイルを作成します。
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. 以下のコマンドを実行し、Nginxを再起動します。
```
service nginx restart
```
3. ローカルブラウザで以下のアドレスにアクセスして、環境設定が成功したかどうかを確認します。
```
http://CVMインスタンスのパブリックIPアドレス
```
以下のような結果が表示されたら、環境設定が成功したことを示します。
![](https://main.qcloudimg.com/raw/64af927320f2121ae4daf15cf2eaba39.png)



## 関連する操作

LNMP環境を構築した後、CVMに関する機能をより多く理解と把握するために、[WordPress Webサイトを手動で構築](https://intl.cloud.tencent.com/document/product/213/8044)できます。

## よくあるご質問

CVMの使用中に問題が発生した場合は、下記のドキュメントを参照しながら実際状況に合わせ分析した上で問題を解決することが可能です。

- CVMのログインに関する問題は、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)ドキュメントをご参照ください。
- CVMのネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)ドキュメントをご参照ください。
- CVMのハードディスクに関する問題は、[システムディスクとデータディスク](https://intl.cloud.tencent.com/document/product/213/17351)ドキュメントをご参照ください。
