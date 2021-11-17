
クライアントでアップロードを開始する前に、アップロード操作中に実行する必要があるアップロード署名を、Appの署名配布サーバーに申請する必要があります。これによって、VODはクライアントにアップロードの権限が付与されているかを確認できます。


## 署名の生成手順

1. **TencentCloud APIの取得**
サーバーAPIの呼び出しに必要なセキュリティ証明（SecretIdとSecretKey）を取得します。具体的な手順は次のとおりです。
	1. コンソールにログインし、【クラウドサービス】>【CAM】>[【APIキー管理】](https://console.cloud.tencent.com/cam/capi)を選択し、「APIキー管理」ページに進みます。
	2. Tencent Cloud APIキーを取得します。キーを作成していない場合は、【キーの作成】をクリックして、SecretIdとSecretKeyのペアを作成することができます。
2. **平文文字列originalの結合**
URL QueryStringのフォーマット要件に従って、平文署名文字列originalを結合します。そのフォーマットは次のとおりです。
```
secretId=[secretId]&currentTimeStamp=[currentTimeStamp]&expireTime=[expireTime]&random=[random]
```
>
	- 上記のoriginalにおける`[secretId]`、`[currentTimeStamp]`、`[expireTime]`、`[random]`は、特定のパラメータ値にご自身で置き換える必要があります。
	- originalには、`secretId`、`currentTimeStamp`、`expireTime`、`random`の4つの必須パラメータが含まれており、オプションのパラメータならいくつでも含めることができます。詳細については、[署名パラメータ](#p2) をご参照ください。
	- パラメータ値は、必ずUrlEncodeを行う必要があります。行わない場合、QueryStringの解析が失敗する恐れがあります。
3. **平文文字列を最終的な署名に変換します**（Javaコードの一部を例とします）
	1. 取得したSecretKeyを使用して、平文文字列originalを[HMAC-SHA1](https://www.ietf.org/rfc/rfc2104.txt) で暗号化し、signatureTmpを取得します。
	```java
	 Mac mac = Mac.getInstance("HmacSHA1");
   SecretKeySpec secretKey = new SecretKeySpec(this.secretKey.getBytes("UTF-8"), mac.getAlgorithm());
   mac.init(secretKey);
	 byte[] signatureTmp = mac.doFinal(original.getBytes("UTF-8"));
	```
	>**signatureTmpは、UTF-8でエンコードされ、HMAC-SHA1で暗号化されたバイト配列です**。
	2. UTF-8を使用して平文文字列originalをバイト配列にエンコードし、次に配列をsignatureTmpでマージし、最後にマージされた結果を[Base64](https://tools.ietf.org/html/rfc4648) にエンコードして、次のような署名signatureを取得します。
```java
String signature = base64Encode(byteMerger(signatureTmp, original.getBytes("utf8")));
```
>**byteMergerとbase64Encodeは、それぞれ配列のマージとBase64エンコードのメソッドです。詳細については、[Java署名サンプルコード](https://intl.cloud.tencent.com/document/product/266/33923#java-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B) をご参照ください**。

## 署名生成の例
VODでは、参考と検証のために、**署名生成サンプルコード**と署名ツールも提供します。
- [クライアントからのアップロード - 署名生成サンプルコード](https://intl.cloud.tencent.com/document/product/266/33923)
- [オンデマンドクライアントからのアップロード - 署名生成ツール](https://video.qcloud.com/signature/ugcgenerate.html)
- [オンデマンドクライアントからのアップロード - 署名検証ツール](https://video.qcloud.com/signature/ugcdecode.html)
		
	
## <span id ="p2"></span>署名パラメータの説明
 
| パラメータ名 | 記入必須 | タイプ | 説明 |
| --- | --- | --- | --- | 
| secretId | はい | String | Tencent Cloud APIキーのSecretId。取得方法については、[クライアントからのアップロードガイド - Tencent Cloud APIキーの取得](https://intl.cloud.tencent.com/document/product/266/33921#p3) をご参照ください。 |
| currentTimeStamp | はい | Integer | 現在のUnixタイムスタンプ。 |
| expireTime | はい | Integer| 署名の有効期限が切れたUnixタイムスタンプ。<br/>```expireTime = currentTimeStamp + 署名の有効期間```<br/>署名の有効期間の最大値は7776000、つまり90日です。 |
| random | はい | Integer | 平文署名文字列を作成するためのパラメータ。10進数で、最大値は`xxxxx`（32ビットの符号なしのバイナリー最大値）です。 |
| classId | いいえ | Integer | ビデオファイルのカテゴリー。デフォルトは0です。 | 
|<span id ="p3"></span> procedure | いいえ | String | 後続のビデオタスク操作、すなわち、ビデオのアップロードが完了した後、タスクフロー操作が自動的に開始されます。このパラメータ値はタスクフローテンプレート名です。VODは、[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058) とテンプレートの命名をサポートします。| 
| taskPriority | いいえ | Integer | 後続のビデオタスクの優先度（procedureが指定されている場合にのみ有効）。値の範囲は[-10，10]、デフォルトは0です。| 
| taskNotifyMode | いいえ | String | タスクフロー状態の変更通知モード（procedureが指定されている場合にのみ有効）。<li>Finish：タスクフローが完全に実行された場合にのみ、イベント通知が開始されます。</li><li>Change：タスクフロー内の各サブタスクのステータスが変更された場合に限り、イベント通知が行われます。</li><li>None：タスクフローのコールバックは受け入れられません。 </li>デフォルトはFinishです。| 
| sourceContext | いいえ | String | ソースコンテキストは、ユーザーリクエスト情報を渡すために使用されます。[アップロード完了コールバック](https://intl.cloud.tencent.com/document/product/266/33950) は、このフィールドの値を返します。最大250文字を入力することが可能です。 |
| oneTimeValid | いいえ | Integer | 署名がワンタイム署名かどうかについては、[クライアントからのアップロードガイド - ワンタイム署名](https://intl.cloud.tencent.com/document/product/266/33921#p4) をご参照ください。<br>デフォルトは0で、ワンタイム署名が無効であることを表し、1はワンタイム署名が有効であることを表します。<br>関連するエラーコードについては、[ワンタイム署名の説明](#p1)をご参照ください。 | 
| vodSubAppId | いいえ | Integer | [サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987) ID。このパラメータを入力しない、0を入力した、またはTencent Cloud AppIdを入力した場合、操作するサブアプリケーションが「メインアプリケーション」となります。 | 
| sessionContext | いいえ | String | セッションコンテキストは、ユーザーリクエスト情報を渡すために使用されます。procedureパラメータが指定されている場合、[タスクフロー状態の変更コールバック](https://intl.cloud.tencent.com/document/product/266/33953) は、フィールド値を返します。最大1000文字を含めることができます。|
| storageRegion | いいえ | String | ストレージリージョンを指定します。コンソールでストレージリージョンを追加することができます。詳細については、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874) をご参照ください。このフィールドには、ストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/33910) を入力してください。|

#### <span id ="p1"></span>ワンタイム署名の説明

- ワンタイム署名を有効にした場合、署名サーバーは、ユーザーに配布される署名が毎回異なることを確認する必要があります（同じタイミングで配布される署名`random`が繰り返されないようにするなど）。確認しない場合、署名重複によるエラーが発生します。
- 署名エラーによってアップロードに失敗し、再試行する場合は、新しい署名を取得する必要があります。
- AndroidおよびJava SDKが原因の署名エラーのエラーコードは`1001`です。



