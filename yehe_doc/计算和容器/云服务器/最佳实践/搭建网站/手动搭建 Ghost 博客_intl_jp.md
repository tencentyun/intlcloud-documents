## 操作シナリオ
GhostはNode.js言語を使用して作成するオープンソースブログプラットフォームです。 Ghostを使用すると、すぐにブログを立ち上げることができ、 オンラインパブリッシングのプロセスを簡略化できます。このドキュメントでは、Tencent CloudのCloud Virtual Machine（CVM）上で、Ghost個人ウェブサイトを手動で構築する方法についてご紹介します。

Ghostウェブサイトを構築するには、Lunux OSおよびコマンドに精通している必要があります。例えば、[Ubuntu環境下でのApt-getによるソフトウェアインストール](https://intl.cloud.tencent.com/document/product/213/2123)等の常用コマンドです。

## ソフトウェアバージョンの例
ここでGhostブログの作成に使用するOSおよびソフトウェアのバージョンと説明は次のとおりです。
- OS：ここではUbuntu 20.04を例として説明します。
- Nginx：Webサーバー。ここではNginx 1.18.0を例として説明します。
- MySQL：データベース。ここではMySQL 8.0.25を例として説明します。
- Node.js：実行環境。ここではNode.js 14.17.0バージョンを例として説明します。
- Ghost：オープンソースブログプラットフォーム。ここではGhost 4.6.4バージョンを例として説明します。


## 前提条件
- Linux CVMを購入済みであること。CVMを購入していない場合は、[Linux CVMのカスタマイズ設定](https://intl.cloud.tencent.com/document/product/213/10517)をご参照ください。
- Ghostブログ設定の過程では、ICP登録が完了し、かつ使用するCVMへの解決が完了しているドメイン名を使用する必要があります。



## 操作手順

### ステップ1：Linuxインスタンスにログインする
[標準方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)します。実際の操作方法に応じて、他のログイン方法を選択することもできます。
- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
-[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501)

### 手順2：新規ユーザーの作成
1. Ubuntu OSのCVMにログインした後、[Ubuntuシステムでrootユーザーを使用してログイン](https://intl.cloud.tencent.com/document/product/213/17278)を参照して、rootユーザーに切り替えてください。
2. 以下のコマンドを実行し、新規ユーザーを作成します。ここでは`user`を例とします。
>!Ghost-CLIとの競合が発生する場合がありますので、`ghost`をユーザー名に使用しないでください。 
>
```
adduser user
```
 1. 表示に従ってユーザーパスワードを入力し、確認してください。パスワードはデフォルトでは表示されません。入力し終わったら**Enter** を押し、次の手順に進んでください。
 2. 実際の状況に応じてユーザー関連情報を入力します。デフォルトでは入力しなくても結構です。**Enter** を押して次の手順に進んでください。
 3. **Y**を入力して情報を確認し、**Enter**を押すと設定が完了します。下図に示します。
 ![](https://main.qcloudimg.com/raw/66ca399607b89f2653668eb4b0cb71f5.png)
3. 以下のコマンドを実行し、ユーザー権限を追加します。
```
usermod -aG sudo user
```
4. 以下のコマンドを実行し、`user`によるログインに切り替えます。
```
su - user
```

### 手順3：インストールパッケージの更新
以下のコマンドを順に実行して、インストールパッケージを更新します。
>?画面上の表示に従って、`user`のパスワードを入力し、**Enter** を押して更新を開始してください。
>
```
sudo apt-get update
```
```
sudo apt-get upgrade -y
```

### 手順4：環境の構築
#### Nginxのインストールと設定
以下のコマンドを実行し、Nginxをインストールします。
```
sudo apt-get install -y nginx 
```

#### MySQLのインストールと設定
1. 以下のコマンドを実行し、MySQLをインストールします。
```
sudo apt-get install -y mysql-server 
```
2. 以下のコマンドを実行し、MySQLに接続します。
```
sudo mysql
```
3. <span id="database"></span>以下のコマンドを実行し、Ghostで使用するデータベースを作成します。ここでは`ghost_data`を例とします。
```
CREATE DATABASE ghost_data;
```
4. <span id="sercet"></span>以下のコマンドを実行し、rootアカウントのパスワードを設定します。
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'rootアカウントパスワード入力';
```
5. 以下のコマンドを実行し、MySQLを終了します。
```
\q
```

#### Node.jsのインストールと設定
1. 以下のコマンドを実行し、 Node.jsのサポートするインストールバージョンを追加します。
>? Ghostのバージョンによって、必要なNode.jsのバージョンが異なります。[upported Node versions](https://ghost.org/docs/faq/node-versions/)および以下のコマンドを参照し、対応するコマンドを実行してください。
>
```
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash
```
2. 以下のコマンドを実行し、Node.jsをインストールします。
```
sudo apt-get install -y nodejs
```

#### Ghost-CLIのインストール
以下のコマンドを実行し、Ghostコマンドラインツールをインストールすると、Ghostのクイック設定を行うことができます。
```
sudo npm install ghost-cli@latest -g
```

### 手順5：Ghostのインストールと設定
1. 次のコマンドを順に実行し、設定してGhostインストールディレクトリに進みます。
```
sudo mkdir -p /var/www/ghost
```
```
sudo chown user:user /var/www/ghost
```
```
sudo chmod 775 /var/www/ghost
```
```
cd /var/www/ghost
```
2. 以下のコマンドを実行し、インストールプログラムを実行します。
```
ghost install
```
3. インストールの過程で関連の設定を行う必要があります。画面および以下の表示を参照して設定を完了してください。下図に示します。
![](https://main.qcloudimg.com/raw/4fa1bccb961fa6c05c01892e5fbfd367.png)
主要な設定は次のとおりです。
 1. **Enter your blog URL**：解決済みのドメイン名を入力します。`http://(ドメイン名)`を入力してください。
 2. **Enter your MySQL  hostname**：データベース接続アドレスを入力します。`localhost`を入力し、**Enter**を押してください。
 3. **Enter your MySQL username**：データベースのユーザー名を入力します。`root`を入力し、**Enter**を押してください。
 4. **Enter your MySQL password**：データベースのパスワードを入力します。 [rootアカウントのパスワード設定](#sercet)で設定済みのパスワードを入力し、**Enter**を押してください。
 5. **Enter your database name**：Ghostで使用するデータベースを入力します。 [データベースの作成](#database)で作成済みの`ghost_data`を入力し、**Enter**を押してください。
 6. **Do you wish to set up SSL?**：HTTPSアクセスを有効にしたい場合は**Y**を入力し、**Enter**を押してください。
 その他の設定は実際の状況に応じて、画面の表示に従って完了してください。設定完了後、画面の下にGhostの管理者アクセス用アドレスが出力されます。
4. ローカルブラウザを使用して、Ghostの管理者アクセス用アドレスにアクセスし、個人ブログの設定を開始します。下図に示します。
>?HTTPSアクセスを有効にしている場合は、`https://`を使用してアクセスまたはブログ設定などの操作を行ってください。
>
【Create your account】をクリックし、管理者アカウントの作成を開始します。
![](https://main.qcloudimg.com/raw/e2eeacd71eec4c27660eeb4797f83f2a.png)
5. 関連情報を入力し、【Last step】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/a7a81f16b811bdceeb429116ee23081c.png)
6. 他の人を招待して一緒にブログを作成することもでき、この手順をスキップすることもできます。
7. 管理インターフェースに入ると、ブログの管理を開始できます。下図に示します。
![](https://main.qcloudimg.com/raw/fd9071dba9748ce8125f8597be0d248a.png)
設定完了後、ローカルブラウザを使用して、設定済みのドメイン名`www.xxxxxxxx.xx`にアクセスすると、個人ブログのトップページを見ることができます。下図に示します。
![](https://main.qcloudimg.com/raw/055decab4524eb9f2f5602fbd0502c7c.png)

## よくあるご質問
CVMの使用中に問題が発生した場合は、下記のドキュメントを参照して、実際の状況に応じて問題を分析して解決できます。
- CVMのログインに関する問題は、[パスワードとキー](https://intl.cloud.tencent.com/document/product/213/18120)、[ログインとリモート接続](https://intl.cloud.tencent.com/document/product/213/17278)ドキュメントをご参照ください。
- CVMのネットワークに関する問題は、 [IPアドレス](https://intl.cloud.tencent.com/document/product/213/17285)、[ポートとセキュリティグループ](https://intl.cloud.tencent.com/document/product/213/2502)ドキュメントをご参照ください。
- CVMのハードディスクに関する問題は、[システムディスクとデータディスク](https://intl.cloud.tencent.com/document/product/213/17351)ドキュメントをご参照ください。

 

 

 
