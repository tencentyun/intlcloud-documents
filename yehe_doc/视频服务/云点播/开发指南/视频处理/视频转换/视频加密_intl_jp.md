ビデオの暗号化とは、ビデオをABSにトランスコードし、ビットレートストリーミングに対して暗号化を行うプロセスを指します。VODのビデオ暗号化では2つのクラスの暗号化スキームを提供しています。
* 商用DRM：現在FairPlayとWidevineの2種類を提供しています。
* 基本DRM：SimpleAESの通常の暗号化です。
<span id="zsy"></span>
## ABSへのトランスコードテンプレート

ビデオ暗号化の目標仕様はABSへのトランスコードの目標仕様と同じです。ABSへのトランスコードパラメータによって、「暗号化に使用する暗号化スキーム」、「変換するビデオストリームのビットレート」、「変換するオーディオストリームのビットレート」などのパラメータを制御することができます。VODではABSへのトランスコードテンプレートを使用してパラメータセットを表します。ABSへのトランスコードテンプレートによって、次の関連パラメータを指定できます。

| パラメータ | 説明 |
| -- | -- |
| パッケージングタイプ | ABSの形式。現在HLSとDashの2種類をサポートしています。 |
| DRMタイプ | ビデオを暗号化して保護するかどうかを選択でき、次のDRM暗号化スキームをサポートしています。<li>FairPlay</li><li>Widevine</li><li>SimpleAES</li> |
| VideoTrackリスト | どの種類のビットレートのビデオストリームが含まれているかを示します。 |
| AudioTrack リスト | どの種類のビットレートのオーディオストリームが含まれているかを示します。 |
| 「低ビットレートから高ビットレートへの変換」のフィルタリングの有無 | 通常は、低ビットレートのオリジナルビデオを高ビットレートにトランスコードしても画質や音質の向上は得られません。「低ビットレートから高ビットレートへの変換」のフィルタリングを有効にすると、不要なトランスコードを回避することができます。|

一般的なパラメータグループを対象に、VODでは [プリセットのABSテンプレート](https://intl.cloud.tencent.com/document/product/266/33932)を提供しています。現在、ABSのカスタマイズテンプレートはサポートしていません。

## タスクの開始

ビデオ暗号化タスクの開始には、「サーバーAPIから直接開始する」、「コンソールから直接開始する」、「アップロード時に実行したいタスクを指定する」の3種類の方法があります。具体的な内容は、ビデオ処理の[タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。

以下は、それぞれの方法のビデオ暗号化タスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) の呼び出しによるタスク開始：リクエストの中の`MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition`パラメータで [ABSへのトランスコードテンプレート](#zsy) のテンプレートIDを指定します。
* コンソールでのビデオに対するタスク開始： [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/33897) を呼び出してタスクフローを作成し、タスクフローの中でABSへのトランスコードタスクを設定します（`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`の中で指定）。コンソールでこのタスクフローを使用して [ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33892)します。
* サーバーからのアップロード時にタスクを指定：[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/33897)を呼び出してタスクフローを作成し、タスクフローの中でABSへのトランスコードタスクを設定します（`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`の中で指定）。[アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120)の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定： [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/33897) を呼び出してタスクフローを作成し、タスクフローの中でABSへのトランスコードタスクを設定します（`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`の中で指定）。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922) の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード： [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/33897) を呼び出してタスクフローを作成し、タスクフローの中でABSへのトランスコードタスクを設定します（`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`の中で指定）。コンソールを介してビデオをアップロードし、 [【アップロードと同時にビデオに対する処理操作を実行】](https://intl.cloud.tencent.com/document/product/266/33890) を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。

## 結果の取得

暗号化タスクを開始した後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931)または同期の [タスクの確認](https://intl.cloud.tencent.com/document/product/266/33931)の2種類の方式でビデオ暗号化タスクの実行結果を取得できます。以下は、ビデオ暗号化タスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1256768367-Procedure-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "FileId":"5285890784246869930",
        "FileName":"アニマルワールド",
        "FileUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/AtUCmy6gmIYA.mp4",
        "MetaData":{
            "AudioDuration":60,
            "AudioStreamSet":[
                {
                    "Bitrate":383854,
                    "Codec":"aac",
                    "SamplingRate":48000
                }
            ],
            "Bitrate":1021028,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":60,
            "Height":480,
            "Rotate":0,
            "Size":7700180,
            "VideoDuration":60,
            "VideoStreamSet":[
                {
                    "Bitrate":637174,
                    "Codec":"h264",
                    "Fps":23,
                    "Height":480,
                    "Width":640
                }
            ],
            "Width":640
        },
        "MediaProcessResultSet":[
            {
                "Type":"AdaptiveDynamicStreaming",
                "AdaptiveDynamicStreamingTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":11
                    },
                    "Output":{
                        "Definition":11,
                        "Package":"hls",
                        "DrmType":"FairPlay",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.11.m3u8"
                    }
                }
            },
            {
                "Type":"AdaptiveDynamicStreaming",
                "AdaptiveDynamicStreamingTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":12
                    },
                    "Output":{
                        "Definition":12,
                        "Package":"hls",
                        "DrmType":"SimpleAES",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.12.m3u8"
                    }
                }
            },
            {
                "Type":"AdaptiveDynamicStreaming",
                "AdaptiveDynamicStreamingTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":21
                    },
                    "Output":{
                        "Definition":21,
                        "Package":"dash",
                        "DrmType":"Widevine",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.21.mpd"
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

コールバックの結果の中で、`ProcedureStateChangeEvent.MediaProcessResultSet`に`Type`が`AdaptiveDynamicStreaming`タイプとなる暗号化されたビデオのABSへのトランスコードの結果が3つあり、それぞれ次のようになっています。

* 暗号化タイプがFairPlayのHLS形式。`Definition`は11。
* 暗号化タイプがSimpleAESのHLS形式。`Definition`は12。
* 暗号化タイプがFairPlayのDash形式。`Definition`は21。


