LAMPとはLinux+Apache+Mysql/MariaDB+Perl/PHP/Pythonを指し、動的サイトまたはサーバーのオープンソースソフトウェアを構築するのによく使われます。プログラムはすべて独立していますが、一緒に使用されるため、それらの互換性がますます高まり、全体で強力なWebアプリケーションプログラムのプラットフォームとなっています。
この課程では以下の過程の完了までを説明します。：Tencent Cloudデータベースのインスタンスを起動し、CVMを介して1つのLAMPアプリケーションプログラムを設定し、Tencent Cloudデータベースのインスタンスの高可用性環境に接続する。
Tencent Cloudデータベースインスタンスを実行すると、データベースと環境のライフサイクルを分離します。これにより、複数のサーバーから同じデータベースに接続できるようになり、データベースのメンテナンスを簡略化されるため、データベースのインストール、設定、バージョンの更新および故障対応の問題を気にする必要がありません。

>本課程で使用したクラウドデータベースのインスタンスとCVMインスタンスは同じリージョンにあります。データベースのインスタンスとCVMインスタンスが同じリージョンにない場合は[外部ネットワークアクセス](https://intl.cloud.tencent.com/document/product/236/3130)をご参照ください。

### クラウドデータベースインスタンスの初期化
クラウドデータベースの購入と初期化については[購入方式](https://intl.cloud.tencent.com/document/product/236/5160) と[MySQLデータベースの初期化](http://intl.cloud.tencent.com/document/product/236/3128)をご参照ください。

### CVMインスタンスのログイン
CVMの購入とアクセスについては[クイックスタートLinux CVM](http://intl.cloud.tencent.com/document/product/213/2936)をご参照ください。この課程ではCentOSシステムを使用しています。

### MySQLクライアントのインストール
1. CVMインスタンスでは`yum`を使用してMySQLクライアントをインストールします。
```
yum install mysql -y
```
![](//mc.qcloudimg.com/static/img/8b952d6d7d767413a6558e82df092d44/image.png)
2. インストール完了後、Tencent Cloudのデータベースインスタンスに接続します。
```
mysql -h hostname -u username -p
```
![](//mc.qcloudimg.com/static/img/297856a53959582220b9bba6f06ce9f6/image.png)
このうち、hostnameはデータベースのインスタンスの内部ネットワークIPアドレスで、usernameはお客様のデータベースユーザー名です。
3. 接続できたら、データベースからすぐに退出し、次の手順の操作を行います。
```
quit;
```

### Apacheサービスのインストール
1. CVMインスタンスで`yum`を使用してApacheをインストールします。
```
yum install httpd -y
```
![](//mc.qcloudimg.com/static/img/dc142f813e8e8474a5994e2e841828f2/image.png)
2. Apacheサービスを起動します。
```
service httpd start
```
3. Apacheをテストします。
>!この手順では、CVMがセキュリティグループにおいて、設定ソースを**all**に設定し、ポートプロトコルを**TCP:80**のインバウンドルールにします。セキュリティグループの設定は[セキュリティグループ](http://intl.cloud.tencent.com/document/product/213/12452)をご参照ください。
>
ローカルのブラウザに`http://115.xxx.xxx.xxx/`（このうち`115.xxx.xxx.xxx`はCVMの公式サイトのIPアドレス）を入力し、下記の画面が現れたら、Apacheの起動に成功しています。
![](https://main.qcloudimg.com/raw/80941070a1a309ba484527473c915221.png)

### PHPのインストール 
1. CVMインスタンスで`yum`を使用してPHPをインストールします。
```
yum install php -y
```
![](//mc.qcloudimg.com/static/img/61a0864ddbb70e65c63ad5093e8165d4/image.png)

### 項目テストLAMP環境の作成
1. CVMの`/var/www/html`ディレクトリでinfo.phpファイルを1つ作成します。コード例は以下のとおりです。
```
<?php phpinfo(); ?>
```
2. Apacheサービスを再起動します。
```
service httpd restart
```
3. ローカルのブラウザに`http://0.0.0.0/info.php`、このうち`0.0.0.0`はCVMの公式サイトのIPアドレスを入力し、以下の画面が現れたら、LAMPサービスのデプロイに成功しています。
![](//mc.qcloudimg.com/static/img/0bc6667d122fe85d505fbe50b507b60a/image.png)
