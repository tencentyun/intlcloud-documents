## 概要
オブジェクトのHTTPヘッダー(メタデータヘッダー)は、HTTPプロトコルでHTML資料をブラウザに渡す前にサーバーによって送信する文字列です。HTTPヘッダー(メタデータヘッダー)を変更することで、ページのレスポンス形式を変更したり、キャッシュ時間の変更などの設定情報を伝達したりすることもできます。オブジェクトのHTTPヘッダーを変更しても、オブジェクト自体は変更されません。

例：HeaderのContent-Encodingをgzipに変更しても、ファイル自体が事前にgzで圧縮されていない場合は、デコードエラーが発生します。

>? CASタイプのオブジェクトは、Headersのカスタマイズをサポートしていません。
>

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで【バケットリスト】をクリックし、バケットリストページに進みます。
3. オブジェクトがあるバケットを見つけ、そのバケット名をクリックし、バケット管理ページに進みます。
4. 左側ナビゲーションバーで【ファイルリスト】を選択し、ファイルリストページに進みます。
5. ヘッダーをカスタマイズしたい単一のオブジェクトを見つけて、右側のアクションバーの【その他の操作】>【カスタムヘッダー】をクリックします。

複数のオブジェクトに対してヘッダーをカスタマイズしたい場合は、複数のオブジェクトにチェックを入れ、上部にある【その他の操作】>【カスタムヘッダー】をクリックします。
![](https://main.qcloudimg.com/raw/88779600818f3670df2f7df62fd1b3a0.png)
6. ポップアップしたウィンドウで、設定するメタデータヘッダーパラメータタイプを選択し、対応するメタデータ値を入力し、【OK】をクリックします。
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
      <td>ファイルコーデック形式 </td>
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
```sh
GET /exampleobject.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

#### レスポンス
```http
HTTP/1.1 200 OK
Content-Language:zh-CN
Content-Type: text/plain
Content-Disposition: attachment; filename*="UTF-8''exampleobject.txt"
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT 
```

次の設定を追加します。

リクエストが再度開始されると、ブラウザまたはクライアントによって取得されるオブジェクトヘッダーの例は、次のとおりになります。

#### リクエスト
```sh
GET /exampleobject.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

#### レスポンス
```http
HTTP/1.1 200 OK
Content-Language:zh-CN
Cache-Control: no-cache
Content-Type: image/jpeg
Content-Disposition: attachment; filename*="abc.txt"
x-cos-meta-md5: 1234
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT
```

