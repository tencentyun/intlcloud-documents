## 故障について

- **現象1**：<span id="FaultPhenomenon1"></span>
 - 会社のネットワークを使用してアップロードする場合は正常に転送されるが、ホームネットワークを使用してアップロードすると転送速度が遅くなる（8Mbps未満）。
 - 携帯電話の4Gネットワークを使用してアップロードする場合は正常に転送されるが、会社のネットワークを使用してアップロードすると転送速度が遅くなる（8Mbps未満）。
- **現象2**：<span id="FaultPhenomenon2"></span>カスタムドメイン名を使用してアップロードすると転送速度が遅くなる。

## 考えられる原因

- 現象1について：
 1. ネットワーク環境によってCOSアクセスの速度が異なる場合は、現在のネットワークキャリアやネットワーク環境に関係がある可能性があります。
 2. ネットワーク環境によってCOSアクセスの速度が異なる場合は、越境アクセスが原因の可能性があります。
- 現象2について：カスタムドメイン名CNAMEを他の製品に切り替え、再びCOSに戻します。例えばContent Delivery Network（CDN）、Cloud Virtual Machine（CVM）、セキュリティ製品などです。

## ソリューション

- [現象1](#FaultPhenomenon1)が発生した場合は、クライアントのネットワーク環境をチェックすることによって自ら対応できます。操作の詳細については、[クライアントネットワークのトラブルシューティング](#SearchTheClientNetwork)をご参照ください。
- [現象2](#FaultPhenomenon2)が発生した場合は、カスタムドメイン名の解決を変更する方法で転送中継リンクを減少させ、転送効率を向上させることができます。操作の詳細については、[カスタムドメイン名解決の変更](#ModifyCustomDomainNameResolution)をご参照ください。

## 処理手順

<span id="SearchTheClientNetwork"></span>
### クライアントネットワークのトラブルシューティング

1. 次のコマンドを実行し、IPアドレスのキャリアとクライアントネットワークキャリアが一致しているかどうかを確認します。
```
ping COSのアクセスドメイン名
```
例：
```
ping examplebucket-1250000000.cos.ap-beijing.mqcloud.com
```
 - 出力する場合は、[手順3](#step03)を実行してください。
 - NOの場合は、[手順2](#step02)を実行してください。
2. <span id="step02"></span> ブラウザがプロキシを設定しているかどうかをチェックします。Chromeブラウザを例にとります。
    1. Chromeブラウザを開き、右上隅の<img src="https://main.qcloudimg.com/raw/41a048f92c3d6160faff7e211bacce76.png"/> > **設定**をクリックし、設定ページを開きます。
    2. **アドバンス**をクリックし、「システム」バーで**お客様のコンピュータでのプロキシ設定**を選択し、OSの設定ウィンドウを開きます。

    プロキシが設定されているかどうかをチェックします。
     - YESの場合は、プロキシを無効にします。
     - NOの場合は、[手順3](#step03)を実行してください。
3. <span id="step03"></span>使用しているWi-Fiルーターに速度制限が存在するかどうかをチェックします。
 - YESの場合は、実際のニーズに応じて適宜リリースしてください。
 - NOの場合は、[手順4](#step04)を実行してください。
4. <span id="step04"></span>現在のネットワークでのCOSへのアップロードの転送パフォーマンスをチェックします。
COSのCOSCMDツールを例に、20MBのオブジェクトのアップロードおよびダウンロードパフォーマンスをテストします。
```
coscmd probe -n 1 -s 20
```
次のような結果が返され、平均速度（Average）、最低速度（Min）、最高速度（Max）がそれぞれ得られます。
![](https://main.qcloudimg.com/raw/2fcecb96df04acc6b0c32c120ccb3c39.png)
5. ブラウザから[ネットワークスピードテスト](https://www.speedtest.cn/)にアクセスし、[手順4](#step04)の結果も踏まえて、クライアントのネットワーク帯域幅占有率が上限に達していないかをチェックします。
 - 手順4の速度がクライアント帯域幅速度より低い場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)ください。
 - 手順4の速度がクライアント帯域幅速度と同じであり、かつキャリアのコミットした帯域幅に達していない場合は、キャリアのカスタマーサービスに連絡してください。
 - 手順4の速度がクライアント帯域幅速度と同じであり、かつキャリアのコミットした帯域幅に達している場合は、[手順6](#step06)を実行してください。
6. <span id="step06"></span>国内のクライアントが海外ノードのbucketにアクセスしている、あるいは海外のクライアントが国内ノードのbucketにアクセスしている状況がないかをチェックします。
 - 「はい」の場合は、COSのグローバルアクセラレーション機能を使用することをお勧めします。
 - 「いいえ」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)ください。

<span id="ModifyCustomDomainNameResolution"></span>
### カスタムドメイン名解決の変更

1. カスタムドメイン名がCOSドメイン名に解決されているかどうかをチェックします。
 - 「はい」の場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)ください。
 一般的なCOSドメイン名は次のとおりです。
```
XXX.cos.ap-beijing.myqcloud.com  （COSデフォルトドメイン名）
XXX.cos.accelerate.myqcloud.com （COSグローバルアクセラレーションドメイン名）
XXX.cos-website.ap-beijing.myqcloud.com（COS静的ページドメイン名）
XXX.picbj.myqcloud.com（COS Cloud Infiniteデフォルトドメイン名）
```
 - 「いいえ」の場合は、[手順2](#2_step02)を実行してください。
一般的な非COSドメイン名は次のとおりです。 
```
XXX.file.myqcloud.comまたはXXX.cdn.dnsv1.com（Tencent Cloud CDNデフォルトドメイン名）
XXX.w.kunlungr.com（aliyunCDNデフォルトドメイン名）
```
2. <span id="2_step02"></span>カスタムドメイン名のCNAMEを必要なCOSドメイン名に解決し、データのアップロードを行います。
例えば、`upload.mydomain.com  cname XXX.cos.ap-beijing.myqcloud.com`などとします。具体的な操作については、[カスタムオリジンサーバードメイン名の有効化](https://intl.cloud.tencent.com/document/product/436/31507)をご参照ください。
3. クライアントのCOSドメイン名を変更します。
C#コードを例にとります。
```
CosXmlConfig config = new CosXmlConfig.Builder()
.SetConnectionTimeoutMs(60000) //接続タイムアウト時間を設定します。単位はミリ秒、デフォルトでは45000msです
.SetReadWriteTimeoutMs(40000) //読み取り/書き込みタイムアウト時間を設定します。単位はミリ秒、デフォルトでは45000msです
.IsHttps(true) //デフォルトhttpsリクエストを設定します 
.SetAppid(appid) //Tencent Cloudアカウントのアカウント識別APPIDを設定します
.SetRegion(region) //デフォルトのバケットリージョンを設定します
.SetHost("XXXXXX.com") //カスタムドメイン名を入力します
.SetDebugLog(true) .Build(); //CosXmlConfigオブジェクトを作成します
```
その他のSDKの呼び出しについては、[SDKの概要](https://intl.cloud.tencent.com/document/product/436/6474)をご参照ください。

