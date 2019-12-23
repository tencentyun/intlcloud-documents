## 機能説明
POST Object restore APIは、COSによってarchiveタイプにアーカイブされたオブジェクトに対して回復することができます。回復された読み取り可能なオブジェクトは一時的なものであり、読み取り可能にする時間およびこの一時コピーを削除する時間を設定することができます。Daysパラメータを使用して一時オブジェクトの期限切れ時間を指定することができます。この時間を超えてもコピーや拡張などの操作をしなければ、この一時オブジェクトはシステムによって自動的に削除されます。一時オブジェクトはarchiveタイプオブジェクトのコピーにすぎず、アーカイブされたソースオブジェクトはこの期間中常に存在します。

## リクエスト
### リクエスト例

```shell
POST /<ObjectKey>?restore HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
 
> Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。


### リクエストヘッダー
#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。
#### 非共通のヘッダー
このリクエスト操作には、特別なリクエストヘッダー情報はありません。

### リクエストボディ
このリクエスト操作の実現では、以下のリクエストボディが必要です。

```shell
<RestoreRequest>
   <Days>2</Days>
   <CASJobParameters>
       <Tier>Bulk</Tier>
   </CASJobParameters>
</RestoreRequest>
```

具体的なデータ説明は以下のとおりです：
<table>
   <tr>
      <th nowrap="nowrap">ノード名称（キーワード）</th>
      <th>ノード名称</th>
      <th>説明</th>
      <th>タイプ</th>
      <th>必須項目</th>
   </tr>
   <tr>
      <td>RestoreRequest</td>
      <td>なし</td>
      <td>データを復元する用のコンテナ</td>
      <td>Container</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>Days</td>
      <td>なし</td>
      <td>一時コピーの期限切れ時間を設定します</td>
      <td>integer</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>CASJobParameters</td>
      <td>なし</td>
      <td>CAS作業パラメータをアーカイブするコンテナ</td>
      <td>Container</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>Tier</td>
      <td>なし</td>
      <td>データを復元するとき、TierはCASでサポートされている3つの回復モードに指定されることができます。それらは、Standard（標準モード、回復タスクは35時間以内に完了）、Expedited（快速モード、回復タスクは15分以内に完了）、およびBulk（一括モード、回復タスクは5-12時間以内に完了します）</td>
      <td>Enum</td>
      <td>はい</td>
   </tr>
</table>



## 応答
### 応答ヘッダー

#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。

### 応答ボディ
この応答ボディはブランクです。

###　エラーコード
このリクエスト操作は、以下のエラーメッセージが発生する可能性があります。一般的なエラー情報については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

エラーコード|説明|HTTPステータスコード
---|---|---
None|回復成功|202 [Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)
RestoreAlreadyInProgress|オブジェクトはすでに回復中|409 [Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)


## 実際のケース

### リクエスト

```shell
POST /exampleobject?restore HTTP/1.1
Accept: */*
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 105
Content-Type: application/x-www-form-urlencoded

<RestoreRequest>
   <Days>2</Days>
   <CASJobParameters>
       <Tier>Bulk</Tier>
   </CASJobParameters>
</RestoreRequest>
```

### 応答

```shell
HTTP/1.1 202 Accepted
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-cos
x-cos-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=
```



