CLBはリクエストログを保存する能力をサポートしているため、お客様はリクエストログをCOSに保存し、ダウンロードして分析することができます。現在、7層LBのログ機能は完全にリリースされており、広州、上海、北京、金融区などの地域をサポートしています。是非、有効化して使用してください。

## ログ機能の有効化
**CLBインスタンス詳細**ページでログアクセス機能を有効にします。

![](https://mc.qcloudimg.com/static/img/17014eeb67628fa78ffe04e2d7a58d8d/log1.png)

対応するCOS中のバケットを選択すると、リクエストログは自動的にバケット下にlb-idという名前のフォルダを作成し、保存します。選択完了後、バケットアドレスをクリックすると直接ログのダウンロードページにジャンプすることができます。

COSのバケットを作成していない場合、[バケットの新規作成](https://console.cloud.tencent.com/cos4/bucket)を行った後に対応する保存位置を選択してください。

## 製品の制限と料金の計算
- 現在、ログの集約粒度は1時間です。
- 現在、CLBは7層（HTTP/HTTPS）ログの保存とダウンロードのみをサポートしています。
- ログデータの伝送は一定の遅延があります。
- 現在、CLBログサービスは`無料`です。COSストレージの無料限度額は[ドキュメント](https://cloud.tencent.com/document/product/436/6240)に示すとおり、50Gの無料ストレージ空間を提供しています。お客様のログの規模が大きい場合、速やかにデータを整理してください。
- ログアクセスを有効にしない場合、Tencent Cloudはデフォルトで3日間のログを保存します。ログアクセスを有効にした場合、保存時間はCOSストレージに従って決まります。

## ログフォーマット及び変数の説明
### ログフォーマット

```
[$stgw_request_id] [$time_local] [$protocol_type] [$server_addr:$server_port] [$server_name] [$remote_addr:$remote_port] [$status]  [$upstream_status] [$proxy_host] [$request] [$request_length] [$bytes_sent] [$http_host] [$http_user_agent] [$http_referer]
[$request_time] [$upstream_response_time] [$upstream_connect_time] [$upstream_header_time] [$tcpinfo_rtt] [$connection] [$connection_requests] [$ssl_handshake_time] [$ssl_cipher] [$ssl_protocol] [$ssl_session_reused]
```

### ログ変数の説明

| 番号 | 変数名 | 説明 |
| :-------- | :-------- | :------ |
| 1 | time_local	|  タイムスタンプ |
| 2 | protocol_type |  プロトコルタイプ（HTTP/HTTPS/SPDY/HTTP2/WS/WSS） |
| 3 | server_addr:server_port  | リクエストのターゲットIPとターゲットポート |
| 4 | server_name | 規則のserver_name |
| 5 | remote_addr:remote_port	| クライアントIP：ポート |
| 6 | status | LBがクライアントに返すステータスコード |
| 7 | upstream_status | RSがLBに返すステータスコード |
| 8 | proxy_host | upstream ID |
| 9 | request | リクエスト行 |
| 10 | request_length | クライアントから受信したリクエストのバイト数 |
| 11 |bytes_sent | 	クライアントに送信したバイト数 |
| 12 |http_host	 | リクエストのドメイン名 |
| 13 |http_user_agent | 	user_agent |
| 14 |http_referer	 | HTTPリクエストのソース |
| 15 | request_time|リクエストの処理時間（受信したクライアントの最初の1バイトからクライアントに送信した最後の1バイトまで、クライアントからCLBへのリクエスト送信、CLBからRSへのリクエスト転送、RSからCLBへのデータレスポンス、CLBからクライアントへのデータ転送を含む合計時間）|
| 16 | upstream_response_time |バックエンドのリクエスト全体にかかる時間（RSへの接続が開始するからRSからのレスポンスの受信が完了するまでの時間）|
| 17 | upstream_connect_time	|RSとTCP接続を構築するのにかかる時間（RSへの接続が開始するからHTTPリクエストの送信が開始するまでの時間）|
| 18 | upstream_header_time	|  RSからHTTPヘッダーの受信が完了するのにかかる時間（RSへの接続が開始するからRSからのHTTPレスポンスヘッダーの受信が完了するまでの時間）|
| 19 | tcpinfo_rtt | TCPに接続されるRTT |
| 20 | connection | 接続ID |
| 21 | connection_requests | 接続におけるリクエスト数 |
| 22 | ssl_handshake_time	|SSLハンドシェイクにかかる時間 |
| 23 | ssl_cipher| 暗号化キット|
| 24 | ssl_protocol	| SSLプロトコルのバージョン |
| 25 | ssl_session_reused |SSL SESSIONマルチプレックス|	 

