プッシュ切断コールバックは、CSSプッシュの成功やCSSプッシュの中断といったライブストリームのステータス情報をプッシュするために使用します。コールバックテンプレートの中でプッシュコールバックやストリーム切断コールバックメッセージの受信サーバーアドレスを設定し、当該テンプレートとプッシュドメイン名を関連付ける必要があります。対応するプッシュアドレスを発行し、CSSプッシュを開始するとTencent Cloud CSSのバックエンドがプッシュ結果をお客様が設定した受信サーバーにコールバックします。

ここでは、主にプッシュ切断コールバックイベントがトリガーされた後、Tencent Cloud CSSがユーザーに送信するコールバックメッセージ通知のフィールドについてご説明します。

## 注意事項
このドキュメントを読む前に、Tencent Cloud CSSによるコールバック機能の設定方法とコールバックメッセージの受信方法についてご理解ください。詳細については、[イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。 


## プッシュ切断イベントのパラメータ説明
### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明 |
|---------|---------|
| CSSプッシュ | event_type = 1 |
| CSSストリーム切断 | event_type = 0 |

### コールバック共通パラメータ
<table>
<tr><th>フィールド名</th><th>タイプ</th><th>説明</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>期限切れ時間、イベント通知サイン期限切れのUNIX タイムスタンプ。<ul style="margin:0"><li>Tencent Cloudからのメッセージ通知のデフォルトの期限切れ時間は10分です。メッセージ通知中の t 値が示す時間が期限切れならば、この通知を無効と判断でき、さらにはネットワークのリプレイアタックを防止することもできます。<li>t の形式は10進数UNIXタイムスタンプとなり、1970年1月1日（UTC/GMT 午後）から経過した秒数となります。</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>イベント通知セキュリティサイン sign = MD5（key + t）。<br>説明：Tencent Cloudが、暗号化 <a href="#key">key</a> と t で文字列を結合した後、MD5でsignの値を算出し、それを通知メッセージに入れます。お客様のバックエンドサーバーは、通知メッセージの受信後、同じアルゴリズムに基づきsignが正確か確認し、さらにメッセージが確実にTencent Cloudバックエンドから来たものかを確認することができます。</td>
</tr></table>

>? [](id:key)keyは、【イベントセンター】>[【CSSコールバック】](https://console.cloud.tencent.com/live/config/callback)の中のコールバックキーとなり、主に認証に使用します。お客様のデータ、情報のセキュリティ保護のため、入力することをお勧めします。

![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### コールバックメッセージのパラメータ

| フィールド名      | タイプ   | 説明                                                         |
| :------------ | :----- | :----------------------------------------------------------- |
| appid         | int    | ユーザー [APPID](https://console.cloud.tencent.com/developer)                                                   |
| app           | string | プッシュドメイン名                                                     |
| appname       | string | プッシュパス                                                     |
| stream_id     | string | CSSストリーム名                                                  |
| channel_id    | string | CSSストリーム名と同じ                                                |
| event_time    | int64  | イベントメッセージ生成のUNIXタイムスタンプ                                   |
| sequence      | string | メッセージシリアルナンバー。1回のプッシュのアクションを表します。1回のプッシュのアクションで同じシリアルナンバーのプッシュとストリーム切断メッセージが生成されます |
| node          | string | CSSアクセスポイントのIP                                              |
| user_ip       | string | ユーザーのプッシュIP                                                  |
| stream_param  | string | ユーザープッシュURLに付帯するパラメータ                                       |
| push_duration | string | ストリーム切断イベント通知プッシュの時間（長さ）。単位：ミリ秒    |                            |
| errcode       | int    | プッシュ切断エラーコード                                                 |
| errmsg        | string | プッシュ切断エラーの説明                                               |
| set_id          | int  | 国内外のプッシュかどうかを判断します。1-6は国内、7-200は海外です   |
|width       |  int   |ビデオ幅。最初のプッシュコールバック時にビデオヘッダー情報が欠落している場合は、0になっている可能性があります   |
|height      |   int  |ビデオ高さ。最初のプッシュコールバック時にビデオヘッダー情報が欠落している場合は、0になっている可能性があります   |

### プッシュ切断エラーコード
プッシュ切断エラーコードおよび対応するエラー原因の詳細については、[ストリーム切断エラーコード](https://intl.cloud.tencent.com/document/product/267/31083)をご参照ください。

### コールバックメッセージの例
```JSON
{
	"app":"test.domain.com",
	
	"appid":12345678,
	
	"appname":"live",
	
	"channel_id":"test_stream",
	
	"errcode":0,
	
	"errmsg":"ok",
	
	"event_time":1545115790,
	
	"event_type":1,
	
	"set_id":2,
	
	"node":"100.121.160.92",
	
	"sequence":"6674468118806626493",
	
	"stream_id":"test_stream",
	
	"stream_param":"stream_param=test",
	
	"user_ip":"119.29.94.245",
	
	"width": 0,
	
	"height": 0,
	
	"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",
	
	"t":1545030873
}
```
