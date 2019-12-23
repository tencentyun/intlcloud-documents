## 機能説明

GET Bucket websiteリクエストは、バケットに関連する静的サイト構成情報を取得するために使用されます。

## リクエスト

### リクエスト例

```shell
GET /?website HTTP/1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

> Authorization：Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。

### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。

#### 非共通のヘッダー

このリクエスト操作には、特別なリクエストヘッダー情報はありません。

### リクエストボディ

このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー

#### 共通の応答ヘッダー

この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。

#### 特有の応答ヘッダー

この応答には、特別な応答ヘッダーがありません。

### 応答ボディ

この応答ボディはapplication/xmlデータとして返され、完全なノードデータを含む内容は以下のようになります：

```shell
<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>index.html</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>https</Protocol>
	</RedirectAllRequestsTo>
	<ErrorDocument>
		<Key>Error.html</Key>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>404.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>docs/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyPrefixWith>documents/</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>img/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>demo.jpg</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```

具体的な説明は以下のとおりです：

| 名称                        | 親ノード                | 説明                                                         | タイプ      | 必須項目 |
| --------------------------- | --------------------- | ------------------------------------------------------------ | --------- | ---- |
| WebsiteConfiguration        | 無し                    | 静的サイト構成、インデックスドキュメント、エラードキュメント、プロトコル変換とリダイレクト規則を含みます  | Container | はい   |
| IndexDocument               | WebsiteConfiguration  | インデックスドキュメント                                                     | Container | はい   |
| Suffix                      | IndexDocument         | インデックスドキュメントを指定します                                                 | String    | はい   |
| ErrorDocument               | WebsiteConfiguration  | エラードキュメント                                                     | Container | いいえ   |
| Key                         | ErrorDocument         | 汎用エラーページを返すように指定します                                             | String    | いいえ   |
| RedirectAllRequestsTo       | WebsiteConfiguration  | すべてのリクエストをリダイレクトします                                               | Container | いいえ   |
| Protocol                    | RedirectAllRequestsTo | Webサイト全体のリダイレクトのプロトコルを指定します。これはhttpsにのみ設定できます                        | String    | いいえ   |
| RoutingRules                | WebsiteConfiguration  | ルーティング規則を設定します。最大100個のRoutingRuleを設定します                     | Container | いいえ   |
| RoutingRule                 | RoutingRules          | プレフィックスマッチのリダイレクトとエラーコードのリダイレクトを含む、単一のリダイレクト規則を設定します         | Container | いいえ   |
| Condition                 | RoutingRule          | リダイレクトが発生する条件を指定します。プレフィックスマッチのリダイレクトとエラーコードのリダイレクトはどちらか一方しか指定できません | Container | いいえ   |
| HttpErrorCodeReturnedEquals | Condition             | リダイレクトエラーコードを指定します。4XX戻りコード構成のみをサポートします。優先度はErrorDocumentより高い | Interger  | いいえ   |
| KeyPrefixEquals             | Condition             | リダイレクトするパスのプレフィックスを指定します                      | String    | いいえ   |
| Redirect                    | RoutingRule           | リダイレクト条件を満たすときのリダイレクトの具体的な置換規則を指定します                 | Container | いいえ   |
| ReplaceKeyWith              | Redirect              | キー全体を指定された内容に置き換えます                                      | String    | いいえ   |
| ReplaceKeyPrefixWith        | Redirect              | マッチされたプレフィックスを指定された内容に置き換えます。ConditonはKeyPrefixEqualsであるとき、設定できます | String    | いいえ   |

###　エラーコード

このリクエスト操作には、特別なエラーメッセージがありません。一般的なエラーメッセージについては、 [エラーコード](https://cloud.tencent.com/document/product/436/7730) ドキュメントを参照してください。

## 実際のケース

### リクエスト

```shell
GET /?website HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Date:Thu, 21 Sep 2017 13:09:53 +0000
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484815944;32557711944&q-key-time=1484815944;32557711944&q-header-list=host&q-url-param-list=website&q-signature=a2d28e1b9023d09f9277982775a4b3b705d0e23e
```

### 応答

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 751
Connection: keep-alive
Date: Thu, 21 Sep 2017 13:15:39 GMT
Server: tencent-cos
x-cos-request-id: NTljM2JiN2FfMjQ4OGY3MGFfNzk4OV84Mg==

<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>index.html</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>https</Protocol>
	</RedirectAllRequestsTo>
	<ErrorDocument>
		<Key>Error.html</Key>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>404.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>docs/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyPrefixWith>documents/</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>img/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>demo.jpg</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```

