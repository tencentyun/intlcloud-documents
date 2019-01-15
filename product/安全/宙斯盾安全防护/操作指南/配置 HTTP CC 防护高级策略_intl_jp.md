
Aegis Anti-DDoSは、HTTP CCの高度保護ポリシーを提供します。設定されたHTTPのリクエスト数が設定されたQPS値を超えると、CC保護ポリシーがCC保護をトリガーします。より詳細な設定説明については、[**カスタム高度セキュリティポリシー**](https://cloud.tencent.com/document/product/685/18800#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AE.89.E5.85.A8.E7.AD.96.E7.95.A5)を参照してください。

## CC保護ポリシーを追加
1. ユーザーは[Aegis高保護コンソール](https://console.cloud.tencent.com/gamesec)に入り、左側のディレクトリで【HTTP CC保護の高度ポリシー】をクリックし、【HTTP CC保護の高度ポリシー】下で、【新しいポリシーを追加】をクリックします。追加が成功したら、「操作」列で【設定】をクリックしてポリシー設定ページに移動します。
![1](https://main.qcloudimg.com/raw/104f8e4356790614dc5a6c86fae350a6.png)
2. サービスの特性と保護のニーズに基づいて、HTTP QPS要求閾値、URLホワイトリスト、IPブラックリスト、およびCCカスタム保護モードなどのポリシーを設定します。保存をクリックすると、ポリシーが正常に追加されます。
![2](https://main.qcloudimg.com/raw/d1f3f4da39f72fe503fc63beb2f56770.png)

## CC保護ポリシーの保護対象IPへの直接なバインディング
1. 【HTTP CC保護の高度ポリシー】をクリックし、「HTTP CC保護の高度ポリシー」下で、「ポリシーID」をクリックします。
![3](https://main.qcloudimg.com/raw/c0b1b6fe627add83cdbba72c4e07c820.png)
2. 【IPリストをバインド】をクリックし、【IPを追加】をクリックします。
![4](https://main.qcloudimg.com/raw/327c94f1844e0dbb62905330d8124ede.png)

## DDoS高保護IPのCC保護ポリシーへのバインディング
1. 【DDoS高保護IP】をクリックし、「DDoS高保護IP」下で、「高保護IP」を選択し、「DDoS高保護IP」の詳細ページに移動します。
![5](https://main.qcloudimg.com/raw/f940b3e007f4730c79915da9df17d368.png)
2. 「高度設定情報」をクリックします。【バインド】をクリックし、CC保護ポリシーを選択して【OK】をクリックします。
![6](https://main.qcloudimg.com/raw/fad935c5a8e80584a9e1d4c49a13369f.png)

## DDoS高保護パケットにおける保護対象IPのためのCC保護ポリシーの設定
1. 【DDoS高保護パケット】をクリックし、「DDoS高保護パケット」下で、「高保護パケットID」を選択し、「DDoS高保護パケット」の詳細ページに移動します。
![7](https://main.qcloudimg.com/raw/5df7d9615961323cb4e13f4bc42338c1.png)
2. 【保護対象IPリスト】をクリックし、設定したいIPを選択し、「CC保護ポリシーを設定」をクリックします。
![8](https://main.qcloudimg.com/raw/d99bfa424cbae30a5fd20424ad41b288.png)
