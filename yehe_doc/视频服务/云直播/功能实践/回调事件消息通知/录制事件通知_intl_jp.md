CSSレコーディングでは、プッシュドメイン名にバインドしたレコーディングテンプレートに基づきライブストリーミング画面をリアルタイムでレコーディングし、生成した対応するレコーディングファイルをVODの中に保存します。またレコーディングのコールバックを、レコーディングファイル情報をプッシュ送信するために利用し、これには主にレコーディングの開始時間、終了時間、生成したレコーディングファイルのID、レコーディングファイルサイズ、ファイルダウンロードアドレスが含まれます。お客様はコールバックテンプレートの中でレコーディングのコールバックメッセージを受信するサーバーアドレスを設定し、このテンプレートとプッシュドメイン名をバインドする必要があります。これにより、ライブストリーミングがレコーディングイベントをトリガーすると、Tencent Cloud CSSのバックエンドがレコーディングファイル情報をお客様の設定した受信サーバーにコールバックします。

ここでは、主にレコーディングコールバックイベントがトリガーされた後、Tencent Cloudバックエンドがユーザーに送信するコールバックメッセージ通知のフィールドについてご説明します。

## 注意事項

- このドキュメントを読む前に、Tencent Cloud CSSによるコールバック機能の設定方法とコールバックメッセージの受信方法についてご理解下さると幸いです。詳細については、[イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。
- レコーディングしたビデオファイルはデフォルトで [VOD](https://console.cloud.tencent.com/vod/overview) コンソールに保存されますので、オンデマンド業務が支払い延滞によりサービス停止にならないよう注意してください。
- APIを介して [レコーディングタスク作成](https://intl.cloud.tencent.com/document/product/267/37309) を実行する時は、レコーディングのコールバックはユーザーのプッシュURLに含まれる [stream_param](#message) パラメータをリターンしません。その他のレコーディング方式ではリターンされます。
- HLS連続レコーディング機能を設定すると、中間でプッシュが中断されてもコールバックしません。デフォルトではストリーミングを継続し、最終的なファイル生成のみコールバックします。


## レコーディングイベントパラメータの説明
### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明           |
| :------- | :------------- |
| CSSレコーディング | event_type = 100 |

[](id:public)
### コールバック共通パラメータ
<table>
<tr><th>フィールド名</th><th>タイプ</th><th>説明</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>期限切れ時間、イベント通知サイン期限のUNIXタイムスタンプ。<ul style="margin:0"><li>Tencent Cloudからのメッセージ通知のデフォルトの期限切れ時間は10分です。メッセージ通知中の t 値が示す時間が期限に達した場合、この通知を無効と判断され、ネットワークのリプレイアタックを防止します。<li>t の形式は10進数UNIXタイムスタンプとなり、1970年1月1日（UTC/GMT 真夜中）から経過した秒数となります。</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>イベント通知セキュリティサイン sign = MD5（key + t）。<br>説明：Tencent Cloudが、暗号化 <a href="#key">key</a> と t で文字列を結合した後、MD5でsignの値を算出し、それを通知メッセージに入れます。お客様のバックエンドサーバーは、通知メッセージの受信後、同じアルゴリズムに基づきsignが正確か確認し、さらにメッセージが確実にTencent Cloudバックエンドから来たものかを確認することができます。</td>
</tr></table>

>? [](id:key)keyは、**イベントセンター>[CSSコールバック](https://console.cloud.tencent.com/live/config/callback)**の中のコールバックキーとなり、主に認証に使用します。お客様のデータ、情報のセキュリティ保護のため、入力することをお勧めします。
![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

[](id:message)

### コールバックメッセージのパラメータ

| フィールド名     | タイプ   | 説明   |
| ----------- | ----------- | ----------- |
| appid        | int    | ユーザー [APPID](https://console.cloud.tencent.com/developer)                                           |
| app          | string | プッシュドメイン名 |
| appname      | string | プッシュパス |
| stream_id    | string | CSSストリーム名                                           |
| channel_id   | string | CSSストリーム名と同じ                                         |
| file_id      | string | VOD file ID、 [VODプラットフォーム](https://intl.cloud.tencent.com/document/product/266/33895)で1つのVODビデオファイルを一意的に特定することができます |                                  |
| file_format  | string | FLV，HLS，MP4，AAC |
| task_id      | string | レコーディングタスクID。APIで作成したレコーディングタスクに対してのみ有効であり、すなわち[CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)によって返されるタスクID |
| start_time   | int64  | レコーディングタスクによるファイル書き込み開始時間。この値をレコーディングコンテンツの開始時間にすることはできません。レコーディングコンテンツの開始時間 = end_time – duration |
| end_time     | int64  | レコーディングタスクによるファイル書き込み終了時刻 |
| duration     | int64  | レコーディングファイルの長さ。単位：秒                                 |
| file_size    | uint64 | レコーディングファイルサイズ。単位：byte                               |
| stream_param | string | ユーザープッシュURLに付帯するパラメータ（カスタマイズ）                                |
| video_url    | string | レコーディングファイルのダウンロードURL                                 |



[](id:example)
### コールバックメッセージの例
<dx-codeblock>
::: JSON JSON
{
"event_type":100,

"appid":12345678,

"app":yourapp,

"appname":yourappname,

"stream_id":"stream_test",

"channel_id":"stream_test",

"file_id":"1234567890",

"file_format":"hls",

"task_id":"UpTbk5RSVhRQ********************0xTSlNTQltlRVRLU1JAWW9EUb",

"start_time":1545047010,

"end_time":1545049971,

"duration":2962,

"file_size":277941079,

"stream_param":"stream_param=test",

"video_url":"http://12345678.vod2.myqcloud.com/xxxx/yyyy/zzzz.m3u8",

"sign":"ca3e25e**********09a9ae7281e300d",

"t":1545030873
}
:::
</dx-codeblock>



 

