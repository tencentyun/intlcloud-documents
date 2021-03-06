## 操作シナリオ
VODのアクティブ化後、システムからデフォルトのドメイン名`xxx.vod2.myqcloud.com`が割り当てられます。VOD中のすべてのリソースには、デフォルトでこのドメイン名が使用されます。 [VODコンソール](https://console.cloud.tencent.com/vod/overview) にログインして、ドメイン名をカスタマイズ、追加、および解決することもできます。
## 前提条件
- VODサービスの申請が成功していること。詳細については、[購入ガイドライン](https://intl.cloud.tencent.com/document/product/266/39506)をご参照ください。
- 中国で展開する業務については、追加するドメイン名がICP登録に成功していることをご確認ください。

## ドメイン名の追加
1. [VODコンソール](https://console.cloud.tencent.com/vod/overview)にログインし、左側ナビゲーションバーの【配信と再生の設定】>【ドメイン名管理】を選択します。
2. 【ドメイン名の追加】をクリックし、ポップアップ表示されたダイアログボックスに [ICP登録]に成功したドメイン名を入力して、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/37dab10b1d498194b8ac7fbf4f977525.png)
>?
>- ドメイン名の追加には数分かかります。ドメイン名を追加すると、ドメイン名リストで、ドメイン名のステータス、CNAME、ドメインタイプ情報を確認することができます。
>- 1つのTencent Cloudアカウントで、最大20個のドメイン名を追加することができます。

## ドメイン名の解決
ドメイン名を追加した後、ユーザーがドメイン名を介してビデオ情報にアクセスできるように、ドメイン名で指定されたDNSプロバイダでCNAMEを設定する必要があります。具体的な操作手順は次のとおりです。
>?以下に、Tencent Cloud解析をDNSプロバイダとして使用する例を示します。CNAMEレコードを追加する場合、DNSプロバイダによって操作がそれぞれ若干異なります。更なる操作については、[CNAME設定](https://intl.cloud.tencent.com/document/product/570/11134)をご参照ください 。

1. [ドメイン名管理](https://console.cloud.tencent.com/domain) コンソールにログインし、【マイドメインネーム】リストから、CNAMEレコードを追加するドメイン名を見つけて、操作列の【解決】をクリックします。
2. このドメイン名の【レコード管理】画面に入り、【レコードの追加】をクリックします。
3. ポップアップ表示されたボックスで、【レコートタイプ】にCNAMEを設定し、【ホストレコード】にドメイン名プレフィックス（例：www）を入力し、【レコード値】にCNAMEドメイン名を入力して、【OK】をクリックします。

>! ユーザーがカスタムドメイン名を追加し、まだビデオを追加していないのに、少量のトラフィックが発生することがありますが、それはドメイン名へのアクセスにより少量のリターンパケットが発生するためで、正常な現象です。


