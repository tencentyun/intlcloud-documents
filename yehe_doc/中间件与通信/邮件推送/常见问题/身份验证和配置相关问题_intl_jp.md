[](id:que1) 

### プッシュ型メールはどのようなID認証メカニズムをサポートしていますか。
SESは、DomainKeys Identified Mail(DKIM)、Sender Policy Framework(SPF)、ドメインベースのメッセージ検証、報告、およびDomain-based Message Authentication, Reporting, and Conformance(DMARC)、MXレコード(MX record)といったあらゆる業界規格のID認証メカニズムをサポートしています。

[](id:que2) 
### 送信ドメイン名を設定するにはどうすればよいですか。
<dx-tabs>
::: ステップ1：DNS解決インターフェースの設定
1. [送信ドメイン名](https://console.cloud.tencent.com/ses/domain)の設定ページで、**新規作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/57ab829c645dcb868dbb1643ffc3378d.png)
2. ドメイン名の入力が完了したら、**提出**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/43d669f7d15b74bd3f1d11dd3c61d969.png)
<dx-alert infotype="explain" title="">
- sampledomain.comはサンプルです。ここにご自身の送信ドメイン名を入力します。
- 入力したドメイン名がsampledomain.comの形式であれば、それはメインドメイン名です。入力したドメイン名がabc.sampledomail.comの形式であれば、メインドメイン名ではありません。メインドメイン名を使用して送信するかどうかによって、それ以降の設定に違いが生じます。詳細については、対応する説明をご参照ください。
</dx-alert>
3. [送信ドメイン名](https://console.cloud.tencent.com/ses/domain)の設定ページに戻り、**検証**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/305ea2b8c9b3c5f10e0dbbe6135b3666.png)
4. 画面にポップアップされる「レコード値」の内容を記録します。[](id:step4)
>?下図はサンプルです。実際の画面に表示される内容に従ってください。
>
![](https://qcloudimg.tencent-cloud.cn/raw/70bfe55a17122848c7f829c5b4b86653.png)
5. ドメイン名がTencent Cloudでホストされている場合は、[DNS解決DNSPodコンソール](https://console.cloud.tencent.com/cns)に進んで検証情報を設定してください。対応する送信ドメイン名をクリックすると、設定詳細ページに進むことができます。
<dx-alert infotype="explain" title="">
ドメイン名が他のドメイン名サービスプロバイダでホストされている場合は、リストの詳細に従ってご自身で設定してください。
</dx-alert>
6. メインドメイン名sampledomain.comを例に、レコードを追加します。上記の [ステップ4](#step4)の対応する「レコード値」を入力します。
  - MX検証
    ホストレコードへの入力：`@`
    レコードタイプの選択：MX
    レコード値への入力：`mxbiz1.qq.com.`。メールサーバーをお持ちの場合は、レコード値にメールサーバーアドレスを入力してください。
<dx-alert infotype="explain" title="">
- 送信ドメイン名がメインドメイン名ではなく、例えばabc.sampledomain.comの場合、ホストレコードにはabcと入力します。
- レコード値の末尾には必ず「.」を入れてください。一部のドメイン名サービスプロバイダでは、MXのレコード値の末尾に自動で追加されます。
</dx-alert>
  - SPF検証：
  ホストレコードへの入力：`@`
  レコードタイプの選択：TXT
  レコード値への入力：`v=spf1 include:qcloudmail.com ~all`
<dx-alert infotype="explain" title="">
- 送信ドメイン名がメインドメイン名ではなく、例えばabc.sampledomain.comの場合、ホストレコードにはabcと入力します。
- 同時に複数のSESサービスプロバイダを使用している場合は、それらすべてのサービスプロバイダのドメイン名をレコード値の中に含めておく必要があります。例えば、 v=spf1 include:qcloudmail.com include:domain1.com ~allのうち、domain1.comは他のSESサービスプロバイダのドメイン名です。送信ドメイン名のDNS設定に、SPFレコードが1つしかないことを確認してください。
</dx-alert>
  - DKIM検証：
    ホストレコードへの入力：`qcloud._domainkey`
  レコードタイプの選択：TXT
  レコード値にはご自身の「レコード値」を入力します。
<dx-alert infotype="explain" title="">
送信ドメイン名がメインドメイン名ではなく、例えばabc.sampledomain.comの場合、ホストレコードにはqcloud._domainkey.abcと入力します。
</dx-alert>
- DMARC検証：
  ホストレコードへの入力：`_dmarc`
  レコードタイプの選択：TXT
  レコード値への入力：`v=DMARC1; p=none`
  <dx-alert infotype="explain" title="">
- 送信ドメイン名がメインドメイン名ではなく、例えばabc.sampledomain.comの場合、ホストレコードには_dmarc.abcと入力します。
- DMARCレコードには必ずvおよびpタグを含めなければなりません。DMARCについてよくご存じの場合は、必要に応じて他のタグを追加することや、タグの値を変更することが可能です。
</dx-alert>

7. 再び[ステップ4](#step4)画面に戻り、**検証提出**をクリックして検証を行います。「現在の値」には、上記のDNS設定で設定した内容が表示されます。検証のステータスが「検証済み」となっていれば、設定は完了です。

:::
::: ステップ2：検証結果
<dx-alert infotype="explain" title="">
「ステップ1」の設定操作を完了し、かつ送信ドメイン名のステータスが「認証成功」となっていれば、このステップで検証を再度行う必要はありません。
</dx-alert>
ここでは、digコマンドを使用してDNSドメイン名サーバーに問い合わせを行い、送信ドメイン名の設定が完了しているかどうかを確認する方法についてご説明します。
コマンドラインに次のコマンドをそれぞれ入力してエンターキーを押し、戻り値が送信ドメイン名設定画面で対応して表示されるレコード値と同じかどうかをそれぞれ確認します。
- `dig mx +short sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/76cf66d8a42bee99a696b505eb8d8b2c.png)
- `dig txt +short sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/f5fe74ee3c0c8312253359f8a3457db1.png)
- `dig txt +short _dmarc.sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/2c53ae3c3789e220e7f939be536152bf.png)
- `dig txt +short qcloud._domainkey.sampledomain.com`
![](https://qcloudimg.tencent-cloud.cn/raw/5c773b8278d5d424a652b396f42fc591.png)


<dx-alert infotype="explain" title="">
上記のコマンドのうち、sampledomain.comはサンプルです。ここにご自身の送信ドメイン名を入力します。
</dx-alert>




:::
</dx-tabs>

<dx-alert infotype="explain" title="">

- 上記の設定と確認を行っても、作成したメールのドメイン名に問題がある場合は、[Tencent Cloud技術スタッフ](https://console.cloud.tencent.com/workorder/category)に問い合わせて、解決を依頼してください。
- Dnspodによる解決が登録されているが、digが使えない場合：ドメイン名が実名認証されていない可能性があります（レジストリの設定により解決が停止されます）。
</dx-alert>
