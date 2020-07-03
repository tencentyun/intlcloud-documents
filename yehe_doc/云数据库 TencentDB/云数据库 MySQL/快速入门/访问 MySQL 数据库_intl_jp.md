MySQLにアクセスする方法は次の2つの方法があります。

- **プライベートネットワークへのアクセス**：CVMを使用して、MySQLのプライベートネットワークのアドレスに直接アクセスします。このアクセス方法は、内部の高速ネットワークを使用し、ディレーが低い。
 - CVMとデータベースは同じアカウントで、同じ[VPC](https://intl.cloud.tencent.com/document/product/215/535）内（同じドメインが確保される）、又は基盤となるネットワーク内でなければなりません。
 - システムはデフォルトでプライベートネットワークのアドレスを提供し、[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンスリスト又はインスタンスの詳細ページから確認できます。

- **パブリックネットワークへのアクセス**：プライベートネットワーク経由で接続できない場合は、パブリックネットワークのアドレスを使用してMySQLにアクセスできます。
 - パブリックネットワークにアクセスするためのアドレスの有効化をサポートするのは、広州、上海、北京、成都、重慶、中国香港、シンガポール、ソウル、東京、シリコンバレーのインスタンスのみです。
 - パブリックネットワークのアドレスは[手動でオンにする](#waiwang)必要があり、[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページで確認できます。また、不要な場合はオフにすることもできます。
 - パブリックネットワークのアドレスをオンにすると、ユーザーのデータベースサービスがパブリックネットワーク上に露出し、データベースが侵入又は攻撃される可能性があります。データベースにアクセスするにはプライベートネットワークを使用することをお勧めします。 
 - MySQLのパブリックネットワークへのアクセスは、データベースの開発又は支援管理に適しています。正式なサービスのアクセスには推奨されません。これは、DDOS攻撃、突発的な大量アクセスなど、支配できない要因によってパブリックネットワークへのアクセスが利用できない可能性があるためです。


次の例では、Windows CVM又はLinux CVMからログインして、それぞれパブリック・プライベートネットワークでMySQLにアクセスする方法を紹介します。
##Windows CVMからのアクセス
1. Windows CVMにログインします。<a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">Windows CVMのカスタムコンフィギュレーション</a>をご参照ください。
2. 標準SQLクライアントをダウンロードします。
>MySQL Workbenchをダウンロードすることをお勧めします。ご使用のシステムに適したバージョンのインストーラをダウンロードします。ダウンロードアドレスについては、[https://dev.mysql.com/downloads/workbench/]をご参照ください。
>
![](https://main.qcloudimg.com/raw/25e78e6614b2967e8c70140b8849a6d6.png)
3. 画面から【Login】、【Sign Up】、【No，thanks，just start my download.】が表示され、【No thanks，just start my download.】を選択して高速ダウンロードを実行します。
![](https://main.qcloudimg.com/raw/f98f84df777a8f8927bec3375781f517.png)
4. このCVMにMySQL Workbenchをインストールします。
>
>- このコンピュータには、Microsoft.NET Framework 4.5とVisual C++Redistributable for Visual Studio 2015がインストールされている必要があります。
>- MySQL Workbenchインストールウィザードの【Download Prerequisites】をクリックし、該当するページにジャンプしてこの2つのソフトウェアをダウンロードしてインストールしてから、MySQL Workbenchをインストールします。
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. MySQL Workbenchを開き、【Database】>【Connect to Database】を選択し、MySQLデータベースインスタンスのプライベートネットワーク（又はパブリックネットワーク）アドレスとユーザー名、パスワードを入力し、【OK】をクリックしてログインします。
 - Hostname：プライベートネットワーク（又はパブリックネットワーク）のアドレスを入力します。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでプライベートネットワーク（又はパブリックネットワーク）アドレスとポート番号を確認できます。パブリックネットワークのアドレスの場合は、オンになっているかを確認してください。[パブリックネットワークのアドレスをオンにする]（#waiwang）をご参照ください。
 - Port：プライベートネットワーク（又はパブリックネットワーク）に対応するポート。
 - Username：デフォルトはrootです。パブリックネットワークへのアクセスでは、個別の[アカウントを新規作成](https://intl.cloud.tencent.com/document/product/236/31900)してアクセス管理を行うことをお勧めします。
 - Password：Usernameのパスワード。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照して変更できます。
![](https://main.qcloudimg.com/raw/8f2aeea985388e545ccf5da8fec908b7.png)
6. ログインに成功したページを図に示します。このページでは、MySQLデータベースの様々なモードやオブジェクトを見ることができ、テーブルの新規作成、データのインサートやクエリーなどの操作を実行することができます。
![](https://main.qcloudimg.com/raw/9ec2f9393a3652727acbb8dfc41ad5b7.png)

##Linux CVMからのアクセス
1. Linux CVMにログインします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/10517" target="_blank">Linux CVMのクイックコンフィグレーション</a>をご参照ください。
2. CentOS 7.2 64ビットシステムのCVMを例に、次のコマンドを実行してMySQLクライアントをインストールします。
```
yum install mysql
```
`Complete！`が表示されると、MySQLクライアントのインストールが完了したことを示しています。
![](https://main.qcloudimg.com/raw/907e047fed90f6cf68752fb386382927.png)
3. アクセス方法に応じて、適切なアクションを選択します。
 - **プライベートネットワークにアクセスする場合：**
    1. 次のコマンドを実行してMySQLデータベースインスタンスにログインします。
```
mysql -h hostname -u username -p
```
      - hostname：ターゲットであるMySQLデータベースインスタンスのプライベートネットワークアドレスに置き換えます。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでプライベートネットワークアドレスを確認できます。
		- username：デフォルトのユーザー名であるrootに置き換えます。
    2. `Enter password：`が表示された後に、MySQLインスタンスのrootアカウントのパスワードを入力します。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照して変更してください。
    この例で、`MySQL[（none）]>`が表示されると、MySQLに正常にログインしたことを示しています。
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **パブリックネットワークにアクセスする場合：**
    1. 次のコマンドを実行してMySQLデータベースインスタンスにログインします。
```
mysql -h hostname -P port -u username -p
```
      - hostname：ターゲットであるMySQLデータベースインスタンスのパブリックネットワークアドレスに置き換えます。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでパブリックネットワークアドレスとポート番号を確認できます。パブリックネットワークのアドレスがオンになっていない場合は、[パブリックネットワークアドレスをオンにする]（#waiwang）をご参照ください。
      - port：パブリックネットワークのポート番号に置き換えます。
      - username：パブリックネットワークにアクセスするためのユーザー名に置き換えます。パブリックネットワークにアクセスする場合は、個別の[アカウントを新規作成](https://intl.cloud.tencent.com/document/product/236/31900)してアクセス管理を行うことをお勧めします。
    2. `Enter password：`が表示されたら、パブリックネットワークアクセス用のユーザー名に対応するパスワードを入力します。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照して変更してください。
    この例では、hostnameは、59281c4exxx.myqcloud.comで、パブリックネットワークポート番号は15311です。
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. プロンプト`MySQL [(none)]>`から、SQL文を実行しようとするMySQLサーバに送信できます。プロンプトについては、[mysql Client Commands](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html)をご参照ください。
以下の図では例として`show databases； `を説明します。
![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)


<span id = "waiwang"></span>
## 付録1：パブリックネットワークにアクセスするためのアドレスをオンにします
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb/ )にログインし、インスタンスリストでインスタンス名又は「操作」列の【管理】をクリックしてインスタンス詳細ページに進みます。
3. インスタンスの詳細画面にある基本情報から【パブリックネットワークアドレス】を見つけ、【有効化】をクリックします。
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
4. 【OK】をクリックすると、パブリックネットワークの有効化状態が処理中になります。
5. 有効化に成功したら、基本情報からパブリックネットワークアドレスを確認することができます。
6. オン・オフをすることで、パブリックネットワークへのアクセス権限をオフすることができます。パブリックネットワークをもう一度有効化したら、ドメイン名に対応するパブリック IPが変わりません。

## 付録2：よくある質問のトラブルシューティング
MySQLに接続できない場合は、[インスタンスに接続できない問題](https://intl.cloud.tencent.com/document/product/236/31928)をご参照ください。


