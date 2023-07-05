## 操作場面
このドキュメントはコンテナクラスター内のNginxサービスを迅速に作成する方法を紹介します。

## 前提条件
-　[Tencent Cloudアカウント登録](https://intl.cloud.tencent.com/register)済みです。
-  クラスターが作成されました。クラスターの作成については、[クラスター作成](https://intl.cloud.tencent.com/document/product/457/30637)をご参照ください。

## 操作手順

### Nginxサービス作成
1. Tencent Kubernetes Engineコンソールにログインし、左側のナビゲーションバーで【[ Clusters ](https://console.cloud.tencent.com/tke2/cluster)】を選択します。
2. 「クラスター管理」ページでサービスを作成する必要のあるクラスターIDを選択し、クラスターのロード「Deployment」ページに入って、【Create】をクリックします。下図の通りです：
![](https://main.qcloudimg.com/raw/036baf23123e7291d5fcfb82a2572e53.png)
3. 「Create Workload」ページで次の情報によって、ロードの基本情報を設定します。下図の通りです：
![](https://main.qcloudimg.com/raw/a1391e5768e6fd5cfe0e6b3c65417a50.png)
  - **ロード名**：作成するロードの名前を入力し、本文はnginxを例として説明します。
  -  **説明**：ロードについての情報を記入します。
  -  **タグ**：key = value、この例ではタグのデフォルト値がk8s-app = **nginx**です。
  -  **ネームスペース**：実際のニーズによって選択します。
  -  **タイプ**：実際のニーズによって選択します。
  -   **ボリューム**：実際のニーズによってロードのマウントを設定します。詳細は[Volume管理](https://intl.cloud.tencent.com/document/product/457/30678)をご参照ください。
4. 次の情報を参照して「インスタンスコンテナ」を設定します。下図の通りです：
![](https://main.qcloudimg.com/raw/2ec2c7c803ee61a2d218f17df785636e.png)
主なパラメータ情報は下記の通りです：
  - **名前**：インスタンスコンテナの名前を入力し、本文はtestを例として説明します。
  - **イメージ**：【 Select an image】をクリックし、ポップアップボックスで【DockerHub Image】> **nginx**を選択して、【OK】をクリックします。
  - **イメージバージョン（Tag）**：デフォルト値`latest`を使用します。
  - **イメージプルポリシー**：次の三つのポリシーを提供し、ニーズによって選択してください。本文は設定しなくてデフォルトポリシーを使用することを例として説明します。
    イメージプルポリシーを設定しなくて、イメージバージョンはnullや`latest`の時、Alwaysポリシーを使用し、そうでなければIfNotPresentポリシーを使用します。
    - **Always**：いつもリモートでこのイメージをプルします。
    - **IfNotPresent**：ローカルイメージをデフォルトで使用し、ローカルにこのイメージがない場合、リモートでこのイメージをプルします。
    - **Never**：ローカルイメージだけを使用し、ローカルにこのイメージがない場合、異常を報告します。
5. 「インスタンス数量」では、次の情報によってサービスのインスタンス数量を設定します。下図の通りです：
![](https://main.qcloudimg.com/raw/51c4971952bbd697ca458a415fd1ce21.png)
 - **手動調整**：インスタンス数量を設定し、本文のインスタンス数量は１に設定します。「＋」や「-」をクリックして、インスタンス数量をコントロールします。
 - **自動調整**：いずれかの設定条件を満たせば、インスタンス（pod）数量を自動的に調整します。詳細は[サービスの自動的なスケールアウトとスケールイン](https://intl.cloud.tencent.com/document/product/457/32424)をご参照ください。
6.   次の提示によって、ロードのアクセス設定をします。下図の通りです：   
![](https://main.qcloudimg.com/raw/aedd2d73ab7e5f79218d8194c9b1c249.png)
 - **Service**：「使用」を選択します。
 - **サービスのアクセス方式**：「パブリックネットワークを提供してアクセス」を選択します。
 - **Cloud Load Balancer**：実際のニーズによって選択します。
 - **ポートマッピング**：TCPプロトコルを選択し、コンテナポートとサービスポートを80に設定します。
 >!サービスのあるクラスターのセキュリティグループはノードネットワークとコンテナネットワークをインターネットにオープンする必要があります。同時に、30000 - 32768ポートをインターネットにオープンする必要もあるし、そうでなければTencent Kubernetes Engineが使用できない問題が発生するかもしれません。詳細は[Tencent Kubernetes Engineセキュリティグループ設定](https://intl.cloud.tencent.com/document/product/457/9084)をご参照ください。
7. 【Create workload】をクリックして、Nginxサービスの作成を完了します。


### Nginxサービスにアクセス

次の二つの方式でNginxサービスにアクセスできます。

#### **Cloud Load Balancer IP**でNginxサービスにアクセス

1. 左側ナビゲーションバーで【[ Clusters ](https://console.cloud.tencent.com/tke2/cluster)】をクリックして、「クラスター管理」ページに入ります。
2. NginxサービスのあるクラスターIDをクリックして、【Service】>【Service】を選択します。
3. サービス管理のページでNginxサービスのCloud Load Balancer　IPをコピーして、次の通りです。
![](https://main.qcloudimg.com/raw/bab54241805b352ae007ece3d130bb4a.png)
4. ブラウザのアドレスバーにCloud Load Balancer　IPを入力し、「**Enter**」を押すと、サービスにアクセスできます。

#### サービスの名前でNginxサービスにアクセス

クラスター内の他のサービスやコンテナはサービスの名前で直接にアクセスできます。

### Nginxサービス検証
サービスは作成されました。サービスにアクセスする時、直接にNginxサーバーのディフォルトウェルカムページに入ります。下図の通りです：
![](https://main.qcloudimg.com/raw/156e6d3b804e6b214ef7600fee4fa9c1.png)

### その他のNginx設定
コンテナの作成に失敗した場合、[よくある質問](https://intl.cloud.tencent.com/document/product/457/8187)をご参照ください。
