## 設定シナリオ

ユーザーがサービスリソースをリクエストする時に、返された**応答メッセージ**にカスタムヘッダーを追加して、オリジン間リソース共有などを実現できます。
応答ヘッダーの設定は、ドメイン名に関連するものです。このため、いったん有効に設定すると、ドメイン名の下にある任意のリソースの応答メッセージが有効になります。応答ヘッダーの設定はクライアント（ブラウザなど）の応答動作にのみ影響し、CDNノードのキャッシュ動作までは影響しません。

## 設定ガイド

### 設定の確認

[CDN コンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションメニューバーで【ドメイン名管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【高度な設定】で「応答ヘッダーの設定」セクションを見つけます。デフォルトでは無効になっています。【ルールの追加】をクリックして、 Response Headerルールを設定できます。
![img](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### 操作タイプ

| 操作タイプ | 説明                                                         |
| :------- | :----------------------------------------------------------- |
| 設定     | 指定したレスポンスヘッダーパラメータの値を設定後の値に変更します。<br/>設定したヘッダーが存在しない場合は、そのヘッダーを追加します。<br>重複するヘッダーパラメータが複数存在する場合は、すべて変更すると同時に、1個のヘッダーに統合します。つまり、ルールを【x-cdn: value1の設定】に設定するとき、リクエストに複数のx-cdn ヘッダーが含まれる場合は、複数のヘッダーをすべて変更して1個のヘッダーのx-cdn: value1に統合します。 |
| 削除     | 指定したレスポンスヘッダーのパラメータを削除します。                                       |

> !
> - 一部のヘッダーはお客様個人での設定/削除はサポートしていません。リストの詳細はドキュメント [注意事項](#noice)をご参照ください。
> - Response Headerルール設定では、最大で10項目を設定できます。
> - 複数のルールで優先度を変更できます。最下部の優先度が最上部よりも高くなっています。同じヘッダーのパラメータが複数の条項のルールを設定した場合は、最下部のものを有効にします。つまり、最下部のものが最優先の条項になります。

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
<td>リソースのクロスドメインの権限問題を解決することに使用します。ドメイン値はそのリソースドメインへのアクセスを定義していて、最大で10個のドメイン設定をサポートします。ソースリクエストHostがドメイン名の設定リストにある場合は、対応する値を戻りヘッダーに直接入力します。ワイルドカード“*”を設定して、すべてのドメインによるリクエストを許可することもできます。詳細は <a href="#acao">Access-Control-Allow-Origin一致パターンの概要</a>をご参照ください。<br>“*” の入力、または複数のドメイン名 / IP / ドメイン名と IPの組み合わせ入力（<code>http://</code> または <code>https://</code>を必ず含めてください。入力見本：<code>http://test.com,http://1.1.1.1</code>、 カンマ区切りとし、最大66字まで）をサポートします。</td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>クロスドメインが許可するHTTPリクエスト方法の設定に使用します。同時に複数の方法を設定することができます。例：<br>Access-Control-Allow-Methods: <code>POST, GET, OPTIONS</code>。</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>プレリクエストする有効時間の指定に使用します。単位は秒。<br>非シンプルクロスドメインリクエストは、正式に通信する前に、 HTTP クエリーリクエストを一度追加する必要があり、これを「プレリクエスト」と呼びます。このクロスドメインリクエストが安全に受信可能かを確認するために使用します。以下のリクエストが非シンプルクロスドメインリクエストと見なされた場合：<br>GET、HEADまたはPOST以外の方式で起動するか、またはPOSTを使用しますが、リクエストデータのタイプはapplication / x-www-form-urlencoded、 multipart / form-data、text / plain以外のデータタイプになります。例えば、application / xml またはtext / xmlになります。<br>カスタマイズしたリクエストヘッドを使用して：Access-Control-Max-Age:<code>1728000</code>にすると、1728000秒（20日）以内に、そのリソースのクロスドメインアクセスに対してその他のプレリクエストを再発信しなくなることを示します。</td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>どのヘッダーが応答する一部としてクライアントに公開できるかを指定するために使用します。<br>デフォルトでは、Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragmaの6種類のヘッダーのみクライアントに公開できます。<br>クライアントをその他のヘッダー情報にアクセスさせたい場合は、以下の設定を行うことができます。複数のヘッダーを入力する場合は、 “,” を用いて区切ります。例：<code>Access-Control-Expose-Headers: Content-Length,X-My-Header</code>は、クライアントがContent-LengthおよびX-My-Headerの2つのヘッダー情報にアクセスできることを示しています。</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>ブラウザのダウンロードを有効にするために用います。同時にデフォルトでダウンロードするファイル名を設定できます。<br>サーバーは、クライアントのブラウザにファイルを発信するとき、ブラウザがサポートするファイルタイプがTXT、JPG などのタイプの場合は、デフォルトでブラウザを直接使用して開きます。ユーザー保存を提示したい場合はContent-Dispositionフィールドの設定によってブラウザでのデフォルト動作をカバーできます。通常での設定は次のとおりです。<br><code>Content-Disposition：attachment;filename=FileName.txt</code></td>
</tr>
<tr>
<td>Content-Language</td>
<td>ページで使用する言語コードを定義するのに用います。通常の設定は次のとおりです。<br><code>Content-Language: zh-CN</code><br><code>Content-Language: en-US</code></td>
</tr>
<tr>
<td>カスタマイズ</td>
<td>カスタマイズHeaderの追加、カスタマイズkey-valueの設定をサポートします。<br>カスタマイズヘッダーパラメータ：英文字の大文字、小文字、数字および-（ハイフン）で構成します。1 ～ 100字まで対応します。<br>カスタマイズヘッダーの値：1 ～ 1000字まで。中国語はサポートしていません。</td>
</tr>
</tbody></table>

[](id:acao)
### Access-Control-Allow-Origin一致パターンの概要

| **一致パターン**   | **フィールド值**                                                     | **説明**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 完全一致         | *                                                            | * を設定する時、応答してヘッダーを追加します： `Access-Control-Allow-Origin:*` |
| 固定一致       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | `https://cloud.tencent.com`からのリクエストで、リストにヒットした場合、応答に次のヘッダーを追加：`Access-Control-Allow-Origin: https://cloud.tencent.com`　`https://www.qq.com`からのリクエストで、リストにヒットしない場合、応答に変化はありません。 |　　
| 第2レベルのワイルドカードドメイン名に一致 | `http://*.tencent.com`                                       |  `https://cloud.tencent.com`からのリクエストで、リストにヒットした場合、応答に次のヘッダーを追加： `Access-Control-Allow-Origin: https://cloud.tencent.com` 　`https://cloud.qq.com`からのリクエストで、リストにヒットしない場合、応答に変化はありません。 |
| ポートに一致       | `https://cloud.tencent.com:8080`                             | `https://cloud.tencent.com:8080`からのリクエストで、リストにヒットした場合、応答に次のヘッダーを追加：`Access-Control-Allow-Origin:https://cloud.tencent.com:8080` `https://cloud.tencent.com`からのリクエストで、リストにヒットしない場合、応答に変化はありません。 |

> ! 特別なポートがある場合は、リストに関連情報を入力する必要があります。任意のポートへの対応はサポートしないため、指定する必要があります。

[](id:noice)
### 注意事項

この機能は以下のヘッダーをサポートしていません。つまり以下のヘッダーは有効になりません。

```
Date
Expires
Content-Type
Content-Encoding
Content-Length
Transfer-Encoding
Cache-Control
If-Modified-Since
Last-Modified
Connection
Content-Range
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
