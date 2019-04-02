ログは、クライアントまたはAPI/SDKを介したログの収集をサポートしています。CLSプラットフォームに収集されたログは特定の規則に従って構成化されます。

## 収集方式

### APIによるログ収集
[CLS API](https://cloud.tencent.com/document/product/614/12445)を呼び出すことで、構造化ログをCLSにアップロードできます。関連資料については、[ログアップロードのAPI](https://cloud.tencent.com/document/product/614/16873)を参照してください。

### SDKによるログ収集
現時点で利用可能なSDKはありません。

### LogListenerクライアントを介してリアルタイムでログを収集します

LogListenerは、CLSが提供するログ収集クライアントです。LogListenerをサーバーにインストールすることで、指定されたパスのログをリアルタイムに収集し、ログの生データに対して構造化処理を実行することができます。以下の手順を実行するだけで、LogListenerを使用して収集できます。

1.Loglistenerをサーバーにインストールします。
2.CLSコンソールにサーバーグループを作成します。
3.ログトピックでサーバーグループを関連付け、関連構成を完了します。

関連資料については、[LogListener操作ガイド](https://cloud.tencent.com/document/product/614/17414)を参照してください。

### LogListenerがログを正常に収集したかどうかを素早く確認します。
1.ユーザーはログ検索を開く必要があります。詳細については、[インデックスを開く](https://cloud.tencent.com/document/product/614/16981)を参照してください。
2.[CLSコンソール](https://console.cloud.tencent.com/cls)にログインし、【ログ検索】をクリックして表示します（ログ収集には短い遅延があります）。

## ログ構造化

ログ構造化は、ログデータがKey-ValueとしてCLSプラットフォームに保存されることを意味します。ログが構造化されたら、構造化ログをダウンロードしたり、キー値を指定して検索したり、ログを構造化して配信したりできます。

- APIを収集すると、構造化されたログデータを直接アップロードできます。
- LogListener収集を使用すると、構造化されていないログ生データを構造的に解析するためにログデーターの構造化された方法を指定できます。例：あなたのログデータは `10002345987;write;error;topic does not exist`である場合、ログを解析するときに区切り記号を指定でき、区切り記号がセミコロンです。全てのキー値（key）はeventid action status msgです。その場合、このログは4つのキー/値のペア、すなわち`eventid:10002345987 action:write status error msg:topic does not exist`。

