## 操作ケース
LNMP環境とは、LinuxOSでのNginx+MySQL/MariaDB+PHPで構成されるウェブサイトサーバーアーキテクチャです。このドキュメントは、Tencent Cloud Virtual Machine(CVM)でLNMP環境を手動で構築する方法について説明します。

LNMP環境を手動で構築するには、Linuxコマンドだけではなく、インストールされているソフトウェアの使用方法とバージョンの互換性についても精通している必要があります。

## サンプルソフトウェアバージョン
このドキュメントでは、LNMP環境の構築に使用されるソフトウェアのバージョンと説明は次のとおりです。
Linux：Linux OS。このドキュメントでは、CentOS8.0を例として説明します。
Nginx：Webサーバー。このドキュメントはNginx1.18.0を例として説明します。
MySQL：データベース。このドキュメントはMySQL8.0.21を例として説明します。
PHP：スクリプト言語。このドキュメントはPHP7.4.11を例とします。

## 前提条件
Linux CVMが必要です。Linux CVMを購入していない場合は、[Linux CVM構成のカスタマイズ](https://intl.cloud.tencent.com/document/product/213/10517)をご参照ください。

## 操作手順
### ステップ1：Linuxインスタンスへのログイン
[Linuxインスタンスに標準的な方法でログインします（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます：
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインします](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSHを使用してLinuxインスタンスにログインします](https://intl.cloud.tencent.com/document/product/213/32501)

### ステップ2：Nginxのインストールと設定
1. 以下のコマンドを実行して、Nginxをインストールします。
>?このドキュメントは、Nginx1.18.0のインストールを例に説明します。[Ngingx公式インストールパッケージ](http://nginx.org/packages/centos/8/x86_64/RPMS/?spm=a2c4g.11186623.2.31.557423bfYPMd6u)からCentOS8のための他のバージョンを入手できます。
>
```
dnf -y install http://nginx.org/packages/centos/8/x86_64/RPMS/nginx-1.18.0-1.el8.ngx.x86_64.rpm
```
2. 次のコマンドを実行して、Nginxバージョンを確認します。
```
nginx -v
```
以下のような結果が返されると、インストールが完了しました。
```
nginx version: nginx/1.18.0
```
3. 次のコマンドを実行して、Nginxコンフィグレーションファイルのパスを確認します。
```
cat /etc/nginx/nginx.conf
```
include構成エントリの`/etc/nginx/conf.d/*.conf`が、Nginxコンフィグレーションファイルのデフォルトパスであることを確認できます。
4. 次のコマンドを実行して、コンフィグレーションファイルのデフォルトパスでバックアップを行います。
```
cd /etc/nginx/conf.d
```
```
cp default.conf default.conf.bak
```
5. 次のコマンドを実行してdefault.confファイルを開きます。
6. **i**を押して編集モードに切り替え、default.confファイルを編集します。
  1. locationのindexエントリにindex.phpを追加します。以下の通りです。
![](https://main.qcloudimg.com/raw/32df0b8ba82278cd96cf86152738677e.png)
  2. location ~ \.php$前の`#`を削除し、次の構成エントリを変更します。
    - rootエントリ（すなわち、locationのrootエントリ）をユーザーのWebサイトのルートディレクトリに変更し、このドキュメントは、`/usr/share/nginx/html;`を例に説明します。
    - fastcgi_passエントリを`unix:/run/php-fpm/www.sock;`に変更します。NginxはUNIXソケットを介してPHP−FPMとの接続を確立します。この設定は`/etc/php-fpm.d/www.conf`ファイル内のlistenの設定と一致します。
    - fastcgi_param  SCRIPT_FILENAME後の`$document_root$fastcgi_script_name;`を`$document_root$fastcgi_script_name;`に変更します。
    変更した後は以下の通りです。
![](https://main.qcloudimg.com/raw/2e4bff09d70399881bfbf995390a58d3.png) 
7. 「**Esc**」を押し、「**:wq**」を入力し、ファイルを保存してから戻ります。
8. 次のコマンドを順次実行して、NTPDを起動し、OS起動時にNTPDが自動で起動してくれるように設定します。
```
systemctl start nginx
```
```
systemctl enable nginx
```

### ステップ3：MySQLのインストールと設定
1. 以下のコマンドを実行して、MySQLをインストールします。
```
dnf -y install @mysql
```
2. 次のコマンドを実行して、MySQLバージョンを確認します。
```
mysql -V
```
以下のような結果が返されると、インストールが完了しました。
```
mysql  Ver 8.0.21 for Linux on x86_64 (Source distribution)
```
3. 次のコマンドを順次実行して、MySQLを起動し、OS起動時にMySQLが自動で起動してくれるように設定します。
```
systemctl enable --now mysqld
```
```
systemctl status mysqld
```
4. 次のコマンドを実行し、MySQLのセキュリティ操作を実行し、パスワードを設定します。
```
mysql_secure_installation
```
次のステップに従って、対応する操作を実行します。
  1. `y`を入力し、**Enter**を押して関連設定を開始します。
  2. パスワード認証ポリシーの強度を選択します。強度の高いパスワード認証ポリシーを選択することをお勧めします。`2`を入力して**Enter**を押します。
    - 0：低い。
    - 1：一般。
    - 2：高い。
  3. MySQLパスワードを設定して確認します。入力されたパスワードはデフォルトでは表示されません。
  4. `y`を入力して**Enter**を押し、パスワードを再入力します。
  5. `y`を入力して**Enter**を押し、匿名ユーザーを削除します。
  6. MySQLへのリモート接続を許可するかどうかを設定します。
    - 必要がない場合：`y`を入力し、**Enter**を押します。
    - 必要な場合：`n`を入力し、**Enter**を押します。
  7. `y`を入力して**Enter**を押し、testライブラリを削除し、testライブラリへのアクセス権を削除します。
  8. `y`を入力して**Enter**を押し、認証テーブルをもう一度読み込みます。

### ステップ4：PHPのインストールと設定
1. 次のコマンドを順次実行して、epelソースを追加して更新します。
```
dnf -y install epel-release
```
```
dnf update epel-release
```
2. 次のコマンドを順次実行して、キャッシュされている不要なパッケージを削除し、ソフトウェアソースを更新します。
```
dnf clean all
```
```
dnf makecache
```
3. 次のコマンドを実行して、remiソースをインストールします。
>?PHP 7.4.11をインストールするにはremiソースをインストールする必要があります。実際にインストールされているPHPのバージョンに合わせてこのコマンドを実行してください。
>
```
dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
```
4. 次のコマンドを実行して、PHP7.4モジュールを起動します。
```
dnf module install php:remi-7.4
```
5. 次のコマンドを実行して、必要なPHPモジュールをインストールします。
```
dnf install php php-curl php-dom php-exif php-fileinfo php-fpm php-gd php-hash php-json php-mbstring php-mysqli php-openssl php-pcre php-xml libsodium
```
6. 次のコマンドを実行して、PHPバージョンを確認します。
```
php -v
```
以下のような結果が返されると、インストールが完了しました。
```
PHP 7.4.11 (cli) (built: Sep 29 2020 10:17:06) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Zend OPcache v7.4.11, Copyright (c), by Zend Technologies
```
7. 次のコマンドを実行して、www.confファイルを開きます。
```
vi /etc/php-fpm.d/www.conf
```
8. **i**を押して編集モードに切り替え、www.confファイルを編集します。
9. user = apacheとgroup = apacheをuser = nginxとgroup = nginxに変更します。以下の通りです。
![](https://main.qcloudimg.com/raw/ceb9c202ebe56c9bd9265e86c0ad2333.png)
10. 「**Esc**」を押し、「**:wq**」を入力し、ファイルを保存してから戻ります。
11. 次のコマンドを順次実行して、PHP-FPMを起動し、OS起動時にPHP-FPMが自動で起動してくれるように設定します。
```
systemctl start php-fpm
```
```
systemctl enable php-fpm
```

#### 環境設定の検証
1. 以下のコマンドを実行して、テストファイルを作成します。
>? `/usr/share/nginx/html`は、Nginxで設定されているWebサイトのルートディレクトリであり、このドキュメントはこのディレクトリを例として説明します。
>
```
echo "<?php phpinfo(); ?>" >> /usr/share/nginx/html/index.php
```
2. ローカルブラウザで次のアドレスにアクセスして、環境設定に成功したかどうかを確認します。インスタンスのパブリックIPアドレスを取得する方法の詳細については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
```
http://云服务器实例的公网 IP/index.php
```
以下のような結果が表示されたら、環境設定に成功したことを示しています。
![](https://main.qcloudimg.com/raw/182c0f73df20d66216a9b73d571b2093.png)

## 関連する操作
LNMP環境の構築が完了した後、CVMに関する機能をより多く理解と把握するために、[WordPressパーソナルサーバーを手動で構築](https://intl.cloud.tencent.com/document/product/213/8044)できます。

## よくあるご質問

CVMの使用中に問題が発生した場合は、下記のドキュメントを参照して、実際の状況に応じて問題を分析して解決できます。

- CVMのログインに関する問題は、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)をご参照ください。
- CVMのネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)をご参照ください。
- CVMのハードディスクに関する問題は、[システムディスクとデータディスク](https://intl.cloud.tencent.com/document/product/213/17351)をご参照ください。

