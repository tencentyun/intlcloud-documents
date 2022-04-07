## 操作場面
[単一インスタンスバージョン WordPress](https://intl.cloud.tencent.com/document/product/457/7205) の例は迅速にWordPressサービスを作成する方法を示します。この方法で作成されたWordPressサービスの特徴は次の通りです：
- データは同じコンテナが運行されているMySQL DBに書き込みます。
- サービスは迅速に起動することができます。
- コンテナがある原因で停止すれば、DBとストレージファイルは失います。

MySQL DBでデータを永遠にストレージすることができます。DBはインスタンス／コンテナが再び起動した後、存在し続けます。このドキュメントは[TencentDB](https://intl.cloud.tencent.com/product/cdb)でMySQL　DBを設定する方法とTencentDBのWordPressサービスを作成して使用する方法を紹介します。

##  前提条件
-　[Tencent Cloudアカウント登録](https://intl.cloud.tencent.com/register)済みです。
- クラスターが作成されました。クラスターの作成については、[クラスター作成](https://intl.cloud.tencent.com/document/product/457/30637)をご参照ください。
>?本文が使用されているDBは[MySQL](https://intl.cloud.tencent.com/document/product/236/5147)です。


## 操作手順

### WordPressサービス作成
#### TencentDB作成
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、DBインスタンスリストの上で【 Create 】をクリックします。下図の通りです：
![](https://main.qcloudimg.com/raw/78b43441e5d296e83e2db9246aaddff7.png)
2. 購入する構成を選択します。詳細は[MySQL](https://intl.cloud.tencent.com/document/product/236/5147)をご参照ください。
>!TencentDBのある地域はクラスターと同じです。そうでなければこのDBに接続できません。

3. DBが成功的に作成された後、[MySQL-インスタンスリスト](https://console.cloud.tencent.com/cdb)で確認できます。
4. DBについて初期化操作を行います。詳細は[MySQLの初期化](https://intl.cloud.tencent.com/document/product/236/3128)をご参照ください。

#### TencentDBを使用するWordPressサービス作成
1. Tencent Cloud　Tencent Kubernetes Engineコンソールにログインし、左側のナビゲーションバーで【[ Cluster](https://console.cloud.tencent.com/tke2/cluster)】を選択します。
2. 「クラスター管理」ページでサービスを作成する必要のあるクラスターIDを選択し、クラスターのロード「Deployment」ページに入って、【Create】をクリックします。下図の通りです：
![](https://main.qcloudimg.com/raw/239bfe0c3488c19139c5359b27d24044.png)
3. 「Workloadの新規作成」ページで次の情報によって、ロードの基本情報を設定します。下図の通りです：
![](https://main.qcloudimg.com/raw/3ff74d307b48b793ac121345e7f19154.png)
 - **ロード名**：作成するロードの名前です。本文はwordpressを例として説明します。
 - **説明**：ロードについての情報を記入します。
 -  **タグ**：key = value、この例ではタグのデフォルト値がk8s-app = **wordpress**です。
 -  **ネームスペース**：必要に応じて選択します。
 -  **タイプ**：必要に応じて選択します。
 - **ボリューム**：必要に応じてロードのマウントを設定します。詳細は[Volume管理](https://intl.cloud.tencent.com/document/product/457/30678)をご参照ください。
4. 次の情報を参照して「インスタンスコンテナ」を設定します。次の通りです。
![](https://main.qcloudimg.com/raw/7e2fccaf2c0168743dc03480cab2a6f3.png)
主なパラメータ情報は下記の通りです。他のオプションはディフォルト設定を保ちます：
  - **名前**：カスタマイズコンテナの名前を入力し、本文はtestを例として説明します。
  - **イメージ**：`wordpress`を入力します。
  - **イメージバージョン（Tag）**：latestを入力します。
  - **イメージプルポリシー**：次の三つのポリシーを提供し、必要に応じて選択します。本文は設定しなくてデフォルトポリシーを使用するのを例として説明します。
イメージプルポリシーを設定しなくて、イメージバージョンはnullやlatestの時、Alwaysポリシーを使用し、そうでなければIfNotPresentポリシーを使用します。
      - **Always**：いつもリモートでこのイメージをプルします。
      - **IfNotPresent**：ローカルイメージをデフォルトで使用し、ローカルにこのイメージがない場合、リモートでこのイメージをプルします。
      - **Never**：ローカルイメージだけを使用し、ローカルにこのイメージがない場合、異常を報告します。
 - **環境変数**：次の構成情報を順番に入力します：
WORDPRESS_DB_HOST = MySQLのプライベートネットワークIP
WORDPRESS_DB_PASSWORD = 初期化の時、記入されたパスワード
5. 次の提示によって、サービスするインスタンス数量を設定します。下図の通りです：
![](https://main.qcloudimg.com/raw/06e71d9208795f57159bdaba8eae45b4.png)
 - **手動調整**：インスタンス数量を設定し、本文のインスタンス数量は１に設定します。「＋」や「ー」をクリックして、インスタンス数量をコントロールします。
 - **自動調整**：いずれかの設定条件を満たせば、インスタンス（pod）数量を自動的に調整します。詳細は[サービスの自動的なスケールアウトとスケールイン](https://intl.cloud.tencent.com/document/product/457/32424)をご参照ください。
6. 次の提示によって、ロードのアクセス設定をします。下図の通りです：
![](https://main.qcloudimg.com/raw/9d0d2970a6df63f6eb83bbc73deb7178.png)
 - **Service**：「使用」を選択します。
 - **サービスのアクセス方式**：「パブリックネットワークを提供してアクセス」を選択します。
 - **Cloud Load Balancer**：必要に応じて選択します。
  - **ポートマッピング**：TCPプロトコルを選択し、コンテナポートとサービスポートを80に設定します。
 >!サービスのあるクラスターのセキュリティグループはノードネットワークとコンテナネットワークをインターネットにオープンしてください。同時に、30000 - 32768ポートをインターネットにオープンする必要もありますが、そうでなければTencent Kubernetes Engineが使用できない問題が発生する場合があります。詳細は[Tencent Kubernetes Engineセキュリティグループ設定](https://intl.cloud.tencent.com/document/product/457/9084)をご参照ください。

7. 【 Create workload】をクリックして、WordPressサービスの作成を完了します。


### WordPressサービスにアクセス
次の二つの方式でWordPressサービスにアクセスできます。

#### Cloud Load Balancer IPでWordPressサービスにアクセス
1. 左側ナビゲーションバーで【[ Clusters](https://console.cloud.tencent.com/tke2/cluster)】をクリックして、「クラスター管理」ページに入ります。
2. WordPressサービスのあるクラスターIDをクリックして、【Service】>【Service】を選択します。
3. サービス管理のページに入って、WordPressサービスのCloud Load Balancer　IPをコピーして、下図の通りです：
![](https://main.qcloudimg.com/raw/f5f9964eacb4752e528ce32d467662a8.png)
4. ブラウザのアドレスバーにCloud Load Balancer　IPを入力し、**Enter**を押すと、サービスにアクセスできます。

#### サービスの名前でサービスにアクセス
クラスター内の他のサービスやコンテナはサービスの名前で直接にアクセスできます。

### WordPressサービス検証
サービスは成功的に作成されました。サービスにアクセスする時、直接にWordPressサーバーの構成ページに入ります。下図の通りです：
![](https://main.qcloudimg.com/raw/903f45d57c58541433b555d487bd2980.png)

### その他のWordPress設定
コンテナの作成に失敗した場合、[よくある質問](https://intl.cloud.tencent.com/document/product/457/8187)をご参照ください。
