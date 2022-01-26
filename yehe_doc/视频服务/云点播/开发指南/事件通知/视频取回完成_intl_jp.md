## イベント名
RestoreMediaComplete

## イベントの説明
Appがイベント通知を構成し、かつアーカイブまたはディープアーカイブされたメディアファイルの解凍または取得が完了している場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」によりイベント通知を取得することができます。イベント通知の内容は、[RestoreMediaTaskの構造](https://intl.cloud.tencent.com/document/product/266/34187)となります。


## 事例
### 通常のコールバック3.0
通常のコールバックモードを選択すると、コールバックURLは次の形式のHTTPリクエストを受信します。

```json
{
    "EventType":"RestoreMediaComplete",
    "RestoreMediaCompleteEvent":{
        "FileId":"24961954183381008",
        "OriginalStorageClass":"ARCHIVE",
        "TargetStorageClass":"STANDARD",
        "RestoreTier":"Standard",
        "RestoreDay":0,
        "Status":0,
        "Message":"Restore success!"
    }
}
```
### 信頼できるコールバック3.0
信頼できるコールバックモードを選択し、[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34183) APIが呼び出された後に、次の形式のHTTPレスポンスを受信します。

```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "EventType":"RestoreMediaComplete",
                "RestoreMediaCompleteEvent":{
                    "FileId":"24961954183381008",
                    "OriginalStorageClass":"ARCHIVE",
                    "TargetStorageClass":"STANDARD",
                    "RestoreTier":"Standard",
                    "RestoreDay":0,
                    "Status":0,
                    "Message":"Restore success!"
                }
            }
        ],
        "RequestId":"335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
