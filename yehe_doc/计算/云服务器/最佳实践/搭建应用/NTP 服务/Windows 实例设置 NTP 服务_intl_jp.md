## ユースケース

このドキュメントでは、Windows ServerでNTPサービスを有効にし、クロックソースサーバーのアドレスを変更する方法について説明します。

Windowsタイムサービス（Windows Time service、 W32Time）は、ローカルシステムとクロックソースサーバー間の時刻を同期するために使用されます。 ネットワークタイムプロトコル（NTP）を使用して、ネットワーク全体でコンピューターのクロックを同期します。  以下では、Windows Server 2016を例として、クライアントとコマンドラインを使用してNTPサービスを有効にし、クロックソースサーバーアドレスを変更する方法について説明します。

## 操作手順

1. [Windowsインスタンスへのリモートログイン](https://intl.cloud.tencent.com/document/product/213/5435)。
2.「管理 > サービス > Windows Time」をクリックします。
![Windows Time](https://main.qcloudimg.com/raw/c5e41df2fc832b0f25f798408163664c.png)
3. 起動の種類は「自動」に設定されています。サービスが起動されていない場合は、「起動」をクリックします。
![w32time](https://main.qcloudimg.com/raw/9201ddaca176a1523d5d12d02b6c8ec5.png)
4. タスクバーの通知領域で、時刻をクリックし、「日付けと時刻」をクリックします。
![時刻設定](https://main.qcloudimg.com/raw/28ba1cf5968466e114e93d222b957f99.png)	
5. 「インターネット時刻」タグに切り替えて、設定の変更をクリックします。
![Internet時刻](https://main.qcloudimg.com/raw/acc52fce975638cef4e39f9f821d66bc.png)
6.  Internet 時刻の設定ウィンドウで、ターゲットクロックソースサーバーのドメイン名またはIPアドレスを入力し、「OK」をクリックします。
![Internet時刻設定](https://main.qcloudimg.com/raw/205ef59f3e8583af965a9381df0a9ef9.png)
7. 設定が完了したら、「日付と時刻」を再度開くと、クロックソースサーバーが変更されていることがわかります。
![確認](https://main.qcloudimg.com/raw/767eee448b33ed38ea7bc2fbdadf780d.png)


