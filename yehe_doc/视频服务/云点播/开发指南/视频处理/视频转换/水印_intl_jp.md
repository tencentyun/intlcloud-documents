ウォーターマークは、ビデオのトランスコーディングまたはスクリーンキャプチャ時に、特定の画像または文字を画面の指定位置に追加するプロセスであり、オフラインタスクです。VODでは以下のタイプのウォーターマークをサポートしています。
- 静的画像ウォーターマーク：PNG形式の画像ウォーターマーク。版権元のLOGO、放送局ロゴなど、通常、ビデオの版権の帰属の表示に利用されます。
- 動的画像ウォーターマーク：APNG形式の動的画像ウォーターマーク。ウォーターマーク画像のダイナミックな変化による效果を実現できます。
- 文字ウォーターマーク：多言語の文字形式ウォーターマーク。ユーザーのニックネームなど、通常、UGSVの中でビデオ制作者の標識に利用されます。

VODではビデオまたはスクリーンキャプチャに対する複数のウォーターマークをサポートし、各ウォーターマークの画面の中でのサイズと位置を指定できます。

## <span id = "sy"></span>
ウォーターマークテンプレート

ウォーターマークの目標仕様にはウォーターマークのタイプ、幅、高さ、位置などのパラメータが含まれます。VODではウォーターマークテンプレートを使用してウォーターマークのパラメータグループを表します。ウォーターマークテンプレートで、以下のウォーターマーク関連パラメータを指定できます。

| パラメータ                     | 説明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| ウォーターマークタイプ（Type）         | 画像と文字の2種類のタイプのウォーターマークを刻印できます。：<li>画像ウォーターマーク：静的画像および動的画像。</li><li>文字ウォーターマーク：多種の言語の文字に対応しています。</li> |
| ウォーターマーク位置（Position）     | ウォーターマークのビデオ画面上の対応する位置。                                 |
| 画像サイズ（ImageSize）    | 画像ウォーターマークがビデオ画面で占める大きさ。                                   |
| 画像コンテンツ（ImageContent） | 画像ウォーターマークの中の画像のバイナリーコンテンツ。                                 |
| フォントサイズ（FontSize）     | 文字ウォーターマークの中のフォントのサイズ。                                       |
| フォントタイプ（FontType）     | 文字ウォーターマークの中の文字のフォントタイプ（宋体など）。                         |
| フォントカラー（FontColor）    | 文字ウォーターマークの中の文字の色（0xRRGGBB）。                           |
| 文字の透明度（FontAlpha）  | 文字ウォーターマークの中の文字の透明度（0～100%）。                         |

コンソールを介して（具体的な操作は [テンプレート設定](https://intl.cloud.tencent.com/document/product/266/14059#.E6.B0.B4.E5.8D.B0.E6.A8.A1.E6.9D.BF)を参照）、または [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34163)を呼び出して、 カスタマイズしたウォーターマークテンプレートを作成し、管理することができます。

## タスクの開始

ウォーターマークの刻印にはトランスコードタスクを開始する必要があり、「サーバーAPIから直接開始」、「コンソールから直接開始」、「アップロード時に実行したいタスクを指定」の3種類の方法があります。詳細内容は、ビデオ処理の [タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask)をご参照ください。

以下は、各種方式のウォーターマーク付きトランスコードタスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) の呼び出しによるタスク開始：リクエストの中の`MediaProcessTask.TranscodeTaskSet`パラメータで [ビデオコンテンツ審査テンプレート](#sy) のテンプレートIDを指定します。
* コンソールでのビデオに対するタスクの開始：コンソールで[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でトランスコーディング時に刻印するウォーターマークの目標仕様を設定します。コンソールでこのタスクフローを使用して[ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33890)します。
* サーバーからのアップロード時にタスクを指定：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でトランスコード時に刻印するウォーターマークの目標仕様を設定します。[アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0)の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定：コンソール で[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でトランスコード時に刻印するウォーターマークの目標仕様を設定します。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でトランスコード時に刻印するウォーターマークの目標仕様を設定します。コンソールを介してビデオをアップロードし、[【アップロードと同時にビデオに対する処理操作を実行】](https://intl.cloud.tencent.com/document/product/266/33890)を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。

## 結果の取得

ウォーターマークのトランスコードタスクの開始後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) 待ちおよび同期の [タスクの確認](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) の2種類の方式でスクリーンキャプチャタスクの実行結果を取得できます。以下は、ウォーターマークのトランスコードタスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

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
                "Type":"Transcode",
                "TranscodeTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":220,
                        "WatermarkSet": [
                            {
                                "Definition": 23120
                            }
                        ]
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20.m3u8",
                        "Size":63120997,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Height":1086,
                        "Width":1920,
                        "Bitrate":513402,
                        "Md5":"084d403c73930ca2f835679af1f37bd3",
                        "Duration":60,
                        "VideoStreamSet":[
                            {
                                "Bitrate":473101,
                                "Codec":"h264",
                                "Fps":24,
                                "Height":480,
                                "Width":640
                            }
                        ],
                        "AudioStreamSet":[
                            {
                                "Bitrate":48581,
                                "Codec":"aac",
                                "SamplingRate":44100
                            }
                        ],
                        "Definition":220
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

コールバックの結果の中で、`ProcedureStateChangeEvent.MediaProcessResultSet`に`Type`が`Transcode`となっている結果が1つあります。トランスコーディングの仕様`Definition`は220で、トランスコーディングと同時にウォーターマークを刻印します。ウォーターマークの仕様`Definition`は23120です。
