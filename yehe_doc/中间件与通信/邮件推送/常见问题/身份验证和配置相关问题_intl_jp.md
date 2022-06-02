[](id:que1) 

### プッシュ型メールはどのようなID認証メカニズムをサポートしていますか。
プッシュ型メールは、DomainKeys Identified Mail(DKIM)、Sender Policy Framework(SPF)、ドメインベースのメッセージ検証、報告、およびDomain-based Message Authentication, Reporting, and Conformance(DMARC)といったあらゆる業界規格の検証メカニズムをサポートしています。

[](id:que2) 
### 送信ドメイン名を設定するにはどうすればよいですか。
<dx-tabs>
::: ステップ1：DNS解決インターフェースの設定
1. [送信ドメイン名](https://console.cloud.tencent.com/ses/domain)の設定ページで、**ドメイン名の新規作成**をクリックし、ドメイン名を入力して送信すれば完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/00947cc2ff7a7dc6855baee29d1a77ee.png)
2. [DNS解決DNSPodコンソール](https://console.cloud.tencent.com/cns)で検証情報を設定します。
3. [](id:step2)[送信ドメイン名](https://console.cloud.tencent.com/ses/domain)の設定ページに戻り、**検証**をクリックします。
4. お客様の送信ドメイン名アドレスをクリックすると、ドメイン名の値を確認できる設定詳細ページに進めます。
![](https://qcloudimg.tencent-cloud.cn/raw/7f5e04d51b3a6976eec099353f62cc07.png)
5. [ステップ3.](#step3)の送信ドメイン名アドレスを[DNS解決DNSPod](https://console.cloud.tencent.com/cns)の解決ページに貼り付けて、レコードの追加を完了します。スペースは避けてください。
 - DKIM検証：
![](https://qcloudimg.tencent-cloud.cn/raw/db505d7e62fc62013e6d39d534dde126.png)
 - SPF検証：
![](https://qcloudimg.tencent-cloud.cn/raw/c29031426e6fc6d7d8d073bb9bffea98.png)
 - _dmarcレコード：
レコード値に`v=DMARC1; p=none;rua=mailto:xxx@163.com;ruf=mailto:xxx@163.com;`と入力します
![](https://qcloudimg.tencent-cloud.cn/raw/64dc22f5ec2da2840115bb869a1ba95e.png)
 <dx-alert infotype="explain"> `xxx@163.com`は一例です。ここに自分のメールアドレスを入力します。</dx-alert>
6. [送信ドメイン名](https://console.cloud.tencent.com/ses/domain)の設定詳細ページに再度戻り、**検証**をクリックすれば完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/b65213aa84bd379a250084e72c8c3a34.png)
:::
::: ステップ2：検証結果
![](https://qcloudimg.tencent-cloud.cn/raw/275fb56fe9faa0a0ab3bd3735f3bd8c5.png)
![](https://qcloudimg.tencent-cloud.cn/raw/695ff02f3096d64481103a13e757362c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c9bc369664b4290a4048f94791f47209.png)

:::
::: 補足：発信ドメイン名が第3レベルドメイン名を使用している場合

1. [送信ドメイン名](https://console.cloud.tencent.com/ses/domain)の設定ページで、**ドメイン名の新規作成**をクリックし、ドメイン名を入力して送信すれば完了です。
2. [DNS解決DNSPodコンソール](https://console.cloud.tencent.com/cns)で検証情報を設定します。
:::
</dx-tabs>

>?
>- 上記の設定と確認を行っても、作成したメールのドメイン名に問題がある場合は、[Tencent Cloud技術スタッフ](https://console.cloud.tencent.com/workorder/category)に問い合わせて、解決を依頼してください。
>- Dnspodによる解決が登録されているが、digが使えない場合：ドメイン名が認証されていない可能性があります（レジストリの設定により解決が停止されます）。

