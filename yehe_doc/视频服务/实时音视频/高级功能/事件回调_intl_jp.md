イベントコールバックサービスは、HTTP/HTTPSリクエストという形でサーバーへのTRTC業務でのイベントの通知をサポートします。イベントコールバックサービスは、ルームイベントグループ（Room Event）とメディアイベントグループ（Media Event）のいくつかのイベントを統合しています。お客様はTencent Cloudに対して、関連の構成情報を提供することができます。

<span id="deploy"></span>
## 構成情報
TRTCコンソールは、セルフサービスのコールバック設定情報をサポートしており、設定が完了した後、イベントコールバック通知を受信できます。詳細な操作ガイドについては、[コールバック設定](https://intl.cloud.tencent.com/document/product/647/39559)をご参照ください。


>!事前に次の情報を準備する必要があります。
>- **必須項目**：コールバック通知を受信するためのHTTP/HTTPSサーバーアドレス。
>- **オプション項目**：署名を計算するためのkeyで、大文字・小文字と数字で構成される最大32文字のkeyをカスタマイズできます。

## タイムアウト・リトライ
イベントコールバックサーバーがメッセージ通知を送信してから5秒以内にお客様のサーバーから応答を受信しない場合、通知は失敗とみなされます。最初の通知が失敗すると、直ちにリトライが行われます。その後の失敗は、メッセージがリトライせずに1分以上続くまで、**10秒**の間隔でリトライし続けます。

<span id="format"></span>
## イベントコールバックメッセージ形式

イベントコールバックメッセージは、HTTP/HTTPS POSTリクエストとしてサーバーに送信されます。ここに、

- 文字エンコード形式：UTF-8。
- リクエスト：bodyの形式はJSONです。
- 応答：HTTP STATUS CODE = 200、サーバーは応答パケットの具体的な内容を無視します。プロトコルとの親和性のため、クライアントの応答内容に、JSON：`{"code":0}`を付けることをお勧めします。


## パラメータの説明
<span id="message"></span>
### コールバックメッセージのパラメータ

- イベントコールバックメッセージのheaderには、次のフィールドが含まれています。
<table id="header">
<tr><th>フィールド名</th><th>値</th></tr></thead><tr>
<td>Content-Type</td><td>application/json</td>
</tr><tr>
<td>Sign</td><td>署名値</td>
</tr><tr>
<td>SdkAppId</td><td>sdk application id</td>
</tr></table>
- イベントコールバックメッセージのbodyには、次のフィールドが含まれています。
<table id="body">
<tr><th>フィールド名</th><th>タイプ</th><th>意味</th>
</tr><tr>
<td>EventGroupId</td><td>Number</td>
<td><a href="#eventId">イベントグループID</a></td>
</tr><tr>
<td>EventType</td>
<td>Number</td>
<td><a href="#event_type">コールバック通知のイベントタイプ</a></td>
</tr><tr>
<td>CallbackTs</td>
<td>Number</td>
<td>イベントコールバックサーバーからお客様のサーバーに送信されるコールバックリクエストのUnixタイムスタンプ。単位はミリ秒</td>
</tr><tr>
<td>EventInfo</td>
<td>JSON Object</td>
<td><a href="#event_infor">イベント情報</a></td>
</tr>
</tbody></table>

<span id="eventId"></span>
### イベントグループID

| フィールド名            | 値   | 意味       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | ルームイベントグループ |
| EVENT_GROUP_MEDIA | 2    | メディアイベントグループ |

<span id="event_type"></span>
### イベントタイプ

| フィールド名                  | 値   | 意味             |
| ----------------------- | ---- | ---------------- |
| EVENT_TYPE_CREATE_ROOM  | 101  | ルームの作成         |
| EVENT_TYPE_DISMISS_ROOM | 102  | ルームの解散         |
| EVENT_TYPE_ENTER_ROOM   | 103  | ルームに参加         |
| EVENT_TYPE_EXIT_ROOM    | 104  | ルームを退出         |
|  EVENT_TYPE_CHANGE_ROLE   | 105  |    ロールの切り替え      |
| EVENT_TYPE_START_VIDEO  | 201  | ビデオデータのプッシュを開始 |
| EVENT_TYPE_STOP_VIDEO   | 202  | ビデオデータのプッシュを停止 |
| EVENT_TYPE_START_AUDIO  | 203  |オーディオデータのプッシュを開始 |
| EVENT_TYPE_STOP_AUDIO   | 204  | オーディオデータのプッシュを停止 |
| EVENT_TYPE_START_ASSIT  | 205  | サブストリームデータのプッシュを開始 |
| EVENT_TYPE_STOP_ASSIT   | 206  | サブストリームデータのプッシュを停止 |

<span id="event_infor"></span>
### イベント情報

| フィールド名  | タイプ   | 意味                              |
| ------- | ------ | --------------------------------- |
RoomId      |     String/Number       |     ルーム名（タイプはクライアントのルーム番号タイプと同様）    |
| EventTs | Number | 時間で発生するUnixタイムスタンプ。単位は秒   |
| UserId  | String | ユーザーID                            |
| Role    | Number | [ロールタイプ](#role_type)（option：入退室時に付帯）  |
| Reason  | Number | [具体的な原因](#reason) （option：入退室時に付帯） |

<span id="role_type"></span>
### ロールタイプ

| フィールド名            | 値   | 意味 |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | キャスター |
| MEMBER_TRTC_VIEWER | 21   | 視聴者 |

<span id="reason"></span>
### 具体的な原因

| フィールド名    | 意味                              |
| -------  | --------------------------------- |
|入室   |<li/>1：正常な入室<li/>2：ネットワークの切り替え<li/>3：タイムアウト・リトライ<li/>4：ルーム間のマイク接続・入室 |
|退室 | <li/>1：正常な退室<li/>2：タイムアウトによる退室<li/>3：ルームのユーザーが削除される<li/>4：マイク接続のキャンセル・退室<li/>5：強制終了|



### 署名計算
署名はHMACSHA256暗号化アルゴリズムによって算出されます。イベントコールバック受信サーバーがコールバックメッセージを受信した後、同じメソッドで署名が算出されます。同様に、Tencent CloudのTRTCのイベントコールバックであり、偽造されていないことを意味します。署名の計算は次のとおりです。
```
//署名Signの計算式のkeyは、署名Signの計算に用いられる暗号化鍵です。
Sign = base64(hmacsha256(key, body))
```



