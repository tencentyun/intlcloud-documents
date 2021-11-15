LAMP (Linux + Apache + MySQL/MariaDB + Perl/PHP/Python) は、動的サイトまたはサーバーのセットアップによく使用されるオープンソースソフトウェアです。プログラムはすべて独立していますが、一緒に使用されるため、それらの互換性がますます高まり、全体で強力なWebアプリケーションプラットフォームとなっています。
このチュートリアルでは、TencentDBインスタンスを起動し、CVMインスタンスを使用してLAMPアプリケーションを構成して、TencentDBインスタンスの高可用性環境に接続するプロセスについて説明します。
TencentDBインスタンスを実行した後、データベースと環境のライフサイクルを分離します。これにより、複数のサーバーを同じデータベースに接続できるようになり、データベースのメンテナンスを簡略化されるため、データベースのインストール、設定、バージョンの更新および故障対応の問題を気にする必要がありません。

>本チュートリアルで使用したTencentDBインスタンスとCVMインスタンスは同じリージョンにあります。TencentDBインスタンスとCVMインスタンスが同じリージョンにない場合は、[パブリックネットワークアクセス](https://intl.cloud.tencent.com/document/product/236/3130)をご参照ください。

### TencentDBインスタンスの初期化
TencentDBインスタンスを購入して初期化する方法の詳細については、[購入方式](https://intl.cloud.tencent.com/document/product/236/5160) と[MySQLデータベースの初期化](http://intl.cloud.tencent.com/document/product/236/3128)をご参照ください。

### CVMインスタンスへのログイン
CVMインスタンスの購入とアクセスについては、[Linux CVMのクイックスタート](http://intl.cloud.tencent.com/document/product/213/2936)をご参照ください。このチュートリアルではCentOSを使用します。

### MySQLクライアントのインストール
1. CVMインスタンスでは`yum`を使用してMySQLクライアントをインストールします。
```
yum install mysql -y
```
![](//mc.qcloudimg.com/static/img/8b952d6d7d767413a6558e82df092d44/image.png)
2. インストール完了後、TencentDBインスタンスに接続します。
```
mysql -h hostname -u username -p
```
![](//mc.qcloudimg.com/static/img/297856a53959582220b9bba6f06ce9f6/image.png)
このうち、hostnameはTencentDBインスタンスのプライベートIPアドレスで、usernameははデータベースのユーザー名です。
3. 接続が成功したら、インスタンスを閉じて次のステップに進むことができます。
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
>!この手順では、CVMインスタンスがセキュリティグループにおいて、ソースが**all**、ポートプロトコルが**TCP:80**であるインバウンドルールを構成する必要があります。セキュリティグループの設定方法の詳細については、[セキュリティグループ](http://intl.cloud.tencent.com/document/product/213/12452)をご参照ください。
>
ローカルブラウザに`http://115.xxx.xxx.xxx/`（このうち`115.xxx.xxx.xxx`はCVMインスタンスのパブリックIPアドレス）を入力し、次の画面が表示されたら、Apacheの起動に成功しています。
![](https://main.qcloudimg.com/raw/80941070a1a309ba484527473c915221.png)

### PHPのインストール 
1. CVMインスタンスで`yum`を使用してPHPをインストールします。
```
yum install php -y
```
![](//mc.qcloudimg.com/static/img/61a0864ddbb70e65c63ad5093e8165d4/image.png)

### LAMP環境をテストするプロジェクトの作成
1. CVMインスタンスの`/var/www/html`ディレクトリでinfo.phpファイルを1つ作成します。コード例は以下のとおりです。
```
<?php phpinfo(); ?>
```
2. Apacheサービスを再起動します。
```
service httpd restart
```
3. ローカルブラウザに `http://0.0.0.0/info.php`（このうち`0.0.0.0`はCVMインスタンスのパブリックIPアドレス）を入力し、次の画面が表示されたら、LAMPサービスのデプロイに成功しています。
![](//mc.qcloudimg.com/static/img/0bc6667d122fe85d505fbe50b507b60a/image.png)
