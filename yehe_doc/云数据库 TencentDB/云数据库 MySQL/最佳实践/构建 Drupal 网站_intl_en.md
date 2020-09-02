Drupalは、コンテンツ管理システムとPHP開発フレームワークで構成され、PHPで記述されたオープンソースのコンテンツ管理フレームワークです。個人のブログから大規模なコミュニティに至るまで、豊富な機能を備えた動的Webサイトを構築するために使用できます。
このチュートリアルでは、CVMインスタンスでDrupal電子商取引サイトを構築する方法について説明します。
ここで使用されるソフトウェア環境には、CentOS v7.2、Drupal v7.56、およびPHP v5.4.16が含まれます。

### CVMインスタンスへのログイン


### MariaDBサービスのインストール
1. CentOS7以上のバージョンではデフォルトでMariaDBデータベースをサポートします。CVMインスタンスで`yum`を使用してMariaDBサービスをインストールします。
```
yum install mariadb-server mariadb -y
```
2. MariaDBサービスを起動します。
```
systemctl start mariadb
```
3. Drupal用のデータベースを作成します。（この項目ではdrupalを使用してデータベース名にしています）
```
mysqladmin -u root -p create drupal
```
ここで、「drupal」は、Drupalサービスで使用されるデータベース名です。
3. データベースのユーザーを作成します。
```
mysql -u root -p
```
ユーザーを認証し、認証が成功したらデータベースを終了します。
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON drupal.* TO 'username'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
exit
```
ここで、「username」と「password」は、それぞれDrupalサービスで使用されるデータベースのユーザー名とパスワードです。

### Apacheサービスのインストール
1. CVMインスタンスで`yum`を使用してApacheをインストールします。
```
yum install httpd -y
```
2. Apacheサービスを起動します。
```
service httpd start
```
3. Apacheをテストします。
> この手順では、CVMインスタンスがセキュリティグループにおいて、ソースが**all**、ポートプロトコルが**TCP:80**であるインバウンドルールを設定する必要があります。セキュリティグループの設定方法の詳細については、[セキュリティグループ](https://cloud.tencent.com/document/product/213/12452)をご参照ください。
>
ローカルブラウザに`http://115.xxx.xxx.xxx/`（このうち`115.xxx.xxx.xxx`はCVMインスタンスのパブリックIPアドレス）を入力してください。次の画面が表示されたら、Apahceは正常に起動しています。
![](https://main.qcloudimg.com/raw/c9b20e150bd5330feef6d978b8308629.png)

### PHPのインストール 
1. CVMインスタンスで`yum`を使用してPHPおよびその拡張機能をインストールします。
```
yum install php php-dom php-gd php-mysql php-pdo -y
```
2. CVMインスタンスの`/var/www/html`ディレクトリにinfo.phpファイルを作成して、PHPが正常にインストールされているかどうかを確認します。そのコード例は次のとおりです。
```
<?php phpinfo(); ?>
```
3. Apacheサービスを再起動します。
```
service httpd restart
```
4. ローカルブラウザに`http://115.xxx.xxx.xxx/info.php`（このうち`115.xxx.xxx.xxx`はCVMインスタンスのパブリックIPアドレス）を入力してください。次の画面が表示されたら、PHPのインストールに成功しています。
![](//mc.qcloudimg.com/static/img/0bc6667d122fe85d505fbe50b507b60a/image.png)

### Drupalサービスのインストール
1. Drupalインストールパッケージをダウンロードします。
```
wget http://ftp.drupal.org/files/projects/drupal-7.56.zip
```
2. パッケージをWebサイトのルートディレクトリに解凍します。
```
unzip drupal-7.56.zip 
mv drupal-7.56/* /var/www/html/
```
3. 翻訳パッケージをダウンロードします。
```
cd /var/www/html/
wget -P profiles/standard/translations http://ftp.drupal.org/files/translations/7.x/drupal/drupal-7.56.zh-hans.po
```
4. `sites`ディレクトリが属する所有者とグループを変更します。
```
chown -R apache:apache /var/www/html/sites
```
5. Apacheサービスを再起動します。
```
service httpd restart
```
6. ローカルブラウザに`http://115.xxx.xxx.xxx/`（このうち`115.xxx.xxx.xxx`はCVMインスタンスのパブリックIPアドレス）を入力し、Drupalインストール画面に進みます。インストールするバージョンを選択し、【Save and continue】をクリックします。
![](https://main.qcloudimg.com/raw/f52af1bb9822ddefc1989df9a0a95e8c.png)
7. 言語を選択し、【Save and continue】をクリックします。
![](https://main.qcloudimg.com/raw/11a8f788ebd0595e6afdff936656c2cc.png)
8. データベースをセットアップし、**MariaDBサービスのインストール**時に設定したデータベース情報を入力します。

9. サイト情報を入力します。
 
10. Drupalのインストールプロセスを完了します。

11. その後は`http://115.xxx.xxx.xxx/`（このうち`115.xxx.xxx.xxx`はCVMのパブリックIPアドレス）にアクセスして、Webサイトをカスタマイズできます。
