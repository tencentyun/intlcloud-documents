## ユースケース

Discuz!は、世界で最も成熟し、最も広範なフォーラムウェブサイトのソフトウェアシステムの1つであり、200万以上のウェブサイトユーザーによって使用されています。 Discuz! を通じてフォーラムを構築できます。本ドキュメントでは、Tencent Cloud CVMで Discuz! フォーラムの構築と必要な LAMP（Linux + Apache + MariaDB + PHP）環境について説明します。


 Discuz! フォーラムを構築するには、 Linuxコマンドに精通している必要があります。例えば[CentOS環境におけるYUMによるソフトウェアをインストールする](https://intl.cloud.tencent.com/document/product/213/2046) 等の通常コマンド。また、インストールするソフトウェアの利用及びバージョン間の互換性を把握することも必要です。

## 事例のソフトウェアバージョン
この記事で作成したDiscuz!フォーラムソフトウェアのバージョンと説明は次の通り：
- Linux：LinuxOS、この記事では、CentOS 7.5 を例とします。
- Apache：Webサーバー、この記事では、 Apache 2.4.15 を例とします。
- MariaDB：データベース、この記事では、 MariaDB 5.5.60 を例とします。
- PHP：スクリプト言語、この記事では、PHP 5.4.16を例とします。
- Discuz!：フォーラムウェブサイトソフトウェア、この記事では、Discuz! X3.2を例とします。


## 操作手順
### 手順１：CVMにログインする
[標準のログイン方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作習慣に応じて、他のログイン方法を選択することもできます：
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSHを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)



### 手順2：LAMP環境の構築 

CentOSシステムの場合、Tencent CloudはCentOS公式のソフトウェアと同期するソフトウェアインストールソースを提供します。同梱されているソフトウェアは現在最も安定したバージョンであり、Yumから直接インストールできます。

<span id="InstallNecessarySoftware"></span>
#### 必要なソフトウェアをインストールして設定する
1. 次のコマンドを実行して、必要なソフトウェアをインストールします（Apache、MariaDB、PHP）：
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server -y
```
2. 下記のコマンドを実行し、サービスを実行します。
```
systemctl start httpd
systemctl start mariadb
systemctl start php-fpm
```
3. <span id="step3"></span>次のコマンドを実行して、rootユーザーがデータベースにアクセスできるためにrootアカウントのパスワードと基本設定を設置します。
>
>- 初期でMariaDBにログインする前に、次のコマンドを実行してユーザーパスワードと基本設定にアクセスします。
>- 初期でrootアカウントのパスワードを入力した後に、エンターキーを押し（rootパスワードの設定時にインターフェースがデフォルトで表示されない）、再度入力して確認します。 インターフェースのプロンプトに従って、基本設定を完了します。
> 
```
mysql_secure_installation
```
4. 次のコマンドを実行し、MariaDBにログインして、[手順3](#step3)で設定したパスワードを入力し、「**Enter**」を押します。
```
mysql -u root -p
``` 
設定したパスワードを入力してMariaDBにログインできる場合、設定は正しいです。 下記画像に示すように：
![](https://main.qcloudimg.com/raw/e22b91cc30bf4155436ab398ee44502a.png)

5. 下記のコマンドを実行し、 MariaDBデータベースから退出します。
```
exit
```

#### 環境設定の検証

環境構築の成功を確認および保証するために、次の操作で検証できます：
1. 次のコマンドを実行して、Apacheのデフォルトルートディレクトリ `/var/www/html` にテストファイル `test.php` を作成します。
```
vim /var/www/html/test.php
```
2. 「**i**」を押して編集モードに切り替え、下記のように記述します：
```
<?php
echo "<title>Test Page</title>";
phpinfo()
?>
```
3.  「**Esc**」を押し、「**:wq**」を入力し、ファイルを保存して戻ります。
4. ブラウザで、`test.php`ファイルにアクセスして、環境設定が成功したかどうかを確認します。
```
http://CVMのパブリックIP IP/test.php 
```
次の画面が表示されたら、LAMP環境の設定に成功しました。
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)



<span id="InstallDiscuz"></span>
### 手順3：Discuz!のインストールと設定  

####  Discuz!をダウンロードする 
次のコマンドを実行して、インストールパッケージをダウンロードします。
```
wget http://download.comsenz.com/DiscuzX/3.2/Discuz_X3.2_SC_UTF8.zip
```

#### インストールの準備
1. 次のコマンドを実行して、インストールパッケージを解凍します。
```
unzip Discuz_X3.2_SC_UTF8.zip
```
2. 次のコマンドを実行して、解凍後の「upload」フォルダー内のすべてのファイルを`/var/www/html/`にコピーします。
```
cp -r upload/* /var/www/html/
```
3. 次のコマンドを実行して、他のユーザーに書き込み権限を付与します。
```
chmod -R 777 /var/www/html
```

#### Discuz!をインストールする
1. Webブラウザーのアドレスバーに、Discuz! サイトのIPアドレス（即ちCVMインスタンスのパブリックIPアドレス）を入力すると、Discuz！インストールインターフェースが表示されます。 <!--下記画像に示すように：
![インストール1](https://mc.qcloudimg.com/static/img/ad97b179b5b4977d86ca09a78ef05a7d/image.png)-->
2. 【同意する】をクリックして、インストール環境の確認画面に入ります。 <!--下記画像に示すように：
![インストール2](https://mc.qcloudimg.com/static/img/c5a521673ed6f1a3528ba67ca5886ee4/image.png)-->
3. カレントの状態が正常であることを確認し、【次へ】をクリックして動作環境の設定画面に入ります。<!--下記画像に示すように：
![インストール3](https://mc.qcloudimg.com/static/img/11a44bd86bfdfcd1fe3dcce6e8f200e6/image.png)-->
4. 新規インストールを選択し、【次へ】をクリックしてデータベースの作成画面に入ります。<!--下記画像に示すように：
![インストール4の変更](https://mc.qcloudimg.com/static/img/5d5184cfb34f98d791c243273b910065/image.png)-->
5. 画面のプロンプトに従って、情報を記入し、Discuz!のデータベースを作成します。
>
>- [必要なソフトウェアのインストール](#InstallNecessarySoftware) で設定したrootアカウントとパスワードを利用してデータベースに接続します。また、システムメールボックス、管理者アカウント、パスワード、および Emailを設定してください。
>- 管理者ユーザーとパスワードを覚えておいてください。
>
6. 【次へ】をクリックしてインストールを開始します。
6. インストールが完了したら、【フォーラムがインストールされました。ここをクリックしてアクセスしてください】をクリックして、フォーラムにアクセスできます。<!--下記画像に示すように：
![インストール5](https://mc.qcloudimg.com/static/img/41dab1ec86120a565bdd790238f271da/image.png)-->


## よくある質問
CVMの使用中に問題があれば、下記のドキュメントを参照しながら実際状況に合わせ分析した上問題を解決することが可能です。
- CVMのログインに関する問題は、 [パスワードとキー]](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)をご参照ください。
- CVMネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)をご参照ください。
- CVMディスクの問題は、[システムディスクとデータディスク](https://intl.cloud.tencent.com/document/product/213/17351)を参照してください。
 
