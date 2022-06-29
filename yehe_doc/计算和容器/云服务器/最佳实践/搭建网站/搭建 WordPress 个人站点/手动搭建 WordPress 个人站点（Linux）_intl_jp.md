## 操作シナリオ
WordPressはPHP言語で開発されたブログプラットホームです。WordPressにより個人のブログプラットホームを構築することが可能です。本節はCentOS 7.6 OSのTencent Cloud CVMを例とし、手動でWordPressの個人サイトを構築することについて説明します。

WordPressの個人ブログを構築するには、Linux コマンド（例：[CentOS環境におけるYUMによるソフトウェアをインストールする](https://intl.cloud.tencent.com/document/product/213/2046) 等の常用コマンドに詳しい必要があります。また、インストールするソフトウェアの利用およびバージョン間の互換性を把握することも必要です。

<dx-alert infotype="notice" title="">
手動による構築プロセスには長い時間がかかる場合があるため、Tencent Cloudは、クラウド市場のイメージ環境を介してWordPressの個人ブログをデプロイすることをお勧めします。
</dx-alert>



## ソフトウェアのバージョン
本節で構築するWordPress個人サイトの構成バージョンとその説明は次のとおりです：
- Linux：Linux OS、本ドキュメントはCentOS 7.6を例として説明します。
- Nginx：Webサーバー、本節ではNginx 1.17.5を例に説明します。
- MariaDB：データベース、本ドキュメントはMariaDB 10.4.8を例として説明します。
- PHP：スクリプト言語、本ドキュメントはPHP 7.2.22を例とします。
- WordPress：ブログプラットフォーム、本節ではWordPress 5.0.4を例に説明します。

## 操作手順 
### ステップ1：CVMにログインする
[標準的な方法を使用してLinuxインスタンスにログインする（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます：
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSHキーを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)



### ステップ2：手動でLNMP環境を構築する
LNMP は Linux、Nginx、MariaDB およびPHPの略称であり、この組み合わせは最もよく使われているWebサーバー稼動環境の1つです。CVMインスタンスを作成しログインした後に、[手動でLNMP環境を構築する](https://intl.cloud.tencent.com/document/product/213/32733) を参考して、基本的な環境を構築できます。


### ステップ3：データベース[](id:database)を構成する


<dx-alert infotype="notice" title="">
MariaDBのバージョンにより、ユーザー認証方法の設定は異なります。手順の詳細については、 MariaDBの公式サイトをご参照ください。
</dx-alert>


1. 以下のコマンドを実行し、MariaDBに入ります。
```shellsession
mysql
```
2. 以下のコマンドを実行し、MariaDBデータベース（「wordpress」を例に）を新規作成します。
```shellsession
CREATE DATABASE wordpress;
```
3. 以下のコマンドを実行し、ユーザーを新規作成します。例えば「user」で、ログインパスワードは「123456」です。
```shellsession
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. 以下のコマンドを実行し、ユーザーに「wordpress」データベースのすべての権限を付与します。
```shellsession
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. 以下のコマンドを実行し、rootアカウントのパスワードを設定します。
<dx-alert infotype="explain" title="">
MariaDB 10.4はCentOSシステムにおいて rootアカウントパスワード不要のログイン機能を追加しました。下記のステップを実行し、自分のrootアカウントパスワードを設定し、保管してください。
</dx-alert>
```shellsession
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('パスワードを入力してください')。
```
6. 以下のコマンドを実行し、すべての構成を有効にします。
```shellsession
FLUSH PRIVILEGES;
```
7. 以下のコマンドを実行し、MariaDBを終了します。
```shellsession
\q
```


### 手順4：WordPressをインストールして設定する
####  WordPressのダウンロード


<dx-alert infotype="explain" title="">
WordPressは、WordPressの公式ウェブサイトから最新のWordPress中国語版をダウンロードしてインストールできます。このドキュメントでは、WordPress中国語版を使用しています。
</dx-alert>


1. 以下のコマンドを実行し、ウェブサイトのルートディレクトリにあるPHP-Nginx設定をテストするための「index.php」ファイルを削除します。
```shellsession
rm -rf /usr/share/nginx/html/index.php
```
2. 以下のコマンドを順に実行し、「/usr/share/nginx/html/」ディレクトリに入り、WordPressをダウンロードしてから解凍します。
```shellsession
cd /usr/share/nginx/html
```
```shellsession
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
```
```shellsession
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```


####   WordPress設定ファイルの変更
1. 以下のコマンドを順に実行し、WordPressのインストールディレクトリに入り、「wp-config-sample.php」ファイルを「wp-config.php」ファイルにコピーし、元のサンプル設定ファイルをバックアップとします。
```shellsession
cd /usr/share/nginx/html/wordpress
```
```shellsession
cp wp-config-sample.php wp-config.php
```
2. 以下のコマンドを実行し、新規作成された設定ファイルを開いて編集します。
```shellsession
vim wp-config.php
```
3.  **i**を押して、編集モードに入り、ファイルのMySQLの部分を見つけ、関連設定情報を [WordPressデータベースの設定](#database) の内容に変更ます。
```shellsession
	// ** MySQL settings - You can get this info from your web host ** //
	/** The name of the database for WordPress */
	define('DB_NAME', 'wordpress');
	
	/** MySQL database username */
	define('DB_USER', 'user');
	
	/** MySQL database password */
	define('DB_PASSWORD', '123456');
	
	/** MySQL hostname */
	define('DB_HOST', 'localhost');
```
4. 変更した後に、**Esc**を押して、**:wq**を入力し、ファイルを保存して戻ります。

### ステップ5： WordPress インストールの確認
1. ブラウザーのアドレス欄に「http://ドメイン名またはCVMインスタンスのパブリックIP/wordpressフォルダー」を入力します。例えば、
```shellsession
http://192.xxx.xxx.xx/wordpress
```
WordPressインストールページに入り、WordPressを設定します。
2. WordPressインストールウィザードの指示に従って、下記のインストール情報を入力し、**WordPressをインストールする**をクリックし、インストールを完了します。
<table>
	<th style="width: 18%;">必要な情報</th>
	<th style="width: 25%;">説明</th>
					<tr>
					<td>
							サイトのタイトル
					</td>
					<td>
							WordPressウェブサイト名。
					</td>
			</tr>
				<tr>
					<td>
							ユーザー名
					</td>
					<td>
							WordPress 管理者の名前。セキュリティのために、 adminと異なる名前を設定することをお勧めします。デフォルトユーザー名であるadmin と比べては、当該名前は一層クラックしにくいようにする必要があります。
					</td>
			</tr>
			<tr>
					<td>
							パスワード
					</td>
					<td>
							デフォルトの強いパスワードまたはカスタマイズパスワードを使用できます。既存のパスワードを重複に使用せず、パスワードを安全の場所に保管してください。
					</td>
			</tr>
				<tr>
					<td>
							メール
					</td>
					<td>
							通知を受信するためのメールアドレスです。
					</td>
			</tr>
	</table>
これからWordPressブログにログインし、ブログ投稿を行うことが可能になります。

## 関連する操作
自分のWordPressブログサイト用に別のドメイン名を設定できます。ユーザーは複雑なIPアドレスを使用せずに、覚えやすいドメイン名でWebサイトにアクセスできます。 一部のユーザーは学習目的でのみWebサイトを構築するため、IPアドレスを使用して直接インストールしては一時的に使用できますが、このような操作はお勧めできません。


## よくあるご質問
CVMの使用中に問題が発生した場合は、下記のドキュメントを参照しながら実際状況に合わせ分析した上で問題を解決することが可能です。
- CVMのログインに関する問題は、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)ドキュメントをご参照ください。
- CVMのネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)ドキュメントをご参照ください。
- CVMのハードディスクに関する問題は、[システムディスクとデータディスク](https://intl.cloud.tencent.com/document/product/213/17351)ドキュメントをご参照ください。



