## 概要

Discuz!は、成熟度が最も高く、世界最大のフォーラムWebサイトのソフトウェアシステムの1つであり、200万人を超えるWebサイトユーザーによって使用されています。 Discuz! を通じてフォーラムを構築できます。本ドキュメントでは、Tencent Cloud CVMインスタンスで Discuz! フォーラムと必要な LAMP（Linux + Apache + MariaDB + PHP）環境を構築する方法について説明します。


手動でDiscuz! フォーラムを構築するには、Linux コマンド（例：[CentOS環境でのYUMを使用してソフトウェアのインストール](https://cloud.tencent.com/document/product/213/2046)）等の常用コマンドに精通している必要があります。また、インストールされているソフトウェアの使い方及びバージョン間の互換性について十分に理解している必要があります。






## ソフトウェアのバージョン
この記事で作成したDiscuz!フォーラムソフトウェアのバージョンと説明は次の通り：
- Linux：Linux OS、本ドキュメントはCentOS 7.6を例として説明します。
- Apache：Webサーバー、この記事では、 Apache 2.4.15 を例として説明します。
- MariaDB：データベース、この記事では、 MariaDB 5.5.60を例として説明します。
- PHP：スクリプト言語、この記事では、PHP 5.4.16を例として説明します。
- Discuz!：フォーラムウェブサイトソフトウェア、この記事では、Discuz! X3.4を例として説明します。


## 操作手順
### ステップ1：CVMにログインする
[標準的な方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます：
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSHキーを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)



### 手順2：LAMP環境を構築する 

CentOSシステムの場合、Tencent CloudはCentOS公式のソフトウェアと同期するソフトウェアインストールソースを提供します。同梱されているソフトウェアは現在最も安定したバージョンであり、Yumを介して直接インストールできます。


#### 必要ソフトウェアをインストールして設定する[](id:InstallNecessarySoftware)
1. 次のコマンドを実行して、必要なソフトウェア（Apache、MariaDB、PHP、Git）をインストールします：
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server git -y
```
2. 下記のコマンドを順に実行して、サービスを起動します。
```
systemctl start httpd
```
```
systemctl start mariadb
```
```
systemctl start php-fpm
```
3. [](id:step3)次のコマンドを実行して、rootアカウントのパスワードと基本構成を設定し、rootユーザーがデータベースにアクセスできるようにします。
<dx-alert infotype="notice" title="">
- MariaDBに初めてログインする前に、次のコマンドを実行してユーザーパスワードの入力と基本設定を行います。
- rootパスワードの入力を求めるプロンプトが初めて表示されたら、 **Enter**を押して rootパスワード設定手順に直接進みます。rootパスワードは設定の際、デフォルトでは画面に表示されません。画面上の指示に従ってその他の基本構成を順に完了してください。
</dx-alert>
```
mysql_secure_installation
```
4. 次のコマンドを実行し、MariaDBにログインして、[手順3](#step3)で設定したパスワードを入力し、**Enter**キーを押します。
```
mysql -u root -p
```
設定したパスワードを入力してMariaDBにログインできる場合、設定は正しいことを示します。 次の図に示すように：
![](https://main.qcloudimg.com/raw/18c54971e141db38c3f483161fefe251.png)
5. 次のコマンドを実行し、 MariaDBデータベースを終了します。
```
\q
```

#### 環境設定の検証

環境が正常に構築されていることを確認するには、次の操作を実行して検証できます：
1. 次のコマンドを実行して、Apacheのデフォルトのルートディレクトリ `/var/www/html` にテストファイル `test.php` を作成します。
```
vim /var/www/html/test.php
```
2. **i**キーを押して編集モードに切り替え、次のように書き込みます。
```
<?php
echo "<title>Test Page</title>";
phpinfo()
?>
```
3. **Esc**を押し、**:wq**を入力して、ファイルを保存して戻ります。
4. ブラウザで、`test.php`ファイルにアクセスして、環境設定が成功したかどうかを確認します。
```
http://CVMのパブリックIP/test.php 
```
次の画面が表示されたら、LAMP環境が正常に設定されていることを示しています。
![](https://main.qcloudimg.com/raw/f511b15ac3016d710c2b1f833e69448d.png)




### 手順3：Discuz!のインストールと設定  [](id:InstallDiscuz)

####  Discuz!をダウンロードする 
次のコマンドを実行して、インストールパッケージをダウンロードします。
```
git clone https://gitee.com/Discuz/DiscuzX.git
```

#### インストールの準備作業
1. 次のコマンドを実行して、ダウンロードしたインストールディレクトリに入ります。
```
cd DiscuzX
```
2. 次のコマンドを実行して、「upload」フォルダ内のすべてのファイルを `/var/www/html/`にコピーします。
```
cp -r upload/* /var/www/html/
```
3. 次のコマンドを実行して、他のユーザーに書き込み権限を割り当てます。
```
chmod -R 777 /var/www/html
```

#### Discuz!をインストールする
1. Webブラウザのアドレスバーに、Discuz!サイトのIPアドレス（CVMインスタンスのパブリックIPアドレス）、または[関連操作](#ConfigureDomain) で取得した利用可能なドメイン名を入力すると、Discuz!インストールインターフェースが表示されます。
<dx-alert infotype="explain" title="">
本ドキュメントでは、インストール手順のみ示しています。低いバージョンであるというセキュリティアラートが表示された場合、より高いバージョンのイメージを使用することを推奨します。
</dx-alert>
2. **同意する**をクリックして、インストール環境の確認ページに進みます。
3. 現在のステータスが正常であることを確認して、 **次のステップ**をクリックし、実行環境の設定ページに進みます。
4. クリーンインストールを選択して、**次のステップ**をクリックし、データベースの作成ページに進みます。
5. 画面上の指示に従って、情報を記入し、Discuz!のデータベースを作成します。
<dx-alert infotype="notice" title="">
- [必要なソフトウェアのインストール](#InstallNecessarySoftware) で設定したrootアカウントとパスワードを利用してデータベースに接続し、システムメールボックス、管理者アカウント、パスワード、およびEmailを設定してください。
- 管理者ユーザーとパスワードを覚えておいてください。
</dx-alert>
6. **次のステップ**をクリックしてインストールを開始します。
6. インストールが完了したら、**フォーラムのインストールが完了しました。ここをクリックしてアクセスしてください**をクリックすれば、フォーラムにアクセスできます。


## 関連操作[](id:ConfigureDomain)
自分のDiscuz!フォーラム個別のドメイン名を設定できます。ユーザーは複雑なIPアドレスを使用せずに、覚えやすいドメイン名でWebサイトにアクセスできます。一部のユーザーは学習目的でのみのフォーラムの構築に、IPを使って直接インストールして臨時に使用する場合がありますが、このような操作はお勧めしません。


## よくあるご質問
CVMの使用中に問題が発生した場合は、下記のドキュメントを参照しながら実際状況に合わせ分析した上で問題を解決することが可能です。
- CVMのログインに関する問題は、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)ドキュメントをご参照ください。
- CVMのネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)ドキュメントをご参照ください。
- CVMのハードディスクに関する事項については、[システムディスクとデータディスク](https://intl.cloud.tencent.com/zh/document/product/213/17351)をご参照ください。



