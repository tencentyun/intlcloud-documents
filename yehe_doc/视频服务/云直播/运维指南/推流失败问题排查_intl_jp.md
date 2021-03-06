[ベストプラクティス - CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558) の例に従って操作してもプッシュが成功しない場合は、本ドキュメントに列挙しているビデオプッシュプロセスの中の「よくあるご質問」に従って、次の順番でチェックしてください。

## 原因調査の考え方

**1. ドメイン名はTencent CloudアドレスにCNAMEされていますか**
    プッシュドメイン名はTencent CloudアドレスにCNAMEされて初めてプッシュに成功します。作成したことのあるプッシュドメイン名にCNAMEがあるかどうかは【Domain Management】で確認できます。その中にCNAMEタイトルバーがあり、この項目の状態にもとづいてプッシュドメイン名にCNAMEがあるかどうかを確認できます。すでにCNAMEされている状態は次のとおりです。
	まだCNAMEされていない場合は、 [CNAME設定](https://intl.cloud.tencent.com/document/product/267/31057) より設定できます。
	
**2. ネットワークは正常ですか。**
RTMPプッシュが利用するデフォルトのポート番号は**1935** です。テスト時に所在するネットワークのファイアウォールが1935ポートの通信を許可しない場合は、サーバーに接続できないという問題が発生します。この場合は、ネットワークを切り替える（たとえば4G）ことで、これが原因で発生した問題かどうかチェックすることができます。

**3. txTimeは期限切れではありませんか。**
ご自分のCSSトラフィックが他人に悪用されることを懸念して、txTimeを現在時刻から5分遅らせるなど、過度に保守的に設定されている場合があります。実際にはtxSercet署名があるためtxTimeの有効期限を短く設定する必要はありません。有効期限を短く設定しすぎると、キャスターがライブストリーミング中にネットワークの切断と再接続を繰り返した場合、プッシュURLが期限切れとなり、プッシュが再開できなくなってしまいます。
txTimeは、通常のライブストリーミングのライブストリーミング時間より長く、現在時刻から12時間後または24時間後に設定することを推奨いたします。

**4. txSecretは正しいですか。**
Tencent Cloudは現在、安全性を確保するため、すべてのプッシュアドレスにホットリンク防止を追加する必要があります。ホットリンク防止の計算エラーまたは期限切れのプッシュURLの場合は、すべてTencent Cloudから**キックアウト**されます。このような状態の場合、ライブストリーミングSDKは **PUSH_WARNING_SERVER_DISCONNECT** イベントを破棄します。[ライブストリーミング SDK DEMO](https://intl.cloud.tencent.com/document/product/1071/38147) このときのパフォーマンスは次のとおりです。
信頼できるプッシュURLの取得方法については、 [ベストプラクティス - CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558) をご参照ください。

**5. プッシュURLがすでに使用されていませんか。**
1つのプッシュURLには同時に1つのプッシュ端末しか接続できないため、2番目にプッシュを試みたclientはTencent Cloudに拒否されます。このような場合は、CSSコンソールにログインして、【ストリーム管理】の【オンラインストリーム】で、このストリームがすでにプッシュされているかどうかを確認したり、【プッシュ禁止】で、このストリームがプッシュ禁止かどうかを確認できます。



