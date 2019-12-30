Tencent Cloud提供のHTTP Header構成機能を利用することにより、お客様のユーザーがサービスリソースをリクエストする時に、返信される**応答メッセージ**の中に構成されたヘッダーを追加し、クロスリージョンのアクセスなどを実現できます。
リソースがノードに命中されていない時には、オリジンプルを行います。この時に、オリジンサーバーにより返されたヘッダー情報も一緒にユーザーに送信されます。リソースがノードのキャッシュに命中された時に、静的コンテンツの加速及びダウンロード加速ケースの場合には、CDNはデフォルトでキャッシュされたオリジンサーバーの Access-Control-Allow-Origin、Timing-Allow-Origin、Content-Disposition、Accept-Rangesのヘッダー情報をユーザーに送信します。
HTTP headerの構成はドメイン名を対象にするため、一旦構成が有効になると、当該ドメイン名における任意リソースに対するユーザーの応答情報には、構成されたヘッダーが追加されます。HTTP headerの構成はクライアント（例えばブラウザー）の応答行為しか影響せず、CDNノードのキャッシュ行為を影響しません。

##構成ガイド
1.  [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のメニュー欄の【ドメイン名管理】を選択し、編集しようとするドメイン名の左側の【管理】をクリックします。
2.【アドバンスド構成】の中で【HTTP Header 構成】モジュールを見つけ、セルフでヘッダーを追加できます。
3.【 HTTP header追加】をクリックすることで、ヘッダーを追加できます。

CDNは下記の6種類の常用ヘッダー構成をサポートしており、カスタマイズのヘッダー構成をも対応しています。
+ Content-Disposition：クライアントのダウンロードリソースをアクティブにし、デフォルトのファイル名を設定します。
+ Content-Language：ページに使用される言語コードを定義することに使われます。
+ Access-Control-Allow-Origin：クロスリージョンリクエストを指定する時に、リソースアクセスを認めるリクエストオリジンです。
+ Access-Control-Allow-Methods：クロスリージョンリクエストを指定する時に、許可されるクロスリージョンのリクエスト方法です。
+ Access-Control-Max-Age：クロスリージョンリクエストを指定する時に、特定リソースのプリリクエストに対し結果を返すのキャッシュ時間です。
+ Access-Control-Expose-Headers：クロスリージョンリクエストを指定する時に、クライアントに表示可能なヘッダーグループです。
+ カスタマイズ：ヘッダーをカスタマイズすることです。

### 汎用構成
#### Content-Disposition
Content-Dispositionはブラウザーのダウンロードをアクティブにすることに使われます。また、デフォルトでダウンロードするファイル名を設定することもできます。サービス側よりクライアントのブラウザーへファイルを発送する時に、TXT、JPG等ブラウザーの対応するファイルタイプである場合は、デフォルトで直接にブラウザーで開きます。ユーザーに対し保存することを注意する必要がある場合は、Content-Dispositionフィールドを構成することによりブラウザーのデフォルト行為を上書きすることができます。常用の構成は下記の通りです。`Content-Disposition：attachment;filename=FileName.txt`

#### Content-Language
Content-Languageはページに使用される言語コードを定義することに使われ、常用の構成は下記の通りです。
`Content-Language: zh-CN`
`Content-Language: en-US`

###クロスリージョン構成
あるドメイン名（例えば ```www.abc.com``` ）におけるあるリソースから、もう一つのドメイン名（例えば```www.def.com```）におけるあるリソースへリクエストを提出する時に、リソースの所属するドメイン名が違うので、 **クロスリージョン **が起こります。異なるプロトコルやポートはクロスリージョンのアクセスを引き起こします。この時に、前者のデータ取得が成功するように、Response Headerの中にクロスリージョンに関する構成を追加しなければなりません。

#### Access-Control-Allow-Origin
- 機能の説明
Access-Control-Allow-Originはリソースのクロスリージョンの権限問題を解決することに使われています。ドメイン値は当該リソースにアクセスできるドメインを定義しています。最大10個のドメインまで構成できます。ソースリクエストHostがドメイン名構成リストにある場合、返しヘッダーに対応する値を直接に入力します。ワイルドカード「*」も構成可能であり、すべてのドメインにリクエストされることが許可されます。
- 操作手順
   1. CDN コンソールにログインし、【ドメイン名管理】ページに入り、設定するドメイン名を選択し、【管理】をクリックします。
   2.【アドバンスト構成】の中で【HTTP Header構成】モジュールを見つけ、【HTTP header追加】をクリックすることで、ヘッダーを追加できます。

>! 最大10個のドメイン名までが構成可能です。1個のドメイン名は1行であり、各ドメイン名はエンターキーで区切られます。

- マッチングモードの説明

| **マッチングモード**   | **ドメイン値**   | **説明**    |
| -------------- | --------------------------- | ------------------------------------ |
| オールマッチング         | *                                                            |*に設定した時に、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加し、且つ値が```*```です。 |
| 固定マッチング       | ```http://www.test.com```<br/>```https://www.test.com```<br/>```http://www.b.com``` | <li>ソースが ```https://www.test.com```であり，リストで命中されている場合は、返されたresponse-headerの中でヘッダー：Access-Control-Allow-Originsを追加し、且つ値が```https://www.test.com```です。</li><li>ソースが ```https://www.b.com```であり、リストで命中されていない場合は、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加する必要がありません。</li> |
| 二級汎用ドメイン名のマッチング | ```http://*.test.com```                                      | <li>ソースが ```http://www.test.com```であり、マッチングしている場合は、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加し、且つ値が```http://www.test.com```です。</li><li>ソースが ```https://www.test.com```であり、マッチングしていない場合は、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加する必要がありません。</li> |
| ポートマッチング       | ```https://www.test.com:8080```                              | <li>ソースが```https://www.test.com:8080```であり、マッチングしている場合は、返されたresponse-headerの中にヘッダーAccess-Control-Allow-Originsを追加し、且つ値が```https://www.test.com:8080```です。</li><li>ソースが```https://www.test.com```であり、マッチングしていない場合は、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加する必要がありません。</li> |

>! 特殊なポートがある場合は、リストに関連情報を記入する必要があります。任意ポートのマッチングを対応しないため、指定しなければなりません。

#### Access-Control-Allow-Methods 
Access-Control-Allow-Methods はクロスリージョンで許可されているHTTPリクエスト方法の設定に使われます。複数の方法を同時に設定することが可能です。下記の通りです。
Access-Control-Allow-Methods: `POST, GET, OPTIONS`

#### Access-Control-Max-Age
Access-Control-Max-Ageはプリリクエストの有効時間を指定することに使われます。
非簡単なクロスリージョンリクエストの場合は、正式に通信する前に、HTTPクエリーリクエストを一回追加する必要があります。それは「プリリクエスト」と言われ、当該クロスリージョンリクエストが安全に受け入れられるかどうかを確認することに使われます。下記リクエストは非簡単なクロスリージョンリクエストと見なされます。
+  GET、HEAD 又はPOST 以外の方式で提出する場合、或いはPOSTを利用するが、リクエストするデータタイプがapplication/x-www-form-urlencoded、 multipart/form-data、text/plain 以外のデータタイプ（例えばapplication/xml又はtext/xml）です。
+ カスタマイズしたリクエストヘッダーを使う場合。

Access-Control-Max-Ageの単位が秒です。設定例は下記の通りです。
Access-Control-Max-Age:` 1728000`

1728000 秒（20 日）以内に、当該リソースのクロスリージョンアクセスに対し再度プリリクエストを送らないことを示しています。

#### Access-Control-Expose-Headers
Access-Control-Expose-Headersはどれらのヘッダーがレスポンスの一部としてクライアントに暴露していいかを指定することに使われます。デフォルトでは、6種類のヘッダーのみがクライアントに暴露することができます。
- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

クライアントにほかのヘッダー情報をアクセスさせたい場合は、下記設定をしてよいです。複数のヘッダーを入力する時に、「、」で区切ります。
> Access-Control-Expose-Headers: Content-Length,X-My-Header

クライアントが Content-LengthとX-My-Headerの情報にアクセスできることを示しています。

### カスタマイズされたヘッダー

カスタマイズされたヘッダーの追加を対応します。key-valueのカスタマイズ設定は下記の通りです。

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

複数のヘッダーを重複に追加する時に、下のほうの優先度は上よりも高いため、一番下にある構成で上書きします。

