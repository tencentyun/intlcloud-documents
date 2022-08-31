ビデオコンテンツ分析は、AIの力を借りてオーディオビデオコンテンツに対してインテリジェントな分析を行う機能であり、オフラインタスクです。オーディオビデオコンテンツ分析を使用することで、ビデオのクラシフィケーション（分類）、タグづけ、カバー画像のキャプチャなどに対してインテリジェントなアドバイスを与え、ビデオプラットフォームでビデオを的確かつ効率的に管理ができるようにサポートします。

オーディオビデオコンテンツ分析には、以下の機能が含まれます。

| 機能名 | 説明 |
| -- | -- |
| インテリジェントクラシフィケーション | ビデオがどのカテゴリーに属するかを知らせます。現在10余りのタイプがあり、<br/>ニュース、エンターテインメント、ゲーム、テクノロジー、グルメ、スポーツ、旅行、アニメ漫画、ダンス、ミュージック、映画TV、自動車などがあります。 |
| インテリジェントタグ | ビデオに付けられるタグについてお知らせします。現在、計3000種余りのタグがあり、例えば、<br/>ゲーム、交通手段、ミュージシャン、レース、ペット、ドラム、自転車、World of Warcraft、コンピューター、学校、ジャケットなどがあります。<br/>  |
| インテリジェントカバー画像 | ビデオの中から1枚または何枚かのスクリーンキャプチャを選定し、カバー画像としての採用を推奨します。  |
| フレーム別インテリジェントタグ | ビデオの1フレームの画面ごとに付けられるタグについてお知らせします。現在、計1000種余りのタグがあり、例えば、<br/>モダンダンス、水上スポーツ、ステーキ、ベビー、子猫、一年生植物、駆逐艦、漫画、芝生、結婚衣装、多機能ホール、パスポートなどがあります。 |

## [](id:sh)オーディオビデオコンテンツ分析テンプレート

オーディオビデオコンテンツ分析のパラメータによって、分析タスクで具体的にどの項目の分析操作を実行するかを制御することができます。VODではオーディオビデオコンテンツ分析テンプレートを使用して、インテリジェント分析のパラメータグループを表示します。

- インテリジェントクラシフィケーションのアクティブ化の有無。
- インテリジェントタグのアクティブ化の有無。
- インテリジェントカバー画像のアクティブ化の有無。
- フレーム別インテリジェントタグのアクティブ化の有無。

一般的な操作の組み合わせを対象に、Video on Demandでは、[プリセットオーディオビデオコンテンツ分析テンプレート](https://intl.cloud.tencent.com/document/product/266/33932)を提供しています。その他、[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34170)を呼び出してカスタマイズしたオーディオビデオコンテンツ分析テンプレートを作成し、管理することができます。

## タスクの開始

オーディオビデオコンテンツ分析タスクの開始には、「サーバーAPIから直接開始」、「コンソールから直接開始」、「アップロード時に実行したいタスクを指定」の3種類の方法があります。詳細内容は、ビデオ処理の[タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。

以下は、各方法のオーディオビデオコンテンツ分析タスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)の呼び出しによるタスク開始：リクエストの中の`AiAnalysisTask`パラメータで[オーディオビデオコンテンツ分析テンプレート](#sh)のテンプレートIDを指定します。
* サーバーAPI[ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123)の呼び出しによるタスク開始：リクエストの中の`AiAnalysisTask`パラメータで[オーディオビデオコンテンツ分析テンプレート](#sh)のテンプレートIDを指定します。
* コンソールでのビデオに対するタスク開始：[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34167)を呼び出してタスクフローを作成し、タスクフローの中でオーディオビデオコンテンツ分析タスクを設定します（`MediaProcessTask.AiAnalysisTask`の中で指定）。コンソールでこのタスクフローを使用して[ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33892)します。
* サーバーからのアップロード時にタスクを指定：[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34167)を呼び出してタスクフローを作成し、タスクフローの中でオーディビデオコンテンツ分析タスクを設定します（`MediaProcessTask.AiAnalysisTask`の中で指定）。[アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120) の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定：[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34167)を呼び出してタスクフローを作成し、タスクフローの中でオーディビデオコンテンツ分析タスクを設定します（`MediaProcessTask.AiAnalysisTask`の中で指定）。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード：[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34167)を呼び出してタスクフローを作成し、タスクフローの中でオーディオビデオコンテンツ分析タスクを設定します（`MediaProcessTask.AiAnalysisTask`の中で指定）。コンソールを介してビデオをアップロードし、[アップロードと同時にビデオに対する処理操作を実行](https://intl.cloud.tencent.com/document/product/266/33890)を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。

## 結果の取得

オーディオビデオコンテンツ分析タスクを開始した後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931)または同期の[タスク確認](https://intl.cloud.tencent.com/document/product/266/33931)の2種類の方式でビデオコンテンツ分析タスクの実行結果を取得できます。以下は、ビデオコンテンツ分析タスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

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
        "AiAnalysisResultSet":[
            {
                "Type":"Classification",
                "ClassificationTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "ClassificationSet":[
                            {
                                "Classification":"動物",
                                "Confidence":80
                            },
                            {
                                "Classification":"旅行",
                                "Confidence":34
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Cover",
                "CoverTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "CoverSet":[
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg",
                                "Confidence":79
                            },
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg",
                                "Confidence":70
                            },
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg",
                                "Confidence":66
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Tag",
                "TagTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "TagSet":[
                            {
                                "Tag":"馬",
                                "Confidence":34
                            },
                            {
                                "Tag":"鳥",
                                "Confidence":27
                            },
                            {
                                "Tag":"植物",
                                "Confidence":13
                            },
                            {
                                "Tag":"ビーチ",
                                "Confidence":11
                            }
                        ]
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

コールバックの結果の中で、`ProcedureStateChangeEvent.AiAnalysisResultSet`に`Type`が`Classification`、`Cover`、`Tag`の3種類の分析結果がありますが、それぞれビデオインテリジェントクラシフィケーション、ビデオインテリジェントカバー画像、ビデオインテリジェントタグを表します。

* `Type`が`Classification`の結果では、`Output.ClassificationSet`の信頼度が最も高いカテゴリーが`動物`、その次のカテゴリーが`旅行`と示されています。
* `Type`が`Cover`の結果`Output.CoverSet`には、3つの採用を推奨するカバー画像が示されています。`CoverUrl`がカバー画像に対応するダウンロードアドレスです。
* `Type`が`Tag`の結果`Output.TagSet`には、4つの採用を推奨するビデオのタグが示され、信頼度の順に上から下へ配列されています。


