CLBはカスタム設定機能をサポートしており、client_max_body_size、ssl_protocolsなどの個別のCLBインスタンスの設定パラメータをユーザーが設定でき、カスタム設定のニーズを満たすことができます。
>?
>- カスタム設定の個数は各リージョンにつき200までとなります。
>- カスタム設定の長さは64kまでとなります。
>- 現在は1つのインスタンスにバインドできるカスタム設定は1つのみです。
>- カスタム設定はCLB（旧「アプリケーション型CLB」）のレイヤー7HTTP/HTTPSリスナーについてのみ有効です。

## CLBカスタム設定パラメータの説明
現在CLBのカスタム設定では次のフィールドをサポートしています。

| 設定フィールド |   デフォルト値/推奨値  |    パラメータ範囲  | 説明  |
| :-------- | :-------- | :------ |:------ |
|ssl_protocols |<ul><li>デフォルト値：TLSv1、TLSv1.1、TLSv1.2</li><li>推奨値：TLSv1.2、TLSv1.3</li></ul> |TLSv1 TLSv1.1 TLSv1.2 TLSv1.3 |使用するTLSプロトコルのバージョンです。 |
|  ssl_ciphers  | [ssl_ciphersデフォルト値](#ssl_ciphers) |  [ssl_ciphersパラメータ範囲](#ssl_ciphers)  | 暗号スイートです。 |
|  client_header_timeout  | 60s |  [30-120]s | Clientリクエストヘッダーを取得する際のタイムアウト時間です。タイムアウトになると408を返します。|
|  client_header_buffer_size | 4k |[1-256]k | Clientリクエストヘッダーを保存するデフォルトのBufferサイズです。 |
|  client_body_timeout | 60s |  [30-120]s | ClientリクエストBodyを取得する際のタイムアウト時間です。Body全体の取得にかかる持続時間ではなく、一定時間データ伝送のないアイドル状態となった場合のタイムアウト時間を指します。タイムアウトになると408を返します。 |
|  client_max_body_size | 60M |[1-10240]M| <ul><li>デフォルトの設定範囲は1M～256Mであり、直接設定するだけで完了です。</li><li>最大10240M、すなわち10Gまでサポートされます。client_max_body_size の設定範囲を256Mより大きくする場合は、<a href="#buffer">proxy_request_buffering</a>の値をoffに設定する必要があります。</li></ul> |
|  keepalive_timeout | 75s | [0-900]s| Client-Serverの長時間接続維持時間です。0に設定すると、長時間接続が無効になります。900sより長く設定したい場合は、[チケット申請](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1)を提出してください。最大3600sまで設定可能です。 |
|  add_header |ユーザーによるカスタム追加|- | クライアントに特定のヘッダーフィールドを返します。形式はadd_header xxx yyyです。</br>例えばクロスドメインのケースでは、`add_header Access-Control-Allow-Methods 'POST, OPTIONS'; add_header Access-Control-Allow-Origin *;`のように設定することができます。|
|  more_set_headers |ユーザーによるカスタム追加|- | クライアントに特定のヘッダーフィールドを返します。形式はmore_set_headers "A:B"です。 |
|  proxy_connect_timeout | 4s | [4-120]s |upstreamバックエンドの接続タイムアウト時間です。|
|  proxy_read_timeout |60s |[30-3600]s|upstreamバックエンドの読み取りの応答タイムアウト時間です。|
|  proxy_send_timeout |60s |[30-3600]s|upstreamバックエンドへのリクエスト送信のタイムアウト時間です。|
|  server_tokens | on | on，off | <ul><li>onはバージョン情報を表示することを表します。</li><li>offはバージョン情報を非表示にすることを表します。</li></ul>|
|  keepalive_requests | 100 | [1-10000] |Client-Serverの長時間接続において送信可能な最多リクエスト数です。|
|  proxy_buffer_size | 4k |[1-32]k| Serverのレスポンスヘッダーのサイズです。デフォルトではproxy_bufferで設定した単独のバッファサイズとなります。proxy_buffer_sizeを設定する場合は、proxy_buffersも同時に設定する必要があります。|
|  proxy_buffers | 8 4k |[3-8] [4-16]k|バッファ数およびバッファサイズです。|
|  <span id="buffer">proxy_request_buffering</span> | off |on，off|<ul><li>onはクライアントのリクエストボディをキャッシュすることを表します。CLBはリクエストをキャッシュし、全体を受信し終わってから分割してバックエンドCVMに転送します。</li><li>offはクライアントのリクエストボディをキャッシュしないことを表します。CLBはリクエストを受信すると、ただちにバックエンドCVMに転送します。この場合、バックエンドCVMにはある程度のパフォーマンス負荷がかかります。</li></ul>|
|  proxy_set_header   |X-Real-Port $remote_port|<ul><li>X-Real-Port $remote_port</li><li>X-clb-stgw-vip $server_addr</li><li>Stgw-request-id $stgw_request_id</li><li>X-Forwarded-Port $vport</li><li>X-Method $request_method</li><li>X-Uri $uri</li></ul>|<ul><li>X-Real-Port $remote_portはクライアントポートを表します。</li><li>X-clb-stgw-vip $server_addrはCLBのVIPを表します。</li><li>Stgw-request-id $stgw_request_idはリクエストIDを表します（CLB内部で使用します）。</li><li>X-Forwarded-PortはCLBリスナーのポートを表します。</li><li>X-Methodはクライアントのリクエストメソッドを表します。</li><li>X-UriはクライアントのリクエストパスのURIを表します。</li></ul> |
|  send_timeout | 60s |[1-3600]s|サーバーからクライアントへのデータ伝送のタイムアウト時間です。連続した2回のデータ送信の間隔であり、リクエスト全体の伝送時間ではありません。|
|  ssl_verify_depth |  1 |[1，10]|クライアント証明書チェーンの検証の深さを設定します。|
|proxy_redirect | http:// https:// | http:// https://  | アップストリームサーバーが返す応答がリダイレクトまたはキャッシュリクエストである場合（HTTPレスポンスコードが301または302の場合）、proxy_redirectはHTTPヘッダーのLocationまたはRefreshフィールド内のhttpをhttpsに再設定し、安全なリダイレクトを実現します。  |
| ssl_early_data  |  off |on，off|TLS 1.3 0-RTTを有効化または無効化します。ssl_protocolsフィールドの値にTLSv1.3が含まれる場合のみ、ssl_early_dataをオンにすると有効になります。**ssl_early_dataをオンにするとリプレイアタックを受けるリスクがありますので、慎重に行ってください。**|
|http2_max_field_size|4k|[1-256]k|HPACKで圧縮されたリクエストヘッダーフィールドの最大サイズ（Size）を制限します。|
|error_page|-|error_page code [ = [ response]] uri|特定のエラーコード（Code）が発生した場合、あらかじめ定義したURIを表示することができます。デフォルトのステータスコード（Response）は302です。URIは必ず`/`で始まるパスでなければなりません。|
| proxy_ignore_client_abort | off | on，off | クライアントが応答の結果を待たずに自主的にCLBとの接続を切断したときに、CLBとバックエンドサーバーの接続を切断するかどうかを設定します。 |


>?このうち、proxy_buffer_sizeとproxy_buffersの設定の値は制約条件である、2 * max（proxy_buffer_size, proxy_buffers.size) ≤（proxy_buffers.num - 1）\* proxy_buffers.sizeを満たす必要があります。例えば、proxy_buffer_sizeが24k、proxy_buffersが8 8kの場合、2 * 24k = 48k、（8 - 1）\* 8k = 56kとなり、このとき48k ≤ 56kであるため、エラーは発生しません。これを満たさない場合はエラーが発生します。
>
## ssl_ciphers設定の説明[](id:ssl_ciphers)
ssl_ciphers暗号スイートを設定する際、形式はOpenSSLで使用する形式と一致させる必要があります。アルゴリズムリストは1つまたは複数の`<cipher strings>`とし、複数のアルゴリズムの間は「:」で区切ります。ALLはすべてのアルゴリズムを表し、「!」はこのアルゴリズムが有効になっていないことを表します。「+」はこのアルゴリズムの配置順を最後にすることを表します。
デフォルトで強制的に無効化される暗号化アルゴリズムは、`!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE`です。

**デフォルト値：**
```plaintext
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE:3DES;
```

**パラメータ範囲：**
```plaintext
ECDH-ECDSA-AES128-SHA256:ECDH-RSA-AES256-SHA:ECDH-ECDSA-AES256-SHA:SRP-DSS-AES-256-CBC-SHA:SRP-AES-128-CBC-SHA:ECDH-RSA-AES128-SHA256:DH-RSA-AES128-SHA256:DH-RSA-CAMELLIA128-SHA:DH-DSS-AES256-GCM-SHA384:DH-RSA-AES256-SHA256:AES256-SHA256:SEED-SHA:CAMELLIA256-SHA:ECDH-RSA-AES256-SHA384:ECDH-ECDSA-AES128-GCM-SHA256:DH-RSA-AES128-SHA:DH-RSA-AES128-GCM-SHA256:DH-DSS-AES128-SHA:ECDH-RSA-AES128-SHA:DH-DSS-CAMELLIA256-SHA:SRP-AES-256-CBC-SHA:DH-DSS-AES128-SHA256:SRP-RSA-AES-256-CBC-SHA:ECDH-ECDSA-AES256-GCM-SHA384:ECDH-RSA-AES256-GCM-SHA384:DH-DSS-AES256-SHA256:ECDH-ECDSA-AES256-SHA384:AES128-SHA:DH-DSS-AES128-GCM-SHA256:AES128-SHA256:DH-RSA-SEED-SHA:ECDH-ECDSA-AES128-SHA:IDEA-CBC-SHA:AES128-GCM-SHA256:DH-RSA-CAMELLIA256-SHA:CAMELLIA128-SHA:DH-RSA-AES256-GCM-SHA384:SRP-RSA-AES-128-CBC-SHA:SRP-DSS-AES-128-CBC-SHA:ECDH-RSA-AES128-GCM-SHA256:DH-DSS-CAMELLIA128-SHA:DH-DSS-SEED-SHA:AES256-SHA:DH-RSA-AES256-SHA:kEDH+AESGCM:AES256-GCM-SHA384:DH-DSS-AES256-SHA:HIGH:AES128:AES256:AES:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE
```

## CLBカスタム設定の例
1. [CLBコンソール](https://console.cloud.tencent.com/loadbalance/index?rid=8)にログインし、左側ナビゲーションバーで**カスタム設定**をクリックします。
2. 「カスタム設定」ページトップでリージョンを選択し、**新規作成**をクリックします。
3. 「カスタム設定の新規作成」ページで設定名とコード設定項目を入力します。コード設定項目の末尾は`;`とします。設定完了後、**完了**をクリックします。
![](https://main.qcloudimg.com/raw/7ef70a06f9509ba8759e5a923515a471.png) 
4. 「カスタム設定」ページに戻り、右側操作バーで**インスタンスにバインド**をクリックします。
5. ポップアップした「インスタンスにバインド」ダイアログボックスでバインドしたいCLBインスタンスを選択し、**送信**をクリックします。
![](https://main.qcloudimg.com/raw/ad8fb7874b9ce1fe7bf5c9366c7e64e7.png)
6. インスタンスをバインドした後、「カスタム設定」ページで、先ほど設定したカスタム設定IDをクリックして詳細ページに進み、**インスタンスのバインド**タブをクリックすると、先ほどバインドしたCLBインスタンスを確認できます。
7. （オプション）インスタンスをバインドした後、インスタンスのリストページで対応するカスタム設定情報を検索することもできます。
>?リストページに「カスタム設定のバインド」列が表示されていない場合は、リストページ右上隅の![](https://main.qcloudimg.com/raw/8cc99da2a299fc570d3d9b314c9dcae6.svg)アイコンをクリックし、ポップアップした「カスタムリストフィールド」ダイアログボックスで「カスタム設定のバインド」オプションにチェックを入れ、**OK**をクリックすると、リストページに「カスタム設定のバインド」列が表示されます。
>
![](https://main.qcloudimg.com/raw/d07bdbc134480fa89f732c93c3861243.png)
デフォルト設定コードの例：
```plaintext
ssl_protocols   TLSv1 TLSv1.1 TLSv1.2;
client_header_timeout   60s;
client_header_buffer_size   4k;
client_body_timeout    60s;
client_max_body_size   60M;
keepalive_timeout    75s;
add_header     xxx yyy;
more_set_headers      "A:B";
proxy_connect_timeout    4s;
proxy_read_timeout    60s;
proxy_send_timeout    60s;
```

