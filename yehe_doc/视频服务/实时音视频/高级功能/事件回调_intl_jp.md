イベントコールバックサービスは、HTTP/HTTPSリクエストという形でサーバーへのTRTC業務でのイベントの通知をサポートします。イベントコールバックサービスは、ルームイベントグループ（Room Event）とメディアイベントグループ（Media Event）のいくつかのイベントを統合しています。お客様は、関連する構成情報をTencent Cloudに提供することでこのサービスをアクティブにすることができます。

[](id:deploy)
## 設定情報
TRTCコンソールでは、自身でのコールバック情報の設定をサポートしており、設定が完了した後、イベントコールバック通知を受信できます。詳細な操作ガイドについては、[コールバック設定](https://intl.cloud.tencent.com/document/product/647/39559)をご参照ください。


>!事前に次の情報を準備する必要があります。
>- **必須項目**：コールバック通知を受信するためのHTTP/HTTPSサーバーアドレス。
>- **オプション項目**：署名を計算するためのkeyで、大文字・小文字アルファベットと数字で構成される最大32文字のkeyをカスタマイズできます。

## タイムアウト・リトライ
イベントコールバックサーバーがメッセージ通知を送信してから5秒以内にお客様のサーバーから応答を受信しない場合、通知は失敗とみなされます。最初の通知が失敗すると、直ちにリトライが行われます。その後の失敗は、メッセージがリトライせずに1分以上続くまで、** 10秒**の間隔でリトライし続けます。

[](id:format)
## イベントコールバックメッセージ形式

イベントコールバックメッセージは、HTTP/HTTPS POSTリクエストとしてサーバーに送信されます。以下がその詳細となります。

- **文字エンコード形式**：UTF-8。
- **リクエスト**：bodyの形式はJSONです。
- **応答**：HTTP STATUS CODE = 200、サーバーは応答パケットの具体的な内容を無視します。プロトコルとの親和性のため、クライアントの応答内容に、JSON：`{"code":0}`を付けることをお勧めします。
- **パケット例**：以下の内容は「ルームイベントグループ-入室」イベントのパケット例です。
<dx-codeblock>
::: JSON JSON
{
    「EventGroupId」: 1、                #ルームイベントグループ
    「EventType」:103、                #入室イベント
    「CallbackTs」: 1615554923704、       #コールバック時間。単位はミリ秒
    "EventInfo": {
        「RoomId」: 12345、                #数字のルーム番号
        「EventTs」: 1615554922、        #イベント発生時間。単位は秒
        「EventTs」: 1615554922661、        #イベント発生時間。単位はミリ秒
        「UserId」: 「test」、               #ユーザーID
        「UniqueId」: 1615554922656、      #固有識別子
        「Role」: 20、                     #ユーザーロール、キャスター
        「TerminalType」: 3、       #端末のタイプ、OS端末
        「UserType」: 3、       #ユーザーのタイプ、Native SDK
        「Reason」: 1        #入室の原因、正常な入室
	}
}
:::
</dx-codeblock>



## パラメータの説明
[](id:message)
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

[](id:eventId)
### イベントグループID

| フィールド名            | 値   | 意味       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | ルームイベントグループ |
| EVENT_GROUP_MEDIA | 2    | メディアイベントグループ |

[](id:event_type)
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

[](id:event_infor)
### イベント情報



| フィールド名  | タイプ   | 意味                              |
| ------- | ------ | --------------------------------- |
|RoomId      |     String/Number       |     ルーム名（タイプはクライアントのルーム番号タイプと同様）    |
|EventTs      |    Number     |      イベントで発生するUnixタイムスタンプ。単位は秒（互換性保留） |
|EventMsTs    |     Number     |     イベントで発生するUnixタイムスタンプ。単位はミリ秒   |
| UserId  | String | ユーザーID                            |
| UniqueId  | Number | [固有識別子](#UniqueId)（option：ルームイベントグループ付与）                            |
| Role    | Number | [ロールタイプ](#role_type)（option：入退室時に付帯）  |
|TerminalType  |  Number    |   [端末のタイプ](#terminal)（option：入室時に付帯）|
|UserType  |  Number   |   [ユーザーのタイプ](#usertype)（option：入室時に付帯）|
| Reason  | Number | [具体的な原因](#reason) （option：入退室時に付帯） |

>?[](id:UniqueId) **固有識別子の定義：**クライアントでネットワークの切り替え、異常退出および再入室プロセスなどの特殊な行為が発生すると、お客様のコールバックサーバーが同じユーザーの複数回の入室および退室コールバックを受信する可能性があり、UniqueIdを使用してユーザーの同一回の入退室を識別することができます。

[](id:role_type)
### ロールタイプ

| フィールド名            | 値   | 意味 |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | キャスター |
| MEMBER_TRTC_VIEWER | 21   | 視聴者 |


[](id:terminal)
### 端末のタイプ
| フィールド名            | 値   | 意味 |
| ------------------ | ---- | ---- |
| TERMINAL_TYPE_WINDOWS | 1 | Windows端末   |
| TERMINAL_TYPE_ANDROID | 2  | Android端末 |
| TERMINAL_TYPE_IOS | 3  | iOS端末 |
| TERMINAL_TYPE_LINUX | 4  | Linux端末 |
| TERMINAL_TYPE_OTHER | 100  | その他 |

[](id:usertype)
### ユーザーのタイプ
| フィールド名            | 値   | 意味 |
| ------------------ | ---- | ---- |
| USER_TYPE_WEBRTC | 1 | webrtc   |
| USER_TYPE_APPLET | 2  | ミニプログラム |
| USER_TYPE_NATIVE_SDK | 3  | Native SDK |


[](id:reason)
### 具体的な原因

| フィールド名    | 意味                              |
| -------  | --------------------------------- |
|入室   |<li/>1：正常な入室<li/>2：Networkingの切り替え<li/>3：タイムアウト・リトライ<li/>4：ルーム間マイク接続による入室 |
|退室 | <li/>1：正常な退室<li/>2：タイムアウトによる退室<li/>3：ルームのユーザーが削除される<li/>4：マイク接続のキャンセルによる退室<li/>5：強制終了|




### 署名計算
署名はHMAC SHA256暗号化アルゴリズムによって算出されます。イベントコールバック受信サーバーがコールバックメッセージを受信した後、同じ方法で署名が算出されます。同様に、Tencent CloudのTRTCのイベントコールバックであり、偽造されていないことを意味します。署名の計算は次のとおりです。
```
//署名Signの計算式のkeyは、署名Signの計算に用いられる暗号化鍵です。
Sign = base64(hmacsha256(key, body))
```

>! bodyはお客様が受信したコールバックリクエストのオリジナルパケットです。いかなる変更も行わないでください。例：
>```
>body="{\n\t\"EventGroupId\":\t1,\n\t\"EventType\":\t103,\n\t\"CallbackTs\":\t1615554923704,\n\t\"EventInfo\":\t{\n\t\t\"RoomId\":\t12345,\n\t\t\"EventTs\":\t1608441737,\n\t\t\"UserId\":\t\"test\",\n\t\t\"UniqueId\":\t1615554922656,\n\t\t\"Role\":\t20,\n\t\t\"Reason\":\t1\n\t}\n}"
>```