## 設定シナリオ
エンドユーザーがビジネスリソースをリクエストする時に、返された**応答メッセージ**の中にカスタムヘッダーを追加して、クロスオリジンアクセスなどを実現できます。
HTTPヘッダーの設定はドメイン名を対象にするため、一旦設定が有効になると、当該ドメイン名における任意のリソースに対するユーザーリクエストの応答メッセージには、設定されたヘッダーが追加されます。HTTP ヘッダーの設定はクライアント（ブラウザーなど）の応答動作しか影響せず、CDNノードのキャッシュ動作を影響しません。

## 設定ガイド
### 設定の確認
[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションメニューバーで【ドメイン管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【高度な設定】でHTTPヘッダー設定を確認できます。デフォルトでは無効になっています。


### 設定の変更
#### 1. 設定の変更
スイッチを切り替えて、HTTPヘッダー設定を追加します。現在、現在、次のヘッダーを設定でき、カスタムヘッダーを追加することもできます。
- Access-Control-Allow-Origin：リソースへのアクセスを許可するクロスオリジンリクエストのソースを指定します。
- Access-Control-Allow-Methods：クロスオリジンリクエストを許可する方法を指定します。
- Access-Control-Max-Age：クロスオリジンリクエストが開始されたときに、特定のリソースに対するプリフライトリクエストの返された結果のキャッシュの有効期間を指定します。
- Access-Control-Expose-Headers：クロスオリジンリクエストが開始されたときにクライアントに表示されるヘッダーを指定します。
- Content-Disposition：クライアントのダウンロードリソースをアクティブにし、デフォルトのファイル名を設定します。
- Content-Language：ページで使用される言語コードを定義するために使用されます。
- カスタム：カスタムヘッダーを追加できます。



**全般設定：Content-Disposition**
Content-Dispositionはブラウザーのダウンロードをアクティブにし、ダウンロードしたリソースのデフォルトのファイル名を設定するために使用されます。サーバーがクライアントブラウザーにファイルを送信する時に、TXT、JPG等ブラウザーでサポートされているタイプのファイルは、デフォルトで直接にブラウザーで開きます。ユーザーに対し保存することを注意する必要がある場合は、Content-Dispositionフィールドを設定することにより、ブラウザーのデフォルト動作を上書きすることができます。一般的な設定は下記のとおりです。
`Content-Disposition：attachment;filename=FileName.txt`

**全般設定：Content-Language**
Content-Languageはページで使用される言語コードを定義することに使われ、一般的な設定は下記のとおりです。
`Content-Language: zh-CN`
`Content-Language: en-US`

**クロスオリジン設定：Access-Control-Allow-Origin**
クロスオリジンアクセスとは、あるドメイン名（例えば `www.abc.com` ）にある特定のリソースから、別のドメイン名（例えば`www.def.com`）にあるリソースへリクエストを送信するシナリオを指します。リソースの所属するドメイン名が異なるため、**クロスオリジンアクセス**が発生します。異なるプロトコルまたはポートを使用すると、クロスオリジンアクセスが発生する可能性があります。この時に、最初のリソースがデータを正常に取得するには、クロスオリジンアクセスに関連する設定を応答ヘッダーに追加する必要があります。
- 機能の説明：
Access-Control-Allow-Originはリソースのクロスオリジンアクセス許可の問題を解決するために使用されます。ドメイン値は当該リソースにアクセスできるドメインを定義しています。最大10個のドメインまで設定できます。ソースリクエストのホストがドメイン名設定リストにある場合、対応する値は、返されたヘッダーに直接入力されます。ワイルドカード「*」を設定して、すべてのオリジンがリソースにアクセスできるようにすることもできます。
- マッチングモードの説明

| **マッチングモード**   | **ドメイン値**                                                     | **説明**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 完全一致         | *                                                            | *に設定する場合、次のヘッダーが応答に追加されます：<br/>`Access-Control-Allow-Origin:*` |
| 固定マッチング       | `http://cloud.tencent.com`<br/> `https://cloud.tencent.com`<br/> `http://www.b.com` | ソースhttps://cloud.tencent.comがリストにヒットした場合、次のヘッダーが応答に追加されます：<br/>`Access-Control-Allow-Origin: https://cloud.tencent.com`<br/>ソース`https://www.qq.com`がリストにヒットしなかった場合、応答は変更されません。 |
|第2レベルのワイルドカードドメイン名のマッチング | `http://*.tencent.com`                                       | ソース`https://cloud.tencent.com`がリストにヒットした場合、次のヘッダーが応答に追加されます：<br/>`Access-Control-Allow-Origin: https://cloud.tencent.com`<br/>ソースhttps://www.qq.comがリストにヒットしなかった場合、応答は変更されません。 |
| ポートマッチング       |`https://cloud.tencent.com:8080`                             | ソース`https://cloud.tencent.com:8080`がリストにヒットした場合、次のヘッダーが応答に追加されます：<br/>`Access-Control-Allow-Origin:https://cloud.tencent.com:8080`<br/>ソース`https://cloud.tencent.com`がリストにヒットしなかった場合、応答は変更されません。 |

>特殊なポートがある場合は、リストに関連情報を記入する必要があります。任意ポートのマッチングを対応しないため、ポートを指定する必要があります。

**クロスオリジン設定：Access-Control-Allow-Methods**

Access-Control-Allow-Methods はクロスオリジンアクセスに許可されるHTTPリクエスト方法を指定するために使用されます。下記のように、複数の方法を同時に設定することが可能です。　
Access-Control-Allow-Methods: `POST, GET, OPTIONS`

**クロスオリジン設定：Access-Control-Max-Age**
Access-Control-Max-Ageはプリフライトリクエストの有効期間の指定に使われます。
単純でないクロスオリジンリクエストの場合、正式に通信する前に、HTTPクエリリクエストを1回追加する必要があります。それは「プリフライトリクエスト」と言われ、当該クロスオリジンリクエストが安全に受け入れ可能かどうかを確認するために使われます。次のリクエストは、単純でないクロスオリジンリクエストと見なされます。
- リクエストは、GET、HEADまたはPOST以外の方式で開始され、またはPOSTをが使用されますが、リクエストするデータタイプがapplication/x-www-form-urlencoded、 multipart/form-data、text/plain 以外のデータタイプ（application/xmlまたはtext/xmlなど）です。
+ カスタムリクエストヘッダーを使用します。
Access-Control-Max-Ageの単位が秒です。設定例は下記の通りです。
Access-Control-Max-Age:`1728000`

1728000秒（20日）以内に、当該リソースに対するクロスオリジンリクエストはプリフライトリクエストを送信しないことを示しています。

**クロスオリジン設定：Access-Control-Expose-Headers**
Access-Control-Expose-Headersは、応答の一部としてクライアントに公開できるヘッダーを指定するために使用されます。デフォルトでは、次の6種類のヘッダーをクライアントに公開できます。
- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

クライアントが他のヘッダー情報にアクセスするようにする場合は、下記のように設定できます。複数のヘッダーを入力する時に、「、」で区切ります。
`Access-Control-Expose-Headers: Content-Length,X-My-Header`
クライアントがContent-LengthとX-My-Headerの情報にアクセスできることを示しています。

**カスタムヘッダー**
カスタムヘッダーを追加し、Key-Value設定をカスタマイズできます。

下記ヘッダーの追加は現在対応されていません。
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
複数のヘッダーが繰り返し追加される場合、下のほうの優先順位は上よりも高いため、下のヘッダーが上のヘッダーを上書きします。

#### 2. 設定を無効にする
HTTPヘッダースイッチを切り替えて、この機能を無効にすることができます。スイッチがOFFの場合、以下の既存の設定がある場合でも、実稼働環境では有効になりません。


>アクセラレーションドメイン名のサービスエリアがグローバルである場合、応答ヘッダーの設定はグローバルに有効になります。現在、中国本土内外で異なる設定はサポートされません
