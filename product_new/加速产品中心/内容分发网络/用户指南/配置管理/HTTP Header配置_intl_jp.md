Tencent Cloudが提供するHTTP Header設定機能を利用することにより、ユーザーがサービスリソースをリクエストする時に、返信される**応答メッセージ**の中に設定されたヘッダーを追加し、クロスオリジンのアクセスなどを実現することができます。
リソースがノードに命中されていない時には、back to originを行います。この時に、オリジンサーバーにより返されたヘッダー情報も一緒にユーザーに送信されます。リソースがノードのキャッシュに命中された時に、静的コンテンツ加速及びダウンロード加速ケースの場合には、CDNサービスはデフォルトでキャッシュされたオリジンサーバーの Access-Control-Allow-Origin、Timing-Allow-Origin、Content-Disposition、Accept-Rangesのヘッダー情報をユーザーに送信します。
HTTP headerの設定はドメイン名を対象にするため、設定が有効になると、当該ドメイン名における任意リソースに対するユーザーの応答情報には、設定されたヘッダーが追加されます。HTTP headerの設定はクライアント（例えばブラウザー）の応答動作しか影響せず、CDNノードのキャッシュ行為を影響しません。

##設定ガイド
1.  [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のメニュー欄の【Domain Management】を選択し、編集しようとするドメイン名の左側の【 Manage】をクリックします。
2.【Advanced Configuration】の中で【HTTP header Configuration】モジュールを見つけ、セルフでヘッダーを追加できます。
3.【Add HTTP header】をクリックすることで、ヘッダーを追加できます。

CDNサービスは下記の6種類の常用ヘッダー設定をサポートしており、カスタマイズのヘッダー設定をも対応しています。
+ Content-Disposition：クライアントをアクティブにしてリソースをダウンロードし、デフォルトのファイル名を設定します。
+ Content-Language：ページで使用される言語コードを定義するために使用されます。
+ Access-Control-Allow-Origin：クロスオリジンリクエストを指定する時に、リソースへのアクセスを認めるリクエストオリジンです。
+ Access-Control-Allow-Methods：クロスオリジンリクエストを指定する時に、許可されるクロスオリジンのリクエスト方法です。
+ Access-Control-Max-Age：クロスオリジンリクエストを指定する時に、特定リソースのプリリクエストに対し結果を返すのキャッシュ時間です。
+ Access-Control-Expose-Headers：クロスオリジンリクエストを指定する時に、クライアントに表示可能なヘッダーグループです。
+ カスタマイズ：ヘッダーをカスタマイズすることです。

### 汎用設定
#### Content-Disposition
Content-Dispositionはブラウザーのダウンロードをアクティブにすることに使われます。また、デフォルトでダウンロードするファイル名を設定することもできます。サービス側よりクライアントのブラウザーにファイルを発送する時に、TXT、JPG等ブラウザーでサポートされているファイルタイプである場合は、デフォルトでブラウザーによって直接開かれます。ユーザーに保存することを注意する必要がある場合は、Content-Dispositionフィールドを設定することにより、ブラウザーのデフォルトの動作を上書きすることができます。常用の設定は下記の通りです。`Content-Disposition：attachment;filename=FileName.txt`

#### Content-Language
Content-Languageはページで使用される言語コードを定義するために使用されます、常用の設定は下記の通りです。
`Content-Language: zh-CN`
`Content-Language: en-US`

###クロスオリジン設定
クロスオリジンは、あるドメイン名（例えば ```www.abc.com``` ）におけるあるリソースから、別のドメイン名（例えば```www.def.com```）におけるあるリソースへリクエストを提出する時に、リソースの所属するドメイン名が異なるために、 **クロスオリジン **が起こります。異なるプロトコルやポートはクロスオリジンのアクセスを引き起こします。この時に、前者がデータを正常に取得できるように、Response Headerの中にクロスオリジンに関する設定を追加しなければなりません。

#### Access-Control-Allow-Origin
- 機能の説明
Access-Control-Allow-Originはリソースのクロスオリジンの権限問題を解決するために使われています。ドメイン値は当該リソースにアクセスできるドメインを定義しています。最大10個のドメイン名設定をサポートします。ソースリクエストHostがドメイン名設定リストにある場合、戻りヘッダーに対応する値を直接に入力します。ワイルドカード「*」も設定可能であり、すべてのドメインにリクエストされることが許可されます。

>! 最大10個のドメイン名設定をサポートします。1個のドメイン名は1行であり、各ドメイン名はエンターキーで区切られます。

- マッチングモードの説明

| **マッチングモード**   | **ドメイン値**   | **説明**    |
| -------------- | --------------------------- | ------------------------------------ |
| オールマッチング         | *                                                            |*に設定した時に、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加し、且つ値が*です。 |
| 固定マッチング       | ```http://www.test.com```<br/>```https://www.test.com```<br/>```http://www.b.com``` | <li>ソースが ```https://www.test.com```であり、リストで命中されている場合は、返されたresponse-headerの中でヘッダー：Access-Control-Allow-Originsを追加し、且つ値が```https://www.test.com```です。</li><li>ソースが ```https://www.b.com```であり、リストで命中されていない場合は、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加する必要がありません。</li> |
| 二級汎用ドメイン名のマッチング | ```http://*.test.com```                                      | <li>ソースが ```http://www.test.com```であり、マッチングしている場合は、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加し、且つ値が```http://www.test.com```です。</li><li>ソースが ```https://www.test.com```であり、マッチングしていない場合は、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加する必要がありません。</li> |
| ポートマッチング       | ```https://www.test.com:8080```                              | <li>ソースが```https://www.test.com:8080```であり、マッチングしている場合は、返されたresponse-headerの中にヘッダーAccess-Control-Allow-Originsを追加し、且つ値が```https://www.test.com:8080```です。</li><li>ソースが```https://www.test.com```であり、マッチングしていない場合は、返されたresponse-headerの中にヘッダー：Access-Control-Allow-Originsを追加する必要がありません。</li> |

> 特殊なポートがある場合は、リストに関連情報を記入する必要があります。任意ポートのマッチングをポートされていないため、指定しなければなりません。

#### Access-Control-Allow-Methods 
Access-Control-Allow-Methods はクロスオリジンで許可されているHTTPリクエスト方法の設定に使われます。複数の方法を同時に設定することが可能です。下記の通りです。
Access-Control-Allow-Methods: `POST, GET, OPTIONS`

#### Access-Control-Max-Age
Access-Control-Max-Ageはプリリクエストの有効時間を指定することに使われます。
非簡単なクロスオリジンリクエストの場合は、正式に通信する前に、HTTPクエリーリクエストを一回追加する必要があります。それは「プリリクエスト」と言われ、当該クロスオリジンリクエストが安全に受け入れられるかどうかを確認することに使われます。下記リクエストは非簡単なクロスオリジンリクエストと見なされます。
+  GET、HEAD 又はPOST 以外の方式で提出する場合、或いはPOSTを利用するが、リクエストするデータタイプがapplication/x-www-form-urlencoded、 multipart/form-data、text/plain 以外のデータタイプ（例えばapplication/xml又はtext/xml）です。
+ カスタマイズしたリクエストヘッダーを使う場合。

Access-Control-Max-Ageの単位が秒です。設定例は下記の通りです。
Access-Control-Max-Age:` 1728000`

1728000 秒（20 日）以内に、当該リソースのクロスオリジンアクセスに対し再度プリリクエストを送らないことを示しています。

#### Access-Control-Expose-Headers
Access-Control-Expose-Headersは応答の一部としてクライアントに公開できるヘッダーを指定するために使用されます。デフォルトでは、6種類のヘッダーのみがクライアントに公開することができます。
- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

クライアントにほかのヘッダー情報をアクセスさせたい場合は、次の設定を行うことができます。複数のヘッダーを入力する時に、「、」で区切ります。
> Access-Control-Expose-Headers: Content-Length,X-My-Header

クライアントが Content-LengthとX-My-Headerの情報にアクセスできることを示しています。

### カスタマイズされたヘッダー

カスタマイズされたヘッダーの追加を対応します。ユーザーはパラメーターリストで[カスタム]を選択できます。
カスタムKey-Value値を入力します。

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

複数のヘッダーを重複に追加する時に、最下位の優先順位は最上位の優先順位よりも高く、最下位の設定によって直接カバーされます。

