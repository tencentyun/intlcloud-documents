## 操作シナリオ
WordPressはPHP言語で開発されたブログプラットホームです。WordPressにより個人のブログプラットホームを構築することが可能です。本ドキュメントはCentOS 7.6 OSのTencent Cloud CVMを例とし、手動でWordPressの個人サイトを構築することについて説明します。



## スキルの要求
WordPressの個人ブログを構築するには、 Linux コマンド（例：[CentOS環境におけるYUMによるソフトウェアをインストールする](https://intl.cloud.tencent.com/document/product/213/2046) 等の常用コマンドに詳しい必要があります。また、インストールするソフトウェアの利用及びバージョン間の互換性を把握することも必要です。
>手動構築には時間がかかりますので、Tencent Cloudは、クラウドマーケットのイメージ環境で WordPress個人ブログをデプロイすることをお薦めします。具体的な手順は [イメージによるWordPress個人サイトの構築](https://cloud.tencent.com/document/product/213/9740)をご参照ください。






## 操作手順 
### ステップ1：CVMにログインする
 Linux CVMにログインします。ログインしていない場合は、CVMのログインパスワードとパブリックIPを用意し、[標準方式による Linux インスタンスログイン](https://intl.cloud.tencent.com/document/product/213/5436) を参考にしログインしてください。

### ステップ2：手動でLNMP環境を構築する
LNMP は Linux、Nginx、MariaDB 及びPHPの略称であり、この組み合わせは最も常用しているWebサーバー稼動環境の一つです。CVMインスタンスを作成しログインした後に、[LNMP環境の手動構築](https://cloud.tencent.com/document/product/213/38056) を参考して、基本的な環境構築を完了できます。



### ステップ3： WordPress データベース<span id="database"></span>を設定します
> MariaDBのバージョンにより、ユーザー認証方法の設定は異なります。具体的な手順は MariaDB公式サイトをご参照ください。
>
1. 下記のコマンドを実行し、 MariaDBに入ります。
```
mysql
```
2. 下記のコマンドを実行し、 MariaDBデータベースを新規作成します。例えば 「wordpress」です。
```
CREATE DATABASE wordpress;
```
3. 下記のコマンドを実行し、ユーザーを新規に作成します。例えば 「user」で、ログインパスワードが `123456`です。
```
CREATE USER 'user'@'localhost' IDENTIFIED BY '123456';
```
4. 下記のコマンドを実行し、ユーザーに 「wordpress」データベースのすべての権限を与えます。
```
GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost' IDENTIFIED BY '123456';
```
5. 下記のコマンドを実行し、すべての設定を有効にします。
```
FLUSH PRIVILEGES;
```
6. 下記のコマンドを実行し、 MariaDBから退出します。
```
\q
```

### ステップ4： rootアカウントを設定する
1. 下記のコマンドを実行し、 MariaDBに入ります。
```
mysql
```
2. 下記のコマンドを実行し、 rootアカウントのパスワードを設定します。
>MariaDB 10.4 は CentOS システムにおいて rootアカウントパスワード無しのログイン機能を追加しました、下記のステップを実行し、自分のrootアカウントパスワードを設定した上、よく覚えてください。
>
```
ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD('パスワードを入力してください');
```
3. 下記のコマンドを実行し、 MariaDBから退出します。
```
\q
```


### ステップ5： WordPressをインストールして設定する
####  WordPressのダウンロード
> WordPress は [WordPress 公式サイト](https://wordpress.org/download/releases/) から WordPress の最新中国語版をダウンロードしインストールすることが可能です。本マニュアルはWordPressの中国語版を採用しています。
>
1. 下記のコマンドを実行し、ウェブサイトのルートディレクトリにあるPHP-Nginx設定のテストに使われる`index.php`ファイルを削除します。
```
rm -rf /usr/share/nginx/html/index.php
```
2. 順次に下記のコマンドを実行し、`/usr/share/nginx/html/`ディレクトリに入り、 WordPressをダウンロードしてから解凍します。
```
cd /usr/share/nginx/html
wget https://cn.wordpress.org/wordpress-5.0.4-zh_CN.tar.gz
tar zxvf wordpress-5.0.4-zh_CN.tar.gz
```



####   WordPress設定ファイルの修正
1. 順次に下記のコマンドを実行し、 WordPressのインストールディレクトリに入り、`wp-config-sample.php`ファイルを`wp-config.php`ファイルにコピーし、元のサンプル設定ファイルをバックアップとして保留します。
```
cd /usr/share/nginx/html/wordpress
cp wp-config-sample.php wp-config.php
```
2. 下記のコマンドを実行し、新規に作成された設定ファイルを開いてから編集します。
```
vim wp-config.php
```
3.  「**i**」 又は 「**Insert**」 を押して、編集モードに入り、ファイルにおける MySQLの部分を見つけ、関連設定情報を [ WordPressデータベースの設定](#database) の内容に修正ます。
```
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
4. 修正した後に、「**Esc**」を押して、「**:wq**」を入力し、ファイルを保存してから戻ります。

### ステップ6： WordPress インストレーションの検証
1. ブラウザーのアドレス欄にCVMインスタンスのパブリックIP及びwordpressフォルダーをを入力します。例えば：
```
http://192.xxx.xxx.xx /wordpress
```
WordPressインストレーションページに入り、 WordPressの設定を始めます。
![WP1の設定](https://main.qcloudimg.com/raw/c79c35b3d75f763561d7024f46983611.png)
2.  WordPressインストレーションガイドのプロンプトに従って下記のインストレーション情報を入力し、【 WordPressをインストールする】をクリックし、インストレーションを完了します。
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
							WordPress 管理者の名前。セキュリティのために、 adminと異なる名前を設定することをお薦めします。デフォルトユーザー名であるadmin と比べては、当該名前は一層クラックしにくいようにする必要があります。
					</td>
			</tr>
			<tr>
					<td>
							パスワード
					</td>
					<td>
							デフォルトのストロングパスワード又はカスタマイズパスワードを使ってよいです。既存のパスワードを重複に利用せず、安全のところにパスワードを保存することを確保してください。
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

## 後続操作
1. 顧客は自分のWordPressブログサイトに対し単独なドメイン名を設定することができます。これにより、顧客のユーザーは複雑なIPアドレスを使わず、覚えやすいドメイン名でサイトにアクセスすることが可能になります。
2. 中国国内におけるサーバーに指向するドメイン名のウェブサイトは、ICP Filing Registrationが必要です。ドメイン名が登録番号を取得する前に、ウェブサイトをアクティブにすることができません。Tencent Cloudで [ICP Filing Registration](https://cloud.tencent.com/product/ba?from=qcloudHpHeaderBa&fromSource=qcloudHpHeaderBa)を行うことが可能です。登録は無料であり、審査には約20日かかります。



## よくある質問
CVMの使用中に問題があれば、下記のドキュメンテーションを参照しながら実際状況に合わせ分析した上問題を解決することが可能です。
- CVMのログインに関する問題は、 [パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)をご参照ください。
- CVMネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)をご参照ください。

