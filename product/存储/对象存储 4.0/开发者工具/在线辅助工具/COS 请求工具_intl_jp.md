## 機能概要

COSリクエストツールは、Tencent Cloud COSが提供するWeb側デバッグツールで、クラウドAPI 3.0 Explorerプラットフォームに組込まれ、APIのデバッグに使用できます。

>! COSリクエストツールから送信されるリクエストは、確実にCOSの業務サーバに送信します。**すべての操作は、実操作に相当します。DELETE類操作を選択するときに、慎重に操作してください。**

現時点でCOSリクエストツールはXML APIバージョンをサポートしますが、JSON APIバージョンをサポートしません。
- JSON APIは、Tencent Cloud COSサービスがXML APIをリリースする前に、ユーザーに提供するCOSにアクセスするためのAPIです。APIと標準XMLのAPI最下層アーキテクチャが同じ、データの相互運用性があり、交互に使うことができますが、API互換性がありません。
- XML APIは、さらに豊富な機能と特性があります。Tencent Cloud COSは、XML APIにバージョンアップすることを強くお勧めします。

## 使用方法

[COSリクエストツール](https://console.cloud.tencent.com/api/explorer?Product=cos)ページをクリックし、「COS」製品を選択し、必要なAPIを選択します。このAPIの対応パラメータを入力し、リクエスト送信をクリックした後に対応するリクエストの応答結果を取得します。

下図のように、COSリクエストツールの全体ページは、左から右の順に製品欄、API欄、パラメータ欄、結果欄があります。それぞれの欄で対応操作を実行できます。最後に結果欄でリクエストを送信し、応答結果と関連するプロセスパラメータ情報を取得します。
![](https://main.qcloudimg.com/raw/6329b432ed56516ca311bcbe5720d13f.png)

COSリクエストツールの詳細操作については、以下の手順を参照してください。

**1. COS製品を選択する**

最左側の製品欄で【COS】をクリックすると、API欄のCOSに関するAPIが表示されます。

>?COSリクエストツールは、クラウドAPI 3.0プラットフォームに組込まれ、このプラットフォームには、その他のTencent Cloud製品のAPIデバッグツールが搭載されます。ニーズに応じてこのプラットフォームでその他の製品を選択し、対応するAPIをデバッグできます。

**2. デバッグするAPIを選択する**

ニーズに応じて対応するAPIを選択し、デバッグを行うことができます。API欄にCOSに関する3つの主なAPI（Service API、Bucket API、Object API）が表示されます。

- Service類API（例えばGET Service）では、このAPIは、アカウントのすべてのバケット情報をリストできます。あなたのAPI暗号鍵情報を入力する必要があります。アカウントの指定地域内のバケット情報を取得するとき、パラメータ欄に対応地域を選択できます。このAPIの詳細情報については、[GET Service](https://cloud.tencent.com/document/product/436/8291)ドキュメントを参照してください。
- Bucket類APIにはバケットを操作するAPI（例えば、PUT Bucket lifecycle）が含まれます。Bucket類APIの詳細については、[Bucket API](https://cloud.tencent.com/document/product/436/7731)を参照してください。
- Object類APIには、オブジェクトを操作するAPI（例えばPUT Object）が含まれます。Object類APIの詳細については、[Object API](https://cloud.tencent.com/document/product/436/7739)を参照してください。

**3. APIに必要なパラメータ情報を入力する**

パラメータ欄は、選択したAPIの必須パラメータを表示します。COSの各APIのパラメータ情報については、[APIドキュメント](https://cloud.tencent.com/document/product/436/10009)を参照してください。

API暗号鍵情報は、APIを呼び出すときに必須入力するパラメータです。APIでバケットまたはオブジェクトなどのリソースを操作するとき、API暗号鍵情報を入力し、今回のAPIリクエスト操作を許可します。CAMコンソールの[API暗号鍵管理](https://console.cloud.tencent.com/cam/capi)ページでAPI暗号鍵情報を取得できます。

>?各APIに対し、COSリクエストツールは、それぞれの必須パラメータ項目の後に赤いアスタリスクタグを追加し、このパラメータ項目は必須入力項目であることを示します。**必須パラメータのみ表示**をチェックし、パラメータ欄の非必須パラメータの表示を削減できます。

**4. リクエストの送信と応答結果の表示**

APIを選択し、適切なパラメータを入力した後、【オンライン呼び出し】タブで【リクエスト送信】ボタンをクリックします。この場合、システムがリクエストをサーバに送信します。リクエストによりバケットまたはオブジェクトリソースを操作します。

>!COSリクエストツールから送信されるリクエストは、確実にCOSの業務サーバに送信します。**すべての操作は、実作に相当します。DELETE類操作を選択するときに、慎重に操作してください。**

リクエストを送信した後、返された結果とリクエストパラメータは、結果欄の下方に表示されます。結果欄の下方の【リクエストパラメータ】でHTTPリクエストボディ情報を確認し、【応答結果】で今回リクエストの応答ボディ情報を確認し、【署名プロセス】で今回リクエストに関わる署名とその生成プロセスを確認することができます。また、システムは【Curl】でCurlの呼び出すステートメントを提供します。

**例**

GET Objectを例として、0001.txtのファイルを取得するためリクエストを送信するとき、【リクエストパラメータ】で今回リクエストするリクエストパラメータ情報が表示されます。今回リクエストするリクエスト例は以下のとおりです。

```
GET https://bucketname-appid.cos.ap-region.myqcloud.com/0001.txt
Host: bucketname-appid.cos.ap-region.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDwqaGoCIWIG4hDWdJUTL5e3hn04xiD5kI&q-sign-time=1543398166;1543405366&q-key-time=1543398166;1543405366&q-header-list=host&q-url-param-list=&q-signature=f50ddd3e0b54a92df9d4efe2d0c3734a8c9007ec
```

最初の行に表示されるのは、HTTP Verbとアクセス対象リンクで、次の行に表示されるのは、アクセス対象ドメイン名で、最後の1行に表示されるのは、今回リクエストする署名情報です。PUT類のリクエストについては、そのリクエストヘッダー情報が複雑であるが、共通リクエストヘッダーが存在します。共通リクエストヘッダーの情報については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)を参照してください。

【署名プロセス】で今回リクエストに関わる署名とその生成プロセスを確認できます。署名アルゴリズムの詳細については、ドキュメント[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)をご覧下さい。リクエスト署名を生成、デバッグする必要がある場合、[COS署名ツール](https://cos5.cloud.tencent.com/static/cos-sign/)を使用することをおすすめします。

COSから返される応答結果は以下のとおりです。

```
200 OK
content-type: text/plain
content-length: 6
connection: close
accept-ranges: bytes
date: Wed, 28 Nov 2018 09:42:49 GMT
etag: "5a8dd3ad0756a93ded72b823b19dd877"
last-modified: Tue, 27 Nov 2018 20:05:26 GMT
server: tencent-cos
x-cos-request-id: NWJmZTYzMTlfOWUxYzBiMDlfOTA4NF8yMWI2YjE=
x-cos-version-id: MTg0NDY3NDI1MzAzODkyMjUzNjM
hello!
```

最初の行`200 OK`は、このリクエストから返されたステータスコード情報を示します。リクエストに失敗した場合、対応するエラーコードを返します。エラーコードの詳細情報については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。次は応答ヘッダー情報です。応答ボディはAPIによって異なりますが、共通応答ヘッダー情報が存在します。共通応答ヘッダーの詳細情報については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)を参照してください。



## 注意事項
【リクエスト送信】ボタンをクリックし、必須パラメータを入力し、リクエストをCOSサーバーに確実に送信したとき、COSはバケットとオブジェクトに対し適切な操作を行います。この操作はキャンセル、ロールバックができませんので、よくご確認のうえしてください。
