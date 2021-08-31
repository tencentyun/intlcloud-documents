## シナリオ

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
### 手順１：CVMにログインする
[標準的な方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます：

- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSHを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)



### 手順2：LAMP環境を構築する 

CentOSシステムの場合、Tencent CloudはCentOS公式のソフトウェアと同期するソフトウェアインストールソースを提供します。同梱されているソフトウェアは現在最も安定したバージョンであり、Yumを介して直接インストールできます。

<span id="InstallNecessarySoftware"></span>
#### 必要なソフトウェアをインストールして設定する
1. 次のコマンドを実行して、必要なソフトウェア（Apache、MariaDB、PHP、Git）をインストールします：
```
yum install httpd php php-fpm php-mysql mariadb mariadb-server git -y
```
2. 下記のコマンドを実行し、サービスを起動します。
```
systemctl start httpd
```
```
systemctl start mariadb
```
```
systemctl start php-fpm
```
3. <span id="step3"></span>次のコマンドを実行して、rootアカウントのパスワードと基本構成を設定し、rootユーザーがデータベースにアクセスできるようにします。
>!
>- 次のコマンドを実行して、MariaDBに初めてログインする前にパスワードを設定します。
>- rootパスワードの入力を求めるプロンプトが表示されたら、 **Enterキー**を押してパスワードを設定します。デフォルトでは、パスワードは表示されません。画面上の指示に従って基本設定を完了します。
> 
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
2. 「**i**」を押して編集モードに切り替え、次のように書き込みます。
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



<span id="InstallDiscuz"></span>
### 手順3：Discuz!のインストールと設定  

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
2. 次のコマンドを実行して、「upload」フォルダー内のすべてのファイルを`/var/www/html/`にコピーします。
```
cp -r upload/* /var/www/html/
```
3. 次のコマンドを実行して、他のユーザーに書き込み権限を割り当てます。
```
chmod -R 777 /var/www/html
```

#### Discuz!をインストールする
1. Webブラウザのアドレスバーに、Discuz!サイトのIPアドレス（CVMインスタンスのパブリックIPアドレス）、または[関連操作](#ConfigureDomain)で取得した利用可能なドメイン名を入力して、 Discuz!インストールインターフェイスが表示されます。
2. 【同意する】をクリックして、インストール環境の確認画面に入ります。 
3. 【次へ】をクリックして動作環境設定画面に入ります。
4. 新規インストールを選択し、【次へ】をクリックしてデータベースの作成画面に入ります。
5. 画面上の指示に従って、情報を記入し、Discuz!のデータベースを作成します。
>!  
>- [必要なソフトウェアのインストール](#InstallNecessarySoftware) で設定したrootアカウントとパスワードを利用してデータベースに接続します。また、システムメールボックス、管理者アカウント、パスワード、および Emailを設定してください。
>- 管理者ユーザーとパスワードを覚えておいてください。
>
6. 【次へ】をクリックしてインストールを開始します。
7. インストールが完了したら、【フォーラムのインストールが完了しました。ここをクリックしてアクセスしてください】をクリックして、フォーラムにアクセスできます。

<span id="ConfigureDomain"></span>
## 関連する操作
自分のDiscuz!フォーラムに個別のドメイン名を設定できます。ユーザーは複雑なIPアドレスを使用せずに、覚えやすいドメイン名でWebサイトにアクセスできます。 一部のユーザーは学習目的でのみWebサイトを構築するため、IPアドレスを使用して直接インストールして使用できますが、このような操作はお勧めできません。

## よくあるご質問
CVMの使用中に問題が発生した場合は、下記のドキュメントを参照して、実際の状況に応じて問題を分析して解決できます。
- CVMのログインに関する問題は、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)ドキュメントをご参照ください。
- CVMのネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)ドキュメントをご参照ください。
- CVMのハードディスクに関する問題は、[システムディスクとデータディスク](https://intl.cloud.tencent.com/document/product/213/17351)ドキュメントをご参照ください。



