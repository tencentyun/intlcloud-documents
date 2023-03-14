プッシュ異常イベントのコールバックは、主にプッシュ異常に関する具体的な情報をコールバックするために使用されます。お客様はプッシュ異常イベントのコールバックでコールバックアドレスを設定する必要があります。Tencent CloudのCSSバックグラウンドでは、設定した受信サーバーにタイプの結果がコールバックされます。
ここでは、プッシュ異常イベントのコールバックをトリガーした後、Tencent Cloud CSSがユーザーに送信するコールバックメッセージ通知フィールドについてご説明します。

## 注意事項

このドキュメントを読む前に、Tencent Cloud CSSによるコールバック機能の設定方法とコールバックメッセージの受信方法についてご理解下さると幸いです。詳細については、[イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。

##　プッシュ異常イベントパラメータの説明
### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明    |
| :------- | :--------------- |
| プッシュ異常イベント | event_type = 321 |

### コールバック共通パラメータ

| パラメータ       | タイプ   | 意味                                  |
| :-------------- | :----- | :------------------------------- |
| appid         |int        | ユーザー APPID             |
| stream_id    | string | CSSストリーム名                                          |
| data_time       | int    | プッシュイベントコールバック時間（単位ms）       |
| report_interval | int    | 異常イベントが発生した場合の上位送信間隔（単位ms） |
| abnormal_event  | json | 詳細な異常イベントグループ               |

#### abnormal_event内のパラメータ説明

<table>
<tr><th>パラメータ</th><th>タイプ</th><th>意味</th></tr>
<tr>
<td>type</td>
<td>int</td>
<td>異常イベントタイプ</td>
</tr><tr>
<td>count</td>
<td>int</td>
<td>異常イベントの単位時間内（上位送信間隔内）の発生回数</td>
</tr><tr>
<td>detail</td>
<td>json</td>
<td><li>desc：異常イベントの記述<li>occur_time：異常イベントの発生時間</td>
</tr><tr>
<td>type_desc_cn</td>
<td>string</td>
<td>異常イベントの日本語記述</td>
</tr><tr>
<td>type_desc_en</td>
<td>string</td>
<td>異常イベントの英語記述</td>
</tr></table>
異常イベントのタイプ

| タイプ | 意味                             |
| :--- | :------------------------------- |
| 1    | ビデオのタイムスタンプのロールバック                   |
| 2    | オーディオのタイムスタンプのロールバック                   |
| 3    | ビデオのタイムスタンプがいきなり大きくなった（1秒を超える）     |
| 4    | オーディオのタイムスタンプがいきなり大きくなった（1秒を超える）     |
| 5    | chunk sizeが大きすぎる（8192を超える）       |
| 6    | 2フレームのビデオフレームの到達時間が長すぎる（3sを超える）　|
| 7    | 2フレームのオーディオフレームの到達時間が長すぎる（3sを超える） |
| 8    | ビデオエンコーディングタイプが変化した             |
| 9    | オーディオエンコーディングタイプが変化した             |
| 10   | ビデオフレームが到着する前にcodecヘッダーがない          |
| 11   | オーディオフレームが到着する前にcodecヘッダーがない          |


>! 
>- 現在のプッシュ異常イベントのコールバックでは、上位送信の間隔ごとに発生した異常イベントをコールバックするため、個々のイベントを設定することができません。異常イベントがない場合、コールバックは行われません。
>- プッシュ異常イベントのコールバックでは、現在のプッシュ異常が統計されるが、他の処理は行われません。


### コールバックメッセージの例

```JSON
{
    "abnormal_event":[
        {
            "count":2,
            "detail":[
                {
                    "desc":"video frame arrive interval too long, interval=3046(msec)",
                    "occur_time":1670588070569
                },
                {
                    "desc":"video frame arrive interval too long, interval=2953(msec)",
                    "occur_time":1670588073522
                }
            ],
            "type":6,
            "type_desc_cn":"ビデオフレームの到達時間差が1000msを超えています",
            "type_desc_en":"video frame arrive interval bigger than 1000(ms)"
        },
        {
            "count":2,
            "detail":[
                {
                    "desc":"audio frame arrive interval too long, interval=3009(msec)",
                    "occur_time":1670588070532
                },
                {
                    "desc":"audio frame arrive interval too long, interval=2917(msec)",
                    "occur_time":1670588073486
                }
            ],
            "type":7,
            "type_desc_cn":"オーディオフレームの到達時間差が1000msを超えています",
            "type_desc_en":"audio frame arrive interval bigger than 1000(ms)"
        }
    ],
    "appid":0,
    "data_time":1670588074971,
    "domain":"xxxx.xxxxx.xxxx.xxxx",
    "event_type":321,
    "interface":"general_callback",
    "path":"xxxx",
    "report_interval":5000,
    "sequence":"000000000000000000",
    "stream_id":"xxxxxx",
    "stream_param":"txSecret=f5828cd4a8a09109304b060172fb3960&txTime=665982e4",
    "timeout":5000
}
```
