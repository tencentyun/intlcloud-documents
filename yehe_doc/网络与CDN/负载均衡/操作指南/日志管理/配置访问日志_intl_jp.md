CLBはレイヤー7（HTTP/HTTPS）アクセスログ（Access Log）の設定をサポートしています。アクセスログは、クライアントリクエストの把握、トラブルシューティングの補助、ユーザー行動の分析と整理などに役立ちます。現在アクセスログはCLSへの保存をサポートしており、分単位でのログレポート、オンラインマルチルール検索をサポートしています。

CLBのアクセスログは主にトラブルシューティングに用いられ、業務上の問題を迅速に特定する上で役立ちます。アクセスログの機能には、ログレポート、ログのストレージと照会があります。
- ログレポートはベストエフォートサービス（Best-Effort Service）です。業務の転送を優先的に保障した後にログレポートを保障します。
- ログのストレージと照会は、現在使用中のストレージサービスに基づいてサービス品質保証（SLA）を提供します。

>?
>- 現在CLBはレイヤー7プロトコル（HTTP/HTTPS）のみ、アクセスログをCLSに保存する設定をサポートしています。レイヤー4プロトコル（TCP/UDP/TCP SSL）ではアクセスログをCLSに保存する設定をサポートしていません。
>- CLBによるアクセスログのCLSへの保存設定機能は無料です。ユーザーにはCLSの料金のみがかかります。
>- この機能は現在一部のリージョンでのみサポートされています。実際には、コンソールのサポートリージョンに準じます。
>



## 方法1：単一のインスタンスにアクセスログを設定する
### ステップ1：アクセスログのCLSへの保存の有効化
1. [CLBコンソール](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3)にログインし、左側ナビゲーションバーの**インスタンス管理**をクリックします。
2. **インスタンス管理**ページで、目的のCLB IDをクリックします。
3. **基本情報**ページの「アクセスログ（レイヤー7）」モジュールで、鉛筆のアイコンをクリックします。
![](https://main.qcloudimg.com/raw/b3f9b4276b4ff2f28ac184478ce7964c.png)
4. ポップアップした**CLSログ保存場所の変更**ダイアログボックスで**ログの有効化**を開き、アクセスログを保存するログセットおよびログトピックを選択し、**送信**をクリックします。ログセットまたはログトピックを作成していない場合は、[関連リソースの新規作成](https://console.cloud.tencent.com/cls/logset)をクリックしてから、具体的な保存場所を選択してください。
![](https://main.qcloudimg.com/raw/33386c84ae812881548d1b621fbe6a70.png)
>?clb_logsetログセット下の、**CLB**の表示があるログトピックを選択することをお勧めします。**CLB**の表示があるログトピックと一般のログトピックとの違いは次の点にあります。
>- **CLB**の表示があるログトピックでは、インデックスはデフォルトで自動作成されます。一般のログトピックでは手動でインデックスを作成する必要があり、作成しなければ検索がサポートされません。
>- **CLB**の表示があるログトピックはデフォルトでダッシュボードをサポートします。一般のログトピックでは手動でダッシュボードを設定する必要があります。
6. 設定完了後にログセットまたはログトピックをクリックすると、CLSコンソールの検索分析ページにリダイレクトされます。
7. （オプション）アクセスログを無効化したい場合は、再度鉛筆のアイコンをクリックし、ポップアップした**CLSログ保存場所の変更**ダイアログボックスで無効化を行い、送信するだけで可能です。

### ステップ2：ログトピックのインデックスの設定
>?単一のインスタンスに設定するアクセスログのログトピックには必ずインデックスを設定しなければならず、そうしなければログが検索できなくなります。
>
設定を推奨するインデックスは次のとおりです。

| キー値インデックス    | フィールドタイプ | 区切り文字 |
| :---------- | :------- | :----- |
| server_addr | text     | 区切り文字は設定不要     |
| server_name | text     | 区切り文字は設定不要     |
| http_host   | text     | 区切り文字は設定不要     |
| status      | long     | -     |
| vip_vpcid   | long     | -     |

具体的な操作は次のとおりです。
1. [CLSコンソール](https://console.cloud.tencent.com/cls)にログインし、左側のナビゲーションバーで**ログトピック**をクリックします。
2. **ログトピック**ページで、目的のログトピックIDをクリックします。
3. ログトピック詳細ページで**インデックスの設定**タブをクリックし、右上隅の**編集**をクリックするとインデックスを追加できます。インデックスフィールドの設定説明については、[インデックスの有効化](https://intl.cloud.tencent.com/document/product/614/39594)をご参照ください。
![](https://main.qcloudimg.com/raw/38b22da412497a25ac9d6d304766d1ac.png)
4. インデックスの設定が完了すると、結果は下図のようになります。
![](https://main.qcloudimg.com/raw/6e2393e34cd06c5d073faba88d34110f.png)

### ステップ3：アクセスログの確認
1. [CLSコンソール](https://console.cloud.tencent.com/cls)にログインし、左側のナビゲーションバーの**検索分析**をクリックします。
3. **検索分析**ページで、ログセット、ログトピックおよび時間範囲を選択し、**検索分析**をクリックすると、CLBがCLSに送信したアクセスログを検索できます。検索構文の詳細については、[構文とルール](https://intl.cloud.tencent.com/document/product/614/37882)をご参照ください。
![](https://main.qcloudimg.com/raw/e15271ea2d1ffac0e735eb254224a5e5.png)

## 方法2：アクセスログの一括設定

### ステップ1：ログセットとログトピックの作成 [](id:step2)
アクセスログをCLSに保存するよう設定したい場合は、先にログセットとログトピックを作成する必要があります。
ログセットとログトピックを作成済みの場合は、スキップして[ステップ2](#step3)から操作を開始することができます。
1. [CLBコンソール](https://console.cloud.tencent.com/clb)にログインし、左側ナビゲーションバーの**アクセスログ**をクリックします。
2. **アクセスログ**ページの左上隅で所属リージョンを選択し、**ログセット情報**のエリアで**ログセットの作成**をクリックします。
3. ポップアップした**ログセットの作成**ダイアログボックスで保存期間を設定し、**保存**をクリックします。
>?各リージョンにつき、作成できるログセットは1つのみです。ログセット名は「clb_logset」となります。
>
4. **アクセスログ**ページの**ログトピック**のエリアで**ログトピックの新規作成**をクリックします。
5. ポップアップした**ログトピックの追加**ダイアログボックスで、ストレージタイプとログの保存期間を選択した後、左側のCLBインスタンスを選択して右側のリストに追加し、**保存**をクリックします。
>?
>- ストレージタイプには標準ストレージと低頻度ストレージがあります。詳細については、[ストレージタイプの概要](https://www.tencentcloud.com/document/product/614/42003)をご参照ください。
>- ログの保存は永久保存および固定期間での保存をサポートしています。
>- ログトピックを新規作成する際は、CLBインスタンスを追加するかどうかを選択できます。ログトピックリストの右側の**操作**列で**管理**をクリックすると、CLBインスタンスを再度追加できます。各CLBインスタンスは1つのログトピックにのみ追加できます。
>- 1つのログセットに複数のログトピック（Topic）を作成することができます。さまざまなCLBログをさまざまなログトピックに保存することが可能であり、これらのログトピックにはデフォルトで**CLB**の表示が付帯します。
>
![](https://qcloudimg.tencent-cloud.cn/raw/bbca8587899b1c721be6aa5695f02d95.png)
6. （オプション）アクセスログを無効化したい場合は、ログトピックリストの右側の**操作**列で**停止**をクリックし、ログの配信を停止します。

### ステップ2：アクセスログの確認[](id:step3)
CLBはアクセスログの変数をキー値とするインデックスを自動的に設定しているため、手動でインデックスを設定する必要はありません。検索分析によってそのままアクセスログの照会を行うことができます。
1. [CLBコンソール](https://console.cloud.tencent.com/clb)にログインし、左側ナビゲーションバーの**アクセスログ**をクリックします。
2. 目的のログトピック右側の**操作**列の**検索**をクリックし、[CLSコンソール](https://console.cloud.tencent.com/cls/search)の「検索分析」ページにリダイレクトします。
3. **検索分析**ページの入力ボックスに検索分析語を入力し、時間範囲を選択して**検索分析**をクリックすると、CLBがCLSに送信したアクセスログを検索できます。
>?検索構文の詳細については、[構文とルール](https://intl.cloud.tencent.com/document/product/614/37803)をご参照ください。
>


## ログ形式および変数の説明
### ログ形式
```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port]  [$server_name] [$remote_addr:$remote_port] [$status] [$upstream_addr] [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer] [$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$vip_vpcid] [$uri] [$server_protocol]
```

### フィールドタイプ
CLSは現在、次の3種類のフィールドタイプをサポートしています。

| 名称   | タイプの説明                 |
| :----- | :----------------------- |
| text   | テキストタイプ                 |
| long   | 整数値タイプ（Int 64）   |
| double | 浮動小数点数値タイプ（64 bit） |

### ログ変数の説明
<table class="table"><thead><tr><th>変数名</th><th>説明</th><th>フィールドタイプ</th></tr></thead>
<tbody><tr><td>stgw_request_id</td><td> リクエストIDです。 </td><td>text</td></tr>
<tr><td>time_local</td><td>アクセスの時間とタイムゾーンです。例えば「01/Jul/2019:11:11:00 +0800」の場合、最後の「+0800」は属するタイムゾーンがUTCの8時間後、すなわち北京時間であることを表します。</td><td>text</td></tr>
<tr><td>protocol_type</td><td>プロトコルタイプ（HTTP/HTTPS/SPDY/HTTP2/WS/WSS）です。</td><td>text</td></tr>
<tr><td>server_addr</td><td>CLBのVIPです。 </td><td>text</td></tr>
<tr><td>server_port</td><td>CLBのVPort、すなわちリスニングポートです。</td><td>long</td></tr>
<tr><td>server_name</td><td> ルールのserver_nameです。CLBのリスナーに設定するドメイン名です。</td><td>text</td></tr>
<tr><td>remote_addr</td><td> クライアントIPです。</td><td>text</td></tr>
<tr><td>remote_port</td><td> クライアントポートです。</td><td>long</td></tr>
<tr><td>status</td><td> CLBがクライアントに返すステータスコードです。 </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> RSアドレスです。</td><td>text</td></tr>
<tr><td>upstream_status</td><td> RSがCLBに返すステータスコードです。 </td><td>text</td></tr>
<tr><td>proxy_host</td><td> stream IDです。 </td><td>text</td></tr>
<tr><td>request</td><td>リクエストラインです。 </td><td>text</td></tr>
<tr><td>request_length</td><td>クライアントから受信したリクエストのバイト数です。 </td><td>long</td></tr>
<tr><td>bytes_sent</td><td>クライアントに送信したバイト数です。 </td><td>long</td></tr>
<tr><td>http_host</td><td> リクエストドメイン名、すなわちHTTPヘッダー内のHostです。</td><td>text</td></tr>
<tr><td>http_user_agent</td><td> HTTPプロトコルヘッダーのuser_agentフィールドです。</td><td>text</td></tr>
<tr><td>http_referer</td><td> HTTPリクエスト元です。 </td><td>text</td></tr>
<tr><td>request_time</td><td>リクエストの処理時間です。クライアントからの最初のバイトの受信時から、クライアントに最後のバイトを送信するまでの時間です。クライアントリクエストがCLBに到着し、CLBがリクエストをRSに転送し、RSが応答データをCLBに送信し、CLBがデータをクライアントに転送するまでのすべての時間が含まれます。</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td>バックエンドのリクエスト全体にかかった時間です。RSへのCONNECT開始からRSが応答の受信を完了するまでの時間を指します。</td><td>double</td></tr>
<tr><td>upstream_connect_time</td><td>RSとの間でTCP接続を確立するためにかかった時間です。RSへのCONNECT開始からHTTPリクエストの送信開始までの時間を指します。</td><td>double</td></tr>
<tr><td>upstream_header_time</td><td>RSからのHTTPヘッダーの受信を完了するまでにかかった時間です。RSへのCONNECT開始から、RSがHTTPレスポンスヘッダーの受信を完了するまでの時間を指します。</td><td>double</td></tr>
<tr><td>tcpinfo_rtt</td><td>TCP接続のRTTです。 </td><td>long</td></tr>
<tr><td>connection</td><td>接続IDです。 </td><td>long</td></tr>
<tr><td>connection_requests</td><td>接続したリクエストの数です。 </td><td>long</td></tr>
<tr><td>ssl_handshake_time</td><td>SSLハンドシェイクの各段階の消費時間を記録します。形式はx:x:x:x:x:x:xです。このうち、コロンで区切られた文字列は、単位がmsで、各段階の消費時間が1ms未満の場合は0と表示されます。
<ul><li>最初のフィールドはSSLセッションを再利用したかどうかを表します。</li>
<li>2番目のフィールドはハンドシェイク全体の時間を表します。</li>
<li>3~7はSSLの各段階の消費時間を表します。</li>
<li>3番目のフィールドはCLBのclient hello受信からserver hell done送信までの時間を表します。</li>
<li>4番目のフィールドはCLBのserver証明書送信開始からserver証明書送信完了までの時間を表します。</li>
<li>5番目のフィールドはCLBの署名計算からserver key exchange送信完了までの時間を表します。</li>
<li>6番目のフィールドはCLBのclient key exchange受信開始からclient key exchange受信完了までの時間を表します。</li>
<li>7番目のフィールドはCLBのclient key exchange受信からserver finished送信までの時間を表します。</li></ul></td><td>text</td></tr>
<tr><td>ssl_cipher</td><td> SSL暗号スイートです。</td><td>text</td></tr>
<tr><td>ssl_protocol</td><td> SSLプロトコルバージョンです。</td><td>text</td></tr>
<tr><td>vip_vpcid</td><td>CLB VIPの属するVPC IDです。パブリックネットワークCLBのvip_vpcidは-1です。</td><td>long</td></tr>
<tr><td>request_method</td><td>リクエストメソッドです。POSTおよびGETリクエストをサポートしています。</td><td>text</td></tr>
<tr><td>uri</td><td>リソース識別子です。</td><td>text</td></tr>
<tr><td>server_protocol</td><td>CLBのプロトコルです。</td><td>text</td></tr>
</tbody></table>

### デフォルトで検索をサポートするログ変数
「CLB」の表示があるログセットの、デフォルトで検索をサポートするフィールドは次のとおりです。
<table class="table"><thead><tr><th>インデックスフィールド</th><th>説明</th><th>フィールドタイプ</th></tr></thead>
<tbody>
<tr><td>time_local</td><td>アクセスの時間とタイムゾーンです。例えば「01/Jul/2019:11:11:00 +0800」の場合、最後の「+0800」は属するタイムゾーンがUTCの8時間後、すなわち北京時間であることを表します。</td><td>text</td></tr>
<tr><td>protocol_type</td><td>プロトコルタイプ（HTTP/HTTPS/SPDY/HTTP2/WS/WSS）です。</td><td>text</td></tr>
<tr><td>server_addr</td><td>CLBのVIPです。 </td><td>text</td></tr>
<tr><td>server_name</td><td> ルールのserver_nameです。CLBのリスナーに設定するドメイン名です。</td><td>text</td></tr>
<tr><td>remote_addr</td><td> クライアントIPです。</td><td>text</td></tr>
<tr><td>status</td><td> CLBがクライアントに返すステータスコードです。 </td><td>long</td></tr>
<tr><td>upstream_addr</td><td> RSアドレスです。</td><td>text</td></tr>
<tr><td>upstream_status</td><td> RSがCLBに返すステータスコードです。 </td><td>text</td></tr>
<tr><td>request_length</td><td>クライアントから受信したリクエストのバイト数です。 </td><td>long</td></tr>
<tr><td>bytes_sent</td><td>クライアントに送信したバイト数です。 </td><td>long</td></tr>
<tr><td>http_host</td><td> リクエストドメイン名、すなわちHTTPヘッダー内のHostです。</td><td>text</td></tr>
<tr><td>request_time</td><td>リクエストの処理時間です。クライアントからの最初のバイトの受信時から、クライアントに最後のバイトを送信するまでの時間です。クライアントリクエストがCLBに到着し、CLBがリクエストをRSに転送し、RSが応答データをCLBに送信し、CLBがデータをクライアントに転送するまでのすべての時間が含まれます。</td><td>double</td></tr>
<tr><td>upstream_response_time</td><td>バックエンドのリクエスト全体にかかった時間です。RSへのCONNECT開始からRSが応答の受信を完了するまでの時間を指します。</td><td>double</td></tr>
</tbody></table>
