## **手順の概要**
CDNの利用手順は、次の図に示します。
![フローチャート](https://mc.qcloudimg.com/static/img/f226c2d0655ce65f25bca945082f7760/quick-start-9.png)
## CDNサービスのアクティブ化
CDNサービスを利用するには、実名認証とCDNサービスのアクティブ化が必要です。お持ちのTencent CloudアカウントのCDNがすでに有効になっている場合、直接[ドメイン名の追加](#yuming)に進んでください。
### 実名認証
1. 新規ユーザーが [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインすると、実名認証の案内が表示されます。【認証へ】をクリックして、実名認証に進みます。
 ![](https://main.qcloudimg.com/raw/8ade7faa62b1158393100f5feabccad5.png)
2. [アカウントセンター](https://console.cloud.tencent.com/developer)に入り、【認証をサブミット】をクリックして認証することもできます。
![](https://main.qcloudimg.com/raw/24bc11aadb6e94a45cc65096bd116b44.png)
3. 認証の詳細手順については、[実名認証ガイド](https://cloud.tencent.com/doc/product/378/3629)を参照してください。個人認証は審議に提出した次第完了できます。法人認証は約1営業日がかかり、認証成功する後にSMS通知が届きます。お客様は、[作業依頼書を提出](https://console.cloud.tencent.com/workorder/category/create?level1_id=1&level2_id=41&level1_name=%E5%85%AC%E5%85%B1%E5%9F%BA%E7%A1%80%E7%B1%BB%E9%97%AE%E9%A2%98&level2_name=%E8%B4%A6%E5%8F%B7%E7%B1%BB) から実名認証の進捗を確認できます。

### サービス情報の補足
実名認証が完了してからは、[CDNコンソール](https://console.cloud.tencent.com/cdn)で実名認証の情報を確認し、サービス内容を選択してから、【次へ】をクリックしてください。
![](https://main.qcloudimg.com/raw/799e2d9d0b5dff6a04142ea28a2c1752.png)

### 支払い方法の選択
CDNはトラフィック課金と帯域幅課金という二つの課金方式を提供しています。お客様は、サービスモデルに応じて課金方式を選択できます。詳細については、[課金説明](https://cloud.tencent.com/doc/product/228/2949)を参照してください。
チェックを入れてサービス条項に同意してから、【CDNのアクティブ化】をクリックすると、加速サービスが利用可能になります。
![](https://main.qcloudimg.com/raw/d3913b3dc5ad769a6d8135a977a756db.png)
アクティブ化したあとは、概要画面でご選択された課金方式を確認できます。
![](https://main.qcloudimg.com/raw/a7e7da71ea365f6ee501178167ff072a.png)

<span id="yuming"></span>
## ドメイン名の追加
### ドメイン名構成の記入
[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側メニューの【ドメイン名管理】をクリックして該当のページに入り、【ドメイン名を追加】をクリックします。
 ![](https://main.qcloudimg.com/raw/a1b7b3aa4b89533045b3cd10825d3afa.png)
2. **ドメイン名**に加速するドメイン名を記入します。対象ドメイン名は、下記の条件を満たす必要があります。
 - すでに中国工信部にICP申告を提出していること。
 - Tencent Cloud CDNに追加されていないこと。
![](https://main.qcloudimg.com/raw/12410d7f22e5763fe2d1aa427b74e5f5.png)

### サービス構成の記入
 **サービスタイプ**の選定は、ドメイン名がスケジューリングするリソースプラットフォームを決めています。異なるリソースプラットフォームの加速構成も異なりますので、お客様のサービスに適したタイプを選択してください。
 - 静的加速：Eコマース、ウェブサイト、ゲーム画像など静的リソースの加速に適しています。
 - ダウンロード加速：ゲームのインストールパッケージ、音声・動画のリソースファイルのダウンロード、携帯電話ファームウェアの配布などに適しています。
 - ストリーミングメディアのオン・デマンド加速：音声・動画のオン・デマンド加速などに適しています。 
 ![](https://main.qcloudimg.com/raw/5a1a60e71ac4bd92f333c42298fcab36.png)
 
### 追加完了
ドメイン名をサブミットすることで、追加を完了します。ドメイン名構成をネットワーク全体のノードにデリバーするには約5～10分がかかるため、しばらくお待ちください。
![](https://main.qcloudimg.com/raw/c551d6d1d89e0d4e23c284106b5bbde3.png)

## CNAMEの構成
### CNAMEの確認
ドメイン名の構成が完了したあと、システムにより対応する**CNAME**が割り当てられます。その拡張子は```.cdn.dnsv1.com``` であり、必ずコンソールに表示されるCNAMEを参照して構成してください。
![](https://main.qcloudimg.com/raw/c7e412b163d8458583e69f8446ada0fe.png)

### CNAMEの変更
CNAMEの構成は、ドメイン名が追加されるDNSプロバイダーの所でを完了する必要があります。構成方法については、[CNAMEの構成](https://cloud.tencent.com/doc/product/228/3121)を参照してください。
### CNAMEのアクティブ化状態を確認
DNSプロバイダーによって、CNAMEのアクティブ化にかかる時間が異なっていますが、一般的には30分以内に完了します。dig方式でCNAMEのアクティブ化状態を確認することもできます。拡張子が```.cdn.dnsv1.com```であるドレイン名をdigした場合、ドメイン名のCNAMEが有効になっています。
![](https://main.qcloudimg.com/raw/4c611fda0209a45d9441a2f0336bbf84.png)
