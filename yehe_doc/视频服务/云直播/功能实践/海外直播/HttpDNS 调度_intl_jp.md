## ソリューションの背景
CSSの海外のプッシュと再生のスケジューリングは、デフォルトではドメイン名のDNS解決を利用してスケジューリングを行います。これは最も一般的で、最も簡単なアクセス方式です。国内外のネットワーク環境は複雑なため、ドメイン名解決エラーまたはトラフィックのクロスネットワークの問題が普遍的に生じています。CSSではHTTPDNSソリューションを使用し、ライブストリーミングのスケジューリングを最適化することをお勧めします。

キャリアのLocalDNSの出口では、認証DNSのターゲットIPアドレスに基づきNATを行うか、または解決リクエストをその他DNSサーバーに転送するため、認証DNSがキャリアのLocalDNS IPを正確に識別できなくなる状況が起き、ドメイン名解決エラーやトラフィックのクロスネットワークなどの問題が引き起こされます。Tencent Cloud HTTPDNSは、世界最先端のDNSクラスター技術を備え、マルチキャリアとカスタマイズパスに対応し、スケジューリングを最適化することができます。

>?  ここではどのようにHTTPDNSスケジューリングソリューションをTencent Cloudの国内および海外のCSSプッシュおよび再生のスケジューリングアクセラレーションに使用するかを説明します。HTTPDNSインタフェースについては [モバイルHTTPDNSの解決](https://intl.cloud.tencent.com/document/product/1130/44468)をご参照ください。

## 事前準備
1. HTTPDNSサービスをアクティブ化するには、Tencent Cloudのモバイル解決HTTPDNSコンソールのサービス [アクティブ化の手順](https://intl.cloud.tencent.com/document/product/1130/44461)をご参照ください。
2. [開発設定ページ](https://console.cloud.tencent.com/httpdns/configure)に進み、承認ID、 DESキーの認証情報を確認します。
![](https://qcloudimg.tencent-cloud.cn/raw/ad5bf89eb5cfe81d4d9b7d19176c622a.png)

## HTTPDNSを使用したアップストリームプッシュのスケジューリング

### 上りアクセスポイントIPのリクエスト

HTTPDNSリクエスト：`http://119.29.29.98/d?dn={$push_domain DES暗号化文字列}&ip={$ip DES暗号化文字列}&id=$id` 、HTTP Getリクエストです。パラメータの意味は次のとおりです。

- push_domain プッシュドメイン名を表し、このフィールドはDESによって暗号化する必要があり、キー情報は[HTTPDNS開発設定ページ](https://console.cloud.tencent.com/httpdns/configure)から取得します。具体的な内容は [DESによる暗号化および復号の説明](https://intl.cloud.tencent.com/document/product/1130/44470)をご参照ください。
- IPフィールドは、リクエスト側のパブリックネットワークのegress IPを表し、このIPに、最終的にスケジューリングするアクセスポイントIPが存在するリージョンとキャリアが示されます。このフィールドも同様にDESによって暗号化する必要があります。
- idフィールドはユーザー認証IDを表し、各ユーザーを一意に識別します。

### アクセスポイントIPの復号

HTTPDNSによって取得したデータはDES暗号文です。DESによって復号し、server_ipを取得する必要があります。具体的な内容は[DESによる暗号化および復号の説明](https://intl.cloud.tencent.com/document/product/1130/44470)をご参照ください。

### アップストリームプッシュURLの結合

ここでのserver_ipは**リクエストした上りアクセスポイントIP**から取得できるIPとなり、したがって結合したプッシュURLは次のとおりになります。`rtmp://server_ip/live/streamname?txTime=xxx&txSecret=xxx&txHost=domain`、最も重要なことは、既存のプッシュパラメータに、業務のプッシュドメイン名を意味するフィールドであるtxHostを新たに追加することです。

## HTTPDNSを使用したダウンストリーム再生のスケジューリング

### 下りアクセスポイントIPのリクエスト

HTTPDNSリクエスト：`http://119.29.29.98/d?dn={$domain DES暗号化文字列}&ip={$ip DES暗号化文字列}&id=$id`、HTTP Getリクエストです。パラメータの意味は次のとおりです。

| フィールド | 意味 |
|---------|---------|
| push_domain | 再生ドメイン名です。このフィールドはDESによって暗号化する必要があり、キー情報は[HTTPDNS開発設定ページ](https://console.cloud.tencent.com/httpdns/configure) によって取得します。具体的な内容は [DESによる暗号化および復号の説明](https://intl.cloud.tencent.com/document/product/1130/44470)をご参照ください。|
| ip | リクエスト側のパブリックネットワークのegress IPを表し、このIPに、最終的にスケジューリングするアクセスポイントIPが存在するリージョンとキャリアが示されます。このフィールドも同様にDESによって暗号化する必要があります。 |
| id | ユーザー認証IDで、各ユーザーを一意に識別します。 |

### アクセスポイントIPの復号

HTTPDNSによって取得したデータはDES暗号文です。DESによって復号し、server_ipを取得する必要があります。具体的な内容は[DESによる暗号化および復号の説明](https://intl.cloud.tencent.com/document/product/1130/44470)をご参照ください。

### ダウンストリーム再生URLの結合
- **HTTP**：FLVおよびHLSの再生プロトコルが含まれ、ここでのserver_ipは、**リクエストした下りアクセスポイントIP**の中から取得できるIPとなり、play_domainは再生ドメイン名を表します。したがってHTTPの再生URLの結合は次のようになります。
```
http://server_ip/play_domain/live/streamname.flv?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```
- **HTTPS**：FLVおよびHLSの再生プロトコルが含まれ、ここでのserver_ipは、**リクエストした下りアクセスポイントIP** の中から取得できるIPとなり、play_domainは再生ドメイン名を表します。HTTPSの結合ルールはプレーヤーのロジックに依存し、**TCPで作成し、接続したターゲットIPをHTTPDNSスケジューリングのserver_ipにすることが要求されます**。具体的にリクエストする再生URLに必要とされるのは通常の再生リクエストです。
```
https://server_ip/play_domain/live/ streamname.flv?xxxxxxxxxx
https://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
https://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```
- **RTMP**：ここでのserver_ipは、**リクエストした下りアクセスポイントIP**の中から取得できるIPとなり、play_domainは再生ドメイン名を表します。したがってRTMPの再生URLは以下のように結合します。
```
rtmp://server_ip/play_domain/live/ streamname?xxxxxxxxxx
```

>? HTTPDNSリクエストは、HTTPDNSアクセスがタイムアウトした、返された結果が非IP形式であった、または空で返されたなど、低確率で異常が生じます。このような低確率な異常イベントが発生した場合は、LocalDNSにアクセスしてドメイン名の解決を行ってください。
