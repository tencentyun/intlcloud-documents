このドキュメントは、Content Delivery Network（CDN）を使い始めたばかりのユーザー向けのガイドです。

## 1. CDNを理解するための基礎知識

- [CDNはどのように機能しますか。](https://intl.cloud.tencent.com/document/product/228/2939)
- [Tencent Cloud CDNを選択する理由とは何ですか。](https://intl.cloud.tencent.com/document/product/228/2941)
- [CDNの様々なユースケースをご紹介します。](https://intl.cloud.tencent.com/document/product/228/32980)
- [Tencent Cloud CDNを使用する上での制限とは何ですか。](https://intl.cloud.tencent.com/document/product/228/32981)
- [CDNの基本概念](https://intl.cloud.tencent.com/document/product/228/36183)



## 2. CDNの課金モード

Tencent Cloud CDNの課金モードには**帯域幅課金**と**トラフィック課金**があります。CDNの課金モードを全面的に理解し、ご自身に最も適した課金プランを選択してください。詳細については、[課金説明](https://intl.cloud.tencent.com/document/product/228/2949)をご参照ください。






## 3. 初心者向け（入門編）

#### 3.1 サービスのアクティブ化と課金方法の選択

Tencent Cloud CDNを使用する前に、Tencent Cloudアカウントを登録し、CDNサービスをアクティブにする必要があります。詳細については、[ゼロから始めるCDNの設定](https://intl.cloud.tencent.com/document/product/228/32978)をご参照ください。

#### 3.2 ドメイン名へのアクセス

アクセラレーションサービスを使用するにはアクセラレーションドメイン名にアクセスする必要があります。CDNは、アクセラレーションドメイン名によりオリジンサーバーリソースをCDNアクセラレーションノードにキャッシュします。これにより、ユーザーは必要なリソースを即座に取得することができ、リソースへのアクセスの高速化を実現します。詳細については、[ドメイン名へのアクセス](https://intl.cloud.tencent.com/document/product/228/5734)をご参照ください。

#### 3.3 CNAMEの設定

接続完了後、Tencent Cloud CDNは対応するCNAMEアドレスを割り当てます。CDNサービスを有効にするには、まずCNAMEを設定する必要があります。詳細については、[CNAMEの設定](https://intl.cloud.tencent.com/document/product/228/3121)をご参照ください。

>? 以下のベストプラクティスを参照して操作を行い、Tencent Cloud CDNをすみやかにマスターし、ドメイン名をアクセラレーションすることもできます。
>- [CDNによるCVMインスタンスへのアクセスアクセラレーション](https://intl.cloud.tencent.com/document/product/228/34035)
>- [CDNによるCOSインスタンスへのアクセスアクセラレーション](https://intl.cloud.tencent.com/document/product/228/34036)




## 4. コンソール画面

以下はCDNコンソールの概要画面です。
[](https://main.qcloudimg.com/raw/95fff730b132974403698b512260f3fb.png)


## 5. コンソール機能の概要
<table>
<thead>
<tr>
<th>次のことをする場合</th>
<th>これを読むことができます</th>
</tr>
</thead>
<tbody><tr>
<td>接続済みのアクセラレーションドメイン名に対して確認、起動、停止の操作を行います。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/5736" target="_blank">ドメイン名の操作</a></td>
</tr>
<tr>
<td>フィルタリングリストの確認、またはタグや項目に応じてクラウドでリソース管理を行います。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32913" target="_blank">ドメイン名の検索</a></td>
</tr>
<tr>
<td>CDNアクセラレーションの効果を最適化し、CDNでの多岐にわたるカスタマイズ設定をサポートします。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6288" target="_blank">設定概要</a></td>
</tr>
<tr>
<td>コンソールの機能ポイントと`Action`値の間のマッピング関係を表示します。</td>　　
<td><a href="https://intl.cloud.tencent.com/document/product/228/35229" target="_blank">コンソールの権限に関する説明</a></td>
</tr>
<tr>
<td>カスタムポリシーステートメントにより、ドメイン名に対してランク別に権限が割り当てられます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35228" target="_blank">ポリシーの作成</a></td>
</tr>
<tr>
<td>項目のランク別の権限承認操作を細分化します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35743" target="_blank">プロジェクトレベルの権限</a></td>
</tr>
<tr>
<td>リアルタイムモニタリングデータにより運用状況を分析します。</td>
<td>リアルタイムモニタリング</a></td>
</tr>
<tr>
<td>ユーザーソースとユーザー分布、および使用状況を分析します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32923" target="_blank">データ分析</a></td>
</tr>
<tr>
<td>CDNノードにキャッシュされたリソースを定期的に整理して、オリジンサーバーに戻り新たに最新のリソースを取得し、キャッシュを更新します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6299" target="_blank">キャッシュ更新</a></td>
</tr>
<tr>
<td>指定されたリソースを前もってアクセラレーションノードにロードします。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/39000" target="_blank">キャッシュ・プリフェッチ</a></td>
</tr>
<tr>
<td>アクセスログをダウンロードし、必要に応じて需要のあるリソースの分析、アクティブユーザーの分析等を行います。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6316" target="_blank">ログのダウンロード</a></td>
</tr>
<tr>
<td>ログデータの迅速な検索と分析を行います。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35380" target="_blank">リアルタイムログ</a></td>
</tr>
<tr>
<td>ネットワーク全体のリアルタイムな状態の概要と詳細を確認します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6311" target="_blank">ネットワーク全体の状態のモニタリング</a></td>
</tr>
<tr>
<td>レポート形式で業務状態を多面的に表示するため、業務状況の分析に役立ちます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6312" target="_blank">運用レポート</a></td>
</tr>
<tr>
<td>CDNコンソールで中国本土のトラフィックパッケージの使用状況を確認します。</td>
<td>トラフィックパッケージの管理</a></td>
</tr>
<tr>
<td>指定されたIPがTencent Cloud CDNノードであるかどうか検証します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/10747" target="_blank">IP所有権のクエリ</a></td>
</tr>
<tr>
<td>アクセスが異常なURLを診断し、問題箇所を迅速に特定することができます。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6304" target="_blank">自己診断ツール</a></td>
</tr>
<tr>
<td>DDoS、CC、WAFなど、あらゆる方面の防護と攻撃の監視を行います。</td>
<td>セキュリティアクセラレーション</a></td>
</tr>
<tr>
<td>Tencent Cloud CDNを使用し、大量の画像配信を行います。</td>
<td>画像最適化</a></td>
</tr>
</tbody></table>


## 6. 初心者のよくあるご質問
## 課金に関する質問
- [CDNの請求書をどのように照会できますか。](https://intl.cloud.tencent.com/document/product/228/31479)
- [購入したCDNの中国本土のトラフィックパッケージを使用しない場合、返品は可能ですか。](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDNはリクエスト数に応じた課金に対応していますか。](https://intl.cloud.tencent.com/document/product/228/31479)
- [オリジンサーバーはCOSを使用しますが、CDNがオリジンサーバーをCOSに戻す際に生じるトラフィックに対して課金されますか。](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDNがオフ（CDNサービスがオフライン）の場合であっても、トラフィックや料金は発生しますか。](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDNは課金方法の変更に対応していますか。](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDNの中国国内におけるトラフィックパッケージの使用管理](https://intl.cloud.tencent.com/document/product/228/31479)
- [ダウンストリームトラフィックが発生した場合のみ課金されますか。](https://intl.cloud.tencent.com/document/product/228/31479)

#### ドメイン名へのアクセスに関する質問

- [CDNはワイルドカードドメイン名へのアクセスをサポートしていますか。](https://intl.cloud.tencent.com/document/product/228/31476)
- [ドメイン名は工業情報化部に登録済みですが、CDNアクセラレーションドメイン名を追加すると、ドメイン名が登録されていないと表示されるのはなぜですか。](https://intl.cloud.tencent.com/document/product/228/31476)
- [CDNの設定に時間はどれくらいかかる。](https://intl.cloud.tencent.com/document/product/228/31476)
- [オリジンサーバーIPは複数設定できますか。](https://intl.cloud.tencent.com/document/product/228/31476)
- [CDNが有効になったかどうか、どのようにして判断をすればよいのでしょうか。](https://intl.cloud.tencent.com/document/product/228/31476)
- [ドメイン名を無効にできるのに削除できないのはなぜですか。](https://intl.cloud.tencent.com/document/product/228/31476)
- [アクセラレーションサービスを無効にするにはどうすればよいですか。](https://intl.cloud.tencent.com/document/product/228/31476)
- [アクセラレーションドメイン名を削除するにはどうすればよいですか。](https://intl.cloud.tencent.com/document/product/228/31476)
- [アクセラレーションドメイン名/オリジンサーバーはポートの設定をサポートしていますか。](https://intl.cloud.tencent.com/document/product/228/31476)
- [CDNからファイルをダウンロードできない場合はどうすればよいですか。](https://intl.cloud.tencent.com/document/product/228/31476)



## 7. フィードバックおよびアドバイス
Tencent Cloud CDNの製品およびサービスを使用する上で何らかの質問やアドバイスがある場合は、以下の方法でフィードバックをお願いいたします。後ほど専門スタッフがお客様の質問に回答いたします。
- 製品のドキュメントの間違い等を発見した場合（リンク先、内容、API エラーなど）は、ドキュメントのページ右側の【ドキュメントに関するフィードバック】をクリックするか、または問題が存在するコンテンツを選択してフィードバックしてください。
- 製品に関する質問がある場合、[チケットを提出](https://console.cloud.tencent.com/workorder/category) でサポートを受けることができます。

