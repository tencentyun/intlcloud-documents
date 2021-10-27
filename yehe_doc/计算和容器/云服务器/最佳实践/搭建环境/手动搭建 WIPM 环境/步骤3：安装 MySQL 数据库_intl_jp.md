## 操作シナリオ
このドキュメントでは、Windows Server 2012 R2 Datacenterエディションの64ビット中国語版OSのCVMを例として、MySQL 8.0.19を構築する具体的な手順についてご紹介します。
通常の状況下では、WindowsシステムにはSQL Serverデータベースが多く使用されますが、SQL Serverは有料製品であり、自ら権限設定を行う必要があるため、 [Tencent Cloudクラウドデータベース TencentDB for SQL Serverインスタンス](https://intl.cloud.tencent.com/product/sqlserver)を購入することもできます。

## 操作手順

### MySQLインストールパッケージをダウンロードする
1. CVMにログインします。
2. CVMでブラウザを開き、[MySQL公式サイト](https://www.mysql.com/)にアクセスし、MySQLインストールパッケージをダウンロードします。

### MySQL基本環境をインストールする

1. MySQLインストールパッケージをダブルクリックして開き、「Choosing a Setup Type」インストール画面で【Developer Default】を選択し、【Next】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/4077db7bfe9f7b97e1d7ddd649efa966.png)
2. 「Check Requirements」インストール画面で【Execute】をクリックし、画面の表示に従ってMySQLの基本環境を設定します。 下図に示します。
![](https://main.qcloudimg.com/raw/16a5f7190d7720562681528072cf8129.png)
3. 【Next】をクリックします。
4. 「Installation」インストール画面で【Execute】をクリックし、MySQLに必要なインストールパッケージをインストールします。下図に示します。
![](https://main.qcloudimg.com/raw/1b4a3e338bb816e7c47b4603a7a1dbb4.png)
5. MySQLに必要なインストールパッケージのインストールが完了した後、【Next】をクリックし、「Product Configuration」設定画面に入ります。


### MySQLの設定

#### MySQLサービスの設定

1. 「Product Configuration」設定画面で、【Next】をクリックします。
2. 「Hight Availability」画面で【Standalone MySQL Server / Classic MySQL Replication】を選択し、【Next】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/5355f286598388f9e9846bf8122e6d98.png)
3. 「Type and Networking」設定画面で、デフォルト設定を維持し、【Next】をクリックします。下図に示します。
>? 
> - デフォルトではTCP/IPネットワークが有効になっています。
> - デフォルトでは3306ポートを使用します。
> 
![](https://main.qcloudimg.com/raw/fbece2fafb34beb5825ae294a8e214fd.png)
4. 「Authentication Method」設定画面で、デフォルト設定を維持し、【Next】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/402624aaf02dce01ca2912d3548c03de.png)
5. rootパスワードを設定し、【Next】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/a0472f0b93c590997e78c2f590a0f901.png)
6. 「Windows Service」設定画面で、デフォルト設定を維持し、【Next】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/a85625c446218a275e743ff0ec599ece.png)
7. 「Apply Configuration」設定画面で、【Execute】をクリックします。
![](https://main.qcloudimg.com/raw/2ee6000630d88774951ddf8aaea16fbb.png)
8. 【Finish】をクリックすると、MySQLサービス設定が完了します。

#### MySQLルーターの設定

1. 「Product Configuration」設定画面で、【Next】をクリックします。
2. 「MySQL Router Configuration」設定画面で、デフォルト設定を維持し、【Finish】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/adece1334b6e1579eb2ace782cf47c59.png)

#### MySQLサンプルの設定

1. 「Product Configuration」設定画面で、【Next】をクリックします。
2. 「Connect To Server」設定画面で、rootのパスワードを入力し、【Check】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/ab8637391012a14ab2e5160c61675912.png)
3. rootパスワードの認証成功後、【Next】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/bff0aece8da11d15a52f4db91b4d7e69.png)
4. 「Apply Configuration」設定画面で、【Execute】をクリックします。
![](https://main.qcloudimg.com/raw/8fe1f90eed50860e064044b314719cf6.png)
5. 【Finish】をクリックすると、MySQLサンプルの設定が完了します。
6. 「Product Configuration」設定画面で、【Next】をクリックします。
7. 「Installation Complete」画面で、実際のニーズに応じて、有効にする必要があるMySQL環境にチェックを入れ、【Finish】をクリックします。下図に示します。
![](https://main.qcloudimg.com/raw/13f46296b85b00ce7e3bd08be13108c9.png)
 - 下図のようなMySQL Workbenchが正常に開けば、MySQLのインストールは成功です。
![](https://main.qcloudimg.com/raw/288f4cfbf1a9671b73dff64a940e0dc1.png)
 - 下図のようなMySQL Shellが正常に開けば、MySQLのインストールは成功です。
![](https://main.qcloudimg.com/raw/90b788ffe3a8f92e0e5e70f35fb94356.png)


### セキュリティグループのルールの追加

購入済みのCVMインスタンスのセキュリティグループのインバウンドルールを追加し、3306ポートを開放します。
具体的な操作については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。






