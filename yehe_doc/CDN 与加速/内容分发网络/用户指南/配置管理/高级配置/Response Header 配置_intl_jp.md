## 設定シナリオ

ユーザーがサービスリソースをリクエストする時に、返された**応答メッセージ**にカスタムヘッダーを追加して、オリジン間リソース共有などを実現できます。
応答ヘッダーの設定は、ドメイン名ディメンションの設定に属します。一旦設定が有効になると、ドメイン名の下にあるすべてのリソースの応答に適用されます。応答ヘッダーの設定はクライアント（ブラウザーなど）の応答動作しか影響せず、CDNノードのキャッシュ動作を影響しません。

## 設定ガイド

### 設定の確認

[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションメニューバーで【ドメイン名管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【高度な設定】で「応答ヘッダーの設定」セクションを見つけます。デフォルトでは無効になっています。【ルールの追加】をクリックして、 Response Headerルールを追加できます。
![img](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### 操作タイプ

| 操作タイプ | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 変更    | 指定された応答ヘッダーパラメータ値を変更します。<br/>重複するヘッダーパラメータが複数存在する場合、それらはすべて変更され、単一のヘッダーにマージされます。<br/>ターゲットヘッダーが存在しない場合、新しいヘッダーが作成されます。 |
| 追加     |指定された応答ヘッダーパラメータを追加します。<br/>デフォルトで、繰り返しヘッダーパラメータの追加を許可します。例：x-cdn:value1,x-cdn:value2。<br/>全く同じヘッド（パラメーターと値は同じ）の追加を許可します。例：x-cdn:value1,x-cdn:value1。<br/><br/>**ご注意：ヘッダーを追加すると、リクエストに影響を与える場合がありますのでご注意ください。最初に変更操作を選択することをお勧めします。** |
| 削除     | 指定された応答ヘッダーパラメータを削除します。                                  |

> !
> - 一部のヘッダーは、自分で追加、削除、または変更することはできません。詳細なリストについては、[注意事項](#noice)をご参照ください。
> - 最大10個のResponse Headerルールを設定でき、複数のルールが設定されている場合、ルールの優先順位を変更できます。ルールリストの一番下にあるルールの優先順位が最も高くなります。

### ヘッダーパラメータ

<table>
<thead>
<tr>
<th style="width:230px">ヘッダーパラメータ</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>Access-Control-Allow-Origin</td>
<td>リソースのクロスドメイン権限の問題を解決するために使用されます。ドメイン値は、リソースへのアクセスを許可するドメインを定義し、最大10個のドメインを設定できます。ソースリクエストホストがヘッダーパラメータ値として設定されている場合、対応する値が応答ヘッダーに入力されます。ワイルドカード「*」を設定して、すべてのドメインがリソースにアクセスできるようにすることもできます。詳細については、<a href="#acao">Access-Control-Allow-Origin マッチングモードの概要</a>をご参照ください。<br>ワイルドカード「*」、または複数のドメイン名/ IP /ドメイン名とIPの入力をサポートします。（<code>http://</code>または<code>https://</code>を含める必要があります。例：<code>http://test.com,http://1.1.1.1</code>、カンマで区切って、最大66のエントリがサポートされます）。</td>　
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>プリフライトリクエストのレスポンスの中で、リソースにアクセスするときに利用できる1つまたは複数のメソッドを指定します。同時に複数のメソッドをサポートします。例：：<br>Access-Control-Allow-Methods: <code>POST, GET, OPTIONS</code>。</td>
</tr>
</tr>
<td>Access-Control-Max-Age</td>
<td>プリフライト・リクエストの有効期間（秒単位）を指定します。<br>プリフライト・リクエストとは、単純でないクロスオリジンリクエストの場合、実際のリクエストを送信する前に、そのリクエストが安全かどうか、前もって OPTIONS リクエストを送信して確かめる仕様です。次のリクエストは、単純でないクロスオリジンリクエストと見なされ：<br>リクエストのメソッドがGET、HEAD、POSTではない場合、またはPOSTリクエストを使用した、リクエストデータ型が application / x-www-form-urlencoded、 multipart / form-data、またはtext / plainではない場合。例、application / xml または text / xml。<br>カスタムリクエストヘッダーが Access-Control-Max-Age:<code>1728000</code>の場合、1,728,000秒（20日）以内に、このリソースへのクロスドメインアクセスに対して別のプリフライトリクエストが送信されないことを示します。</td>
</tr>
</tr>
<td>Access-Control-Expose-Headers</td>
<td>レスポンスの一部としてどのヘッダーを公開するかを、その名前を列挙して示します。<br>既定では、次の6つのヘッダーをクライアントに公開できます：Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma。<br>クライアントが他のヘッダー情報にアクセスできるようにしたい場合、次の設定を行うことができます。複数のヘッダーを入力する場合は、「、」で区切る必要があります。例えば：<code>Access-Control-Expose-Headers: Content-Length,X-My-Header</code>、クライアントがContent-LengthとX-My-Headerヘッダー情報にアクセスできることを示します。</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>ブラウザでダウンロードを有効にし、ダウンロードしたリソースのデフォルトのファイル名を設定するために使用されます。<br>サーバーがクライアントブラウザーにファイルを送信する時に、TXT、JPGなど、ブラウザでサポートされているファイルタイプの場合、デフォルトでブラウザによって直接開かれます。ユーザーに保存を促す必要がある場合、Content-Dispositionフィールドを設定することにより、ブラウザーのデフォルト動作を上書きすることができます。一般的な設定は下記のとおり：<br><code>Content-Disposition：attachment;filename=FileName.txt</code></td>
</tr>
<tr>
<td>Content-Language</td>
<td>ページで使用される言語コードを指定します。一般的な設定は次のとおり：<br><code>Content-Language: zh-CN</code><br><code>Content-Language: en-US</code></td>
</tr>
<tr>
<td>カスタム</td>
<td>カスタムヘッダーとカスタムKey-Value設定の追加をサポートします。<br>カスタムヘッダーパラメータ：大文字と小文字、数字、および-で構成され、長さは1 - 100 文字にする必要があります。<br>カスタムヘッダー値：長さは1 - 1000 文字にする必要があり、中国語はサポートされていません。</td>
</tr>
</tbody></table>

[](id:acao)
### Access-Control-Allow-Origin マッチングモードの概要

| **マッチング方式**   | **ドメイン値**                                                     | **説明**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 完全マッチング         | *                                                            | *に設定する場合、ヘッダー `Access-Control-Allow-Origin:*` がすべての応答に追加されます。 |
| 固定マッチング       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` |  `https://cloud.tencent.com`からのリクエストで、リストにヒットした場合、応答に次のヘッダーを追加： `Access-Control-Allow-Origin: https://cloud.tencent.com`。 `https://www.qq.com`からのリクエストで、リストにヒットしない場合、応答は変わりません。 |
|第2レベルのワイルドカードドメイン名のマッチング | `http://*.tencent.com`                                       |`https://cloud.tencent.com`からのリクエストで、リストにヒットした場合、応答に次のヘッダーを追加：`Access-Control-Allow-Origin: https://cloud.tencent.com` 。 `https://cloud.qq.com`からのリクエストで、リストにヒットしない場合、応答は変わりません。 |
| ポートマッチング       | `https://cloud.tencent.com:8080`                             | `https://cloud.tencent.com:8080`からのリクエストで、リストにヒットした場合、応答に次のヘッダーを追加： `Access-Control-Allow-Origin:https://cloud.tencent.com:8080`。 `https://cloud.tencent.com`からのリクエストで、リストにヒットしない場合、応答は変わりません。 |

>! 特殊なポートがある場合は、リストに関連情報を記入する必要があります。任意のポートマッチングをサポートしないため、指定しなければなりません。

[](id:noice)
### 注意事項

現在、次のヘッダーを追加、削除、または変更することはできません。

```
Date
Expires
Content-Type
Content-Type
Content-Length
Transfer-Encoding
Cache-Control
If-Modified-Since
Last-Modified
Connection
Connection
ETag
Accept-Ranges
Age
Authentication-Info
Proxy-Authenticate
Retry-After
Set-Cookie
Vary
WWW-Authenticate
Content-Location
Content-MD5
Content-Range
Meter
Allow
Error
```
