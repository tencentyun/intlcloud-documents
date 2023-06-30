## 操作場面
WordPressは、PHP言語を使用して開発されたブログプラットフォームです。ユーザーは、PHPとMySQLデータベースをサポートするサーバーに、自分のウェブサイトを設置することができます。また、WordPressをコンテンツ管理システム(CMS)として使用することも可能です。

このドキュメントはDocker Hubの公式イメージ`wordpress`で公的にアクセス可能なWordPressウェブサイトを作成する方法を紹介します。


##  前提条件
>!
>- `wordpress`このイメージにはWordPressのすべての運行環境が含まれているので、直接プルしてサービスを作成すればいいです。
>- 単一インスタンスバージョンのWordPressを作成するのはテスト用のみです。データの持続的な保存は保証できません。自作のMySQLやTencentDBでデータを保存することをお勧めします。詳細は[TencentDBを使用しているWordPress](/doc/product/457/7447)をご参照ください。 
>
-　[Tencent Cloudアカウント登録](https://intl.cloud.tencent.com/register)済みです。
- クラスターが作成されました。クラスターの作成については、[クラスター作成](https://intl.cloud.tencent.com/document/product/457/30637)をご参照ください。

## 操作手順
### WordPressサービス作成
1. Tencent Kubernetes Engineコンソールにログインし、左側のナビゲーションバーで**[ Cluster ](https://console.cloud.tencent.com/tke2/cluster)**を選択します。
2. 「クラスター管理」ページでサービスを作成する必要のあるクラスターIDを選択し、クラスターのロード「Deployment」ページに入って、** Create**をクリックします。下図の通りです：
![](https://main.qcloudimg.com/raw/1e32ac2e0e8d99315305f1b55034d691.png)
3. 「Create Workload」ページで次の情報によって、ロードの基本情報を設定します。下図の通りです：
![](https://main.qcloudimg.com/raw/a1c6b34a108a7a24d3f22e7048dec3ef.png)
 - **ロード名**：作成するロードの名前を入力し、本文はwordpressを例として説明します。
 - **説明**：ロードについての情報を記入します。
 - **タグ**：key = value、この例ではタグのデフォルト値はk8s-app = **wordpress**です。
 - **ネームスペース**：実際の必要に応じて選択します。
 - **タイプ**：実際の必要に応じて選択します。
 - **データボリューム**：実際の必要に応じてロードのマウントを設定します。詳細は[Volume管理](https://intl.cloud.tencent.com/document/product/457/30678)をご参照ください。
4. 次の提示によって、**インスタンスコンテナ**を設定します。
主なパラメータ情報は下記の通りです。他のオプションはディフォルト値を保ちます：
 - **名前**：カスタマイズコンテナの名前を入力し、本文はtestを例として説明します。
 - **イメージ**：`wordpress`を入力します。
 - **イメージバージョン（Tag）**：latestを入力します。
 - **イメージプルポリシー**：次の三つのポリシーを提供し、必要に応じて選択してください。本文は設定しなくてデフォルトポリシーを使用するのを例として説明します。
   イメージプルポリシーを設定しなくて、イメージバージョンはnullや`latest`の時、Alwaysポリシーを使用し、そうでなければIfNotPresentポリシーを使用します。
    - **Always**：いつもリモートでこのイメージをプルします。
    - **IfNotPresent**：ローカルイメージをデフォルトで使用し、ローカルにこのイメージがない場合、リモートでこのイメージをプルします。
    - **Never**：ローカルイメージだけを使用し、ローカルにこのイメージがない場合、異常を報告します。
6. 次の提示によって、サービスするインスタンス数量を設定します。下図の通りです：
![](https://main.qcloudimg.com/raw/649c9a62a29a77d09451e6d0dc487d58.png)
 - **手動調整**：インスタンス数量を設定し、本文のインスタンス数量は１に設定します。「＋」や「ー」をクリックして、インスタンス数量をコントロールします。
 - **自動調整**：いずれかの設定条件を満たせば、インスタンス（pod）数量を自動的に調整します。詳細は[サービスの自動的なスケールアウトとスケールイン](https://intl.cloud.tencent.com/document/product/457/32424)をご参照ください。
8. 次の提示によって、ロードの**アクセス設定（Service）**をします。
 - **Service**：「使用」を選択します。
 - **サービスのアクセス方式**：「パブリックネットワークLBでアクセス」を選択します。
 - **Cloud Load Balancer**：実際の必要に応じて選択します。
 - **ポートマッピング**：TCPプロトコルを選択し、コンテナポートとサービスポートを80に設定します。
>!サービスのあるクラスターのセキュリティグループはノードネットワークとコンテナネットワークをインターネットにオープンしてください。同時に、30000 - 32768ポートをインターネットにオープンする必要もありますが、そうでなければTencent Kubernetes Engineが使用できない問題が発生する場合があります。詳細は[Tencent Kubernetes Engineセキュリティグループ設定](https://intl.cloud.tencent.com/document/product/457/9084)をご参照ください。
9. **Create Workload**をクリックし、wordpressサービスの作成を完了します。


###  WordPressサービスにアクセス

次の二つの方式でWordPressサービスにアクセスできます。

#### Cloud Load Balancer IPでWordPressサービスにアクセス
1. 左側ナビゲーションバーで**[ Cluster](https://console.cloud.tencent.com/tke2/cluster)**をクリックして、「クラスター管理」ページに入ります。
2. WordPressサービスのあるクラスターIDをクリックして、**Services and Routes** > **Service**を選択します。
3. サービス管理のページに入って、WordPressサービスのCloud Load Balancer　IPをコピーして、次の通りです。
![](https://main.qcloudimg.com/raw/8a8ea1dc181ab31660313ed0883bc980.png)
4. ブラウザのアドレスバーにCloud Load Balancer　IPを入力し、「**Enter**」を押すと、サービスにアクセスできます。

#### サービスの名前でサービスにアクセス
クラスター内の他のサービスやコンテナはサービスの名前で直接にアクセスできます。

### WordPressサービス検証
サービスは成功的に作成されました。サービスにアクセスする時、直接にWordPressサーバーの構成ページに入ります。次の通りです。
![](https://main.qcloudimg.com/raw/4ccbffc42a7f9381e2595175ea32be65.png)

### その他のWordPress設定
コンテナの作成に失敗した場合、[よくある質問](https://intl.cloud.tencent.com/document/product/457/8187)をご参照ください。

