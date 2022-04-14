本文では、TKEを使用してコンテナクラスターを速やかに作成する方法について説明します。


## ステップ1：Tencent Cloudアカウントの登録
Tencent Cloudのアカウント登録が済んでいる場合は、このステップを無視してかまいません。
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/zh/document/product/378/17985" target="_blank"  style="color: white; font-size:13px;">ここをクリックしてTencent Cloudのアカウントを登録します</a></div>

##　ステップ2：オンラインチャージ
TKEは当面、サービス料金がかかりません。ユーザーが実際に使用したクラウドリソースに応じて課金されます。ここで「ホスティングクラスター」を作成します。このモードでは、クラスターのワーカーノード、永続的なストレージおよびサービスにバインディングされたCLBなどのサービスについて料金を支払ってください。購入前に、アカウントにチャージしてください。詳細については、[オンラインチャージ](https://intl.cloud.tencent.com/document/product/555/7425)ドキュメントをご参照ください。



##　ステップ3：サービス認証
[Tencent Cloudコンソール](https://console.cloud.tencent.com/)で**クラウド製品**>**TKE**を選択し、[TKEコンソール]に移動し、画面の提示に従って、TKE認証を行います。（TKE認証を行った場合は、このステップを省略してください。）

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster?rid=1" target="_blank"  style="color: white; font-size:13px;">ここをクリックしてサービス認証を実行してください</a></div>


##　ステップ4：クラスターの新規作成
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster/create?rid=1" target="_blank"  style="color: white; font-size:13px;">ここをクリックしてクラスター作成ページに進みます</a></div>

### クラスターの情報
「クラスター情報」ページで、クラスター名を入力し、クラスターが存在する地域、クラスターネットワークおよびコンテナネットワークを選択します。その他のデフォルト・オプションはそのままにして、「**次へ**」をクリックします。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/48966b45ba60fe9116bb58edec3c58dd.png)

 - **クラスター名**：作成するクラスターの名前を入力します。ここでは、「test」を例に挙げます。
 - **所在地域**：あなたに最も近い地域を選択してください。
 - **クラスターネットワーク**：ノードのネットワークアドレス範囲内のIPアドレスをクラスター内のCVMに割り当てます。ここでは、既存のVPCネットワークを選択します。
 - **コンテナネットワーク**：コンテナネットワークアドレス範囲内のIPアドレスをクラスターのコンテナに割り当てます。ここで利用可能なコンテナネットワークを選択します。


### モデルの選択
[モデルの選択]ページで、課金モードを確認し、アベイラビリティーゾーンとそれに対応するサブネットを選択し、ノードのモデルを確認して、[**次へ**]をクリックします。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/ef0eddd2e2a0ea044774c4ee65d0a2ef.png)

- **ノードのソース**：**新規ノード**と**既存ノード**の2つのオプションが用意されています。ここでは、「新規ノード」を選択します。
- **Masterノード**：**プラットフォームホスティング**と**個別デプロイ**の2つのクラスターモードから選択できます。ここでは、「プラットフォームホスティング」を選択します。
- **課金モード**：**従量課金**1つの課金モードを提供します。ここでは「従量課金」を選択します。
- **Worker設定**：このモジュールでは、アベイラビリティーゾーンとそれに対応するサブネットを選択し、ノードのモデルを確認するだけで済みます。その他の設定項目はデフォルトのままです。
  - **アベイラビリティーゾーン**：ここでは「広州三区」を選択します。
  - **ノードネットワーク**：現在のVPCネットワークのサブネットを選択します。
  - **モデル**：ここでは、「S1.SMALL1（標準型S1、1コア1GB）」を選択します。

### CVMの設定
「CVMの設定」ページで、ログイン方法を選択し、その他の設定項目はデフォルトのままにして、「**次へ**」をクリックします。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/83501db19590eccb230c482ae37bd3a9.png)

- **ログイン方式**：**キーの即時関連付け**、**パスワードの自動生成**、および**パスワードの設定**の3つのログイン方法があります。ここでは「パスワードの自動生成」を選択します。

### コンポーネント構成
「コンポーネントの構成」ページでは、必要に応じてストレージ、監視、イメージなどのコンポーネントを選択できます。インストールが不要な場合は、**次へ**をクリックします。ここでは、コンポーネントをインストールせず、その他の設定項目はデフォルトのままにします。

### 情報の確認
「情報の確認」ページで、クラスターで選択した設定情報および料金を確認し、「**完了**」をクリックします。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/bebdbb0524ba191175daa935b9d7d986.png)


支払いが完了すると、最初のクラスターを作成できます。次に、[TKEコンソール](https://console.cloud.tencent.com/tke2/cluster?rid=1)で、作成したホスティングクラスターを表示できます。

##　ステップ5：クラスタ－の表示
作成されたクラスターが[クラスターリスト](https://console.cloud.tencent.com/tke2/cluster?rid=1)に表示されます。クラスターIDをクリックすると、クラスターの詳細ページに移動できます。クラスターの「基本情報」ページでは、クラスター情報、ノードおよびネットワーク情報などを表示できます。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/0f36c74372186d3efdf1ba2f1751f228.png)




##　ステップ6：クラスターの削除
クラスターの起動時にリソースの消費が開始されます。このステップでは、不要なコストを回避するために、すべてのリソースをパージする方法を説明します。

1.左側のナビゲーションバーで「**クラスター**」を選択し、「クラスターの管理」ページでクラスター削除行の右側の**その他** >**削除**を選択します。下図の通りです：
![](https://qcloudimg.tencent-cloud.cn/raw/9431c8e5c0038ec85e1e04edbc217b0c.png)
2.「クラスターの削除」ウィンドウで情報を確認したら、**OK**をクリックしてクラスターを削除します。





##　次の手順：クラスターの使用
本文では、TKEでクラスターを作成および削除する方法について学習しました。作成したクラスターでは、ワークロードを設定し、サービスを作成できます。一般的なタスクは次のとおりです：
- [簡易Nginxサービスの構築](https://intl.cloud.tencent.com/document/product/457/7851)
- [単一インスタンス版のWordPress](https://intl.cloud.tencent.com/document/product/457/7205)
- [TencentDBを用いたWordPress](https://intl.cloud.tencent.com/document/product/457/7447)
- [Hello Worldサービスの手動構築](https://intl.cloud.tencent.com/document/product/457/7204)
- [簡易Webアプリケーションの構築](https://intl.cloud.tencent.com/zh/document/product/457/6996)


## 問題が発生した場合
ご迷惑をおかけしまして、誠に申し訳ございません。[チケットを提出(https://console.intl.cloud.tencent.com/workorder)してサポートを依頼してください。
