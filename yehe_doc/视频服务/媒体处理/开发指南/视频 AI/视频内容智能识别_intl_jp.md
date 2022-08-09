ビデオコンテンツインテリジェント認識は、AIを使用して、ビデオのコンテンツに対してインテリジェントな認識を行う機能です。ビデオに対しコンテンツのインテリジェント認識タスクを実行すると、実行結果には、インテリジェント認識の評点、インテリジェント認識アドバイス、疑わしいビデオの断片などが含まれます。結果の中の「インテリジェント認識アドバイス」に基づいて、ビデオの公開を許可するかどうかを決定でき、健全なソーシャルネットワーク環境の構築を支援することができます。

## 分析結果
ビデオコンテンツインテリジェント認識では、ビデオ画面、ASR文字、OCR文字の3種類を対象として認識を行います。詳細は下表のとおりです。

<table>
<tr>
<th style="text-align:center">対象</th><th >操作</th><th>説明</th>
</tr><tr>
<td rowspan=4 style="text-align:center">ビデオ画面<br>（人および物体）</td>
</tr><tr>
<td>不快感を与える情報</td>
<td>ビデオ画面に対して不快感を与える情報の検査を行います。検査内容には次が含まれます。
    <li>vulgar：低俗</li>
    <li>intimacy：親密な行為</li>
    <li>sexy：セクシー</li>
</td>
</tr><tr>
<td>不適切と感じる情報</td>
<td>ビデオ画面に対して不適切と感じる情報の検査を行います。検査内容には次が含まれます。
    <li>bloody：血生臭い画面</li>
    <li>explosion：爆発・火災</li>
    <li>violation_photo：違法な画像</li>
    <li>guns：武器・銃</li>
</td>
</tr><tr>
</tr><tr>
<td rowspan=2 style="text-align:center">ASR文字<br>（音声の中の文字）</td>
<td>不快感を与える情報
<td>音声の中の文字に対して不快感を与える情報の検査を行い、疑わしいキーワードを認識します</td>
</tr><tr>
<td>不適切と感じる情報</td>
<td>音声の中の文字に対して不適切と感じる情報の検査を行い、疑わしいキーワードを認識します</td>
</tr><tr>
<td rowspan=2 style="text-align:center">OCR文字<br>（画面の中の文字）</td>
<td>不快感を与える情報</td>
<td>画面の中の文字に対して不快感を与える情報の検査を行い、疑わしいキーワードを認識します</td>
</tr><tr>
<td>不適切と感じる情報</td>
<td>画面の中の文字に対して不適切と感じる情報の検査を行い、疑わしいキーワードを認識します</td>
</tr>
</table>

#### パラメータの説明

| フィールド     | タイプ   | 意味                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| confidence | Float  | インテリジェント認識の評点（0 - 100）、評点が高いほど、疑わしさが大きくなります                |
| suggestion | String | インテリジェント認識アドバイスには、pass、review、blockの3種類があります。<ul style="margin:0;"><li >pass：疑わしさは高くありません。そのまま適合とすることを推奨します</li><li>review：疑わしさが高めです。人による再審査を推奨します</li><li>block：疑わしさが非常に高いため、不適合とすることを推奨します</li></ul> |
| segments   | Array  | ビデオに疑わしい部分がある場合、ビデオの中のどの部分に不適切なコンテンツの疑いがあるのかを具体的に特定できるようにします         |



## タスクの開始
### 操作説明
ビデオコンテンツインテリジェント認識タスクの開始には、「APIを介して手動で開始」と「アップロードを介して自動的にトリガー」という2つの方法があります。

- **APIを介して手動で開始：**[ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/1041/33640)インターフェースを呼び出し、リクエストの中のAiContentReviewTask パラメータで[ビデオコンテンツインテリジェント認識テンプレート](#sh)のテンプレートIDを指定します。
- **アップロードを介して自動的にトリガー：**コンソールで[ワークフローを作成](https://intl.cloud.tencent.com/document/product/1041/33485)し、コンテンツインテリジェント認識を有効にした後、 ワークフローにバインドされたトリガーディレクトリにビデオをアップロードします。 

[](id:sh)
### ビデオコンテンツインテリジェント認識テンプレートの作成
ビデオコンテンツインテリジェント認識パラメータによって、インテリジェント認識タスクで具体的にどの項目のインテリジェント認識操作を実行するかを制御できます。MPSでは、ビデオコンテンツインテリジェント認識テンプレートを使用してインテリジェント認識パラメータグループを表示し、ビデオコンテンツインテリジェント認識テンプレートによって、インテリジェント認識タスクにおける以下のいずれかまたはいくつかの操作項目の実行を指定できます。
- ビデオ画面の不快感を与える情報に対する認識
- ビデオ画面の不適切と感じる情報に対する認識
- ASR文字の不快感を与える情報に対する認識
- ASR文字の不適切と感じる情報に対する認識
- OCR文字の不快感を与える情報に対する認識
- OCR文字の不適切と感じる情報に対する認識

一般的な操作の組み合わせを対象に、MPSでは、[プリセットのビデオコンテンツインテリジェント認識テンプレート](https://intl.cloud.tencent.com/document/product/1041/33476)を提供しています。その他、 [サーバーAPI](https://intl.cloud.tencent.com/document/product/1041/33675)を呼び出してカスタマイズしたビデオコンテンツインテリジェント認識テンプレートを作成し、管理することもできます。

## 結果の取得
ビデオコンテンツインテリジェント認識タスクを開始した後、同期的な[タスクの確認](https://intl.cloud.tencent.com/document/product/1041/33497)の実行、および非同期的な[結果通知](https://intl.cloud.tencent.com/document/product/1041/33499)の待機という2種類の方式で、ビデオコンテンツインテリジェント認識タスクの実行結果を取得できます。

以下は、コンテンツインテリジェント認識タスクの開始後、「タスクの確認」方式で取得する結果のサンプルです（値がnullのフィールドは省略）。
```json
{
    "TaskType":"WorkflowTask",
    "Status":"FINISH",
    "CreateTime":"2019-07-16T06:21:27Z",
    "BeginProcessTime":"2019-07-16T06:21:28Z",
    "FinishTime":"2019-07-16T06:21:46Z",
    "WorkflowTask":{
        "TaskId":"2356768367-WorkflowTask-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "InputInfo":{
            "Type":"COS",
            "CosInputInfo":{
                "Bucket":"MyVideoBucket-235303****",
                "Region":"ap-beijing",
                "Object":"/input/AnimalWorld.mp4"
            }
        },
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

        ],
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
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx1.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
                            },
                            {
                                "StartTimeOffset":16.5,
                                "EndTimeOffset":18,
                                "Confidence":80,
                                "Suggestion":"review",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx2.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
                            },
                            {
                                "StartTimeOffset":41,
                                "EndTimeOffset":49,
                                "Confidence":97,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx3.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
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
        "AiAnalysisResultSet":[

        ],
        "AiRecognitionResultSet":[

        ]
    },
    "TasksPriority":0,
    "SessionId":"",
    "SessionContext":"",
    "RequestId":"xxx-xxx-xxx"
}
```

確認結果の中の、`WorkflowTask.AiContentReviewResultSet`にTypeがPorn、Terrorism、Politicalという3タイプのインテリジェント認識結果があります。

- TypeがPornの結果では、`Output.Suggestion`がblockとなっており、インテリジェント認識の可能性が高いため、不適合とすることを推奨しています。インテリジェント認識の信頼度は98点、インテリジェント認識の原因はsexy（セクシー）となっています。
- TypeがPornの結果の`Output.SegmentSet`には、インテリジェント認識によって疑いがあると判断された3か所のビデオ部分が示されています。各部分のStartTimeOffsetとEndTimeOffsetは、その部分の開始・終了時間を表します。
- TypeがTerrorismとPoliticalの結果には、ビデオに不適切なコンテンツの疑いがないことが示されています。
