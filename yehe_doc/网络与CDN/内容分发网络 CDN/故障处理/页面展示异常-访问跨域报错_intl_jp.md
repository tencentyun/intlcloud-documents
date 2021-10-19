
## 現象の説明

下図に示すように、フロントエンドはページエラーや表示異常などの問題を引き起こすクロスドメインエラーを報告します。

![](https://main.qcloudimg.com/raw/af636dbb5bba454bb79234cd7b49dca2.png)

## 考えられる原因

クロスドメインでは、ブラウザの同一オリジンポリシーの制限により、またウェブページのセキュリティを考慮する観点から、スクリプトを介してリクエストが各種ソースに送信されると、このリクエストの応答がブラウザによってブロックされるため、フロントエンドがエラーまたはページが正常に表示されない事象を報告します。リクエストURLの**プロトコル、ドメイン名、ポート**のいずれかが現在のページのURLと異なる場合はクロスドメインです。

## 解決方法

1. 次に示すように、ページ異常エラーがクロスドメインが原因であるかどうかを確認します。
![](https://main.qcloudimg.com/raw/78d05383b9040d313c05add33a1737df.png)
2. CDNコンソールで対応するHTTPレスポンスヘッダーを設定し、このリソースへのアクセスを許可するドメインを定義します。

## 処理手順

1. <a href="https://console.cloud.tencent.com/cdn/domains">CDNコンソール</a>にログインし、対応するドメイン名管理-高度な設定-HTTPレスポンスヘッダーの設定で Access-Control-Allow-Originヘッダーパラメータを設定します。下図に示すように、すべてのドメイン名によって開始されたクロスドメインリクエストが許可されます。詳細については、[Access-Control-Allow-Originマッチングモードの説明](#ac)をご参照ください。

2. または次に示すように、クロスドメインリクエストの開始を許可する単一または複数の既知のドメイン名/IPに的を絞って設定します。
また業務上の必要性に応じて、Access-Control-Request-Method、Access-Control-Request-Headers、Access-Control-Max-Ageなどのヘッダーパラメータを追加することで、ブラウザが受信可能なリクエストの方法、追加できるヘッダー、事前リクエストの有効時間などを制限することもできます。詳細については、[パラメータサポートリスト](#ap)をご参照ください。


>! COS側のバケットでクロスドメインアクセスを設定済みである場合は、正常なアクセスを保証するため、CDNコンソール <a href="https://intl.cloud.tencent.com/document/product/228/35320">のHTTPレスポンスヘッダー</a> でクロスドメインルールを同期的に設定してください。

[](id:ap)
### パラメータサポートリスト

| ヘッダーパラメータ            | 説明                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| Access-Control-Allow-Origin   | リソースのクロスドメインの権限問題を解決することに使用します。ドメイン値はそのリソースドメインへのアクセスを定義しています。ソースリクエストHostがドメイン名の設定リストにある場合は、対応する値を戻りヘッダーに直接入力します。ワイルドカード`*`を設定して、すべてのドメインによるリクエストを許可することもできます。詳細は[Access-Control-Allow-Originマッチングモードの説明](#ac)をご参照ください。` 「*」`の入力、または複数のドメイン名/IP/ドメイン名とIPの組み合わせ入力（「http://」または「https://」を必ず含める必要があります。入力見本：「http://test.com,http://1.1.1.1」、 カンマ区切り）（注意：最大1000文字まで入力可能）をサポートしています。 |
| Access-Control-Allow-Methods  | クロスドメインが許可するHTTPリクエスト方法の設定に使用します。同時に複数の方法を設定することができます。例： Access-Control-Allow-Methods: `POST, GET, OPTIONS`。 |
| Access-Control-Max-Age        | プレリクエストする有効時間の指定に使用します。単位は秒。非シンプルクロスドメインリクエストは、正式に通信する前に、HTTP照会リクエストを一度追加する必要があり、これを「プレリクエスト」と呼びます。このクロスドメインリクエストが安全に受信可能かを確認するために使用します。以下のリクエストが非シンプルクロスドメインリクエストと見なされた場合：GET、HEADまたはPOST以外の方式で起動するか、またはPOSTを使用しますが、リクエストデータのタイプはapplication / x-www-form-urlencoded、 multipart / form-data、text / plain以外のデータタイプになります。例えば、application / xml またはtext / xmlになります。カスタマイズしたリクエストヘッドを使用して：Access-Control-Max-Age:`1728000`にすると、1728000秒（20日）以内に、そのリソースのクロスドメインアクセスに対してその他のプレリクエストを再発信しなくなることを示します。 |
| Access-Control-Expose-Headers | どのヘッダーが応答する一部としてクライアントに公開できるかを指定するために使用します。デフォルトでは、Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragmaの6種類のヘッダーのみクライアントに公開できます。クライアントをその他のヘッダー情報にアクセスさせたい場合は、以下の設定を行うことができます。複数のヘッダーを入力する場合は、 「,」 を用いて区切ります。例：Access-Control-Expose-Headers: Content-Length,X-My-Headerは、クライアントがContent-LengthおよびX-My-Headerの2つのヘッダー情報にアクセスできることを示しています。

[](id:ac)
### Access-Control-Allow-Origin一致パターンの概要

| **一致パターン**   | **フィールド值**                                                     | **説明**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 完全一致         | `*`                                                            | `*` を設定する時、応答してヘッダーを追加します： `Access-Control-Allow-Origin:*` |
| 固定一致       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | ソース`https://cloud.tencent.com`がリストにヒットした場合、レスポンスしてヘッダーを追加します： `Access-Control-Allow-Origin: https://cloud.tencent.com` ソースが `https://www.qq.com`でリストにヒットしない場合、レスポンスに変化はありません。 |
| セカンダリ汎用ドメイン名に一致 | `https://*.tencent.com`                                       | ソース`https://cloud.tencent.com`がリストにヒットした場合、応答してヘッダーを追加します： `Access-Control-Allow-Origin: https://cloud.tencent.com`ソースが`https://cloud.qq.com`でリストにヒットしない場合、レスポンスに変化はありません。 |
| ポートに一致       | `https://cloud.tencent.com:8080`                             | ソースが `https://cloud.tencent.com:8080`でリストにヒットした場合、応答してヘッダーを追加します： `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` ソースが `https://cloud.tencent.com`でリストにヒットしない場合、レスポンスに変化はありません。 |

> !特別なポートがある場合は、リストに関連情報を入力する必要があります。任意のポートへの対応はサポートしないため、指定する必要があります。
