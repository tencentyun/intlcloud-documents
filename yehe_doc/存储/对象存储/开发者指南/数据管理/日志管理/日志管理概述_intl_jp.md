## 概要
ログ管理機能は、指定したソースバケットへの詳細なアクセス情報を記録し、これらの情報をログファイル形式で指定のバケットに保存することで、バケットのより適切な管理を実現するものです。

ターゲットバケット内のログレコードのパスは次のとおりです。

```shell
ターゲットバケット/パスプレフィックス{YYYY}/{MM}/{DD}/{time}_{random}_{index}
```

ログは5分に1回生成され、1件のレコードにつき1行となります。各レコードに複数のフィールドが含まれ、フィールドの間はスペースで区切られます。単一のログファイルは最大256MBまでであり、この5分間に生成されたログの量が256MBを超えた時点で、ログが複数のログファイルに分割される点に注意が必要です。現在サポートされているログフィールドは次のとおりです。

| フィールド番号 | 名 称         | 意 味                  | 例                                                                        |
| :--------: | :---------------: | :-----------------------: | ----------------------------------------------------------------------------- |
| 1        | eventVersion    | レコードのバージョン             | 1.0                                                                          |
| 2        | bucketName      | バケット名          | examplebucket-1250000000                                                      |
| 3        | qcsRegion       | リクエストリージョン             | ap-beijing                                                                    |
| 4        | eventTime       | イベント時間（リクエスト終了時間、UTC 0時 タイムスタンプ） | 2018-12-01T11:02:33Z                                                          |
| 5        | eventSource     | ユーザーがアクセスしたドメイン名 | examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com                        |
| 6        | eventName       | イベント名             | UploadPart                                                                    |
| 7        | remoteIp        | ソースIP                 | 192.168.0.1                                                                   |
| 8        | userSecretKeyId | ユーザーアクセスKeyId        | AKIDNYVCdoJQyGJ5b1234                                                       |
| 9        | reservedFiled | 予約フィールド   | 予約フィールドは`-`と表示されます。 |
| 10       | reqBytesSent    | リクエストバイト数（Bytes） | 83886080                                                                      |
| 11       | deltaDataSize   | ストレージ量変更のリクエスト（Bytes） | 808                                                                   |
| 12       | reqPath         | リクエストのファイルパス          | /folder/text.txt                                                              |
| 13       | reqMethod       | リクエストメソッド             | put                                                                           |
| 14       | userAgent       | ユーザーUA                | cos-go-sdk-v5.2.9                                                             |
| 15       | resHttpCode     | HTTP戻りコード           | 404                                                                      |
| 16       | resErrorCode    | エラーコード                | NoSuchKey                               |
| 17       | resErrorMsg     | エラーメッセージ             | The specified key does not exist.                                      |
| 18       | resBytesSent    | 戻りバイト数（Bytes）   | 197                                                                           |
| 19       | resTotalTime    | リクエスト総消費時間（ミリ秒、応答のTTLB-リクエストのTTFBと同じ） | 4295        |
| 20       | logSourceType   | ログソースタイプ          | USER（ユーザーアクセスリクエスト）、CDN（CDN back-to-originリクエスト）                                                           |
| 21       | storageClass    | ストレージタイプ             | STANDARD，STANDARD_IA，ARCHIVE                                              |
| 22       | accountId    | バケット所有者のID             | 100000000001                                              |
| 23       | resTurnAroundTime    | リクエストサーバー消費時間（ミリ秒、応答のTTFB-リクエストのTTLBと同じ）             | 4295                                              |
| 24       | requester    | アクセス者のアカウント。<br>アクセス者がルートアカウントの場合、アカウント形式は`ルートアカウントUIN:ルートアカウントUIN`となります。<br>アクセス者がサブアカウントの場合、アカウント形式は`ルートアカウントUIN:サブアカウントUIN`となります。<br>アクセス者が[サービスアカウント](https://intl.cloud.tencent.com/document/product/598/19421)の場合、アカウント形式は`権限を承認されたルートアカウントUIN:ロールID`となります。<br>匿名アクセスの場合は、`-`と表示されます             |    100000000001:100000000001          |
| 25       | requestId    | リクエストID             | NWQ1ZjY4MTBfMjZiMjU4NjRfOWI1N180NDBiYTY=      |
| 26       | objectSize    | オブジェクトサイズ（Bytes）             | 808。マルチパートアップロードを使用した場合、objectSizeフィールドはアップロード完了後にしか表示されません。各パートのアップロード中、このフィールドには`-`と表示されます |
| 27       | versionId    | オブジェクトのバージョンID             | ランダムな文字列                                              |
| 28       | targetStorageClass    | ターゲットバケットのタイプ。コピー操作のリクエストを送信すると、このフィールドが記録されます             | STANDARD，STANDARD_IA，ARCHIVE        |
| 29     | referer    | リクエストのHTTP referer             | `*.example.com`または111.111.111.1       |
| 30       | requestUri    | リクエストのURI             | "GET /fdgfdgsf%20/%E6%B5%AE%E7%82%B9%E6%95%B0 HTTP/1.1"       |
| 31       | vpcId    | VPCリクエストのID            | "0"(VPCではない)/"12345"(VPC。「0」以外のstringとします)       |

>!
> - 現在、COSのログ管理機能でサポートされているリージョンには、北京、上海、広州、南京、重慶、成都、中国香港、シンガポール、ソウル、トロント、シリコンバレー、ムンバイがあります。
> - ログ管理機能を使用するには、ソースバケットとターゲットバケットが同一のリージョンにあることが必要です。
> - ログを保存するターゲットバケットはソースバケットと同じにすることもできますが、推奨されません。
> - 現時点では、XML APIおよびXML APIをベースにして実装したSDK、ツールなどによってバケットへのアクセスリクエストを行った場合にのみ、ログが記録されます。JSON APIおよびJSON APIをベースにして実装したSDK、ツールなどによるアクセスでは、ログは記録されません。
> - ユーザーのニーズおよび業務の発展に応じて、COSはアクセスログに新しいフィールドを追加する場合があります。ログ解析の際に必ず適切に処理してください。
> 

## ログ管理の有効化
### コンソールの使用
ログ管理機能はコンソールでスピーディーに有効化することができます。操作ガイドについては、[ログ管理の設定](https://intl.cloud.tencent.com/document/product/436/17040) のコンソールガイドをご参照ください。

### APIの使用 
APIを使用して、指定のバケットでログ管理機能を有効化する場合は、次の手順をご参照ください。
1. ログロールを作成します。
2. ログロールに権限をバインドします。
3. ログ管理を有効化します。

#### 1. ログロールの作成
ログロールを作成します。具体的なインターフェースの情報については、[CreateRole](https://intl.cloud.tencent.com/document/product/598/33561)をご参照ください。
このうち、roleNameは必ずCLS_QcsRoleとします。
policyDocumentは次のとおりです。
```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal":{
			"service": "cls.cloud.tencent.com"
		}
	}]
}
```
#### 2. ログロールへの権限のバインド
ロール権限に権限をバインドします。具体的なインターフェースの情報については、[AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/33562)をご参照ください。
このうち、policyNameはQcloudCOSAccessForCLSRoleとします。roleNameは手順1のCLS_QcsRoleとします。roleNameの作成時に返されたroleIDを使用することもできます。

#### 3. ログ管理の有効化
インターフェースを呼び出してログ管理機能を有効化します。具体的なインターフェースの情報については、[PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054)をご参照ください。ログを保存するターゲットバケットはソースバケットと同一のリージョンにあることが必要です。
