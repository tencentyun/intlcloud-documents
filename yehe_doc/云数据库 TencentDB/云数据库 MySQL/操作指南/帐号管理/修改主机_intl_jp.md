## 操作シナリオ
TencentDB for MySQLコンソールでデータベースアカウントによって認証されたホストアドレスを変更することにより、データベースへのクライアントアクセスを制御して、データベースのアクセスセキュリティを向上させることができます。

##　操作手順
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインします。
2. インスタンスリストから変更するインスタンスを選択し、インスタンス名又は【操作】列の【管理】をクリックすると、インスタンス管理ページが表示されます。
3. 【データベース管理】>【アカウント管理】タブを選択して、ホストを変更するアカウントを見つけて、【その他】>【ホストを変更】を選択します。
![](https://main.qcloudimg.com/raw/9f6a4add3bde860cde8c9565f4f0a3d5.png)
4. ポップアップされたホスト変更ダイアログボックスで、新しいホストアドレスを入力して【OK】をクリックすれば、アカウントによって認証されたホストアドレスを変更することができます。
> ホストアドレスはIPアドレスをサポートしています。すべてのクライアントが、このデータベースアカウントを使用してデータベースにアクセスすることを許可する場合は、「%」を入力してください。
>
![](https://main.qcloudimg.com/raw/113ed501aa7687c9812da29e9314daeb.png)


