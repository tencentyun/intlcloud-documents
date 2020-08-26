[MySQLコンソール](https://console.cloud.tencent.com/cdb)又は[API](https://intl.cloud.tencent.com/document/product/236/15860)でパラメータの一部を確認、変更でき、また、コンソールでパラメータ変更履歴を問い合わせることもできます。

## パラメータ値の変更
>
>- 変更されたパラメータを有効にするためにインスタンスを再起動する必要がある場合は、再起動するかを確認するメッセージが表示されます。サービスの低いピーク時に操作すること、及びアプリケーションの再接続メカニズムを確認することを推奨します。
>- パラメータの変更を送信する前に、パラメータの横にある<img src="https://main.qcloudimg.com/raw/81fc2494e8b61ff36a63d23cccb61cd1.png"  style="margin:0;">又は変更ページの【キャンセル】をクリックして変更をキャンセルできます。

### パラメータの一括変更
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、【インスタンスリスト】ページでインスタンス名又は操作列の【管理】をクリックして、【インスタンス管理】ページに入ります。
2. 【データベース管理】>【パラメータ設定】ページを選択し、【パラメータの一括変更】をクリックします。
![](https://main.qcloudimg.com/raw/3ec389dafa09276ae66b00a71445d9d3.png)
3. 「パラメータ実行値」カラムで、変更したいパラメータを選択して変更を実行し、間違いがないことを確認した後、【変更の確認】をクリックします。
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. 表示されたダイアログボックスで同意をチェックし、【OK】をクリックします。

### 個々のパラメータの変更
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、【インスタンスリスト】ページでインスタンス名又は操作列の【管理】をクリックして、【インスタンス管理】ページに入ります。
2. 【データベース管理】>【パラメータ設定】ページを選択し、ターゲットであるパラメータの行を選択し、「パラメータ実行値」カラムで<img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">をクリックしてパラメータ値を変更します。
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. 「パラメータ変更可能値」カラムからの提示に従って、ターゲットであるパラメータの値を入力し、<img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;">をクリックして保存を実行します。<img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;">をクリックして操作をキャンセルします。
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. 表示されたダイアログボックスで、【OK】をクリックします。

### パラメータテンプレートからのインポート
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、【インスタンスリスト】ページでインスタンス名又は操作列の【管理】をクリックして、【インスタンス管理】ページに入ります。
2. 【データベース管理】>【パラメータ設定】ページを選択し、【テンプレートからインポート】をクリックします。
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. 表示されたダイアログボックスで、パラメータテンプレートを選択し、【インポートして元のパラメータを上書き】をクリックします。
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)

### パラメータのインポート
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、【インスタンスリスト】ページでインスタンス名又は操作列の【管理】をクリックして、【インスタンス管理】ページに入ります。
2. 【データベース管理】>【パラメータ設定】ページを選択し、【パラメータのインポート】をクリックします。
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. 表示されたダイアログボックスで、アップロードするファイルを選択した後、【インポートして元のパラメータを上書き】をクリックします。
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
	
## パラメータ変更履歴の確認
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、【インスタンスリスト】ページでインスタンス名又は操作列の【管理】をクリックして、【インスタンス管理】ページに入ります。
2. 【データベース管理】>【パラメータ設定】ページを選択し、右の【最近の変更履歴】をクリックします。
![](https://main.qcloudimg.com/raw/6d6318fce61fc78c6ff3611479ae5714.png)
3. 【パラメータの最近変更履歴】ページでは、最近のパラメータ変更履歴を確認できます。
![](https://main.qcloudimg.com/raw/4c616b40d058f114e8f75c4021c02648.png)

