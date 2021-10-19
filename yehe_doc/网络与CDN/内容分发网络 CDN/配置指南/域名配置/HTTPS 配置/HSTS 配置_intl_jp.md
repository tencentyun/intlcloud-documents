

## 概要

HTTP Strict TransportSecurity （HSTS）は、Institution of Electronics and Telecommunication Engineers（IETE）によって設計されたWebセキュリティポリシーメカニズムです。HSTS はブラウザなどのクライアントに、ドメインはHTTPSのみを使用してアクセスするように指示し、ウェブサイト全体で100%の暗号化を実現するのに役立ちます。

## 設定の制限事項

- expireTimeの範囲は0〜365日で、秒単位で構成されます。
- サブドメイン名を含めるかどうかを選択することにより、includeSubDomainパラメータを制御できます。
- HSTS設定を有効にするには、HTTPSアクセラレーション設定を最初に完了する必要があります。
- HSTS設定を有効にした後、[強制リダイレクト](https://intl.cloud.tencent.com/document/product/228/35214)を有効にしてHTTPリクエストをHTTPSリクエストにリダイレクトすることをお勧めします。そうしないと、HTTPリクエストの場合、ブラウザはHTTPリクエストのHSTSキャッシュを作成しません。

## 設定ガイド

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左のサイドバーメニューで、【ドメイン名管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【HTTPS設定】でHSTS設定モジュールを確認できます。デフォルトでは無効になっています。
![](https://main.qcloudimg.com/raw/4e44076b3485c9de15776134af7d5e96.png)
スイッチを「ON」に切り替えて設定します。
![](https://main.qcloudimg.com/raw/5a98a2ede54d4eceb8b5f4f0a8bbaa3b.png)
【OK】をクリックした後、設定されたコンテンツに従って応答ヘッダー値を決定し、【編集】をクリックして変更できます。
![](https://main.qcloudimg.com/raw/e22e2cf4ad493379db7f1bcf49cfa03a.png)

## 例

ドメイン名`cloud.tencent.com`のHSTS設定は以下の通りであると仮定する：
![](https://main.qcloudimg.com/raw/58e49b2b5a0b94f21fa3547dda08daed.png)
応答ヘッダーは以下のとおり：
![](https://main.qcloudimg.com/raw/910e57e5abdedba4a33b4e4748a81318.png)

