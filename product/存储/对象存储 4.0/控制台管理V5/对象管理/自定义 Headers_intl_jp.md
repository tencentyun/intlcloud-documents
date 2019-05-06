## 概要
オブジェクトのHTTPヘッダー（Header）は、サーバーがHTTPプロトコルでHTML資料をブラウザに送信する前に送信する文字列です。HTTPヘッダー（Header）を変更することによって、ページの応答形式を変更し、またはキャッシュ時間の変更などの構成情報を送信することができます。オブジェクトのHTTPヘッダーを変更しても、オブジェクト自体は変更されません。
例えば、Header内のContent-Encodingをgzipに変更したが、ファイル自体が事前にgzで圧縮されていないと、デコードエラーが発生します。

## 操作手順
1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、左側のメニューバー【バケットリスト】を選択し、バケットリストページに入ります。オブジェクトが位置するバケットをクリックし、バケットに入ります。
  ![アクセス権限1](https://main.qcloudimg.com/raw/b90ad17947a0ec530db87210f4b9027d.png)
2. ヘッダーを設定する必要があるオブジェクトを見つけて、オブジェクトの右側の【詳細】をクリックします。
  ![HTTPヘッダーの設定1](https://main.qcloudimg.com/raw/4282ea6ea80d720a6f76604f1c2bf62f.png)
3. ファイルリストの下方で【カスタマイズHeader】を見つけて、【Headerの追加】をクリックし、設定する必要があるパラメータタイプを選択し（カスタマイズコンテンツにはカスタマイズ名称を入力する必要があります）、対応する値を入力します。COSは、以下の6つのオブジェクトHTTPヘッダータグを構成のために提供します。ヘッダーの構成についての説明は以下のとおりです。構成が完了した後、【保存】をクリックします。

|        HTTPヘッダー        |          説明          |              例               |
| :---------------------: | :--------------------: | :-----------------------------: |
|      Content-Type       |    ファイルのMIME情報    |           image/jpeg            |
|      Cache-Control      |     ファイルのキャッシュメカニズム     |      no-cache;max-age=200       |
|   Content-Disposition   |    MIMEプロトコルの拡張     | attachment;filename="fname.ext" |
|    Content-Encoding     |     ファイルのコーディングフォーマット     |              UTF-8              |
|         Expires         | キャッシュの有効期限を制御するために使用されます |  Wed、 21 Oct 2015 07:28:00 GMT  |
| x-cos-meta-［カスタマイズコンテンツ］ |       カスタマイズコンテンツ       |           カスタマイズコンテンツ            |

![](https://main.qcloudimg.com/raw/ce52b4ffee10a75eb12b1e780f678768.png)


## 例

APPIDが1250000000で、名称がexamplebucket-1250000000のバケットを作成します。バケットのルートディレクトリにオブジェクトexampleobject.txtをアップロードします。

オブジェクトのHTTPヘッダーがカスタマイズされていない場合、ブラウザまたはクライアントがダウンロードする時に取得したオブジェクトヘッダーの例は以下のとおりです：
#### リクエスト
```http
GET /exampleobject.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

#### 応答
```http
HTTP/1.1 200 OK
Content-Language:zh-CN
Content-Type: text/plain
Content-Disposition: attachment; filename*="UTF-8''exampleobject.txt"
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT
```

以下の構成を追加します：
![HTTPヘッダーの設定3](//mc.qcloudimg.com/static/img/bcba7754ca585143371935a9f4f0228a/image.png)
再度リクエストを送信すると、ブラウザまたはクライアントが取得したオブジェクトヘッダーの例は以下のとおりです：
#### リクエスト
```http
GET /exampleobject.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

#### 応答
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
