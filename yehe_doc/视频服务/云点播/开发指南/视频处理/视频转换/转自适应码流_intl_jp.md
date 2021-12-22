ABSへのトランスコードとは、ビデオをトランスコードしてパッケージングし、ABSの出力ファイルを生成するプロセスを指します。その特徴は、複数のビットレートの音声ビデオファイルと1つのマニフェストファイル（manifest）が含まれていることで、プレーヤーは現在の帯域幅に応じて、最適なビットレートを動的に選択して再生することができます。現在最も幅広く活用されているABSの形式は、 [Master Playlist](https://developer.apple.com/documentation/http_live_streaming/example_playlists_for_http_live_streaming/creating_a_master_playlist) 形式でのHLSです。

VODは、ビデオのHLSおよびMPEG-DASH形式のABSへの変換機能をサポートしています。この機能を使用すると、次の事項が可能になります。
* プレーヤーが現在の帯域幅に応じて最適なビットレートを動的に選択して再生し、視聴者に素晴らしい体験をもたらします。
* メインストリームのプレーヤーそのものがHLSアダプティブビットレートストリーミングをサポートしているため、プレーヤーをカスタマイズする必要がありません。
* VODでは [Super player  SDK](https://intl.cloud.tencent.com/document/product/266/7836)を提供し、統合した後、ABSを素早く、簡単に再生できるようにしています。



## [](id:zsy)ABSへのトランスコードテンプレート

ABSへのトランスコードのパラメータによって、ABSの中の各サブストリームの「ビデオトランスコーディングパラメータ」、「オーディオトランスコーディングパラメータ」などのパラメータを制御できます。VODではABSテンプレートを使用してパラメータグループを表します。ABSテンプレートによって、以下の関連パラメータを指定することができます。

| パラメータ | 説明 |
| -- | -- |
| パッケージングタイプ | ABSの形式。現在HLSとMPEG-DASHをサポートしています。 |
|暗号化タイプ|	HLS形式のみがSimpleAES暗号化をサポートしており、DASHは暗号化をサポートしていません|
| サブストリーム仕様 | 幾つのサブストリームを出力するか、および各サブストリームのビデオトランスコーディングパラメータならびにオーディオトランスコーディングパラメータを制御します。<li>ビデオトランスコーディングパラメータ：解像度、ビットレート、フレームレート、エンコード形式など</li><li>オーディオトランスコーディングパラメータ：サンプリングレート、サウンドチャンネル数、エンコード形式など</li> |
| 「低解像度から高解像度への変換」のフィルタリングの有無 | 通常は、低解像度のオリジナルビデオを高解像度に変換しても画質と音質の向上は得られません。「低解像度から高解像度への変換」のフィルタリングを有効にすると、不要なトランスコードを回避することができます|

一般的なパラメータグループを対象に、VODでは[プリセットのABSテンプレート](https://intl.cloud.tencent.com/document/product/266/33932)を提供しています。同時に、ABSへのトランスコードテンプレートのカスタマイズもサポートしています。

## タスクの開始

ABSへのトランスコードタスクの開始には、「サーバーAPIからの直接の開始」、「コンソールからの直接の開始」、「アップロード時に実行したいタスクを指定」の3種類の方法があります。具体的な内容は、ビデオ処理の [タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。

以下は、各種方式のABSタスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) の呼び出しによるタスク開始：リクエストの中の`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`パラメータで [ABSへのトランスコードテンプレート](#zsy) のテンプレートIDを指定します。
* コンソールでのビデオに対するタスク開始： [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34167) を呼び出してタスクフローを作成し、タスクフローの中でABSへのトランスコードタスクを設定します（`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`の中で指定）。コンソールでこのタスクフローを使用して [ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33892)します。
* サーバーからのアップロード時にタスクを指定：[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34167)を呼び出してタスクフローを作成し、タスクフローの中でABSへのトランスコードタスクを設定します（`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`の中で指定）。[アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120)の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定： [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34167) を呼び出してタスクフローを作成し、タスクフローの中でABSへのトランスコードタスクを設定します（`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`の中で指定）。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922) の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード： [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34167) を呼び出してタスクフローを作成し、タスクフローの中でABSへのトランスコードタスクを設定します（`MediaProcessTask.AdaptiveDynamicStreamingTaskSet`の中で指定）。コンソールを介してビデオをアップロードし、 [【アップロードと同時にビデオに対する処理操作を実行】](https://intl.cloud.tencent.com/document/product/266/33890) を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。

## 結果の取得

ABSへのトランスコードタスクの開始後、非同期の [結果通知](https://intl.cloud.tencent.com/document/product/266/33931)  待ちおよび同期の [タスクの確認](https://intl.cloud.tencent.com/document/product/266/33931) の2種類の方式でABSへのトランスコードタスクの実行結果を取得できます。以下は、ABSへのトランスコードタスク開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

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
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "Package":"hls",
                        "DrmType":"",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.10.m3u8"
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
                        "Definition":20
                    },
                    "Output":{
                        "Definition":20,
                        "Package":"dash",
                        "DrmType":"",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.20.mpd"
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

コールバックの結果の中で、`ProcedureStateChangeEvent.MediaProcessResultSet`に`Type`が`AdaptiveDynamicStreaming`となる結果が2つあり、`Definition`がそれぞれ10と20になっています。

