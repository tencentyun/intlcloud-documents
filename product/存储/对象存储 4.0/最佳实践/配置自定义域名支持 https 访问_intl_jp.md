ユーザーは自分のドメイン名（`test.cos.com`のようなカスタマイズドメイン名）を介してバケット（Bucket）内のオブジェクト（Object）にアクセスすることができます。具体的な操作のガイドは以下のとおりです：
- [CDN加速を有効化する時にHTTPSアクセスをサポートするようにカスタマイズドメイン名を構成します](#CDN加速を有効化します)
- [CDN加速を無効化する時にHTTPSアクセスをサポートするようにカスタマイズドメイン名を構成します](#CDN加速を無効化します)

<span id="CDN加速の有効化"></span>
## CDN加速の有効化
### 一、カスタマイズドメイン名のバインディング
バケットを自分のドメイン名にバインディングし、CDN加速を有効化します。操作ガイドについては、 [ドメイン名管理--カスタマイズドメイン名](/doc/product/436/6252#CDN加速の有効化)を参照してください。
### 二、HTTPSアクセスの構成
CDNコンソールでHTTPS構成を行い、操作ガイドについては、 [HTTPS構成](/doc/product/228/6295)を参照してください。
<span id="CDN加速の無効化"></span>
## CDN加速の無効化
このチャプターでは、例として、COSにおいてリバースプロキシを介してhttpsアクセスをサポートするようにカスタマイズドメイン名（CDN加速を無効化する）を構成する操作ステップを紹介します。この例では、CDN加速を有効化することなく、直接的にカスタマイズドメイン名`https://test.cos.com`を介して属する地域が南中国で、名称がtesthttps-12345678のバケットにアクセスすることを実現し、具体的な操作ステップは以下のとおりです：

### 一、カスタマイズドメイン名のバインディング
バケットtesthttpsをドメイン名`https://test.cos.com`にバインディングし、CDN加速を無効化します。操作ガイドについては、[ドメイン名管理--カスタマイズドメイン名](/doc/product/436/6252#CDN加速の無効化)を参照してください。
### 二、ドメイン名へのリバースプロキシの構成
サーバーにおいてドメイン名`https://test.cos.com`にリバースプロキシを構成します。具体的な構成については、以下を参照してください（以下のNginx構成はあくまでも参照です）。
```
server {
    listen        443;
    server_name  test.cos.com ;

    ssl on;
    ssl_certificate /usr/local/nginx/conf/server.crt;
    ssl_certificate_key /usr/local/nginx/conf/server.key;

    error_log logs/test.cos.com.error_log;
    access_log logs/test.cos.com.access_log;
    location / {
        root /data/www/;
        proxy_pass  http://testhttps-12345678.cos.ap-guangzhou.myqcloud.com; //バケット（Bucket）のデフォルトダウンロードドメイン名の構成
    }

}
```
そのうち`server.crt;`、`server.key`はユーザー自身（カスタマイズ）のドメイン名のHTTPS証明書です。ドメイン名にHTTPS証明書がない場合、 [Tencent Cloud SSL証明書](https://cloud.tencent.com/product/ssl)ページで申請することができます。
一時的に証明書がない場合、以下の構成情報を削除できますが、アクセスする時にアラームが表示され、続行をクリックしてアクセスできます：
```
    ssl on;
    ssl_certificate /usr/local/nginx/conf/server.crt;
    ssl_certificate_key /usr/local/nginx/conf/server.key;
```

### 三、サーバーへのドメイン名の解決
ドメイン名のDNS解決サービスプロバイダでドメイン名を解決してください。Tencent Cloud Analysisを使用する場合、[クラウド解決コンソール](https://console.cloud.tencent.com/cns/domains)に移動して、ドメイン名`test.cos.com`をステップ2におけるサーバーのIPに解決してください。ガイドについては、[ドメイン名解決](/doc/product/302/3446)を参照してください。
### 高度な構成
#### ブラウザからWebページを直接的に開く
HTTPSアクセスをサポートするようにカスタマイズドメイン名を構成した後、ドメイン名を介してバケット（Bucket）内のオブジェクト（Object）をダウンロードできます。ビジネスのニーズに応じて、直接的にブラウザでWebページ、画像などにアクセスしようとする場合、静的サイト機能により実現できます。操作ガイドについては、[静的サイト設定](/doc/product/436/6249)を参照してください。
![画像1](//mc.qcloudimg.com/static/img/bdd63d54f805e4975e82c95b37f675f0/image.png)
構成が完了した後、Nginx構成に1行の情報を追加し、Nginxを再起動し、ブラウザのキャッシュを更新すればよいです。
```
proxy_set_header Host $http_host;
```
#### referホットリンク保護の構成
バケット（Bucket）が一般公開される場合、ホットリンクされるリスクがあります。ユーザーはホットリンク保護の設定により、Refererのホワイトリストを有効化し、悪意のあるホットリンクを防止できます。具体的な操作ステップは以下のとおりです：
1. [COSコンソール](https://console.cloud.tencent.com/cos5/index) でホットリンク保護設定機能を有効化し、ホワイトリストを選択します。操作ガイドについては、[ホットリンク保護の設定](/doc/product/436/6250)を参照してください。
![画像2](//mc.qcloudimg.com/static/img/788556013c4d3ebd6b728d8c22a8adb5/image.png)
2. Nginx構成に1行の情報を追加し、Nginxを再起動し、ブラウザのキャッシュを更新します。
```
proxy_set_header   Referer www.test.com;
```
3. 設定が完了した後、ファイルを直接的に開くと、エラーが発生します：`errorcode：-46616`；エラーメッセージ：referホワイトリストにヒットしません。しかしながら、プロキシを介してカスタマイズドメイン名にアクセスすることで、Webページを正常に開くことができます。
![画像3](//mc.qcloudimg.com/static/img/005099e6a30398c600bb945b6b1c34e7/image.png)
