## ソリューションの背景
CSS海外のプルと再生のスケジューリングは、デフォルトでは、ドメイン名のDNS解決を利用してスケジューリングを行います。これは最も一般的で、最も簡単なアクセス方式です。海外のネットワーク環境は複雑なため、ドメイン名解決エラーまたはトラフィックのクロスネットワークの問題が遍く存在します。よってCSSでは、HttpDNSソリューションを活用し、海外でのライブストリーミングスケジューリングを最適化することをお勧めします。

キャリアのLocalDNSの出口では、認証DNSのターゲットIP アドレスに基づきNATを行うか、または解決リクエストをその他DNSサーバーに転送するため、認証DNSがキャリアのLocalDNS IPを正確に識別できなくなる状況が起き、ドメイン名解決エラーやトラフィックのクロスネットワークの問題が引き起こされます。
Tencent Cloud HttpDNS は、世界最先端のDNSクラスタ技術を備え、マルチキャリアとカスタマイズパスに対応し、スケジューリングを最適化することができます。詳細については、[HttpDNS]をご参照ください。


>?ここでは、無料版のHttpDNSを使って、 HttpDNSスケジューリングソリューションをTencent Cloudの海外のCSSに利用する方法を説明します。無料版のHttpDNSインターフェースについては、[ドキュメント]をご参照ください。 

## HttpDNSを使用した上りプッシュのスケジューリング

### 1. 上りアクセスポイントIPのリクエスト
`http://119.29.29.29/d?dn=$push_domain.&ip=$ip`, HTTP Getリクエスト。 パラメータの意味は次のとおりです。
- push_domainはプッシュドメイン名を表します。
- IPフィールドは、リクエスト側の外部ネットワークのegress IPを表し、このIPに、最終的にスケジューリングするアクセスポイントIPが存在するリージョンとキャリアが示されます。


### 2. 上りプッシュURLの接合
ここでのserver_ipは、**リクエストした上りアクセスポイント IP**の中から取得できるIPとなり、したがって接合したプッシュURLは次のようになります。
`rtmp://server_ip/live/streamname?txTime=xxx&txSecret=xxx&txHost=domain`、最も重要なことは、既存のプッシュパラメータの中に業務のプッシュドメイン名のフィールドtxHostを新たに追加することです。

## HttpDNSを使用した下り再生のスケジューリング

### 1. 下りアクセスポイントIPのリクエスト
`http、://119.29.29.29/d?dn=$domain.&ip=$ip`, HTTP Getリクエスト。 パラメータの意味は次のとおりです。
- domainは再生ドメイン名を表します。
- IPフィールドは、リクエスト側の外部ネットワークのegress IPを表し、このIPに、最終的にスケジューリングするアクセスポイントIPが存在するリージョンとキャリアが示されます。


### 2. 下り再生URLの結合
- HTTP：FLVおよびHLSの再生プロトコルが含まれ、ここでのserver_ipは、**リクエストした下りアクセスポイントIP**の中から取得できるIPとなり、play_domainは再生ドメイン名を表します。したがってHTTPの再生URLの結合は次のようになります。

```
http://server_ip/play_domain/live/streamname.flv?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```

- HTTPS：FLVおよびHLSの再生プロトコルが含まれ、ここでのserver_ipは、**リクエストした下りアクセスポイントIP**の中から取得できるIPとなり、play_domainは再生ドメイン名を表します。HTTPSの結合ルールはプレーヤーのロジックに依存し、**TCPで構築した接続先のターゲットIPをHttpDNSスケジューリングのserver_ipにすることが要求されます**。具体的にリクエストする再生URLに必要とされるのは通常の再生リクエストです。

```java
https://play_domain/live/ streamname.flv?xxxxxxxxxx
https://play_domain/live/ streamname.m3u8?xxxxxxxxxx
https://play_domain/live/ streamname -123.ts?xxxxxxxxxx
```

- RTMP：ここでのserver_ipは、**リクエストした下りアクセスポイントIP**の中から取得できるIPとなり、play_domainは再生ドメイン名を表します。したがってRTMPの再生URLは以下のように結合します。

```
rtmp://server_ip/play_domain/live/ streamname?xxxxxxxxxx
```

>!上記のソリューションはいずれもCSSの海外のスケジューリングプラットフォームに依存し、中国国内での使用にはご参照いただけません。中国国内でHttpDNSを使用してCSSスケジューリングを最適化したい場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してお問い合わせください。
