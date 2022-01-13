プルリツイートコールバックは主にプルリツイートタスクのステータス情報をコールバックするために使用されます。プルリツイートタスクでコールバックアドレスを設定する必要があり、Tencent Cloud CSSのバックグラウンドがタイプの結果をお客様の設定した受信サーバーにコールバックします。

ここでは、主にプッシュ切断コールバックイベントがトリガーされた後、Tencent Cloud CSSがユーザーに送信するコールバックメッセージ通知のフィールドについてご説明します。

 

## 注意事項

このドキュメントに目を通す前に、Tencent Cloud CSSではコールバック機能をどのように設定し、コールバックメッセージをどのように受信するのかを理解している必要があります。具体的な内容については、[イベント通知の受信方法](https://intl.cloud.tencent.com/document/product/267/38080)をご参照ください。

 

## プルリツイートイベントパラメータの説明

### イベントタイプパラメータ

| イベントタイプ | フィールド設定値の説明     |
| :------- | :--------------- |
|プルリツイート | event_type = 314 |


### コールバック共通パラメータ

| パラメータ        | タイプ | 意味                                            |
| ---------------  | ----------- | ----------- |
| appid         |int        | ユーザー APPID             |
| callback_event  | string     | コールバックイベントのタイプ           |
| source_urls     | string     | プルソース URL             |
| to_url          | string     | プッシュターゲット URL           |
| stream_id    | string | CSSストリーム名                                          |
| task_id         | string           | タスクID               |
| [msg](#msg)     | string           | イベントごとの詳細なコールバック情報 |

[](id:msg)
#### msg 内パラメータの説明

| パラメータ        | タイプ | 意味                                            |
| ---------------  | ----------- | ----------- |
| task_start_time  | int        | タスク開始時間、ミリ秒タイムスタンプ  |
| url | String | 現在プルされているソースURL  |
| index            | string     | VODファイルが配置されるリストのインデックス     |
| duration     | int　　  |VODファイルの継続時間、秒                                 |
| task_start_time  | int        | タスク終了時間、ミリ秒タイムスタンプ  |
| code             | string           | タスク終了エラーコード         |
| message      | String?          | タスク終了エラー情報。                   |

### コールバックメッセージの例

#### TaskStart - タスク開始のコールバック
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "TaskStart",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"task_start_time\":0}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_230753472*****21162358-upload-45eb/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118148",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>

#### VodSourceFileStart - VODファイル開始のコールバック
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "VodSourceFileStart",
    
    "callback_url": "http://you.callback.url",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"url\":\"http://remit-tx-ugcpub.douyucdn2.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\",\"index\":0,\"duration\":14920}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118145",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>


#### VodSourceFileFinish - VODファイル終了のコールバック
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "VodSourceFileFinish",
    
    "callback_url": "http://you.callback.url",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"url\":\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\",\"index\":0,\"duration\":14920}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_466247620*****3100448-upload-216b/playlist.m3u8\"]\n",
    
    "stream_id": "testvod",
    
    "task_id": "118145",
    
    "to_url": "rtmp://5000.livepush.myqcloud.com/live/testvod"
}
:::
</dx-codeblock>

#### TaskExit - タスク終了のコールバック
<dx-codeblock>
::: JSON JSON
{
    "appid": 4,

    "callback_event": "TaskExit",
    
    "event_type": 314,
    
    "interface": "general_callback",
    
    "msg": "{\"message\":\"write packet error.\",\"code\":-22,\"task_exit_time\":0}",
    
    "product_name": "pullpush",
    
    "source_urls": "[\"http://yourURL.cn/live/normal_230753472*****21162358-upload-4\"]\n"
}
:::
</dx-codeblock>

>!
>- VODビデオプルリツイート設定のコールバック順序は次のとおりです：「TaskStart-タスク開始のコールバック」 > 「VodSourceFileStart-VODファイル開始のコールバック」 > 「VodSourceFileFinish-VODファイル終了のコールバック」。
>- 「TaskStart-タスク開始のコールバック」 と「VodSourceFileStart-VODファイル開始のコールバック」 の間には**2s以内**の間隔があります。
>- プルリツイートのコールバック設定はプルリツイートタスクで設定します。具体的な操作方法については、[プルリツイート](https://intl.cloud.tencent.com/zh/document/product/267/2818)をご参照ください。


