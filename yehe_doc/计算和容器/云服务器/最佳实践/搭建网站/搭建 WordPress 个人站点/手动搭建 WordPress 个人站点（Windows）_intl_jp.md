## 概要
WordPressはPHP言語で開発されたブログプラットホームです。WordPressにより個人のブログプラットホームを構築することが可能です。このドキュメントでは、Windows Server 2012 OSのTencent Cloud CVMを例として取り上げ、手動でWordPressの個人サイトを構築することについて説明します。

<dx-alert infotype="notice" title="">
手動による構築プロセスには長い時間がかかる場合があるため、Tencent Cloudは、クラウド市場のイメージ環境を介してWordPressの個人ブログをデプロイすることをお勧めします。
</dx-alert>



## ソフトウェアバージョン
WordPressの個人サイトは、PHP 5.6.20以降のバージョンおよびMySQL 5.0以降のバージョンで構築できます。セキュリティを強化するために、WordPressの個人サイトを構築するとき、PHP 7.3以降のバージョンおよびMySQL 5.6以降のバージョンを選択してインストールすることをお勧めします。

このドキュメントでは、構築するWordPressの個人サイトの構成バージョンおよびその説明は次のとおりです：
- Windows：Windows OSです。このドキュメントでは、64ビットの中国語版のWindows Server 2012 R2 Data Center Editionを例として説明します。
- IIS：Webサーバーです。このドキュメントでは、IIS 8.5を例として説明します。
- MySQL：データベースです。このドキュメントでは、MySQL 8.0.19を例として説明します。
- PHP：スクリプト言語です。このドキュメントでは、PHP 7.1.30を例として説明します。
- WordPress：ブログプラットフォームです。このドキュメントでは、WordPress 5.9を例として説明します。


## 操作手順

### ステップ1：CVMにログインする
[RDPファイルを使用したWindowsインスタンスへのログイン（推奨）](https://intl.cloud.tencent.com/zh/document/product/213/5435)。
また、実際の操作習慣に応じて、[リモートデスクトップとの接続によるWindowsインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/32498)。

### 手順2：WIPM環境を構築する
[WIPM環境の手動構築](https://intl.cloud.tencent.com/zh/document/product/213/33143)を参照して、以下のとおり操作します：
1. IISサービスをインストールします。
2. PHP 5.6.20以降のバージョンの環境をデプロイします。
3. MySQL 5.6以降のバージョンのデータベースをインストールします。

### 手順3：WordPressをインストールして設定する

<dx-alert infotype="explain" title="">
WordPressは、WordPressの公式ウェブサイトから最新のWordPress中国語版をダウンロードしてインストールできます。このドキュメントでは、WordPress中国語版を使用しています。
</dx-alert>



1. WordPressをダウンロードして、WordPressインストールパッケージをCVMに解凍します。
例えば、WordPressインストールパッケージを`C:\wordpress`ディレクトリに解凍します。
2. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"> >  <img src="https://main.qcloudimg.com/raw/ca83b4e70e201fe9ff98dc1f2b207cee.png" style="margin: -3px 0px;"> >  **MySQL 5.6 Command Line Client**をクリックして、MySQLTencent Cloud Command Line Interfaceクライアントを開きます。
3. MySQL Tencent Cloud Command Line Interfaceクライアントでは、次のコマンドを実行して、WordPressデータベースを作成します。
例えば、「wordpress」データベースを作成します。
```
create database wordpress;
```
4. WordPressの解凍したインストールパスで、`wp-config-sample.php`ファイルを見つけてコピーし、ファイルの名前を`wp-config.php`に変更します。
5. テキストエディタで`wp-config.php`ファイルを開き、関連する設定情報を[手順3：MySQLデータベースをインストールする](https://intl.cloud.tencent.com/document/product/213/10190)の内容に変更します。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/5900f1b371a512f7c058783caeccc719.png)
6. `wp-config.php`ファイルを保存します。
7. <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: -3px 0px;">をクリックして、サーバーマネージャーを開きます。
8. サービスマネージャーの左側ナビゲーションバーで**IIS**を選択し、右側のIIS管理ウィンドウで**サーバー**列のサーバー名を右クリックして、**Internet Information Sevices (IIS)マネージャー**を選択します。
9. 開かれた「Internet Information Sevices (IIS)マネージャー」ウィンドウで、左側のナビゲーションバーにあるサーバー名を展開して、**ウェブサイト**をクリックして、「ウェブサイト」管理ページに進みます。
10. **ウェブサイト**の下のポート80にバインディングされているウェブサイトを削除します。
ウェブサイトのバインディングポートを別の占有されていないポート番号に変更することもできます。例えば、8080ポートに変更します。
11. 右側の**操作**列で、**ウェブサイトの追加**をクリックします。
12. ポップアップ表示されたウィンドウで、下記情報を記入して、**OK**をクリックします。
    - **ウェブサイト名**：wordpressなど、ユーザーによってカスタマイズされます。
    - **アプリケーションプール**：**DefaultAppPool**として選択します。
    - **物理パス**：`C:\wordpress`など、WordPressが解凍された後のパスを選択します。
13. PHPの解凍したインストールパスで、`php.ini`ファイルを開き、次の内容を変更します。
    1. PHPバージョンに応じて、対応する構成パラメータを変更します：
       - PHPバージョン5.Xの場合、`extension=php_mysql.dll`を見つけて、前の`;`を削除します。
       - PHPバージョン7.Xの場合、`extension=php_mysqli.dll`または`extension=mysqli`を見つけて、前の`;`を削除します。
    2. `extension_dir = "ext"`を見つけて、前の`;`を削除します。
14. `php.ini`ファイルを保存します。

### ステップ4：WordPressの設定を確認する

1. ブラウザを使用して`http://localhost/wp-admin/install.php`にアクセスし、WordPressインストールページに進み、WordPressを設定します。
2. WordPressインストールウィザードの指示に従って、下記のインストール情報を入力し、**WordPressをインストールする**をクリックし、インストールを完了します。
<table>
	<tr><th width="16%">必要な情報</th><th>説明</th></tr>
	<tr><td>サイトタイトル</td><td>WordPressウェブサイト名です。</td></tr>
	<tr><td>ユーザー名</td><td>WordPress管理者の名前です。セキュリティのために、adminと異なる名前を設定することをお勧めします。デフォルトユーザー名であるadminと比べて、この名前はクラックしにくいです。</td></tr>
	<tr><td>パスワード</td><td>強力なデフォルトパスワードまたはカスタマイズパスワードを使用できます。既存のパスワードを再利用しないでください。また、パスワードを安全な場所に保管してください。</td></tr>
	<tr><td>Eメール</td><td>通知を受け取るために使用されるEメールアドレスです。</td></tr>
</table>
これからWordPressブログにログインし、ブログ投稿を行うことが可能になります。

## よくあるご質問
CVMの使用中に問題が発生した場合は、下記のドキュメントを参照しながら実際状況に合わせ分析した上で問題を解決することが可能です：
- CVMのログインに関する問題については、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)をご参照ください。
- CVMのネットワークに関する問題については、[IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)をご参照ください。
- CVMのハードディスクに関する問題については、[システムディスクとデータディスク](https://intl.cloud.tencent.com/zh/document/product/213/17351)をご参照ください。

