## 接続方法
次の2つの方法を使用して TencentDB for MySQLに接続できます。
- **プライベートネットワーク接続**：CVMインスタンスを使用して、TencentDBインスタンスのプライベートネットワークアドレスに接続できます。この接続方法は、Tencent Cloudの高速プライベートネットワークを使用し、超低遅延を実現します。
 - CVMとデータベースは同じアカウントで、同じリージョンの同じ[ VPC](https://intl.cloud.tencent.com/document/product/215/535) 内、又は同じクラシックネットワーク内にある必要があります。
 - プライベートネットワークアドレスはデフォルトでシステムによって提供され、[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンスリスト又はインスタンスの詳細ページから確認できます。
>?異なるVPC内のCVMおよびTencentDBインスタンス（同じアカウント/異なるアカウント、同じリージョン/異なるリージョンを含む）は、プライベートネットワーク接続方法については、[Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003)をご参照ください。
>
- **パブリックネットワーク接続**：プライベートネットワークを介して接続できない場合は、パブリックネットワークアドレスを介してTencentDB for MySQLインスタンスに接続できます。パブリックネットワークアドレスは[手動で有効にする](#waiwang)必要があります。これは、[TencentDB for MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンスの詳細ページから確認でき、不要になった場合は無効にすることができます。
 - 広州、上海、北京、成都、重慶、南京、中国香港、シンガポール、ソウル、東京、シリコンバレー、フランクフルトの各地域のマスターインスタンスは、パブリックネットワーク接続の有効化をサポートしています。
 - パブリックネットワークアドレスを有効にすると、ユーザーのデータベースサービスがパブリックネットワークに公開され、データベースが侵入又は攻撃される可能性があります。データベースに接続するにはプライベートネットワークを使用することをお勧めします。  
 - TencentDBへのパブリックネットワーク接続は、データベースの開発又は支援管理に適しています。正式なサービスのアクセスには推奨されません。これは、DDOS攻撃、突発的な大量アクセスなど、制御できない要因によってパブリックネットワーク接続が利用できなくなる可能性があるためです。


次の例では、Windows CVM又はLinux CVMインスタンスからログインして、プライベートネットワークとパブリックネットワークを介してTencentDB for MySQLインスタンスに接続する方法について説明します。
## Windows CVMインスタンスから接続する方法
1. Windows CVMインスタンスにログインします。詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">Windows CVMのカスタム設定</a>をご参照ください。
2. 標準SQLクライアントをダウンロードします。
>?MySQL Workbenchをダウンロードすることをお勧めします。ご使用のシステムに適したバージョンのインストーラをダウンロードします。ダウンロードアドレスについては、https://dev.mysql.com/downloads/workbench/をご参照ください。
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. 画面から【Login】、【Sign Up】、【No，thanks，just start my download.】が表示され、【No thanks，just start my download.】を選択して高速ダウンロードを実行します。
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. このCVMインスタンスにMySQL Workbenchをインストールします。
>?
>- このコンピュータには、Microsoft.NET Framework 4.5とVisual C++Redistributable for Visual Studio 2015をインストールする必要があります。
>- MySQL Workbenchインストールウィザードの【Download Prerequisites】をクリックし、該当するページにジャンプしてこの2つのソフトウェアをダウンロードしてインストールしてから、MySQL Workbenchをインストールします。
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. MySQL Workbenchを開き、【Database】>【Connect to Database】を選択し、MySQLデータベースインスタンスのプライベートネットワーク（又はパブリックネットワーク）アドレスとユーザー名、パスワードを入力し、【OK】をクリックしてログインします。
 - Hostname：プライベートネットワーク（又はパブリックネットワーク）アドレスを入力します。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでプライベートネットワーク（又はパブリックネットワーク）アドレスとポート番号を確認できます。パブリックネットワークアドレスの場合は、[パブリックネットワークアドレスを有効にする](#waiwang)の説明に従って有効になっているかどうかを確認してください。
 - Port：プライベートネットワーク（又はパブリックネットワーク）に対応するポート。
 - Username：ユーザー名はデフォルトで「root」です。パブリックネットワーク接続の場合、接続制御を容易にするために別の[アカウントを作成](https://intl.cloud.tencent.com/document/product/236/31900)することをお勧めします。
 - Password：Usernameのパスワード。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照して変更できます。
![](https://main.qcloudimg.com/raw/946b50fb05de11d7c68c2262ac4fe933.png)
6. ログインに成功したページを図に示します。このページでは、MySQLデータベースの様々なモードやオブジェクトを見ることができ、テーブルの新規作成、データの挿入やクエリなどの操作を実行することができます。
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

## Linux CVMインスタンスから接続する方法
1. Linux CVMインスタンスにログインします。詳細については、<a href="https://cloud.tencent.com/document/product/213/2936" target="_blank">Linux CVMのカスタム設定</a>をご参照ください。
2. CentOS 7.2 64ビットシステムのCVMインスタンスを例に、次のコマンドを実行してMySQLクライアントをインストールします。
```
yum install mysql
```
`Complete！`が表示されると、MySQLクライアントのインストールが完了したことを示しています。
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)

3. 接続方法に基づいて、対応する操作を実行します。
 - **プライベートネットワーク接続：**
    1. 次のコマンドを実行して、TencentDB for MySQLインスタンスにログインします。
```
mysql -h hostname -u username -p
```
      - hostname：ターゲットであるTencentDB for MySQLインスタンスのプライベートネットワークアドレスに置き換えます。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでプライベートネットワークアドレスを確認できます。
    	- username：デフォルトのユーザー名rootに置き換えます。
    2. `Enter password：`のプロンプトが表示されたら、MySQLインスタンスのrootアカウントのパスワードを入力します。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照してパスワードをリセットしてください。
    この例で、`MySQL[（none）]>`が表示されると、MySQLに正常にログインしたことを示しています。
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **パブリックネットワーク接続：**

    1. 次のコマンドを実行して、TencentDB for MySQLインスタンスにログインします。
```
mysql -h hostname -P port -u username -p
```
      - hostname：ターゲットであるTencentDB for MySQLインスタンスのパブリックネットワークアドレスに置き換えます。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページでパブリックネットワークアドレスとポート番号を確認できます。パブリックネットワークアドレスが有効になっていない場合は、[パブリックネットワークアドレスを有効にする](#waiwang)の説明に従って有効にします。
      - port：パブリックネットワークのポート番号に置き換えます。
      - username：パブリックネットワークにアクセスするためのユーザー名に置き換えます。接続制御を容易にするために、[別のアカウント](https://intl.cloud.tencent.com/document/product/236/31900) を作成することをお勧めします。
    2. `Enter password：`が表示されたら、パブリックネットワーク接続用のユーザー名に対応するパスワードを入力します。パスワードを忘れた場合は、[パスワードのリセット](https://intl.cloud.tencent.com/document/product/236/31901)を参照してパスワードをリセットしてください。
    この例では、ホスト名は、59281c4exxx.myqcloud.comで、パブリックネットワークポート番号は15311です。
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. `MySQL [(none)]>`プロンプトで、SQLステートメントをMySQLサーバーに送信して実行できます。特定のコマンドラインについては、[mysql クライアントコマンド](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html)をご参照ください。
以下の図では例として`show databases； `を説明します。
![](https://mc.qcloudimg.com/static/img/76b4346a84f7388ae263dc6c09220fc0/image.png)


## [付録1：パブリックネットワーク接続アドレスを有効にする](id:waiwang)
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb/ )にログインし、インスタンスリストでインスタンス名又は「操作」列の【管理】をクリックしてインスタンス詳細ページに進みます。
2. [基本情報]セクションで、パブリックネットワークアドレスを有効にします。
>?パブリックネットワークアドレスとパブリックネットワークポート情報がある場合は、パブリックネットワークアドレスが有効になっていることを示しています。
>
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
3. 表示されるダイアログボックスで、【OK】をクリックします。
>?
>- 有効化に成功したら、基本情報からパブリックネットワークアドレスを確認することができます。
>- パブリックネットワークアクセスは、スイッチを使用して無効にすることができます。パブリックネットワークを再度有効にすると、ドメイン名に対応するパブリックネットワークアドレスが変わりません。

## 付録2：ネットワーク接続の検証方法
telnetコマンドを使用してネットワーク接続の問題をすばやくトラブルシューティングして特定することをお勧めします。詳細については、 [telnet コマンド](https://intl.cloud.tencent.com/document/product/236/31929)をご参照ください。

telnetコマンドを介してTencentDBインスタンスのネットワーク接続が良好であることを確認したが、CVMでコマンドラインを介してTencentDBインスタンスにログインしようとするとエラーメッセージが表示された場合は、[インスタンスへの接続に関する問題]](https://intl.cloud.tencent.com/document/product/236/37783)をご参照ください。

## 付録3：接続できないインスタンスのトラブルシューティング
インスタンスに接続できないなどの問題が発生した場合は、 [接続確認ツール](https://intl.cloud.tencent.com/document/product/236/31927)を使用してインスタンスへの接続に関するトラブルシューティングを行い、チェックレポートに従って[インスタンスに接続できない時の対処法](https://intl.cloud.tencent.com/document/product/236/37864)ドキュメントを参考して適切な解決策を見つけることをお勧めします。

