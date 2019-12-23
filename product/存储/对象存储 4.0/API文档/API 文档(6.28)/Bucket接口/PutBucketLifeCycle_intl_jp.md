## 機能説明
COSを使用すると、ユーザーはライフサイクル構成でバケット内のオブジェクトのライフサイクルを管理できます。ライフサイクル構成には、一連のオブジェクト規則に適用される1つ以上の規則セットが含まれます（各規則はCOSのために一つの操作を定義します）。
これらの操作は、次の2つのタイプに分けられます：
- *変換操作：**オブジェクトが別のストレージクラスに変換する時間を定義します。例えば、オブジェクトが作成されてから30日後に、オブジェクトを低頻度ストレージ（アクセス頻度が低い場合はSTANDARD_IA）タイプに変換することを選択できます。CASへのデータのダウングレードもサポートします（アーカイブ、低コスト、現在国内キャンパスをサポート）。具体的なパラメータについては、リクエスト例の説明にあるTransitionアイテムを参照してください。
- **期限切れ操作：**オブジェクトの期限切れ時間を指定します。COSは自動的にユーザーのために期限切れのオブジェクトを削除します。

### 詳細分析

PUT Bucket lifecycleは、バケットのために新しいライフサイクル構成を作成するように使用されます。もしこのバケットにはライフサイクルが構成されている場合、このAPIを使用して新しい構成を作成すると同時に、元の構成が上書きされます。

## リクエスト
### リクエスト例

```shell
PUT /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Date: GMT Date
Authorization: Auth String 
Content-MD5: MD5
```
>Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）

### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。

#### 非共通のヘッダー

**必須ヘッダー**
このリクエスト操作の実現では、以下の必須ヘッダーを使用します：

| 名称               | 説明      | タイプ     | 必須項目   |
| ---------------- | ----------- | ------ | ---- |
| Content-MD5       | RFC 1864の中で定義された、**Base64**エンコードされた128-bit内容MD5チェック値。このヘッダーは、ファイルの内容が変更されたかどうかを確認するために使用されます。| String | はい    |


### リクエストボディ
このAPIリクエストのリクエストボディの具体的なノード内容は：

```shell
<LifecycleConfiguration>
  <Rule>
    <ID></ID>
    <Filter>
      <Prefix></Prefix>
    </Filter>
    <Status></Status>
    <Transition>
      <Days></Days>
      <StorageClass></StorageClass>
    </Transition>
    <NoncurrentVersionExpiration>
      <NoncurrentDays></NoncurrentDays>
    </NoncurrentVersionExpiration>
  </Rule>
  <Rule>
    <ID></ID>
    <Filter>
      <Prefix></Prefix>
    </Filter>
    <Status></Status>
    <Transition>
      <Days></Days>
      <StorageClass></StorageClass>
    </Transition>
    <NoncurrentVersionTransition>
      <NoncurrentDays></NoncurrentDays>
      <StorageClass></StorageClass>
    </NoncurrentVersionTransition>
  </Rule>
  <Rule>
    <ID></ID>
    <Filter>
      <Prefix></Prefix>
    </Filter>
    <Status></Status>
    <Expiration>
      <ExpiredObjectDeleteMarker></ExpiredObjectDeleteMarker>
    </Expiration>
    <NoncurrentVersionExpiration>
      <NoncurrentDays></NoncurrentDays>
    </NoncurrentVersionExpiration>
  </Rule>
</LifecycleConfiguration>
```

具体的な説明は以下のとおりです：

|ノード名称（キーワード）|    親ノード|    説明    |タイプ|    必須項目|
|---|---|---|---|---|
|LifecycleConfiguration    |無し    |ライフサイクル構成    |Container    |はい|
|Rule|    LifecycleConfiguration    |規則説明    |Container|    はい|
|Filter    |LifecycleConfiguration.Rule    |Filterは、規則の影響を受けるオブジェクトのセットを説明するために使用されます    |Container    |はい|
|Status    |LifecycleConfiguration.Rule    |規則が有効かどうかを示します。列挙値：Enabled、Disabled     |Container    |はい|
|ID    |LifecycleConfiguration.Rule|唯一地を識別する規則のために使用されます。長さは255文字以下です    |String    |いいえ|
|And    |LifecycleConfiguration.Rule.Filter    |プレフィックスを組み合わせるために使用されます    |Container    |いいえ|
|Prefix    |LifecycleConfiguration.Rule.Filter<br>またはLifecycleConfiguration.Rule.Filter.And    |規則に適用されるプレフィックスを指定します。プレフィックスと一致するオブジェクトはこの規則の影響を受けます。プレフィックスは最大1つです   |Container    |いいえ|
|Expiration    |LifecycleConfiguration.Rule    |規則期限切れ属性    |Container    |いいえ|
|Transition    |LifecycleConfiguration.Rule    |規則変換属性、オブジェクトがStandard_IAまたはArchiveに変換される時間  |Container    |いいえ|
|Days    |LifecycleConfiguration.Rule.Transition<br>またはExpiration    |オブジェクトの最終変更日から何日後に、規則に対応するアクションが実行されるかを示します。Transitionの場合、このフィールドの有効値は負ではない整数です；Expirationの場合、このフィールドの有効値は正の整数です。最大3650日間をサポートします   |Integer    |いいえ|
|Date    |LifecycleConfiguration.Rule.Transition<br>またはExpiration    |規則に対応するアクションの実行時間を示します    |String    |いいえ|
|ExpiredObjectDeleteMarker    |LifecycleConfiguration.Rule.Expiration    |期限切れオブジェクト削除タグを削除します。列挙値true、false    |String    |いいえ|
|AbortIncompleteMultipartUpload    |LifecycleConfiguration.Rule    |マルチパートアップロードの実行を継続するための最大許容時間を設定します    |Container    |いいえ|
|DaysAfterInitiation    |LifecycleConfiguration.Rule<br>.AbortIncompleteMultipartUpload    |マルチパートアップロードの開始から何日後に、アップロードを完了する必要があるかを示します    |Integer    |はい|
|NoncurrentVersionExpiration    |LifecycleConfiguration.Rule    |現在のバージョン以外のオブジェクトの有効期限を示す    |Container    |いいえ|
|NoncurrentVersionTransition    |LifecycleConfiguration.Rule    |現在のバージョン以外のオブジェクトをSTANDARD_IAまたはARCHIVEに変換する時間を示します    |Container    |いいえ|
|NoncurrentDays    |LifecycleConfiguration.Rule<br>.NoncurrentVersionExpiration<br>またはNoncurrentVersionTransition    |オブジェクトが非最新バージョンになってから何日後に、規則に対応するアクションを実行するかを示します。Transitionの場合、このフィールドの有効値は負ではない整数です；Expirationの場合、このフィールドの有効値は正の整数です。最大3650日間をサポートします |Integer    |いいえ|
|StorageClass    |LifecycleConfiguration.Rule.Transition<br>またはNoncurrentVersionTransition    |オブジェクトのターゲット保存タイプを指定します。枚举值：STANDARD_IA、ARCHIVE   |String    |はい|


## 応答
### 応答ヘッダー

#### 共通の応答ヘッダー 
この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。

### 応答ボディ
この応答ボディは空を返します。

###　エラーコード
以下は、このリクエストが発生する可能性がある特別で一般的なエラー状況です。具体的なエラー原因について、返したメッセージを参照して問題を解決します。COSエラーコードの情報、または製品のすべてのエラーリストの詳細については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

|エラーコード|HTTPステータスコード|説明|
|--------|--------|----------|
|NoSuchBucket|404 Not Found|アクセスするバケットが存在しません|
|MalformedXML|400 Bad Request| XMLフォーマットが不正です。restful apiドキュメントとよく比較してください|
|InvalidRequest|400 Bad Reques|リクエストは不正です。エラーの説明に「Conflict lifecycle rule」が表示されている場合は、xmlデータ内の複数のルールに競合する部分があることを意味します。|
|InvalidArgument|400 Bad Reques|リクエストパラメータは不正です。エラーの説明に「Rule ID must be unique. Found same ID for more than one rule」が表示されている場合は、複数のルールのIDフィールドが同じであることを表します。|

## 実際のケース

### リクエスト
```shell
PUT /?lifecycle HTTP/1.1
Host:examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 11:59:33 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1502855771;1502935771&q-key-time=1502855771;1502935771&q-header-list=content-md5;host&q-url-param-list=lifecycle&q-signature=f3aa2c708cfd8d4d36d658de56973c9cf1c24654
Content-MD5: LcNUuow8OSZMrEDnvndw1Q==
Content-Length: 348
Content-Type: application/x-www-form-urlencoded

<LifecycleConfiguration>
  <Rule>
    <ID>id1</ID>
    <Filter>
       <Prefix>documents/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Transition>
      <Days>100</Days>
      <StorageClass>ARCHIVE</StorageClass>
    </Transition>
  </Rule>
  <Rule>
    <ID>id2</ID>
    <Filter>
       <Prefix>logs/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Expiration>
      <Days>10</Days>
    </Expiration>
  </Rule>
</LifecycleConfiguration>
```

### 応答
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Wed, 16 Aug 2017 11:59:33 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDMzYTRfMjQ4OGY3Xzc3NGRfMWY=
```

