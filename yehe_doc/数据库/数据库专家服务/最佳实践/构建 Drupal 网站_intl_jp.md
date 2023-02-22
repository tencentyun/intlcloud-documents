Drupalは、PHP言語で記述されたオープンソースのコンテンツ管理フレームワーク(Content Management Framework)であり、コンテンツ管理システム(Content Management System)とPHP開発フレームワーク(Framework)で構成されます。Drupalは、さまざまな機能とサービスを提供するダイナミックウェブサイトを構築するために使用でき、個人のブログから大規模なコミュニティまで、さまざまなアプリケーションのウェブサイトプロジェクトをサポートできます。
このチュートリアルを通じて、Cloud Virtual Machine(CVM)でDrupal eコマースウェブサイトを構築する方法を学ぶことができます。
使用するソフトウェア環境：CentOS7.2、Drupal7.56、PHP5.4.16。

### CVMインスタンスへのログイン
CVMの購入とアクセスについては、[Linux CVMのクイックスタート](https://www.tencentcloud.com/document/product/213/10517)をご参照ください。

### MariaDBサービスのインストール
1. CentOS7以降のバージョンはデフォルトでMariaDBデータベースをサポートするため、MariaDBデータベースを使用します。CVMインスタンスでは、`yum`を使用してMariaDBサービスをインストールします。
```
yum install mariadb-server mariadb -y
```
2. MariaDBサービスを起動します。
```
systemctl start mariadb
```
3. Drupal用のデータベースを作成します。（このプロジェクトは、データベース名としてdrupalを使用します）
```
mysqladmin -u root -p create drupal
```
ここで、drupalはDrupalサービスが使用するデータベース名です。
3. データベースのユーザーを作成します。
```
mysql -u root -p
```
ユーザーを承認し、承認が成功したらデータベースを終了します。
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON drupal.* TO 'username'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
exit
```
ここで、usernameはDrupalサービスが使用するデータベースのユーザー名で、passwordはDrupalサービスが使用するデータベースのパスワードです。

### Apacheサービスのインストール
1. CVMインスタンスでは、`yum`を使用してApacheをインストールします。
```
yum install httpd -y
```
2. Apacheサービスを起動します。
```
service httpd start
```
3. Apacheをテストします。
>!この手順では、CVMは、セキュリティグループでソースを**all**、ポートプロトコルを**TCP:80**とするインバウンドルールを構成する必要があります。セキュリティグループ構成については、[セキュリティグループ](https://intl.cloud.tencent.com/document/product/213/12452)をご参照ください。
>
ローカルブラウザに`http://115.xxx.xxx.xxx/`（ここで、`115.xxx.xxx.xxx`はCVMのパブリックネットワークIPアドレス）を入力すると、次の画面が表示され、Apacheが正常に起動しました。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/uIMz720_4.png)

### PHPのインストール 
1. CVMインスタンスでは、`yum`を使用してPHPおよびその拡張機能をインストールします。
```
yum install php php-dom php-gd php-mysql php-pdo -y
```
2. CVMの`/var/www/html`ディレクトリ下で、info.phpフォルダを作成してPHPが正常にインストールされたかどうかを確認します。サンプルコードは次の通りです：
```
<?php phpinfo(); ?>
```
3. Apacheサービスを再起動します。
```
service httpd restart
```
4. ローカルブラウザに`http://115.xxx.xxx.xxx/info.php`（ここで、`115.xxx.xxx.xxx`はCVMのパブリックネットワークIPアドレス）を入力すると、次の画面が表示され、PHPが正常にインストールされました。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/sphx991_5.png)

### Drupalサービスのインストール
1. Drupalインストールパッケージをダウンロードします。
```
wget http://ftp.drupal.org/files/projects/drupal-7.56.zip
```
2. ウェブサイトのルートディレクトリに解凍します。
```
unzip drupal-7.56.zip 
mv drupal-7.56/* /var/www/html/
```
3. 中国語翻訳パッケージをダウンロードします。
```
cd /var/www/html/
wget -P profiles/standard/translations http://ftp.drupal.org/files/translations/7.x/drupal/drupal-7.56.zh-hans.po
```
4. `sites`ディレクトリの所有者グループを変更します。
```
chown -R apache:apache /var/www/html/sites
```
5. Apacheサービスを再起動します。
```
service httpd restart
```
6. ローカルブラウザに`http://115.xxx.xxx.xxx/`（ここで、`115.xxx.xxx.xxx`はCVMのパブリックネットワークIPアドレス）を入力すると、Drupalのインストールインターフェースに進みます。インストールするバージョンを選択し、【Save and continue】をクリックします。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Bzap853_6.png)
7. インストールする言語を選択し、【Save and continue】をクリックします。
8. データベースを設定し、**mariadbサービスのインストール**で構成したデータベース情報を入力します。
9. サイト情報を入力します。
10. Drupalのインストールを完了します。
11. その後で、`http://115.xxx.xxx.xxx/`（ここで、`115.xxx.xxx.xxx`はCVMのパブリックネットワークIPアドレス）にアクセスして、ウェブサイトをパーソナライズ設定することができます。
