## 設定シナリオ

Tencent Cloud CDNは、Back-to-Originリクエストヘッダーの追加をサポートします。

-  X-Fiorward-Forヘッダを通じて、実際のクライアントIPをオリジンサーバーに転送することをサポートします。
- X-Forward-Port ヘッダーを通じて実際のクライアントポートをオリジンサーバーに転送することをサポートし、オリジンサーバー側の分析に用います。
- さまざまなカスタムヘッダーの追加をサポートします。

カスタムback-to-originリクエストヘッダーの設定と削除もサポートします。

## 設定ガイド

### 設定の確認

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションウィンドウで【ドメイン名管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【back-to-origin設定】タブを選択して、[Back-to-origin Request Headerの設定]セクションを見つけます。 この機能はデフォルトで無効になっています。
![img](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)

### 操作タイプ

| 操作タイプ | 説明                                                        |
| -------- | ------------------------------------------------------------ |
| 設定     | 指定されたリクエストヘッダーパラメータの値を設定します。<br/>設定されたヘッダーが存在しない場合、そのヘッダーが追加されます。<br/>back-to-originリクエストヘッダーパラメータがすでに存在する場合、設定された新しいリクエストヘッダーが古いリクエストヘッダーを上書きし、一意になります。 |　
| 追加     | 指定されたback-to-originリクエストヘッダーパラメータを追加します。<br/>設定されたヘッダーがすでに存在する場合、追加されたリクエストヘッダーが古いヘッダーを上書きし、一意になります。 |　
|削除    | 指定された応答ヘッダーパラメータを削除します。                               |

>!
> - 最下位の優先度が最上位よりも高い-この相対位置の優先度は、複数のヘッダールールの追加、複数のヘッダールールの削除または複数のヘッダールールの設定など、同じタイプのヘッダー操作に制限されます。
> - 一つのback-to-originリクエストヘッダーパラメータに複数のルールが混在している場合は、操作タイプの優先度に従って実行され、その順序は追加>削除>設定となります。例えば、X-CDNヘッダーの追加、削除、設定が同時に存在するルールでは、最初に追加、次に削除、最後に設定という順に実行します。 

### ヘッダーパラメータ

| ヘッダーパラメータ       | 説明                                                       |
| -------------- | ------------------------------------------------------------ |
| X-Forward-For  | 実際のクライアントIPを転送するために使用されます。デフォルト値は$ client_ip変数であり、変更できません。|
| X-Forward-Port | 実際のクライアントポートを転送するために使用されます。デフォルト値は$remote_port変数であり、変更できません。 |
| カスタムヘッダー    | デフォルトのキーの長さは1～100文字で、0～9の数字、a - z、A - Zの英文字、および特殊記号「-」で構成されます。<br>Valueの長さは1～1000文字で、漢字はサポートされていません。<br>一部の標準ヘッダーは、ユーザーが設定、追加、または削除できません。詳細なリストについては、[注意事項](#noice)をご覧ください。 |

> !
> - 最大10のback-to-originリクエストヘッダールールを設定できます。
> - 有効なタイプは、すべてのファイル、ファイルタイプ、ファイルディレクトリ、および指定されたファイルパスの4つのモードをサポートします。正規表現マッチングは一時的にサポートしていません。



## 設定例

アクセラレーションドメイン名`cloud.tencent.com` のback-to-origin Request Headerが次のように設定されているとします。
![img](https://main.qcloudimg.com/raw/397759f6f138183d3f1ba60b33c7effc.png)
アクセスされたリソースが`http://cloud.tencent.com/test/test.mp4`の場合、

1.`*`ルールにヒットすると、`X-Forward-For:$client_ip` ヘッダーが追加され、back-to-origin中に$client_ipを実際のクライアントIPに置き換えます。
2. `.mp4`ファイルタイプおよび`/test`パスにヒットすると、同じヘッダー操作タイプ - 追加であることから、最下位の優先度が最上位より高くなり、`x-cdn:Tencent`のヘッダーが追加されます。

<span id="noice"></span>

## 注意事項
次の標準ヘッダーは、一時的にback-to-origin Request Headerの設定/追加/削除をサポートしていません。

| www-authenticate              | authorization                    | proxy-authenticate             | proxy-authorization                 |
| ----------------------------- | -------------------------------- | ------------------------------ | ----------------------------------- |
| age                           | cache-control                    | clear-site-data                | expires                             |
| pragma                        | warning                          | accept-ch                      | accept-ch-lifetime                  |
| early-data                    | content-dpr                      | dpr                            | device-memory                       |
| save-data                     | viewport-width                   | width                          | last-modified                       |
| etag                          | if-match                         | if-none-match                  | if-modified-since                   |
| if-unmodified-since           | vary                             | connection                     | keep-alive                          |
| accept                        | accept-charset                   | expect                         | max-forwards                        |
| access-control-allow-origin   | access-control-max-age           | access-control-allow-headers   | access-control-allow-methods        |
| access-control-expose-headers | access-control-allow-credentials | access-control-request-headers | access-control-request-method       |
| origin                        | timing-allow-origin              | dnt                            | tk          
| content-disposition           | content-length                   | content-type                   | content-encoding                    |
| content-language              | content-location                 | forwarded                      | x-forwarded-host                    |
| x-forwarded-proto             | via                              | from                           | host                                |
| referer-policy                | allow                            | server                         | accept-ranges                       |
| range                         | if-range                         | content-range                  | cross-origin-embedder-policy        |
| cross-origin-opener-policy    | cross-origin-resource-policy     | content-security-policy        | content-security-policy-report-only |
| expect-ct                     | feature-policy                   | strict-transport-security      | upgrade-insecure-requests           |
| x-content-type-options        | x-download-options               | x-frame-options(xfo)           | x-permitted-cross-domain-policies   |
| x-powered-by                  | x-xss-protection                 | public-key-pins                | public-key-pins-report-only         |
| sec-fetch-site                | sec-fetch-mode                   | sec-fetch-user                 | sec-fetch-dest                      |
| last-event-id                 | nel                              | ping-from                      | ping-to                             |
| report-to                     | transfer-encoding                | te                             | trailer   
| report-to                     | transfer-encoding                | te                             | trailer                             |
| sec-websocket-version         | accept-push-policy               | accept-signature               | alt-svc                             |
| date                          | large-allocation                 | link                           | push-policy                         |
| retry-after                   | signature                        | signed-headers                 | server-timing                       |
| service-worker-allowed        | sourcemap                        | upgrade                        | x-dns-prefetch-control              |
| x-firefox-spdy                | x-pingback                       | x-requested-with               | x-robots-tag                        |
| x-ua-compatible               | max-age                          |                                |                                     |
