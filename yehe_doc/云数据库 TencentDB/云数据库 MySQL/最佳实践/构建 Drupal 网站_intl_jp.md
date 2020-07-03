DrupalはPHP言語が作成したオープンソースのコンテンツ管理フレームワーク（Content Management Framework）を使用しています。コンテンツ管理システム（Content Management System）とPHP開発フレームワーク（Framework）で構成されます。Drupalは様々な機能とサービスを提供する動的Webサイトを構築するのに使用し、個人のブログから大型コミュニティ等の各種様々なネットワーク項目をサポートできます。
この課程では、Tencent CloudのCVM上でDrupalの電子商取引サイトを構築する方法が理解できます。
使用するソフトウェア環境はCentOS7.2、Drupal7.56、PHP5.4.16です。

### CVMインスタンスへのログイン


### Maria DBサービスのインストール
1. CentOS7以上のバージョンではデフォルトでMariaDBデータベースをサポートします。CVMインスタンスで`yum`を使用してMariaDBサービスをインストールします。
```
yum install mariadb-server mariadb -y
```
2. Maria DBサービスを起動します。
```
systemctl start mariadb
```
3. Drupalのデータベースを作成します。（この項目ではdrupalを使用してデータベース名にしています）
```
mysqladmin -u root -p create drupal
```
このうち、drupalはDrupalサービスを使用したデータベース名です。
3. データベースのユーザーを作成します。
```
mysql -u root -p
```
ユーザーを承認して、正常に承認されたら、データベースから退出します。
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON drupal.* TO 'username'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
exit
```
このうち、usernameはDrupalサービスを使用したデータベースユーザー名とし、passwordはDrupalサービスを使用したデータベースのパスワードとします。

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
>!この手順では、CVMがセキュリティグループにおいて、設定ソースを**all**に設定し、ポートプロトコルを**TCP:80**のインバウンドルールにします。セキュリティグループの設定は[セキュリティグループ](https://cloud.tencent.com/document/product/213/12452)をご参照ください。
>
ローカルのブラウザに`http://115.xxx.xxx.xxx/`（このうち`115.xxx.xxx.xxx`はCVMの公式サイトのIPアドレス）を入力し、下記の画面が現れたら、Apacheの起動に成功しています。
![](https://main.qcloudimg.com/raw/c9b20e150bd5330feef6d978b8308629.png)

### PHPのインストール 
1. CVMインスタンスで`yum`を使用してPHPおよびその拡張をインストールします。
```
yum install php php-dom php-gd php-mysql php-pdo -y
```
2. CVM`/var/www/html`ディレクトリ下でinfo.phpファイルを1つ作成してPHPのインストールが成功したか検査します。そのコード例は次のとおりです。
```
<?php phpinfo(); ?>
```
3. Apacheサービスを再起動します。
```
service httpd restart
```
4. ローカルのブラウザに`http://115.xxx.xxx.xxx/info.php`（このうち`115.xxx.xxx.xxx`はCVMの公式サイトのIPアドレス）を入力し、下記の画面が現れたら、PHPのインストールに成功しています。
![](//mc.qcloudimg.com/static/img/0bc6667d122fe85d505fbe50b507b60a/image.png)

### Drupalサービスのインストール
1. Drupalインストールパッケージをダウンロードします。
```
wget http://ftp.drupal.org/files/projects/drupal-7.56.zip
```
2. Webサイトルートディレクトリに解凍します。
```
unzip drupal-7.56.zip 
mv drupal-7.56/* /var/www/html/
```
3. 中国語翻訳パッケージをダウンロードします。
```
cd /var/www/html/
wget -P profiles/standard/translations http://ftp.drupal.org/files/translations/7.x/drupal/drupal-7.56.zh-hans.po
```
4. `sites`ディレクトリが属するマスターグループを修正します。
```
chown -R apache:apache /var/www/html/sites
```
5. Apacheサービスを再起動します。
```
service httpd restart
```
6. ローカルのブラウザに`http://115.xxx.xxx.xxx/`（このうち`115.xxx.xxx.xxx`はCVMの公式サイトのIPアドレス）を入力し、Drupalインストール画面に進みます。インストールバージョンを選択し、【Save and continue】をクリックします。
![](https://main.qcloudimg.com/raw/f52af1bb9822ddefc1989df9a0a95e8c.png)
7. 言語を選択し、【Save and continue】をクリックします。
![](https://main.qcloudimg.com/raw/11a8f788ebd0595e6afdff936656c2cc.png)
8. データベースを設定し、**mariadbのインストールサービス**に設定したデータベース情報を入力します。

9. サイト情報を入力します。
 
10. Drupalのインストールを完了させます。

11. その後は`http://115.xxx.xxx.xxx/`（このうち`115.xxx.xxx.xxx`はCVMの公式サイトのIPアドレス）にアクセスしてサイトに個別化設定を行うことができます。
