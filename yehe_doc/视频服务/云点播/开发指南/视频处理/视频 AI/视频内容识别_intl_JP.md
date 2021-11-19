ビデオコンテンツ認識は、AIの力を借りてビデオコンテンツに対してインテリジェントな認識を行う機能であり、オフラインタスクです。ビデオコンテンツ認識を使用することで、ビデオ画面の中の文字、オープニング・エンディング、音声の中の文字を認識することができ、このビデオコンテンツ認識の結果に基づき、ビデオを的確かつ効果的に管理することができます。ビデオコンテンツ認識には以下の機能が含まれます。

| 機能名 | 機能説明 | 活用例 |
| -- | -- | -- |
| 音声全文認識 | 音声の中に登場するすべての文字を認識します | <li>スピーチのコンテンツのための字幕生成</li><li>ビデオの音声コンテンツに対するデータ分析</li>  |
| テキスト全文認識 | 画面の中に登場するすべての文字を認識します | 画面の中の文字に対するデータ分析  |
| 音声キーワード認識 | 音声の中に存在するキーワードを認識します | <li>音声の中のセンシティブワードの調査</li><li>音声の中に登場する特定のキーワードのサーチ</li>  |
| テキストキーワード認識 | 画面の中に存在するキーワードを認識します | <li>画面の中のセンシティブワードの調査</li><li>画面の中に登場する特定のキーワードのサーチ</li>  |
| ビデオの始まりと終わりの認識 | ビデオの始まりと終わりを認識します | <li>プログレスバーの中の始まり、終わり、本編の位置のタグ付け</li><li>ビデオの前後のムダな部分を一括除去</li> |


一部のコンテンツ認識機能は、素材コーパスに依存する必要があります。これにはパブリックコーパスとカスタマイズコーパスの2種類があります。

* パブリックコーパス：VODのプリセットの素材コーパス。
* カスタマイズコーパス：ユーザー自身で作成、管理する素材コーパス。

| 認識タイプ | パブリックコーパス | カスタマイズコーパス |
| -- | -- | -- |
| 音声単語認識 | 現時点ではサポートしていません| サポートしています。[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/37583) を呼び出してキーワードのコーパスを管理します|
| 文字単語認識 | 現時点ではサポートしていません| サポートしています。[サーバーAPI](https://intl.cloud.tencent.com/document/product/266/37583) を呼び出してキーワードのコーパスを管理します


## [](id:sh)ビデオコンテンツ認識テンプレート

ビデオコンテンツ認識は複数の認識機能を統合しており、パラメータによって細かく制御する必要があります。制御のターゲットは次となります。

* 有効にする認識タイプ：コンテンツ認識の中のどの機能を有効にするか。
* 使用する素材コーパス：インテリジェント認識に対して使用するのはパブリックコーパスかカスタマイズコーパスか。
* フィルタリング点数の指定：インテリジェント認識の信頼度が何点に達したら結果を戻すか。
* フィルタリングタグの指定：インテリジェント認識のタグがどの範囲にある結果を戻すかを指定。

一般的な操作の組み合わせを対象に、VODでは、[プリセットのビデオコンテンツ認識テンプレート](https://intl.cloud.tencent.com/document/product/266/33932)を提供しています。その他、 [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/37568) を呼び出してカスタマイズしたビデオコンテンツ認識テンプレートを作成し、管理することができます。-->

## タスクの開始

ビデオコンテンツ認識タスクの開始には、「サーバーAPIから直接開始する」、「コンソールから直接開始する」、「アップロード時に実行したいタスクを指定する」の3種類の方法があります。具体的な内容は、ビデオ処理の[タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。

以下は、各方法のビデオコンテンツ認識タスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) の呼び出しによるタスク開始：リクエストの中の`AiRecognitionTask`パラメータで [ビデオコンテンツ認識テンプレート](#sh) のテンプレートIDを指定します。
* サーバーAPI[ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123) の呼び出しによるタスク開始：リクエストの中の`AiRecognitionTask`パラメータで [ビデオコンテンツ認識テンプレート](#sh) のテンプレートIDを指定します。
* コンソールでのビデオに対するタスク開始： [サーバーAPI](https://intl.cloud.tencent.com/zh/document/product/266/37583) を呼び出してタスクフローを作成し、タスクフローの中でビデオコンテンツ認識タスクを設定します（`MediaProcessTask.AiRecognitionTask`の中で指定）。コンソールでこのタスクフローを使用して [ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33892)します。
* サーバーからのアップロード時にタスクを指定： [サーバーAPI](https://intl.cloud.tencent.com/zh/document/product/266/37583) を呼び出してタスクフローを作成し、タスクフローの中でビデオコンテンツ認識タスクを設定します（`MediaProcessTask.AiRecognitionTask`の中で指定）。[アップロードの申請](https://intl.cloud.tencent.com/zh/document/product/266/34120) の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定： [サーバーAPI](https://intl.cloud.tencent.com/zh/document/product/266/37583) を呼び出してタスクフローを作成し、タスクフローの中でビデオコンテンツ認識タスクを設定します（`MediaProcessTask.AiRecognitionTask`の中で指定）。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922) の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード： [サーバーAPI](https://intl.cloud.tencent.com/zh/document/product/266/37583) を呼び出してタスクフローを作成し、タスクフローの中でビデオコンテンツ認識タスクを設定します（`MediaProcessTask.AiRecognitionTask`の中で指定）。コンソールを介してビデオをアップロードし、 [アップロードと同時にビデオに対する処理操作を実行](https://intl.cloud.tencent.com/document/product/266/33890) を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。

## 結果の取得

ビデオコンテンツ認識タスクを開始した後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931)または同期の [タスク確認](https://intl.cloud.tencent.com/document/product/266/33931)の2種類の方式でビデオコンテンツ認識タスクの実行結果を取得できます。以下は、ビデオコンテンツ認識タスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1400155958-Procedure-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "FileId":"5285890784363430543",
        "FileName":"名作選",
        "FileUrl":"http://1400155958.vod2.myqcloud.com/xxx/xxx/aHjWUx5Xo1EA.mp4",
        "MetaData":{
            "AudioDuration":243,
            "AudioStreamSet":[
                {
                    "Bitrate":125599,
                    "Codec":"aac",
                    "SamplingRate":48000
                }
            ],
            "Bitrate":1459299,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":243,
            "Height":1080,
            "Rotate":0,
            "Size":44583593,
            "VideoDuration":243,
            "VideoStreamSet":[
                {
                    "Bitrate":1333700,
                    "Codec":"h264",
                    "Fps":29,
                    "Height":1080,
                    "Width":1920
                }
            ],
            "Width":1920
        },
        "AiRecognitionResultSet":[
            {
                "Type":"FaceRecognition",
                "FaceRecognitionTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "ResultSet":[
                            {
                                "Id":183213,
                                "Type":"Default",
                                "Name":"張三",
                                "SegmentSet":[
                                    {
                                        "StartTimeOffset":10,
                                        "EndTimeOffset":12,
                                        "Confidence":97,
                                        "AreaCoordSet":[
                                            830,
                                            783,
                                            1030,
                                            599
                                        ]
                                    },
                                    {
                                        "StartTimeOffset":12,
                                        "EndTimeOffset":14,
                                        "Confidence":97,
                                        "AreaCoordSet":[
                                            844,
                                            791,
                                            1040,
                                            614
                                        ]
                                    }
                                ]
                            },
                            {
                                "Id":236099,
                                "Type":"Default",
                                "Name":"lisi",
                                "SegmentSet":[
                                    {
                                        "StartTimeOffset":120,
                                        "EndTimeOffset":122,
                                        "Confidence":96,
                                        "AreaCoordSet":[
                                            579,
                                            903,
                                            812,
                                            730
                                        ]
                                    }
                                ]
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

コールバックの結果の中で、`ProcedureStateChangeEvent.AiRecognitionResultSet`に`Type`が`FaceRecognition`となる認識結果があります。

`Type`が`FaceRecognition`の結果では、`Output.ResultSet`の中に認識した人物が2人含まれており、それぞれ`張三`と`lisi`となっています。`SegmentSet`にはインテリジェント認識がビデオに登場した時間帯（`StartTimeOffset`と`EndTimeOffset`により確定）および画面の中の座標（`AreaCoordSet`により確定）が示されています。


