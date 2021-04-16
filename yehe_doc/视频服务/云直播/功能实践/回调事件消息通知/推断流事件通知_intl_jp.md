プッシュ切断コールバックは、LVBプッシュの成功やLVBプッシュの中断といったライブストリームのステータス情報をプッシュするために使用します。コールバックテンプレートの中でプッシュコールバックやストリーム切断コールバックメッセージの受信サーバーアドレスを設定し、当該テンプレートとプッシュドメイン名を関連付ける必要があります。対応するプッシュアドレスを生成し、LVBプッシュを開始するとTencent Cloud LVBのバックエンドがプッシュ結果をお客様が設定した受信サーバーにコールバックします。

ここでは、主にプッシュ切断コールバックイベントがトリガーされた後、Tencent Cloud LVBがユーザーに送信するコールバックメッセージ通知のフィールドについてご説明します。

## 注意事項
このドキュメントを読む前に、Tencent Cloud LVBによるコールバック機能の設定方法とコールバックメッセージの受信方法についてご理解ください。詳細については、[イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。 


## プッシュ切断イベントのパラメータ説明
### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明 |
|---------|---------|
| LVBプッシュ | event_type = 1 |
| LVBストリーム切断 | event_type = 0 |

### コールバック共通パラメータ
<table>
<tr><th>フィールド名</th><th>タイプ</th><th>説明</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>期限切れ時間、イベント通知サイン期限切れのUNIXタイムスタンプ。<ul style="margin:0"><li>Tencent Cloudからのメッセージ通知のデフォルトの期限切れ時間は10分です。メッセージ通知中の t 値が示す時間が期限切れならば、この通知を無効と判断でき、さらにはネットワークのリプレイアタックを防止することもできます。<li>t の形式は10進数UNIXタイムスタンプとなり、1970年1月1日（UTC/GMT 真夜中）から経過した秒数となります。</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>イベント通知セキュリティサイン sign = MD5（key + t）。<br>説明：Tencent Cloudが、暗号化 <a href="#key">key</a> と t で文字列を結合した後、MD5でsignの値を算出し、それを通知メッセージに入れます。お客様のバックエンドサーバーは、通知メッセージの受信後、同じアルゴリズムに基づきsignが正確か確認し、さらにメッセージが確実にTencent Cloudバックエンドから来たものかを確認することができます。</td>
</tr></table>

>? <span id="key"></span>keyは、【イベントセンター】>[【ライブストリーミングコールバック】](https://console.cloud.tencent.com/live/config/callback)におけるコールバックキーで、主に認証のために使用します。お客様のデータ情報を安全に保護するため、入力することをお勧めします。
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### コールバックメッセージのパラメータ

| フィールド名      | タイプ   | 説明                                                         |
| :------------ | :----- | :----------------------------------------------------------- |
| appid         | int    | ユーザー [APPID](https://console.cloud.tencent.com/developer)                                                   |
| app           | string | プッシュドメイン名                                                     |
| appname       | string | プッシュパス                                                     |
| stream_id     | string | LVBストリーム名                                                  |
| channel_id    | string | LVBストリーム名と同じ                                                |
| event_time    | int64  | イベントメッセージ生成のUNIXタイムスタンプ                                   |
| sequence      | string | メッセージシリアルナンバー。1回のプッシュのアクションを表します。1回のプッシュのアクションで同じシリアルナンバーのプッシュとストリーム切断メッセージが生成されます |
| node          | string | LVBアクセスポイントのIP                                              |
| user_ip       | string | ユーザーのプッシュIP                                                  |
| stream_param  | string | ユーザープッシュURLに付帯するパラメータ                                       |
| push_duration | string | ストリーム切断イベント通知プッシュの時間（長さ）。単位：ミリ秒                               |
| errcode       | int    | プッシュ切断エラーコード                                                 |
| errmsg        | string | プッシュ切断エラーの説明                                               |

### プッシュ切断エラーコード
プッシュ切断エラーコードおよび対応するエラーの原因について、詳細は[ストリーム切断エラーコード](https://intl.cloud.tencent.com/document/product/267/31083)をご参照ください。

### コールバックメッセージの例

```
{
"app":"test.domain.com",

"appid":12345678,

"appname":"live",

"channel_id":"test_stream",

"errcode":0,

"errmsg":"ok",

"event_time":1545115790,

"event_type":1,

"node":"100.121.160.92",

"sequence":"6674468118806626493",

"stream_id":"test_stream",

"stream_param":"stream_param=test",

"user_ip":"119.29.94.245",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```