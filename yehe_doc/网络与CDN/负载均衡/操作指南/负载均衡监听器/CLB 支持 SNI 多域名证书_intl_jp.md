
サーバー名表示（Server Name Indication，SNI）とは、サーバーとクライアント間のSSL/TLSを改善するために用いられるもので、1台のサーバーにつき1つの証明書しか使用できない問題を主に解決します。SNIをサポートすることは、サーバーに複数の証明書をバインドできることを意味します。クライアントがSNIを使用するには、サーバーとの間でSSL/TLS接続を確立する前に、接続したいドメイン名を指定する必要があり、サーバーはこのドメイン名に基づいて適切な証明書を返します。

## ユースケース
Tencent Cloud CLBのレイヤー7HTTPSリスナーはSNIをサポートしています。つまり、複数の証明書のバインドをサポートし、リスニングルール内のドメイン名ごとに異なる証明書を使用できます。例えば、同一のCLBの`HTTPS:443`リスナーで、`*.test.com`が証明書1を使用している場合、このドメイン名からのリクエストは1組のサーバーに転送され、証明書2を使用している`*.example.com`からのリクエストは別の1組のサーバーに転送されます。

## 前提条件
[CLBインスタンスを購入](https://buy.cloud.tencent.com/lb)していること。


## 操作手順
1. [CLBコンソール](https://console.cloud.tencent.com/clb)にログインします。
2. [リスナーの設定](https://intl.cloud.tencent.com/document/product/214/32516#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.85.8D.E7.BD.AE.E7.9B.91.E5.90.AC.E5.99.A8)の操作手順を参照してリスナーを設定し、HTTPSリスナーを設定する際にSNIを有効化します。
![](https://main.qcloudimg.com/raw/a70af5870cf3c02a97368f9bbb46f74f.png)
3. リスナーに転送ルールを追加する際、ドメイン名ごとに異なるサーバー証明書を設定し、【次のステップ】をクリックします。続いてヘルスチェックとセッション維持の設定を完了します。
![](https://main.qcloudimg.com/raw/e35b92e86b8bade2a0a77a64461a418d.png)
