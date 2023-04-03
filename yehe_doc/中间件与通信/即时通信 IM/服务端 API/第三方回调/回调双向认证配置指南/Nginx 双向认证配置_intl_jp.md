## Nginx HTTPS双方向認証の設定フロー
>!ご利用のドメイン名の証明書が期限切れになった場合、ドメイン名の証明書を変更し、以下の説明に従って改めて設定してください。

サードパーティ開発者のドメイン名`http://www.example.com`を例として説明します。具体的には、以下の2つの場合があります：

- **サードパーティ開発者が信頼できる第三者機関が発行した証明書を持っている場合**
 - 開発者は信頼できる第三者機関が`www.example.com`に対して発行した証明書`www.example.com.crt`とプライベートキー`www.example.com.key`を用意します。証明書は信頼できる第三者機関(iTrusChina、globalsignなど）が発行したものを使用しなければならないことに注意してください。
 - IMは、開発者のバックグラウンドにリクエスト側（すなわち、IM）の証明書を検証するCA証明書[TencentQQAuthCA.crt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TencentQQAuthCA.crt.zip)を提供します。
 - 以下のNginx HTTPS双方向認証設定を参考にして設定します。

- **サードパーティ開発者がIMにドメイン名の証明書の発行をリクエストする場合**
 - 開発者はコンソールで[コールバックのURLを設定](https://intl.cloud.tencent.com/document/product/1047/34520)します。例えば、`www.example.com`。
 - IMは開発者のドメイン名`www.example.com`に対して証明書`www.example.com.crt`とプライベートキー`www.example.com.key`を発行します。開発者はコンソールから[証明書をダウンロード](https://intl.cloud.tencent.com/document/product/1047/34520#.E4.B8.8B.E8.BD.BD-https-.E5.8F.8C.E5.90.91.E8.AE.A4.E8.AF.81.E8.AF.81.E4.B9.A6)できます。
 - IMは、開発者のバックグラウンドにリクエスト側（すなわち、IM）の証明書を検証するCA証明書[TencentQQAuthCA.crt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TencentQQAuthCA.crt.zip)を提供します。
 - 以下のNginx HTTPS双方向認証設定を参考にして設定します。

## Nginx HTTPS双方向認証設定（参考）

1. `www.example.com.crt`、`www.example.com.key`、`TencentQQAuthCA.crt`をNginxのインストールディレクトリのconfフォルダにコピーします。
2. 以下のように**nginx.conf**設定ファイルを編集します。
```
server {
    listen	  443 ssl;
    ssl_protocols TLSv1 TLSv1.1;
    server_name            www.example.com; # ドメイン名
    ssl_certificate        www.example.com.crt; # Tencent Cloudがサードパーティに発行する証明書
    ssl_certificate_key    www.example.com.key; # 証明書とペアになるプライベートキー
    ssl_verify_client on; # リクエストの送信元を認証する
    ssl_client_certificate TencentQQAuthCA.crt; # Tencent Cloud認定のCA証明書
    location / {
        root   html;
        index  index.html index.htm;
    }
}
```
