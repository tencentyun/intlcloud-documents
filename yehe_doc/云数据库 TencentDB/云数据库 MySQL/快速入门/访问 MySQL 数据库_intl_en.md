TencentDB for MySQLには、次の2つの方法でアクセスできます。

- **プライベートネットワークへのアクセス**：CVMインスタンスを使用して、TencentDBインスタンスのプライベートネットワークアドレスにアクセスできます。このアクセス方法は、Tencent Cloudの高速プライベートネットワークを使用し、ディレーが低い。
 - CVMとデータベースは同じアカウントで、同じリージョンの同じ[ VPC](https://intl.cloud.tencent.com/document/product/215/535)、又は基盤となるネットワーク内でなければなりません。
 - プライベートネットワークアドレスはデフォルトでシステムによって提供され、[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンスリスト又はインスタンスの詳細ページから確認できます。

- **パブリックネットワークへのアクセス**：プライベートネットワーク経由で接続できない場合は、パブリックネットワークアドレスを使用してMySQLインスタンスにアクセスできます。
 - パブリックネットワークアドレスは、広州、上海、北京、成都、重慶、中国香港、シンガポール、ソウル、東京、シリコンバレー地域のインスタンスでのみ有効にすることができます。
 - パブリックネットワークアドレスを[手動で有効にする](#waiwang)必要があり、[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページで確認できます。また、不要な場合は無効にできます。
 - パブリックネットワークアドレスを有効にすると、ユーザーのデータベースサービスがパブリックネットワークに公開され、データベースが侵入又は攻撃される可能性があります。データベースにアクセスするにはプライベートネットワークを使用することをお勧めします。 
 - MySQLのパブリックネットワークへのアクセスは、データベースの開発又は支援管理に適しています。正式なサービスのアクセスには推奨されません。これは、DDOS攻撃、突発的な大量アクセスなど、制御できない要因によってパブリックネットワークへのアクセスが利用できない可能性があるためです。


次の例では、Windows CVM又はLinux CVMからログインして、プライベートネットワークとパブリックネットワークを介してTencentDB for MySQLインスタンスにアクセスする方法について説明します。
## Windows CVMからのアクセス
1. Windows CVMインスタンスにログインします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">Windows CVMのカスタム設定</a>をご参照ください。
2. 標準SQLクライアントをダウンロードします。
>MySQL Workbenchをダウンロードすることをお勧めします。ご使用のシステムに適したバージョンのインストーラをダウンロードします。ダウンロードアドレスについては、[https://dev.mysql.com/downloads/workbench/]をご参照ください。
>
![](https://main.qcloudimg.com/raw/25e78e6614b2967e8c70140b8849a6d6.png)
3. 画面から【Login】、【Sign Up】、【No，thanks，just start my download.】が表示され、【No thanks，just start my download.】を選択して高速ダウンロードを実行します。
![](https://main.qcloudimg.com/raw/f98f84df777a8f8927bec3375781f517.png)
4. このCVMインスタンスにMySQL Workbenchをインストールします。
>
>- このコンピュータには、Microsoft.NET Framework 4.5とVisual C++Redistributable for Visual Studio 2015がインストールされている必要があります。
>- MySQL Workbenchインストールウィザードの【Download Prerequisites】をクリックし、該当するページにジャンプしてこの2つのソフトウェアをダウンロードしてインストールしてから、MySQL Workbenchをインストールします。
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. MySQL Workbenchを開き、【Database】>【Connect to Database】を選択し、MySQLデータベースインスタンスのプライベートネットワーク（又はパブリックネットワーク）アドレスとユーザー名、パスワードを入力し、【OK】をクリックしてログインします。
 - Hostname：プライベートネットワーク（又はパブリックネットワーク）アドレスを入力します。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでプライベートネットワーク（又はパブリックネットワーク）アドレスとポート番号を確認できます。パブリックネットワークアドレスの場合は、[パブリックネットワークアドレスを有効にする](#waiwang)の説明に従って有効になっているかどうかを確認してください。
 - Port：プライベートネットワーク（又はパブリックネットワーク）に対応するポート。
 - Username：ユーザー名はデフォルトで「root」です。パブリックネットワークへのアクセスでは、個別の[アカウントを新規作成](https://intl.cloud.tencent.com/document/product/236/31900)してアクセス管理を行うことをお勧めします。
 - Password：Usernameのパスワード。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照して変更できます。
![](https://main.qcloudimg.com/raw/8f2aeea985388e545ccf5da8fec908b7.png)
6. ログインに成功したページを図に示します。このページでは、MySQLデータベースの様々なモードやオブジェクトを見ることができ、テーブルの新規作成、データの挿入やクエリーなどの操作を実行することができます。
![](https://main.qcloudimg.com/raw/9ec2f9393a3652727acbb8dfc41ad5b7.png)

## Linux CVMからのアクセス
1. Linux CVMインスタンスにログインします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/10517" target="_blank">Linux CVMのカスタム設定</a>をご参照ください。
2. CentOS 7.2 64ビットシステムのCVMインスタンスを例に、次のコマンドを実行してMySQLクライアントをインストールします。
```
yum install mysql
```
`Complete！`が表示されると、MySQLクライアントのインストールが完了したことを示しています。
![](https://main.qcloudimg.com/raw/907e047fed90f6cf68752fb386382927.png)
3. アクセス方法に応じて、適切なアクションを選択します。
 - **プライベートネットワークにアクセスする場合：**
    1. 次のコマンドを実行して、TencentDB for MySQLインスタンスにログインします。
```
mysql -h hostname -u username -p
```
      - hostname：ターゲットであるTencentDB for MySQLインスタンスのプライベートネットワークアドレスに置き換えます。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでプライベートネットワークアドレスを確認できます。
		- username：デフォルトのユーザー名であるrootに置き換えます。
    2. `Enter password：`が表示された後に、MySQLインスタンスのrootアカウントのパスワードを入力します。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照してパスワードをリセットしてください。
    この例で、`MySQL[（none）]>`が表示されると、MySQLに正常にログインしたことを示しています。
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **パブリックネットワークにアクセスする場合：**
    1.次のコマンドを実行して、TencentDB for MySQLインスタンスにログインします。
```
mysql -h hostname -P port -u username -p
```
      - hostname：ターゲットであるTencentDB for MySQLインスタンスのパブリックネットワークアドレスに置き換えます。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでパブリックネットワークアドレスとポート番号を確認できます。パブリックネットワークアドレスが有効になっていない場合は、[パブリックネットワークアドレスを有効にする](#waiwang)をご参照ください。
      - port：パブリックネットワークのポート番号に置き換えます。
      - username：パブリックネットワークにアクセスするためのユーザー名に置き換えます。パブリックネットワークにアクセスする場合は、個別の[アカウントを新規作成](https://intl.cloud.tencent.com/document/product/236/31900)してアクセス管理を行うことをお勧めします。
    2. `Enter password：`が表示されたら、パブリックネットワークアクセス用のユーザー名に対応するパスワードを入力します。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照してパスワードをリセットしてください。
    この例では、ホスト名は、59281c4exxx.myqcloud.comで、パブリックネットワークポート番号は15311です。
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. `MySQL [(none)]>`プロンプトで、SQLステートメントを実行しようとするMySQLサーバに送信できます。特定のコマンドラインについては、[mysql クライアントコマンド](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html)をご参照ください。
以下の図では例として`show databases； `を説明します。
![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)


<span id = "waiwang"></span>
## 付録1：パブリックネットワークアクセスの有効化
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb/ )にログインし、インスタンスリストでインスタンス名又は「操作」列の【管理】をクリックしてインスタンス詳細ページに進みます。
3. インスタンスの詳細画面にある基本情報から【パブリックネットワークアドレス】を見つけ、【有効】をクリックします。
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
4. 【OK】をクリックすると、有効化プロセスが開始されます。
5. 有効化に成功したら、基本情報からパブリックネットワークアドレスを確認することができます。
>オン・オフをすることで、パブリックネットワークへのアクセス権限をオフすることができます。パブリックネットワークをもう一度有効化したら、ドメイン名に対応するパブリックネットワークアドレスが変わりません。

## 付録2：よくある質問のトラブルシューティング
TencentDB for MySQLに接続できない場合は、[インスタンスに接続できない問題](https://intl.cloud.tencent.com/document/product/236/31928)をご参照ください。


