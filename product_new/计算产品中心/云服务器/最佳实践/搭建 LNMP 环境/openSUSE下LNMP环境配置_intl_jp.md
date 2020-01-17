## 操作シナリオ 
LNMP環境は、LinuxでNginx + MySQL + PHP ウェブサイトのサーバアーキテクチャを表します。 このドキュメントでは、openSUSE42.3でLNMP環境の構築について説明します。
このドキュメントには、ソフトウェアのインストールが含まれています。ソフトウェアのインストール方法を良く理解していることを確認して、[openSUSE環境でzypperによるソフトウェアのインストール](https://intl.cloud.tencent.com/document/product/213/2047)を参照してください。
LNMPの構成と使用バージョンについて説明する：
- Linux：Linuxシステムであり、本文ではopenSUSE42.3を使用する
- Nginx：Webサーバープログラムであり、Webアプリケーションを解析する。本文ではNginx1.14.2を使用する
- MySQL：データベースの管理システムであり、本文ではMySQL5.6.43を使用する
- PHP：WebサーバーはWebページを生成するプログラムであり、本文ではPHP7.0.7を使用する

## 操作手順
### イメージソースの設定
1. CVMにログインします。
2. 以下のコマンドを実行して、イメージソースを追加します。
```
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/oss suseOss
zypper ar https://mirrors.cloud.tencent.com/opensuse/distribution/leap/42.3/repo/non-oss suseNonOss
```
3. 以下のコマンドを実行して、イメージソースを更新します。
```
zypper ref
```

### Nginxをインストール・設定する
1. 以下のコマンドを実行して、Nginxをインストールします。
``` 
zypper install -y nginx
```
2. 以下のコマンドを順番に実行して、Nginxサービスを起動し、スタートアップを自動起動に設定します。
```
systemctl start nginx
systemctl enable nginx
```
3. 以下のコマンドを実行して、Nginx設定ファイルを修正します。
```
vim /etc/nginx/nginx.conf
```
4. 「** i **」或は「**Insert**」を押して、編集モードに切り替えます。
5. server{...}を検索し、以下の内容に置き換えます。
```
server {
	listen       80;
	server_name  localhost;

	#access_log  /var/log/nginx/host.access.log  main;
	location / {
			root   /srv/www/htdocs/;
			index  index.php index.html index.htm;
	}

	#error_page  404              /404.html;
	# redirect server error pages to the static page /50x.html
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
			root   /srv/www/htdocs/;
	}

	# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    location ~ \.php$ {
			root           /srv/www/htdocs/;
			fastcgi_pass   127.0.0.1:9000;
			fastcgi_index  index.php;
			fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
			include        fastcgi_params;
	}
}
```
7. 入力が完了したら、「**Esc**」を押し、「**:wq**」を入力して、ファイルを保存して戻ります。
8. 以下のコマンドを実行して、Nginxサービスをリスタートします。
```
systemctl restart nginx
```
9. 以下のコマンドを実行して、`index.html`ホームページを新規作成します。
```
vi /srv/www/htdocs/index.html
```
10. 「**i**」または「**Insert**」を押して、編集モードに切り替え、以下の内容を入力します：
```html
<p> hello world!</p>
```
10. 入力が完了したら、「**Esc**」を押し、「**:wq**」を入力して、ファイルを保存して戻ります。
11. ブラウザで、openSUSE CVM インスタンスのパブリックIPにアクセスして、Nginxサービスが正常に実行されているかを確認します。
下図に示すように、Nginxのインストール・設定が成功したことを表します。
![](https://main.qcloudimg.com/raw/df09d1fe6baed50cebd89ef7402db4b2.png)

### MySQLをインストール・設定する
1. 以下のコマンドを実行して、MySQLをインストールします。
```
zypper install -y mysql-community-server mysql-community-server-tools
```
2. 以下のコマンドを順番に実行して、MySQLサービスを起動し、スタートアップを自動起動に設定します。
```
systemctl start mysql 
systemctl enable mysql
```

3. 以下のコマンドを実行して、初めてMySQLにログインします。
> 初めてMySQLにログインする時、システムはパスワードを入力することを提示しますが、パスワードを入力しない場合は、「**Enter**」を押して、MySQLに入ります。
>
```
mysql -u root -p
```
下図に示すように、MySQLに正常に入りました。
![](https://main.qcloudimg.com/raw/1e9daf876fb08c70674789865688f695.png)
4. 以下のコマンドを実行して、rootパスワードを修正します。
```
update mysql.user set password = PASSWORD('ここで新しいパスワードを入力してください') where user='root';
```
5. 以下のコマンドを実行して、設定を有効にします。
```
flush privileges;
```
6. 以下のコマンドを実行して、MySQLを終了します。
```
\q
```

### PHPをインストール・設定する
以下のコマンドを実行して、PHPをインストールします。
```
zypper install -y php7 php7-fpm php7-mysql
```

### NginxはPHP-FPMと統合する
1. 以下のコマンドを順番に実行して、`/etc/php7/fpm`ディレクトリに移動して、`php-fpm.conf.default`ファイルをコピーして、`php-fpm.conf`ファイルにリネームします。
```
cd /etc/php7/fpm
cp php-fpm.conf.default php-fpm.conf
``` 
2. 以下のコマンドを順番に実行して、`/etc/php7/fpm/php-fpm.d`ディレクトリに移動して、`www.conf.default`ファイルをコピーして、`www.conf`にリネームします。
```
cd /etc/php7/fpm/php-fpm.d
cp www.conf.default www.conf
```
4. 以下のコマンドを順番に実行して、サービスを起動し、スタートアップを自動起動に設定します。
```
systemctl start php-fpm
systemctl enable php-fpm
```

## 環境設定の検証
1. 以下のコマンドを実行して、テストファイルindex.phpを作成します。
```
vim /srv/www/htdocs/index.php
```
2. 「**i**」或は「**Insert**」を押して、編集モードに切り替え、以下の内容を入力します：
```
<?php
	echo "hello new world!";
?>
```
3. 「**Esc」キーを押し、「**:wq**」を入力して、ファイルを保存して戻ります。
4. ブラウザーで、openSUSE CVMのパブリックIPにアクセスします。
下図に示すように、LNMP環境は正常に構築しました。
![](https://main.qcloudimg.com/raw/0adc6168e7407931c597228520b35413.png)

