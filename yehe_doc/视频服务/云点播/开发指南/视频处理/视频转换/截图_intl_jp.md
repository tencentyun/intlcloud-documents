スクリーンキャプチャはビデオの特定の位置の映像を切り取り、画像を生成するプロセスであり、オフラインタスクです。VODでは次のタイプのスクリーンキャプチャを提供しています。
- 指定タイムポイントのスクリーンキャプチャ：1組のタイムポイントを指定し、これらの時タイムポイントのビデオの画像を切り取ります。
- サンプリングスクリーンキャプチャ：同じ時間間隔でビデオから複数枚の画像を切り取ります。
- 1枚の画像を切り取りカバー画像を作成：1つのタイムポイントを指定してスクリーンキャプチャを行い、そのURLをメディアリソースのシステムの中で当該ビデオのカバー画像にします。
- スプライトイメージの切り取り：同じ時間間隔でビデオから複数枚の小さな画像を切り取り、組み合わせてやや大きめの画像（スプライトイメージ）を作成します。

スクリーンキャプチャ機能を使用すれば、次のようなユースケースに対応できます。
- ビデオのためのカバー画像を生成：ビデオのスクリーンキャプチャを使用してビデオのカバー画像を作成します。
- サムネイル：スプライトイメージは複数の小さな画像（サムネイル）を埋め込んだ大きな画像で、ビデオの概要を表現するためによく使われます。
- プレビューの再生：スプライトイメージにVTTファイルを組み合わせることで、プレーヤーのプログレスバー上のプレビュー効果を実現できます。
<span id = "jt"></span>
## スクリーンキャプチャテンプレート


スクリーンキャプチャの目標仕様。スクリーンキャプチャのファイル形式、スクリーンキャプチャの幅と高さなどのパラメータが含まれます。VODではスクリーンキャプチャテンプレートを使用してスクリーンキャプチャのパラメータグループを表します。スクリーンキャプチャテンプレートによって、次のスクリーンキャプチャ関連パラメータを指定することができます。

### タイムポイントスクリーンキャプチャテンプレート

タイムポイントスクリーンキャプチャテンプレートは、「指定タイムポイントスクリーンキャプチャ」と「1枚の画像を切り取りカバー画像を作成」の2種類のタスクに用います。

| パラメータ                 | 説明                                                         |
| -------------------- | ------------------------------------------------------------ |
| 形式（Format）       | スクリーンキャプチャのファイル出力形式。現在はJPGのみをサポートしています。                         |
| 幅（Width）        | スクリーンキャプチャの幅。範囲は128px～4096px。                             |
| 高さ（Height）     | スクリーンキャプチャの高さ。範囲は128px～4096px。                             |
| 塗りつぶしタイプ（FillType） | スクリーンキャプチャの幅と高さの比率とオリジナルビデオの幅と高さの比率が異なるときに、スクリーンキャプチャの処理方式が、「塗りつぶし」になります。一般的な塗りつぶしタイプには次のようなものがあります。<li>引き伸ばし：画像を引き伸ばして、フレーム全体に広げます。画像は「圧縮されたり」、「長く延びたり」します。</li><li>黒で補填：画像の幅と高さの比率は変えず、縁の余った部分は黒で補填します。</li><li>白で補填：画像の幅と高さの比率は変えず、縁の余った部分は白で補填します。</li><li>ガウシアンぼかし：画像の幅と高さの比率は変えず、縁の余った部分はガウシアンぼかしを入れて画面を埋めます。</li> |

一般的な仕様を対象に、VODでは [プリセットのタイムポイントスクリーンキャプチャテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#screenshot01)を提供しています。その外、コンソールを介して、カスタマイズしたスクリーンキャプチャテンプレートを作成し、管理することができます。具体的な操作は、 [テンプレート設定](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF)をご参照ください。

### サンプリングスクリーンキャプチャテンプレート

サンプリングスクリーンキャプチャテンプレートは、「サンプリングスクリーンキャプチャ」のタスクに使用します。

| パラメータ                   | 説明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 形式（Format）       | スクリーンキャプチャのファイル出力形式。現在はJPGのみをサポートしています。                         |
| 幅（Width）        | スクリーンキャプチャの幅。範囲は128px～4096px。                             |
| 高さ（Height）     | スクリーンキャプチャの高さ。範囲は128px～4096px。                             |
| サンプリング方式（SampleType） | サンプリング方式は2種類に分かれます。<li>パーセンテージによるサンプリング：例えば、5%の間隔でサンプリングした場合、生成されるスクリーンキャプチャの枚数は20枚になります。</li><li>時間間隔によるサンプリング：例えば、10sの間隔でサンプリングした場合、スクリーンキャプチャの枚数はビデオの長さによって決まります。</li> |
| サンプリング間隔（Interval）   | サンプリング間隔の長さ：<li>パーセンテージによるサンプリングの場合、間隔はパーセンテージになります。</li><li>時間間隔によるサンプリングの場合、間隔は秒になります。</li> |
| 塗りつぶしタイプ（FillType） | スクリーンキャプチャの幅と高さの比率とオリジナルビデオの幅と高さの比率が異なるときに、スクリーンキャプチャの処理方式が、「塗りつぶし」になります。一般的な塗りつぶしタイプには次のようなものがあります。<li>引き伸ばし：画像を引き伸ばして、フレーム全体に広げます。画像は「圧縮されたり」、「長く延びたり」します。</li><li>黒で補填：画像の幅と高さの比率は変えず、縁の余った部分は黒で補填します。</li><li>白で補填：画像の幅と高さの比率は変えず、縁の余った部分は白で補填します。</li><li>ガウシアンぼかし：画像の幅と高さの比率は変えず、縁の余った部分はガウシアンぼかしを入れて画面を埋めます。</li> |

一般的な仕様を対象に、VODでは [プリセットのサンプリングスクリーンキャプチャテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#screenshot02)を提供しています。その外、コンソールを介して、カスタマイズしたスクリーンキャプチャテンプレートを作成し、管理することができます。具体的な操作は、 [テンプレート設定](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF)をご参照ください。

### スプライトイメージテンプレート

スプライトイメージテンプレートは、「スプライトイメージのスクリーンキャプチャ」タスクに使用します。

| パラメータ                   | 説明                                       |
| ---------------------- | ------------------------------------------ |
| 形式（Format）         | スプライトイメージのファイル出力形式。現在はJPGのみをサポートしています。     |
| 小さい画像の幅（Width）      | スプライトイメージの中の小さい画像の幅。                       |
| 小さい画像の高さ（Height）   | スプライトイメージの中の小さい画像の高さ。                       |
| 小さい画像の行数（Rows）       | 1枚の大きな図の中にある小さい図の行数。                   |
| 小さい画像の列数（Columns）    | 1枚の大きな図の中にある小さい画像の列数。                   |
| サンプリング方式（SampleType） | 小さい画像のサンプリング方式。現在は時間間隔によるサンプリングのみをサポートしています。 |
| サンプリング間隔（Interval）   | どの位の間隔で1枚の小さい画像をサンプリングするかのサンプリング間隔。     |

>!
>- Width × Columns は128px～4096pxの間にする必要があります（大きい図の幅が128px～4096pxの間）。
>- Height × Rows は128px～4096pxの間にする必要があります（大きい図の高さが128px～4096pxの間）。

一般的な仕様を対象に、VODでは [プリセットのスプライトイメージスクリーンキャプチャテンプレート](https://intl.cloud.tencent.com/document/product/266/33932#screenshot03)を提供しています。その外、コンソールを介して、カスタマイズしたスクリーンキャプチャテンプレートを作成し、管理することができます。具体的な操作は、 [テンプレート設定](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF)をご参照ください。

## タスクの開始

スクリーンキャプチャタスクの開始には、「サーバーAPIから直接開始」、「コンソールから直接開始」、「アップロード時に実行したいタスクを指定」の3種類の方法があります。詳細内容は、ビデオ処理の [タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask)をご参照ください。

以下は、各種方式のスクリーンキャプチャタスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) の呼び出しによるタスク開始：リクエストの中の`MediaProcessTask.SnapshotByTimeOffsetTaskSet`パラメータで [スクリーンキャプチャテンプレート](#sh) のテンプレートIDを指定します。
* コンソールでのビデオに対するタスクの開始：コンソールで[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でターゲットのスクリーンキャプチャの仕様を設定します。コンソールでこのタスクフローを使用して[ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33890)します。
* サーバーからのアップロード時にタスクを指定：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でターゲットのスクリーンキャプチャの仕様を設定します。[アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0)の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定：コンソール で[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でターゲットのスクリーンキャプチャの仕様を設定します。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でターゲットのスクリーンキャプチャの仕様を設定します。コンソールを介してビデオをアップロードし、[アップロードと同時にビデオに対する処理操作を実行](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4)を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。

## 結果の取得

スクリーンキャプチャタスクの開始後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) 待ちおよび同期の [タスクの確認](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) の2種類の方式でスクリーンキャプチャタスクの実行結果を取得できます。以下は、スクリーンキャプチャタスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

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
                "Type":"SnapshotByTimeOffset",
                "SnapshotByTimeOffsetTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10,
                        "Definition":[3, 6, 9]
                    },
                    "Output":{
                        "Definition":10,
                        "PicInfoSet": [
                            {
                                "TimeOffset":3,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                            },
                            {
                                "TimeOffset":6,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg"
                            },
                            {
                                "TimeOffset":9,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg"
                            }
                        ]
                    }
                }
            },
            {
                "Type":"SampleSnapshot",
                "SampleSnapshotTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "PicInfoSet": [
                            {
                                "TimeOffset":6,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                            },
                            {
                                "TimeOffset":12,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg"
                            },
                            {
                                "TimeOffset":18,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg"
                            },
                            {
                                "TimeOffset":24,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx4.jpg"
                            },
                            {
                                "TimeOffset":30,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx5.jpg"
                            },
                            {
                                "TimeOffset":36,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx6.jpg"
                            },
                            {
                                "TimeOffset":42,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx7.jpg"
                            },
                            {
                                "TimeOffset":48,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx8.jpg"
                            },
                            {
                                "TimeOffset":54,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx9.jpg"
                            },
                            {
                                "TimeOffset":60,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx10.jpg"
                            }
                        ]
                    }
                }
            },
            {
                "Type":"ImageSprites",
                "ImageSpriteTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "Height":80,
                        "Width":142,
                        "TotalCount":1,
                        "ImageUrlSet":[
                            "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                        ],
                        "WebVttUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
                    }
                }
            },
            {
                "Type":"CoverBySnapshot",
                "CoverBySnapshotTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10,
                        "PositionType":"Time",
                        "PositionValue":0
                    },
                    "Output":{
                        "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.jpg"
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

コールバックの結果の中で、`ProcedureStateChangeEvent.MediaProcessResultSet`に`Type`が`SnapshotByTimeOffset`、`SampleSnapshot`、`ImageSprites`、`CoverBySnapshot`の結果があり、それぞれタイムポイントスクリーンキャプチャ、サンプリングスクリーンキャプチャ、スプライトイメージ切り取り、1枚の画像を切り取りカバー画像を作成の数種類等のスクリーンキャプチャタスクを表しています。
