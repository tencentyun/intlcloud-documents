## 概要
オブジェクトのHTTPヘッダー(Header)は、HTTPプロトコルでHTML資料をブラウザに送信する前にサーバーによって送信する文字列です。HTTPヘッダー(Header)を変更することで、ページのレスポンス形式を変更したり、キャッシュタイムの変更といった設定情報を伝達したりすることもできます。オブジェクトのHTTPヘッダーを変更しても、オブジェクト自体は変更されません。

例：HeaderのContent-Encodingをgzipに変更しても、ファイル自体が事前にgzで圧縮されていない場合は、デコードエラーが発生します。

>?CASタイプのオブジェクトは、Headersのカスタマイズをサポートしていません。

## 操作手順
1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、左側メニューバーの【バケットリスト】を選択して、バケットリストページに進みます。オブジェクトがあるバケットをクリックし、バケットに進みます。
2. バケットの「ファイルリスト」モジュールで、カスタムヘッダーが必要な単一オブジェクトを見つけ、右側の操作バーで、右側の【その他の操作】>【カスタムヘッダー】をクリックして設定します。複数のオブジェクトのカスタムヘッダーが必要な場合は、複数のオブジェクトにチェックを入れ、【その他の操作】メニューのスライダーをプルダウンして、【カスタムヘッダー】を選択すれば完了です。
![](https://main.qcloudimg.com/raw/88779600818f3670df2f7df62fd1b3a0.png)
3. **Headersのカスタマイズ**ポップアップウィンドウで、【Headerの追加】をクリックし、設定したいパラメータのタイプを選択し、対応する値を入力します。COSは、設定用に以下6つのオブジェクトHTTPヘッダー識別子を提供しています。ヘッダーの設定についての説明は次のとおりです。設定が完了した後、【保存】をクリックすればOKです。
![](https://main.qcloudimg.com/raw/191fbd1b903069b5e546bb237b050ee2.png)
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
      <td>UTF-8</td>
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
![](https://main.qcloudimg.com/raw/2474d24e7d1d365e0c736572aae8f652.png)
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

