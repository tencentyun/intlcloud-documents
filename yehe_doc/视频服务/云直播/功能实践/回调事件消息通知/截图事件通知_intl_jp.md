LVBスクリーンキャプチャとは、決まった時間間隔でリアルタイムのライブストリーミングの画像を切り取り、画像を生成することを指します。通知のコールバックによってスクリーンキャプチャ情報を取得でき、またスクリーンキャプチャのデータは、LVBポルノ検出、ライブルームのサムネイルなどの多様なシナリオに応用できます。

## 注意事項

- このドキュメントを読む前に、Tencent Cloud LVBがどのようにコールバック機能を設定するかを理解していただく必要があります。具体的な内容については、 [イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。
- スクリーンキャプチャコールバックイベントがトリガーされた後に取得するスクリーンキャプチャ情報は、LVBポルノ検出、ライブルームのサムネイルなどの多様なシナリオに応用できます。

## スクリーンキャプチャイベントのパラメータ説明

### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明           |
| :------- | :------------- |
| LVBスクリーンキャプチャ | event_type = 200 |

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

>? <span id="key"></span>key は【機能テンプレート】>[【コールバック設定】](https://console.cloud.tencent.com/live/config/callback)の中のコールバックキーとなり、主に認証に使用します。お客様のデータ、情報のセキュリティ保護のため、入力することをお勧めします。
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### コールバックメッセージのパラメータ


| フィールド名     | タイプ   | 説明                        |
| :----------- | :----- | :-------------------------- |
| stream_id    | string | LVBストリーム名                  |
| channel_id   | string | LVBストリーム名と同じ                |
| create_time  | int64  | スクリーンキャプチャ生成のUNIXタイムスタンプ        |
| file_size    | int    | スクリーンキャプチャファイルサイズ。単位：byte   |
| width        | int    | スクリーンキャプチャの幅。単位：ピクセル          |
| height       | int    | スクリーンキャプチャの高さ。単位：ピクセル          |
| pic_url      | string | スクリーンキャプチャのファイルパス `/path/name.jpg`  |
| pic_full_url | string | スクリーンキャプチャのダウンロードURL                |

### コールバックメッセージの例

```
{
"event_type":200,

"stream_id":"stream_name",

"channel_id":"stream_name",

"create_time":1545030273,

"file_size":7520,

"width":640,

"height":352,

"pic_url":"/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"pic_full_url":"http://testbucket-1234567890.cos.region.myqcloud.com/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```








