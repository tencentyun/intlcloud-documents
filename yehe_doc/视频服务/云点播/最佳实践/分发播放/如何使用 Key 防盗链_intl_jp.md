

## ご使用にあたっての注意事項

### Demo機能紹介
このDemoは、VOD[Keyホットリンク防止](https://intl.cloud.tencent.com/document/product/266/33986)システムの使用方法を提示するもので、コンソールでのKeyホットリンク防止の有効化、ホットリンク防止署名の配布サービスの構築およびホットリンク防止署名を使用してのビデオ再生を含んでいます。

### アーキテクチャおよびフロー

Demoは、Serverless Cloud Function（SCF）を基にHTTPサービスを構築して、クライアントからホットリンク防止署名を取得するためのリクエストを受信します。サービスは、リクエストBodyからのVODのビデオオリジナルURLを取得し、ホットリンク防止署名を計算して、ホットリンク防止署名付きのURLをクライアントに返します。

システムは主に4つの構成部分に及びます：開発者、API Gateway、Serverless Cloud Function、VODであり、このうちAPI GatewayおよびServerless Cloud Functionは、下図に示すとおりこのDemoのデプロイオブジェクトです。
<img src="https://main.qcloudimg.com/raw/f30d9b832b388c9ffe35551ef26743b4.png" width="600">

具体的な業務フローは次のとおりです。

1. VODコンソールでビデオのオリジナルURLを取得します（実際の本番環境では、プレーヤーがビジネスバックエンドからビデオのURLをリクエストする必要がありますが、ここではフローを簡素化するために、開発者がその業務行為をシミュレーションします）。
2. ビデオのオリジナルURLを使用して、SCFにホットリンク防止署名をリクエストします。
3. ホットリンク防止署名付きのビデオURLを使用して、VOD CDNをリクエストして、ビデオを再生します。

> ?DemoのSCFコードはPython3.6を使用して開発されており、このほかSCFはPython2.7、Node.js、Golang、PHP、Javaなどの複数のプログラミング言語もサポートしています。開発者は状況に応じて自由に選択できます。詳細は [SCF開発ガイド](https://intl.cloud.tencent.com/document/product/583/11061)をご参照ください。

### 料金
ここで提供するVOD Keyホットリンク防止署名の配布サービスであるDemoは無料のオープンソースですが、構築および使用のプロセスにおいて以下の料金が発生することがあります。

- サービスのデプロイスクリプト実行に使用するため、Tencent CloudのCloud Virtual Machine（CVM）を購入します。詳細については、[CVM料金](https://intl.cloud.tencent.com/zh/document/product/213/2180)をご参照ください。
- Serverless Cloud Function（SCF）を使用して署名配布サービスを提供するには、 [SCF料金](https://intl.cloud.tencent.com/document/product/583/12284) および [SCF無料限度額](https://intl.cloud.tencent.com/document/product/583/12282)をご参照ください。
- Tencent Cloud API Gatewayを使用して、 SCFのためにパブリックネットワークインターフェースを提供します。詳細は [API Gateway料金](https://intl.cloud.tencent.com/document/product/628/11771)をご参照ください。
- VODのストレージはアップロードしたビデオを保存するために消費されます。詳細については、[ストレージ料金](https://intl.cloud.tencent.com/document/product/266/14666)および[ストレージリソースパック](https://intl.cloud.tencent.com/zh/document/product/266/14666)をご参照ください。
- VODのトラフィックはビデオを再生するために消費されます。詳細については、[トラフィック課金](https://intl.cloud.tencent.com/document/product/266/14666)および[トラフィックリソースパック](https://cloud.tencent.com/document/product/266/14667)をご参照ください。

## Keyホットリンク防止署名の配信サービスのクイックデプロイ

### 手順1：Tencent Cloud CVMの準備[](id:p1)

デプロイスクリプトは、1台のTencent Cloud CVM上で実行させる必要があります。要件は次のとおりです。

- リージョン：任意。
- モデル：公式サイトは最低構成（1コア1GB）であればOKです。
- パブリックネットワーク：パブリックIPを有する必要があります。帯域幅は1Mbps以上。
- OS：公式パブリックイメージ`Ubuntu Server 16.04.1 LTS 64ビット`または`Ubuntu Server 18.04.1 LTS 64ビット`。

CVMの購入方法は [操作ガイド - インスタンス作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。システムの再インストール方法は [操作ガイド - システム再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

>!
>- Keyホットリンク防止署名配布サービスのDemo自身はCVMに依存していません。CVMを使用してデプロイスクリプトを実行しているだけです。
>- 上述の条件に適合するTencent Cloud CVMがない場合は、その他のパブリックネットワークアクセスを備えたLinux（CentOS、Debianなど）またはMac機器でデプロイスクリプトを実行することもできます。ただし、OSの違いによってスクリプトの特定のコマンドを修正する必要があります。具体的な修正方式については、開発者自身で検索してください。

### 手順2：VODのアクティブ化ならびにKeyホットリンク防止の設定[](id:p2)

1. [クイックスタート - 手順1](https://intl.cloud.tencent.com/document/product/266/8757) を参照してVODサービスをアクティブにします。
2. アクティブにした後、 [ホットリンク防止の設定](https://intl.cloud.tencent.com/document/product/266/14060) ドキュメントを参照して、 Keyホットリンク防止を有効にし、ホットリンク防止Keyを記録します。
![](https://qcloudimg.tencent-cloud.cn/raw/c43642ea12afda47aff5ca5205f63f4f.png)
>!ここではKeyホットリンク防止をアクティブにして、Refererホットリンク防止はアクティブにはしません。 Refererホットリンク防止を同時にアクティブにした場合、以下のテスト方法では、Refererホットリンク防止要件に適合しないことから、リクエストが失敗することがあります。

### 手順3：APIキーおよびAPPIDの取得[](id:p3)

Keyホットリンク防止署名配布サービスのDemoのデプロイおよび稼働プロセスは、開発者のAPIキー（SecretIdおよびSecretKey）およびAPPIDまで使用する必要があります。

- まだキーを作成していない場合は、[キー作成ドキュメント](https://intl.cloud.tencent.com/document/product/598/34228) を参照して、新しいAPIキーを作成してください。キーを作成済みの場合は、[キー表示ドキュメント](https://intl.cloud.tencent.com/document/product/598/34228)を参照してAPIキーを取得してください。
- コンソールの [アカウント情報](https://console.cloud.tencent.com/developer) 画面で下部に示すとおり、APPIDを表示することができます。
  ![](https://main.qcloudimg.com/raw/0e7dda93add5f53b2da07d16cf6f4406.png)

### 手順4：ホットリンク防止署名配布サービスのデプロイ

[手順1で準備したCVM](#p1)（ログイン方法の詳細は [操作ガイド - Linuxにログイン](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください）にログインして、リモートターミナルで以下のコマンドを入力して実行します。

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;export APPID=125xxxxxxx;export ANTI_LEECH_KEY=xxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/anti_leech_sign_scf.sh
```

>? [手順3](#p3) で取得した内容をコマンドのSECRET_ID 、SECRET_KEY 、APPIDに割り当ててください。 [手順2](#p2)で取得したホットリンク防止KeyをANTI_LEECH_KEYに割り当てます。

このコマンドでは、GithubからDemoソースコードをダウンロードして、インストールスクリプトを自動的に実行します。インストールのプロセスには数分間必要になり（CVMのネットワーク状況次第）、その間、リモートターミナルは以下に示す情報を出力します。

```
[2020-06-04 15:57:10]pip3インストール開始。
[2020-06-04 15:57:18]pip3インストール成功。
[2020-06-04 15:57:18]Tencent Cloud SCFツールインストール開始。
[2020-06-04 15:57:19]scfインストール成功。
[2020-06-04 15:57:19]scf設定開始。
[2020-06-04 15:57:20]scf設定完了。
[2020-06-04 15:57:20]VOD Keyホットリンク防止署名配布サービスのデプロイを開始。
[2020-06-04 15:57:30]VOD Keyホットリンク防止署名配布サービスのデプロイを完了。
[2020-06-04 15:57:32]サービスアドレス：https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/anti_leech_sign
```

出力ログの署名配布サービスアドレス（例：`https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/callback`）をコピーします。

> !出力ログで以下に示す警告が現れた場合は、通常CVMはデプロイしたばかりのサービスドメイン名を直ちに解析できないことから、その警告は無視してもかまいません。
> ```
> [2020-04-25 17:18:44]警告：Keyホットリンク防止署名配布サービスがテストに失敗しました。
> ```

### 手順5： Keyホットリンク防止のテスト

[ビデオのアップロード - ローカルからのアップロード手順](https://intl.cloud.tencent.com/document/product/266/33890) の説明に従って、1個のテストビデオをVODにアップロードします。アップロードの完了後、【クイックビュー】をクリックしてから、右側の【アドレスコピー】をクリックしてそのビデオのURLをコピーします。
![](https://qcloudimg.tencent-cloud.cn/raw/ac27b65a2bb0cc91ac9f71b141a31cb2.png)
CVMのコマンドラインで`curl`コマンドを実行してこのURLへの直接アクセスをテストします。結果はKeyホットリンク防止規則に適合しなかったことから、サーバーにアクセスを拒絶されます。HTTPリターンコードは403になります（テスト時は、コマンドのURLを実際のURLに置換してください。以下同じ）。

```
ubuntu@VM-69-2-ubuntu:~$ curl -I "http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4"
HTTP/1.1 403 Forbidden
Server: NWS_VP
Connection: keep-alive
Date: Thu, 04 Jun 2020 08:27:54 GMT
Content-Type: text/plain
Content-Length: 14
```
CVMコマンドラインで`curl`コマンドを実行して、手順4でデプロイされたサービスからのホットリンク防止署名付きのURLをリクエストします（`-d`は、POSTメソッドを使用してリクエストを開始し、付帯するパラメータはビデオURLです）。
```
ubuntu@VM-69-2-ubuntu:~$ curl -d 'http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4' https://service-xxxxxxxx-125xxxxxxx.gz.apigw.tencentcs.com/release/anti_leech_sign; echo
http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4?t=5ed8b8d2&exper=0&rlimit=0&us=455041&sign=fe6394007c2e7aef39fc70a02e897f69
```
`curl`コマンドを再度使用して、前の手順で得たホットリンク防止署名付きのURLにアクセスすれば、正常にアクセスできます（HTTPリターンコードは200）。
```
ubuntu@VM-69-2-ubuntu:~$ curl -I "http://125xxxxxxx.vod2.myqcloud.com/f888c998vodcq125xxxxxxx/c849148f528xxxxxxxxxxxxxxxx/xxxxxxxxxx.mp4?t=5ed8b8d2&exper=0&rlimit=0&us=455041&sign=fe6394007c2e7aef39fc70a02e897f69"
HTTP/1.1 200 OK
Server: tencent-cos
Connection: keep-alive
Date: Thu, 04 Jun 2020 08:37:17 GMT
Last-Modified: Fri, 22 May 2020 15:06:15 GMT
Content-Type: video/mp4
Content-Length: 232952632
Accept-Ranges: bytes
ETag: "1da6be3a0d1da5edae4ff0b1feff02cf-223"
x-cos-hash-crc64ecma: 16209801220610226954
x-cos-request-id: NWVkOGIyYmVfZDUyMzYyNjRfYWMwMF85YjkyNzA=
X-Daa-Tunnel: hop_count=4
X-NWS-LOG-UUID: b404f43e-3c86-4c54-8a78-fb78e4e85cf2 add71e19fb08c6d9dbe1b21a2fb157bf
Access-Control-Allow-Credentials: true
Access-Control-Allow-Headers: Origin,No-Cache,X-Requested-With,If-Modified-Since,Pragma,Last-Modified,Cache-Control,Expires,Content-Type,X_Requested_With,Range
Access-Control-Allow-Methods: GET,POST,OPTIONS
Access-Control-Allow-Origin: *
```
>?ブラウザでホットリンク防止署名付きのURLにアクセスして、ビデオを再生してホットリンク防止署名を検証できます。ただし、この方法はビデオ形式に要件があり、一般にH.264でエンコードされたMP4ファイルを使用すれば良好な互換性がありますので、このビデオを選択使用することをお勧めします。Postmanなどのサードパーティツールを使用してHTTPリクエストを送信することもできます。使用方法の詳細はご自身でご検索ください。 

## システム設計の説明

### インターフェースプロトコル

Keyホットリンク防止署名配布クラウド関数は、API Gatewayによって対外的なインターフェースを提供します。具体的なインターフェースプロトコルは以下のとおりです。

| サービス               | クラウド関数名        | インターフェース形式  | リクエスト内容     | 返信内容         |
| ------------------ | --------------- | --------- | ------------ | ---------------- |
| Keyホットリンク防止署名配布 | anti_leech_sign | HTTP POST | ビデオオリジナルURL |ホットリンク防止署名付きURL |

### 署名配布サービスコードの解読

1. `main_handler()`はエントリー関数です。
2. `parse_conf_file()`を呼び出して、`config.json`ファイルから設定情報を読み取ります。設定項目の説明は以下のとおりです（詳細パラメータは [Keyホットリンク防止署名パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)をご参照ください）。
<table>
<thead>
<tr>
<th>フィールド</th>
<th>データ型</th>
<th>機能</th>
</tr>
</thead>
<tbody>
<tr>
<td>key</td>
<td>String</td>
<td>Keyホットリンク防止キー</td>
</tr>
<tr>
<td>t</td>
<td>Integer</td>
  <td>署名有効時間、単位：秒。リクエストが処理されているときは、このパラメータとSCFサーバーの現在の時間を足し合わせると、ホットリンク防止パラメータのtになります</td>
</tr>
<tr>
<td>exper</td>
<td>Integer</td>
<td>プレビュー時間</td>
</tr>
<tr>
<td>rlimit</td>
<td>Integer</td>
<td>署名にアクセスできるクライアントIPの最大数</td>
</tr>
</tbody></table>
3. リクエストのBodyから`Dir`パラメータを解析して、ローカルで`t`および`us`のパラメータを生成し、設定ファイルからは`exper`および`rlimit`のパラメータを読み取ります。
```
       original_url = event["body"]
       parse_result = urlparse(original_url)
       directory = path.split(parse_result.path)[0] + '/'
       # 署名パラメータ
       timestamp = int(time.time())
       rand = random.randint(0, 999999)
       sign_para = {
           "t": hex(timestamp + configuration['t'])[2:],
           "exper": configuration['exper'],
           "rlimit": configuration['rlimit'],
           "us": rand
       }	
```
4. `generate_sign()`を呼び出してホットリンク防止署名を計算します。詳細なアルゴリズムは [ホットリンク防止署名](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)をご参照ください。
5. QueryStringを生成してオリジナルURLの最後に追加して、URLをホットリンク防止署名と連結します。
```
       sign_para["sign"] = signature
       query_string = urlencode(sign_para)
       new_parse_result = parse_result._replace(query=query_string)
       signed_url = urlunparse(new_parse_result)
```
6. 署名を返します 。返されるデータの形式と説明については [クラウド関数の統合レスポンス](https://intl.cloud.tencent.com/document/product/583/12513)をご参照ください。
```
       return {
           "isBase64Encoded": False,
           "statusCode": 200,
           "headers": {"Content-Type": "text/plain; charset=utf-8",
                       "Access-Control-Allow-Origin": "*",
                       "Access-Control-Allow-Methods": "POST,OPTIONS"},
           "body": signed_url
       }
```

   

