## 操作シナリオ
RabbitMQは、高度なメッセージキュープロトコル（Advanced Message Queuing Protocol、AMQP）を実現したオープンソースのメッセージブローカーです。サーバー側はErlang言語を用いて作成され、Python、Ruby、.NET、Java、JMS、C、PHP、ActionScript、XMPP、STOMP、AJAXなど多様なクライアントをサポートしています。ユーザビリティ、拡張性および高可用性などのメリットがあり、本節を参考にして、RabbitMQをTencent Cloud CVMで配置することができます。

## ソフトウェア
本節の説明例に使用するソフトウェアバージョンおよびその構成は次の通りです。
- Linux：Linux OS。このドキュメントでは、CentOS 7.7を例として説明します。
- RabbitMQ Server：オープンソースのメッセージブローカーです。本節では、RabbitMQ Server 3.6.9を例として説明します。
- Erlang：プログラミング言語です。本節では、Erlang 19.3を例として説明します。


##  前提条件
- Linux CVMを購入済みであること。
- Linuxインスタンスのセキュリティグループルールはすでに設定されています。ポート80、5672、15672を開きます。詳細については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。

## 操作手順
### Erlangのインストール
1. [標準方法を使用してLinuxインスタンスにログインします（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)。実際の操作方法に応じて、他のログイン方法を選択することもできます。
	- [リモートログインソフトウェアを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32502)
	- [SSHキーを使用してLinuxインスタンスにログインする](https://intl.cloud.tencent.com/document/product/213/32501)
2. 以下のコマンドを実行して、依存関係をインストールします。
```
yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
```
3. 次のコマンドを実行して、Erlangインストールパッケージをダウンロードします。
```
wget http://erlang.org/download/otp_src_19.3.tar.gz
```
4. 次のコマンドを実行して、Erlangインストールパッケージを解凍します。
```
tar xzf otp_src_19.3.tar.gz
```
5. 次のコマンドを実行して、Erlangフォルダを作成します。
```
mkdir /usr/local/erlang
```
6. 次のコマンドを順次実行して、Erlangをコンパイルしてインストールします。
```
cd otp_src_19.3
```
```
./configure --prefix=/usr/local/erlang --without-javac
```
```
make && make install
```
7. 次のコマンドを実行して、profile構成ファイルを開きます。
```
vi /etc/profile
```
8. **i**を押して編集モードに入り、ファイルの最後に次のように入力します。
```
export PATH=$PATH:/usr/local/erlang/bin
```
9. **Esc**キーを押し、**:wq**を入力し、ファイルを保存してから終了します。
10. 次のコマンドを実行して、直ちに環境変数を有効にします。
```
source /etc/profile
```

### RabbitMQ Serverのインストール
1. 次のコマンドを実行して、RabbitMQ Serverインストールパッケージをダウンロードします。
```
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_9/rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
ここでは、RabbitMQバージョン3.6.9を例として取り上げ、また、RabbitMQの公式ウェブサイトから提供されているダウンロードアドレスを使用します。ダウンロードリンクが機能していない場合、またはRabbitMQの別のバージョンが必要な場合は、[rabbitmq-server](https://github.com/rabbitmq/rabbitmq-server/releases)にアクセスしてインストール情報を取得してください。
10. 次のコマンドを実行して、署名キーをインポートします。
```
rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
```
11. 次のコマンドを順次実行して、RabbitMQ Serverをインストールします。
```
cd
```
```
yum install rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
12. 次のコマンドを順次実行して、RabbitMQの自動起動を設定してRabbitMQを起動します。
```
systemctl enable rabbitmq-server
```
```
systemctl start rabbitmq-server
```
13. 次のコマンドを実行して、RabbitMQのデフォルトのguestアカウントを削除します。
```
rabbitmqctl delete_user guest
```
14. <span id="Step6"></span>次のコマンドを実行して、新しいユーザーを作成します。
```
rabbitmqctl add_user ユーザー名 パスワード
```
15. 次のコマンドを実行して、新しいアカウントを管理者アカウントとして設定します。
```
rabbitmqctl set_user_tags ユーザー名 administrator
```
16. 次のコマンドを実行して、管理者アカウントにすべての権限を付与します。
```
rabbitmqctl set_permissions -p / ユーザー名 ".*" ".*" ".*"
```


### インストールの検証
1. 次のコマンドを実行して、RabbitMQのWeb管理画面を開きます。
```
rabbitmq-plugins enable rabbitmq_management
```
2. ブラウザーを開いて、以下のアドレスにアクセスします。
```
http://インスタンスのパブリックIPアドレス:15672
```
インスタンスのパブリックIPアドレスを取得する方法の詳細については、[パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)をご参照ください。
次のように表示画面が表示されると、RabbitMQ Serverのインストールに成功したことを意味します。
![](https://main.qcloudimg.com/raw/aacb15db11b5cf80dd6b7ba1dc80d331.png)
3. [ステップ6](#Step6)で作成した管理者ユーザーを使用してログインし、RabbitMQ管理インターフェースに入ります。下図のとおりです。
![](https://main.qcloudimg.com/raw/7f8d24062541be6ba8b271483343b20a.png)

