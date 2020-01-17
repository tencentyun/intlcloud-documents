### Elastic Network Interfaceは何ですか？

[Elastic Network Interface](https://intl.cloud.tencent.com/product/eni)（ENI）は、Virtual Private CloudのCVMをバインディングする一種のElasticネットワークインターフェースであり、複数のCVMの間で自由にマイグレーションすることができます。ENIはネットワーク管理の設定及び信頼性の高いネットワークソリューションの構築に役立ちます。

ENIはVirtual Private Cloud、アベイラビリティーゾーンとサブネットの属性があり、同じアベイラビリティーゾーン中のCVMのみバインディングできます。一台のCVMは複数のENIをバインディング可能であり、具体的なバインディング数はCVM仕様により定められます。

### CVMはENIを利用する場合は、どのような制限がありますか？

使用制限一覧の[ENIに関する制限](https://intl.cloud.tencent.com/document/product/213/15379)部分をご参照ください。

### ENIはどのような基本情報がありますか？

[ENI概要](https://intl.cloud.tencent.com/document/product/213/6514) **の関連概念**部分をご参照ください。

### どのようにENIを作成しますか？

[ENIの作成](https://intl.cloud.tencent.com/document/product/576/18534)をご参照ください。

### どのようにENIを確認しますか？

[ENIの確認](https://intl.cloud.tencent.com/document/product/576/18533)をご参照ください。

### どのようにENIをCVMのインスタンスにバインディングしますか？

[クラウドホストのバインディングと設定](https://intl.cloud.tencent.com/document/product/576/18535)をご参照ください。

### どのようにCVMインスタンスのENIを設定しますか？

[クラウドホストのバインディングと設定](https://intl.cloud.tencent.com/document/product/576/18535)をご参照ください。

### どのようにENIのプライベートIPを修正・カスタマイズしますか？

VPCのCVMはENIのプライベートIPを修正・カスタマイズすることをサポートします。コンソールでの操作手順は以下のように：

1. [Virtual Private Cloudコンソール](https://console.cloud.tencent.com/vpc/vpc?rid=1)にログインします。
2. 左側ナビゲーションバーで、【IPとENI】>【ENI】をクリックし、ENIリスト画面に入ります。
3. ENIの【 ID/名称】をクリックし、ENIの詳細画面に入り、ENI情報を確認します。
4.【IPv4 アドレス管理】タブを選択し、【プライベートIPのアサイン】をクリックします。
5. ポップアップウインドウで、 アサインしたIP 方式を**手動記入**に選択し、修正したいIP アドレスを入力してください。
6.【OK】をクリックして操作を完了させます。

コンソールで修正した後、同時にENIの設定ファイルを修正する必要があります。[クラウドホストのバインディングと設定](https://intl.cloud.tencent.com/document/product/576/18535)をご参照ください。
