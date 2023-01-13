## 概要
オブジェクトのHTTPヘッダー(メタデータヘッダー)は、HTTPプロトコルでHTML資料をブラウザに渡す前にサーバーによって送信する文字列です。HTTPヘッダー(メタデータヘッダー)を変更することで、ページのレスポンス形式を変更したり、キャッシュ時間の変更などの設定情報を伝達したりすることもできます。オブジェクトのHTTPヘッダーを変更しても、オブジェクト自体は変更されません。

例：HeaderのContent-Encodingをgzipに変更しても、ファイル自体が事前にgzで圧縮されていない場合は、デコードエラーが発生します。

>? CASタイプのオブジェクトは、Headersのカスタマイズをサポートしていません。
>

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリストページに進みます。
3. オブジェクトがあるバケットを見つけ、そのバケット名をクリックし、バケット管理ページに進みます。
4. 左側ナビゲーションバーで**ファイルリスト**を選択し、ファイルリストページに進みます。
5. カスタムヘッダーが必要なオブジェクトを見つけ、右側の操作バーで、**その他の操作>カスタムヘッダー**をクリックして設定します。複数のオブジェクトのカスタムヘッダーが必要な場合は、複数のオブジェクトにチェックを入れ、上の**その他の操作>カスタムヘッダー**をクリックして設定できます。
6. ポップアップしたウィンドウで、設定するメタデータヘッダーパラメータタイプを選択し、対応するメタデータ値を入力し、**OK**をクリックします。
COSは、次の6種類のオブジェクトHTTPヘッダー識別子の設定を提供しています。ヘッダーの設定に関する説明は、次のとおりです。
<table>
   <tr>
      <th>HTTPヘッダー</th>
      <th>説明</th>
      <th>事例</th>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>ファイルのMIME情報</td>
      <td>image/jpeg</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>ファイルのキャッシュメカニズム</td>
      <td>no-cache;max-age=200</td>
   </tr>
   <tr>
      <td>Content-Disposition</td>
      <td>MIMEプロトコルの拡張</td>
      <td>attachment;filename="fname.ext"</td>
   </tr>
   <tr>
      <td>Content-Encoding</td>
      <td>ファイルのエンコード形式</td>
      <td>gzip</td>
   </tr>
   <tr>
      <td>Expires</td>
      <td>キャッシュの失効日を制御するために使用します</td>
      <td>Wed, 21 Oct 2015 07:28:00 GMT</td>
   </tr>
   <tr>
      <td>x-cos-meta-[拡張子のカスタマイズ]</td>
      <td>ユーザーカスタマイズコンテンツ</td>
      <td>x-cos-meta-via: homepage</td>
   </tr>
</table>


## 事例

APPIDが1250000000で、名前がexamplebucket-1250000000のバケットを作成します。バケットのルートディレクトリに、オブジェクトexampleobject.txtをアップロードしています。

オブジェクトのHTTPヘッダーがカスタマイズされていない場合、ブラウザまたはクライアントによって、ダウンロード時に取得されるオブジェクトヘッダーの例は次のとおりになります。

#### リクエスト

```plaintext
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:16 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511316;1586518516&q-key-time=1586511316;1586518516&q-header-list=date;host&q-url-param-list=&q-signature=1bd1898e241fb978df336dc68aaef4c0acae****
Connection: close
```

#### レスポンス

```plaintext
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Disposition: attachment; filename*="UTF-8''exampleobject.txt"
Access-Control-Allow-Origin: *
Last-Modified: Fri, 10 Apr 2020 09:35:05 GMT 
```

次の設定を追加します。

リクエストが再度開始されると、ブラウザまたはクライアントによって取得されるオブジェクトヘッダーの例は、次のとおりになります。

#### リクエスト

```plaintext
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:16 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511316;1586518516&q-key-time=1586511316;1586518516&q-header-list=date;host&q-url-param-list=&q-signature=1bd1898e241fb978df336dc68aaef4c0acae****
Connection: close
```

#### レスポンス

```plaintext
HTTP/1.1 200 OK
Cache-Control: no-cache
Content-Type: image/jpeg
Content-Disposition: attachment; filename*="abc.txt"
x-cos-meta-md5: 1234
Access-Control-Allow-Origin: *
Last-Modified: Fri, 10 Apr 2020 09:35:05 GMT 
```

