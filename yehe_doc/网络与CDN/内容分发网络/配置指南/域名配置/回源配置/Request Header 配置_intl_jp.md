
## 設定シナリオ

Tencent Cloud CDNは、back-to-originリクエスト ヘッダーの追加をサポートしています。

-  X-Forward-For ヘッダーにより、オリジンサーバーへの実際のクライアントIPの伝送をサポートします。
-  X-Forward-Port ヘッダーにより、オリジンサーバーへの実際のクライアントIPの伝送をサポートし、オリジンサーバー側の分析に用います。
- 各種のカスタムヘッダーの追加をサポートしています。

## 設定ガイド

### 設定の制約

- カスタマイズによるリクエストヘッダーの設定ルールは最大で10件設定できます。
- 有効化のタイプは、すべてのファイル、ファイルタイプ、ファイルディレクトリ、指定されたファイルパスの4つのモードをサポートしています。正規表現マッチングは現在サポートしていません。
- ユーザー側が送信するリクエストにヘッダー情報がすでに存在する場合は、設定したRequest Headerは、back-to-origin時に元のヘッダーに上書きされます。
- ルールが複数件あるヘッダーの設定が重複するときは、優先度は上から下に低いものから高いものとなり、一番下の優先度がトップよりも高くなります。
- カスタマイズヘッダーのKeyの値の長さのデフォルトは1～100文字で、0～9の数字、a - z、A - Zの英文字、特殊記号「-」で構成されます。
- カスタマイズヘッダーの Valueの長さは1～1000文字で、中国語はサポートしていません。
- 一部の標準ヘッダーは、自主的な追加をサポートしていません。具体的なリストは、ドキュメントの最後の説明をご覧ください。

### 設定についての説明

[CDN コンソール](https://console.cloud.tencent.com/cdn)にログインし、メニューバーの中から【ドメイン名管理】を選択して、ドメイン名右側の【管理】をクリックすると、【back-to-origin設定】にback-to-origin Request Headerの設定が見つかります。デフォルトの状態では無効になっており、何も設定されていません。
![](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)
無効の状態で、back-to-originヘッダールールを新規追加できます。
![](https://main.qcloudimg.com/raw/e2972a9d697e45b3f081b68ea5e6badb.png)

> !
> 1. ユーザー端末の実際のIP情報をもたせるヘッダーがX-Forward-Forです。その値はデフォルトで $client_ip 変数となり、変更することはできません。
> 2. ユーザー側の実際のポート情報をもたせるためのヘッダーが、X-Forward-Portです。その値はデフォルトで $remote_port変数となり、変更することはできません。

ルール追加が完了し、この時に全体の設定が無効状態であると有効化しません。
![](https://main.qcloudimg.com/raw/10c8061c2e98c8828e3b153c028db86e.png)
【優先度の調整】ボタンによって、ルールの上下の順序を調整できます。ネットワーク全体のCDNノードにリリースしたい場合は、上側の設定スイッチをクリックすれば実現できます。
![](https://main.qcloudimg.com/raw/61cdbb7d9e12968695b16a08d33d79f7.png)

## 設定例

アクセラレーションドメイン名`cloud.tencent.com`のback-to-origin Request Header を設定する場合は次のようになります。
![](https://main.qcloudimg.com/raw/397759f6f138183d3f1ba60b33c7effc.png)
アクセスするリソースが次となる場合、`http://cloud.tencent.com/test/test.mp4`
1. `*`のルールにヒットすると、`X-Forward-For:$client_ip`のヘッダーが追加され、back-to-origin時に $client_ipが実際のクライアントIPに置換されます。
2. `.mp4`ファイルタイプおよび`/test`パスにヒットすると、1番下の優先度がトップの優先度より高くなり、これにより`x-cdn:Tencent`のヘッダーが追加されます。

## 注意事項

以下の標準ヘッダーは、現在back-to-origin Request Headerの追加をサポートしていません。

<table>
<tbody><tr>
<td>www-authenticate</td>
<td>authorization</td>
<td>proxy-authenticate</td>
<td>proxy-authorization</td>
</tr>
<tr>
<td>age</td>
<td>cache-control</td>
<td>clear-site-data</td>
<td>expires</td>
</tr>
<tr>
<td>pragma</td>
<td>warning</td>
<td>accept-ch</td>
<td>accept-ch-lifetime</td>
</tr>
<tr>
<td>early-data</td>
<td>content-dpr</td>
<td>dpr</td>
<td>device-memory</td>
</tr>
<tr>
<td>save-data</td>
<td>viewport-width</td>
<td>width</td>
<td>last-modified</td>
</tr>
<tr>
<td>etag</td>
<td>if-match</td>
<td>if-none-match</td>
<td>if-modified-since</td>
</tr>
<tr>
<td>if-unmodified-since</td>
<td>vary</td>
<td>connection</td>
<td>keep-alive</td>
</tr>
<tr>
<td>accept</td>
<td>accept-charset</td>
<td>expect</td>
<td>max-forwards</td>
</tr>
<tr>
<td>access-control-allow-origin</td>
<td>access-control-max-age</td>
<td>access-control-allow-headers</td>
<td>access-control-allow-methods</td>
</tr>
<tr>
<td>access-control-expose-headers</td>
<td>access-control-allow-credentials</td>
<td>access-control-request-headers</td>
<td>access-control-request-method</td>
</tr>
<tr>
<td>origin</td>
<td>timing-allow-origin</td>
<td>dnt</td>
<td>tk</td>
</tr>
<tr>
<td>content-disposition</td>
<td>content-length</td>
<td>content-type</td>
<td>content-encoding</td>
</tr>
<tr>
<td>content-language</td>
<td>content-location</td>
<td>forwarded</td>
<td>x-forwarded-host</td>
</tr>
<tr>
<td>x-forwarded-proto</td>
<td>via</td>
<td>from</td>
<td>host</td>
</tr>
<tr>
<td>referer</td>
<td>referer-policy</td>
<td>allow</td>
<td>server</td>
</tr>
<tr>
<td>accept-ranges</td>
<td>range</td>
<td>if-range</td>
<td>content-range</td>
</tr>
<tr>
<td>cross-origin-embedder-policy</td>
<td>cross-origin-opener-policy</td>
<td>cross-origin-resource-policy</td>
<td>content-security-policy</td>
</tr>
<tr>
<td>content-security-policy-report-only</td>
<td>expect-ct</td>
<td>feature-policy</td>
<td>strict-transport-security</td>
</tr>
<tr>
<td>upgrade-insecure-requests</td>
<td>x-content-type-options</td>
<td>x-download-options</td>
<td>x-frame-options(xfo)</td>
</tr>
<tr>
<td>x-permitted-cross-domain-policies</td>
<td>x-powered-by</td>
<td>x-xss-protection</td>
<td>public-key-pins</td>
</tr>
<tr>
<td>public-key-pins-report-only</td>
<td>sec-fetch-site</td>
<td>sec-fetch-mode</td>
<td>sec-fetch-user</td>
</tr>
<tr>
<td>sec-fetch-dest</td>
<td>last-event-id</td>
<td>nel</td>
<td>ping-from</td>
</tr>
<tr>
<td>ping-to</td>
<td>report-to</td>
<td>transfer-encoding</td>
<td>te</td>
</tr>
<tr>
<td>trailer</td>
<td>sec-websocket-key</td>
<td>sec-websocket-extensions</td>
<td>sec-websocket-accept</td>
</tr>
<tr>
<td>sec-websocket-protocol</td>
<td>sec-websocket-version</td>
<td>accept-push-policy</td>
<td>accept-signature</td>
</tr>
<tr>
<td>alt-svc</td>
<td>date</td>
<td>large-allocation</td>
<td>link</td>
</tr>
<tr>
<td>push-policy</td>
<td>retry-after</td>
<td>signature</td>
<td>signed-headers</td>
</tr>
<tr>
<td>server-timing</td>
<td>service-worker-allowed</td>
<td>sourcemap</td>
<td>upgrade</td>
</tr>
<tr>
<td>x-dns-prefetch-control</td>
<td>x-firefox-spdy</td>
<td>x-pingback</td>
<td>x-requested-with</td>
</tr>
<tr>
<td>x-robots-tag</td>
<td>x-ua-compatible</td>
<td>max-age</td>
<td></td>
</tr>
</tbody></table>
