
### ローカルのSQLファイルをTencentDB for MySQLインスタンスにインポートするにはどうすればよいですか。
>?2ノードおよび3ノードのTencentDB for MySQLインスタンスのみがSQLファイルのインポートをサポートします。
>
1. [TencentDB for MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンス名をクリックして管理画面に進みます。
2. 【データベース管理】≻【データベースリスト】≻【データのインポート】を選択します。インポートするファイルを選択してから、ターゲットデータベースを選択し、【OK】をクリックしてデータをインポートします。
>?インポートする単一のSQLファイルのサイズは2GB以下である必要があります。ファイル名には、英字、数字、およびアンダーラインのみを含めることができます。
>
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
詳細については、[SQLファイルのインポート](https://intl.cloud.tencent.com/document/product/236/8466)をご参照ください。

### データベースのデータをどうやってエクスポートしますか。
- バックアップデータをエクスポートするには、[コンソール](https://console.cloud.tencent.com/cdb)でインスタンス名をクリックして管理画面に入り、【バックアップと復元】タブを選択してダウンロードします。
- リアルタイムデータをエクスポートするには、[読み取り専用インスタンス](https://intl.cloud.tencent.com/document/product/236/7270)を購入し、インスタンスに接続後、mysqldumpツールを使用してリアルタイムデータを取得できます。

### 7GBのデータベースを TencentDB for MySQL インスタンスに移行する最速の方法は何ですか。
[データ移行](https://intl.cloud.tencent.com/zh/document/product/571/34103)機能を使用することをお勧めします。お客様のソースデータベースに直接接続してデータを同期できます。

