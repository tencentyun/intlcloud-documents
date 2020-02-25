
Tencent Cloudが提供するHTTP Header設定機能を利用することにより、ユーザーがサービスリソースをリクエストする時に、返信される**レスボンス**のヘッダーに設定した情報を追加し、クロスオリジンのアクセスなどを実現することができます。
リソースがノードに命中されなかった場合に、back to originを行います。この場合、オリジンサーバーにより返された情報にヘッダー情報も一緒にユーザーに送信されます。リソースがノードのキャッシュに命中され、かつ静的コンテンツ加速またはダウンロード加速の場合には、CDNサービスはデフォルトでキャッシュされたオリジンサーバーの Access-Control-Allow-Origin、Timing-Allow-Origin、Content-Disposition、Accept-Rangesのヘッダー情報をユーザーに送信します。
HTTP headerの設定はドメイン名を対象にするため、設定が有効になると、当該ドメインに属する任意のリソースに対するリクエストは、設定されたヘッダー情報がレスボンスのヘッダー部分に追加されます。HTTP headerの設定はクライアント（例えばブラウザー）の応答動作しか影響せず、CDNノードのキャッシュ行為に影響しません。


##設定ガイド
1.  [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のメニュー欄の【Domain Management】を選択し管理画面に入り、表示されるドメインリストの中で編集したいドメインをクリックします。
2.【Advanced Configuration】の中で一番下に【HTTP header Configuration】をスクロールします。HTTP Headerの設定はデフォルトでOFFになっています。
3.【HTTP Header】をクリックし、表示される画面にヘッダー情報の追加を行います。


CDNサービスは下記の6種類の一般的なヘッダー設定をサポートしており、カスタマイズのヘッダー設定も対応しています。
+ Content-Disposition：クライアント側をアクティブにしてリソースのダウンロード及びデフォルトのファイル名の設定を行います。
+ Content-Language：ページで使用される言語コードを定義するために使用されます。
+ Access-Control-Allow-Origin：クロスオリジンリクエストを指定する時に、リソースへのアクセスを認めるリクエストオリジンを設定します。
+ Access-Control-Allow-Methods：クロスオリジンリクエストを指定する時に、許可されるクロスオリジンのリクエスト方法を設定します。
+ Access-Control-Max-Age：クロスオリジンリクエストを指定する時に、特定リソースのプリリクエストに対するレスボンスのキャッシュ時間を設定します。
+ Access-Control-Expose-Headers：クロスオリジンリクエストを指定する時に、クライアント側で確認できるヘッダーグループを設定します。
+ カスタマイズ：上記以外にヘッダーに対する設定です。


### 汎用設定
#### Content-Disposition
Content-Dispositionはブラウザーのダウンロードをアクティブにすることに使われます。また、デフォルトでダウンロードする際のファイル名を設定することもできます。サーバー側からクライアント側のブラウザーにファイルを送信する際に、TXT、JPG等のブラウザーでサポートされているファイルフォーマットの場合は、デフォルトでブラウザーで開かれます。ユーザーに保存することを提示する必要がある場合は、Content-Dispositionフィールドを設定することにより、ブラウザーのデフォルトの動作を上書きすることができます。一般的な設定は下記の通りです。`Content-Disposition：attachment;filename=FileName.txt`

#### Content-Language
Content-Languageはページで使用される言語コードを定義するのに使用されます。一般的な設定は下記の通りです。
`Content-Language: zh-CN`
`Content-Language: en-US`









###クロスオリジン設定
クロスオリジンは、あるドメイン名（例えば ```www.abc.com``` ）におけるあるリソースから、別のドメイン名（例えば```www.def.com```）におけるあるリソースへリクエストする時に、リソースの所属するドメインが異なるために、 **クロスオリジンリクエスト **が起こります。異なるプロトコルやポートはクロスオリジンリクエストを引き起こします。この場合に、前者がデータを正常に取得できるように、Response Headerの中にクロスオリジンに関する設定を追加しなければなりません。

#### Access-Control-Allow-Origin
- 機能の説明
  Access-Control-Allow-Originはリソースのクロスオリジンの権限問題を解決するために使われています。ドメイン値は当該リソースにアクセスできるドメインを定義しています。リクエスト元のHostがドメイン名設定リストの中に存在する場合は、レスボンスのヘッダーに要求される値を直接に記載します。ワイルドカード「*」を設定することで、すべてのドメインからのリクエストを許可することができます。

>! 最大10個のドメイン名設定をサポートします。1個のドメイン名は1行づつ記載し、複数ドメイン名間はエンターキーで区切ってください。


- マッチングモードの説明

| **マッチングモード**   | **ドメイン値**   | **説明**    |
| -------------- | --------------------------- | ------------------------------------ |
| オールマッチング         | *                                                            |「*」に設定した時に、返されたresponse-headerの中に：Access-Control-Allow-Originsを追加し、且つ値が「*」にします。|
| 固定マッチング       | ```http://www.test.com```<br/>```https://www.test.com```<br/>```http://www.b.com``` | </li> もしソース元が ```https://www.test.com```であり、リストの中から命中された場合は、返されたresponse-headerの中に：Access-Control-Allow-Originsを追加し、且つ値が```https://www.test.com```にします。</li><li>ソース元が ```https://www.b.com```であり、リストの中から命中されなかった場合は、返されたresponse-headerの中に：Access-Control-Allow-Originsを追加する必要がありません。</li> |
| セカンドレベル汎用ドメイン名のマッチング| ```http://*.test.com```                                      | <li>ソース元が ```http://www.test.com```であり、マッチングされた場合は、返されたresponse-headerの中に：Access-Control-Allow-Originsを追加し、且つ値が```http://www.test.com```にします。</li><li>ソース元が ```https://www.test.com```であり、マッチングされなかった場合は、返されたresponse-headerの中に：Access-Control-Allow-Originsを追加する必要がありません。</li> |
| ポートマッチング       | ```https://www.test.com:8080```                              | <li>ソース元が```https://www.test.com:8080```であり、マッチングされた場合は、返されたresponse-headerの中に：Access-Control-Allow-Originsを追加し、且つ値が```https://www.test.com:8080```にします。</li><li>ソース元が```https://www.test.com```であり、マッチングされなかった場合は、返されたresponse-headerの中に：Access-Control-Allow-Originsを追加する必要がありません。</li> |

> 特殊なポートが存在する場合は、関連情報をリストに記載する必要があります。任意ポートのマッチングをサポートされていないため、指定しなければなりません。

#### Access-Control-Allow-Methods 

Access-Control-Allow-Methods はクロスオリジンを許可するHTTPリクエスト方法の設定に使われます。複数のリクエスト方法を同時に設定することが可能です。設定方法は下記の通りです。
Access-Control-Allow-Methods: `POST, GET, OPTIONS`




#### Access-Control-Max-Age
Access-Control-Max-Ageはプリリクエストの有効時間を指定することに使われます。
Non-Simpleクロスオリジンリクエストの場合は、正式に通信する前に、HTTPクエリーリクエストを一回追加する必要があり、「プリリクエスト」と言います。この方法を用いて当該クロスオリジンリクエストが安全かどうかを確認することに使われます。下記リクエストはNon-Simpleクロスオリジンリクエストと見なされます。
+  GET、HEAD 又はPOST 以外の方式でリクエストを行う場合、或いはPOSTを利用するが、リクエストするデータタイプがapplication/x-www-form-urlencoded、 multipart/form-data、text/plain 以外のデータタイプ（例えばapplication/xml又はtext/xml）です。
+  カスタマイズしたリクエストヘッダーを使う場合。

Access-Control-Max-Ageの単位が秒です。設定例は下記の通りです。
Access-Control-Max-Age:` 1728000`

1728000 秒（20 日）以内に、同一リクエスト元からの当該リソースへのクロスオリジンアクセスは、再度プリリクエストを送らないことを示しています。


#### Access-Control-Expose-Headers

Access-Control-Expose-Headersはどのヘッダー情報はレスボンスの一部としてクライアントに公開できるかを指定するために使用されます。デフォルトでは、6種類のヘッダー情報のみがクライアントに公開することができます。
- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

クライアントにほかのヘッダー情報を公開したい場合は、次の設定を行うことができます。複数のヘッダー情報を記載する際に、「,」で区切ってください。
> Access-Control-Expose-Headers: Content-Length,X-My-Header


クライアントが Content-LengthとX-My-Headerの情報に公開できることを示しています。

### カスタマイズヘッダー

ヘッダーのカスタマイズ追加を対応します。ユーザーはパラメーターリストで[Custom]を選択できます。
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

複数のヘッダーを重複に追加された場合に、最下位は最上位より優先順位が高いため、優先順位の高い設定に従います。

