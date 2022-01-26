## Event Name
RestoreMediaComplete

## Event Description
If the application is configured with event notification, after a media file is unfrozen or retrieved from the ARCHIVE or DEEP_ARCHIVE storage class, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`RestoreMediaTask` structure](https://intl.cloud.tencent.com/document/product/266/34187).


## Example
### Normal callback v3.0
If you choose the normal callback mode, the callback URL will receive an HTTP request in the following format:

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
### Reliable callback v3.0
If you choose the reliable callback mode, after the [PullEvents](https://intl.cloud.tencent.com/document/product/266/34183) API is called, an HTTP response in the following format will be received.

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
