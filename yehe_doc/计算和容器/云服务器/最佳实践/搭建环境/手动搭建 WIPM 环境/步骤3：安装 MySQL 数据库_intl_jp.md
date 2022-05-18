## 概要
本ドキュメントでは、Windows Server 2012 R2 データセンターバージョン64ビット英語版OSのCVMを例として、MySQL 8.0.19の構築を具体的な手順を紹介します。
通常の状況下では、WindowsシステムにはSQL Serverデータベースが多く使用されますが、SQL Serverは優勝製品であり、自ら認証を行う必要があるため、 [TencentDB for SQL Serverインスタンス](https://intl.cloud.tencent.com/product/sqlserver)を購入することもできます。

## 操作手順

### MySQLインストールパッケージをダウンロードする
1. CVMにログインします。
2. CVMでブラウザを開き、[MySQL公式サイト](https://www.mysql.com/)にアクセスし、MySQLインストールパッケージをダウンロードします。

### MySQL基本環境をインストールする

1. 下図に示すように、MySQLインストールパッケージをダブルクリックして開き、「Choosing a Setup Type」インストール画面で**Developer Default**を選択し、**Next**をクリックします：
![](https://qcloudimg.tencent-cloud.cn/raw/46578b0e47c0a8283c72680070578916.png)
2. 「Check Requirements」インストール画面で**Execute**をクリックし、画面の表示に従ってMySQLの基本環境を設定します。
3. **Next**をクリックします。
4. 「Installation」インストール画面で**Execute**をクリックし、MySQLに必要なインストールパッケージをインストールします。
5. MySQLに必要なインストールパッケージのインストールが完了した後、**Next**をクリックして「Product Configuration」設定画面に入ります。


### MySQLの設定

#### MySQLサービスの設定

1. 「Product Configuration」設定画面で、**Next**をクリックします。
2. 下図に示すように、「Hight Availability」画面で**Standalone MySQL Server / Classic MySQL Replication**を選択し、**Next**をクリックします：
![](https://qcloudimg.tencent-cloud.cn/raw/821c0ab18a477ffdf3458889ff698b08.png)
3. 下図に示すように、「Type and Networking」設定画面で、デフォルト設定を維持し、**Next**をクリックします。
<dx-alert infotype="explain" title="">
- デフォルトではTCP/IPネットワークを有効にします。
- デフォルトでは3306ポートを使用します。
</dx-alert>
4. Authentication Methodの設定画面で、<b>Use Legacy Authentication Method(Retain MySQL 5.x Compatibility)</b>を選択し、**Next**をクリックします。下図の通りです：
このドキュメントはWordPressのWebサイトを構築するためのオプションを設定しています。必要に応じたオプションを選択できます。
![](https://qcloudimg.tencent-cloud.cn/raw/599dff879af20e25ce1d8e7fb5b1a33f.png)
5. 下図に示すように、rootパスワードを設定し、**Next**をクリックします：
![](https://qcloudimg.tencent-cloud.cn/raw/a85f3a6affb6d71dda27a7a1fe5a5870.png)
6. 下図に示すように、「Windows Service」設定画面で、デフォルト設定を維持し、**Next**をクリックします：
7. 「Apply Configuration」設定画面で、**Execute**をクリックします。
8. **Finish**をクリックし、MySQLサービス設定が完了します。

#### MySQLルーターの設定

1. 「Product Configuration」設定画面で、**Next**をクリックします。
2. 下図に示すように、「MySQL Router Configuration」設定画面で、デフォルト設定を維持し、**Finish**をクリックします：
![](https://qcloudimg.tencent-cloud.cn/raw/f13a5db6d40390a3b5c650e00720d587.png)

#### MySQLサンプルの設定

1. 「Product Configuration」設定画面で、**Next**をクリックします。
2. 下図に示すように、「Connect To Server」設定画面で、rootのパスワードを入力し、**Check**をクリックします。
3. 下図に示すように、rootパスワードの認証成功後、**Next**をクリックします：
![](https://qcloudimg.tencent-cloud.cn/raw/5e4157ae76b5ae7aa4f7e9d99f40bfe8.png)
4. 「Apply Configuration」設定画面で、**Execute**をクリックします。
5. **Finish**をクリックして、MySQLサンプルの設定が完了します。
6. 「Product Configuration」設定画面で、**Next**をクリックします。
7. 下図に示すように、「Installation Complete」画面で、実際のニーズに応じて、有効にする必要があるMySQL環境にチェックを入れ、**Finish**をクリックします。
   - 下図のようなMySQL Workbenchが正常に開けば、MySQLのインストールは完了です。
   ![](https://qcloudimg.tencent-cloud.cn/raw/7f960c3d6e8c26f9fb68ee9de5d5b96b.png)
   - 下図のようなMySQL Shellが正常に開けば、MySQLのインストールは完了です。
   ![](https://qcloudimg.tencent-cloud.cn/raw/985d2e239aae0bcc1d84f51e3eecd296.png)


### セキュリティグループルールの追加

購入済みのCVMインスタンスのセキュリティグループのインバウンドルールを追加し、3306ポートを開放します。
具体的な操作については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。





