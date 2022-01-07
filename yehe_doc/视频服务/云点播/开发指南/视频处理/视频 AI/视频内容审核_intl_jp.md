ビデオコンテンツ審査は、AIの力を借りて、ビデオのコンテンツに対してインテリジェントな審査を行う機能であり、オフラインタスクです。タスクの実行結果の中には、審査の評点、審査のアドバイス、疑わしいビデオの断片などが含まれています。「審査のアドバイス」にもとづき、ビデオ管理者はビデオの公開を許可するかを決定でき、不正なビデオによる法的リスクやブランドのダメージを効果的に回避することができます。

VODはビデオ画面、ASRテキスト、OCRテキストの3つのオブジェクトに対してスマート認識を行うことができ、その操作には不快感を与える情報、危険を感じる情報、不適切と感じる情報を含みます。

<table>
    <tr>
        <th style="width:20%">
            オブジェクト
        </th>
        <th style="width:10%">
            操作
        </th>
        <th>
            説明
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            ビデオ画面（人および物体）
        </td>
    </tr>
    <tr>
        <td>
            不快感を与える情報
        </td>
        <td>
				    ビデオ画面の不快感を与える情報に対する認識を行います。認識内容には以下を含みます。
				    <li>vulgar：低俗</li>
				    <li>intimacy：親密な行為</li>
				    <li>sexy：セクシー</li>
        </td>
    </tr>
    <tr>
        <td>
            危険を感じる情報
        </td>
        <td>
				    ビデオ画面の危険を感じる情報に対する認識を行います。認識内容には以下を含みます。
				    <li>militant：武装グループ</li>
				    <li>guns：武器・銃</li>
				    <li>bloody：血生臭い画面</li>
				    <li>police：警察部隊</li>
				    <li>crowd：群衆</li>
        </td>
    </tr>
    <tr>
        <td>
            不適切と感じる情報
        </td>
        <td>
            ビデオ画面の不適切と感じる情報に対する認識を行います。認識内容には以下を含みます。
				    <li>violation_photo：違法な画像</li>
				    <li>politician：話題の人物</li>
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            ASR文字（音声の中の文字）
        </td>
        <td>
				    不快感を与える情報
        <td>
            音声の中の文字に対して不快感を与える情報の認識を行い、疑わしいキーワードを認識します
        </td>
    </tr>
    <tr>
        <td>
            不適切と感じる情報
        </td>
        <td>
            音声の中の文字に対して不適切と感じる情報の認識を行い、疑わしいキーワードを認識します
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            OCR文字（画面の中のテキスト）
        </td>
        <td>
				    不快感を与える情報
        </td>
        <td>
            画面の中の文字に対して不快感を与える情報の認識を行い、疑わしいキーワードを認識します
        </td>
    </tr>
    <tr>
        <td>
            不適切と感じる情報
        </td>
        <td>
            画面の中の文字に対して不適切と感じる情報の認識を行い、疑わしいキーワードを認識します
        </td>
    </tr>
</table>


| フィールド     | タイプ   | 意味                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| confidence | Float  | 審査の評点（0 - 100）、評点が高いほど、疑わしさが大きくなります                |
| suggestion | String | 審査のアドバイスには、pass、review、block の3種類があります。<ul><li>pass：疑わしさは高くありません。審査通過とします</li><li>review：疑わしさが高めです。人による再審査を推奨します</li><li>block：疑わしさが非常に高いため、直接ブロックすることを推奨します</li></ul> |
| segments   | Array  | ビデオに疑わしい部分がある場合、ビデオの中のどの部分に違法性の疑いがあるのかを具体的に特定できるようにします         |

## [](id:sh)ビデオ審査テンプレート

ビデオ審査のパラメータによって、審査タスクで具体的にどの項目の審査の操作を実行するかを制御できます。VODでは、ビデオ審査テンプレートを使用して審査のパラメータグループを表示し、ビデオ審査テンプレートによって、審査タスクの中で、以下のいずれかまたはいくつかの操作項目の実行を指定できます。
- ビデオ画面の不快感を与える情報に対する認識
- ビデオ画面の危険を感じる情報に対する認識
- ビデオ画面の不適切と感じる情報に対する認識
- ASR文字の不快感を与える情報に対する認識
- ASR文字の不適切と感じる情報に対する認識
- OCR文字の不快感を与える情報に対する認識
- OCR文字の不適切と感じる情報に対する認識

一般的な操作の組み合わせを対象に、VODでは、[プリセットのビデオ審査テンプレート](https://intl.cloud.tencent.com/document/product/266/33932)を提供しています。その他、 [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/37566) を呼び出してカスタマイズしたビデオ審査テンプレートを作成し、管理することができます。

## タスクの開始

ビデオコンテンツ審査タスクの開始には、「サーバーAPIから直接開始」、「コンソールから直接開始」、「アップロード時に実行したいタスクを指定」の3種類の方法があります。詳細内容は、ビデオ処理の[タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。

以下は、各方法のビデオコンテンツ審査タスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) の呼び出しによるタスク開始：リクエストの中の`AiContentReviewTask`パラメータで [ビデオコンテンツ審査テンプレート](#sh) のテンプレートIDを指定します。
* サーバーAPI[ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123) の呼び出しによるタスク開始：リクエストの中の`AiContentReviewTask`パラメータで [ビデオコンテンツ審査テンプレート](#sh) のテンプレートIDを指定します。
* コンソールでのビデオに対するタスクの開始：コンソールで[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でビデオコンテンツ審査を有効にします。コンソールでこのタスクフローを使用して[ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33892)します。
* サーバーからのアップロード時にタスクを指定：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でビデオコンテンツ審査を有効にします。[アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0)の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定：コンソールで[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でビデオコンテンツ審査を有効にします。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922) の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でビデオコンテンツ審査を有効にします。コンソールを介してビデオをアップロードし、[アップロードと同時にビデオに対する処理操作を実行](https://intl.cloud.tencent.com/document/product/266/33890)を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。

## 結果の取得

ビデオ審査タスクを開始した後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931)または同期の [タスク確認](https://intl.cloud.tencent.com/document/product/266/33931)の2種類の方式でビデオ審査タスクの実行結果を取得できます。以下は、審査タスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。
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
        "AiContentReviewResultSet":[
            {
                "Type":"Porn",
                "PornTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":98,
                        "Suggestion":"block",
                        "Label":"sexy",
                        "SegmentSet":[
                            {
                                "StartTimeOffset":9.5,
                                "EndTimeOffset":14,
                                "Confidence":98,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx1.jpg",
                                "PicUrlExpireTimeStamp":1530005146
                            },
                            {
                                "StartTimeOffset":16.5,
                                "EndTimeOffset":18,
                                "Confidence":80,
                                "Suggestion":"review",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx2.jpg",
                                "PicUrlExpireTimeStamp":1530005146
                            },
                            {
                                "StartTimeOffset":41,
                                "EndTimeOffset":49,
                                "Confidence":97,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx3.jpg",
                                "PicUrlExpireTimeStamp":1530005146
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Terrorism",
                "TerrorismTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":0,
                        "Suggestion":"pass",
                        "SegmentSet":[

                        ]
                    }
                }
            },
            {
                "Type":"Political",
                "PoliticalTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":0,
                        "Suggestion":"pass",
                        "SegmentSet":[

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

コールバック結果の中で、`ProcedureStateChangeEvent.AiContentReviewResultSet`に`Type`が`Porn`、`Terrorism`、`Political`の3タイプの審査結果があり、それぞれビデオ画面の不快感を与える情報、ビデオ画面の危険を感じる情報、ビデオ画面の不適切と感じる情報を表しています。

* `Type`が`Porn`の結果では、`Output.Suggestion`が`block`となっており、不快感を与える情報である可能性が高いため、ブロックを推奨しています。不快感を与える情報の信頼度は98点、原因は`sexy`（セクシー）となっています。
* `Type`が`Porn`の結果の`Output.SegmentSet`には、不快感を与える情報の疑いがあると判断された3か所のビデオ部分が示されています。各部分の`StartTimeOffset`と`EndTimeOffset`は、その部分の開始・終了時間を表します。
* `Type`が`Terrorism`と`Political`の結果には、ビデオに危険を感じる情報と不適切と感じる情報の疑いがないことが示されています。


