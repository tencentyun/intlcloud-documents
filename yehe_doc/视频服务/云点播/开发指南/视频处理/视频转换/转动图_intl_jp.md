アニメーション画像とは、ビデオフィルムを切り取り、動画（GIF、WEBPなど）を生成するプロセスを指し、オフラインタスクとなります。動画は1組の連続したフレームをシームレスに循環させ、これにより小さい容量でアニメーション効果を実現します。
>? 動画への変換時、オリジナルビデオの中の開始時間と終了時間の指定をサポートしています。すなわち「ビデオの1区間を切り取り」動画に変換します。
<span id = "zdt"></span>
## アニメーション画像生成テンプレート


アニメーション画像の目標仕様。動画形式、幅と高さ、フレームレートなどのパラメータが含まれます。VODではアニメーション画像生成テンプレートを使用してアニメーション画像パラメータグループを表し、アニメーション画像生成テンプレートによって、以下の動画関連パラメータを指定することができます。

| パラメータ             | 説明                                         |
| ---------------- | -------------------------------------------- |
| 形式（Format）   | 動画ファイルの出力形式。現在はGIFとWEBPのみをサポートしています。 |
| 幅（Width）        | 動画の幅。範囲は128px～4096px。                             |
| 高さ（Height）     | 動画の高さ。範囲は128px～4096px。                             |
| フレームレート（FPS）      | サポートするフレームレート範囲：1fps～60fps。                    |

一般的な仕様を対象に、VODでは [プリセットのアニメーション画像生成テンプレート](https://intl.cloud.tencent.com/document/product/266/33932#cinemagraph)を提供しています。その外、コンソールを介して、カスタマイズしたアニメーション画像生成テンプレートを作成し、管理することができます。具体的な操作は、 [テンプレート設定](https://intl.cloud.tencent.com/document/product/266/14059#.E8.BD.AC.E5.8A.A8.E5.9B.BE.E6.A8.A1.E6.9D.BF)をご参照ください。

## タスクの開始
アニメーション画像タスクの開始には、「サーバーAPIから直接開始」、「コンソールから直接開始」、「アップロード時に実行したいタスクを指定」の3種類の方法があります。詳細内容は、ビデオ処理の [タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask)をご参照ください。

以下は、各種方式のアニメーション画像タスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) の呼び出しによるタスク開始：リクエストの中の`MediaProcessTask.AnimatedGraphicTaskSet`パラメータで [アニメーション画像生成テンプレート](#zdt)のテンプレートIDを指定します。
* コンソールでのビデオに対するタスクの開始：コンソールで[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でアニメーション画像の目標仕様を設定します。コンソールでこのタスクフローを使用して[ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33890)します。
* サーバーからのアップロード時にタスクを指定：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でアニメーション画像の目標仕様を設定します。[アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0)の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定：コンソール で[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でターゲットのアニメーション画像の仕様を設定します。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でアニメーション画像の目標仕様を設定します。コンソールを介してビデオをアップロードし、[【アップロードと同時にビデオに対する処理操作を実行】](https://intl.cloud.tencent.com/document/product/266/33890)を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。

## 結果の取得

アニメーション画像タスクの開始後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) 待ちおよび同期の [タスクの確認](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) の2種類の方式でアニメーション画像の実行結果を取得できます。以下は、アニメーション画像タスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

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
            "Bitrate":1021028、
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":60,
            "Height":480,
            "Rotate":0,
            "Size":7700180,
            "VideoDuration":60,
            "VideoStreamSet":[
                {
                    "Bitrate":637174、
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
                "Type":"AnimatedGraphics",
                "AnimatedGraphicTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":20001,
                        "StartTimeOffset":2,
                        "StartTimeOffset":5
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20001.webp",
                        "Definition":20001,
                        "Container":"webp",
                        "Height":480,
                        "Width":640,
                        "Bitrate":324271,
                        "Size":121601,
                        "Md5":"084d403c73930ca2f835679af1f37bd3",
                        "StartTimeOffset":3,
                        "EndTimeOffset":5
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

コールバックの結果の中で、`ProcedureStateChangeEvent.MediaProcessResultSet`に`Type`が`AnimatedGraphics`となる結果が1つあり、`Definition`が20001となっています。
