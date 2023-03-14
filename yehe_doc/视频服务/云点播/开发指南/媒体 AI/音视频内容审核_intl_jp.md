オーディオビデオコンテンツ審査は、AIの力を借りて、オーディオビデオのコンテンツに対してインテリジェントな審査を行う機能であり、オフラインタスクです。タスクの実行結果の中には、審査の評点、審査のアドバイス、疑わしいビデオの断片などが含まれています。「審査のアドバイス」に基づき、ビデオ管理者はビデオの公開を許可するかを決定でき、不正なビデオによる法的リスクやブランドのダメージを効果的に回避することができます。

VODでは画面上の画像、画面内のテキスト、音声内のテキスト、声のコンテンツの4種類を対象に審査を行うことができます。審査タグにはポルノ、暴力・テロ、喘ぎ声があります。

<table>
    <tr>
        <th style="width:20%">
            オブジェクト
        </th>
        <th style="width:20%">
            審査タグ
        </th>
        <th>
            説明
        </th>
    </tr>
    <tr>
        <td rowspan=3>
            画面上の画像
        </td>
    </tr>
    <tr>
        <td>
            ポルノ（Porn）
        </td>
        <td>
				    ポルノ、わいせつな用語など。
        </td>
    </tr>
    <tr>
        <td>
            暴力・テロ（Terror）
        </td>
        <td>
				    暴力、血生臭いコンテンツ、テロ組織に関するコンテンツなど。
        </td>
    </tr>
		<tr>
        <td rowspan=1>
           音声
        </td>
        <td>
				    喘ぎ声（Moan）
        </td>
        <td>
            きわどい声。
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            音声内のテキスト（ASR）
        </td>
        <tr>
        <td>
            ポルノ（Porn）
        </td>
        <td>
				    ポルノ、わいせつな用語など。
        </td>
    </tr>
    <tr>
        <td>
            暴力・テロ（Terror）
        </td>
        <td>
				    暴力、血生臭いコンテンツ、テロ組織に関するコンテンツなど。
        </td>
    </tr>
        <td rowspan=3>
            画面内のテキスト（OCR）
        </td>
        <tr>
        <td>
            ポルノ（Porn）
        </td>
        <td>
				    ポルノ、わいせつな用語など。
        </td>
    </tr>
    <tr>
        <td>
            暴力・テロ（Terror）
        </td>
        <td>
				    暴力、血生臭いコンテンツ、テロ組織に関するコンテンツなど。
        </td>
    </tr>
</table>

オーディオビデオ審査結果部分のフィールドの説明：

| フィールド     | タイプ   | 意味                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| Confidence | Float  | 審査の評点（0 - 100）。評点が高いほど、疑わしさが大きくなります                |
| Suggestion | String | 審査のアドバイス。pass、review、blockの3種類があります。<ul><li>pass：疑わしさは高くありません。審査通過を推奨します</li><li>review：疑わしさが高めです。人による再審査を推奨します</li><li>block：疑わしさが非常に高いため、直接ブロックすることを推奨します</li></ul> |
| Form   | String  | 審査の形式。次の種類があります。<ul><li>Image：画面上の画像</li><li>Voice：声</li><li>OCR：画面内の文字</li><li>ASR：音声内の文字</li></ul> |
| Label   | String  | 審査タグ。次の種類があります。<ul><li>Porn：ポルノ</li><li>Terror：暴力・テロ</li><li>Moan：喘ぎ声</li></ul> |

## [](id:sh)オーディオビデオ審査テンプレート

オーディオビデオ審査のパラメータによって、審査タスクで具体的にどの審査タグを検出するかを制御できます。VODでは、ビデオ審査テンプレートを使用して審査のパラメータグループを表示し、ビデオ審査テンプレートによって、審査タスクの中で以下のどのタグ（1つまたは複数）を検出するかを指定できます。
- ポルノ（Porn）
- 暴力・テロ（Terror）
- 喘ぎ声（Moan）

一般的な操作の組み合わせを対象に、VODでは、[プリセットのオーディオビデオ審査テンプレート](https://intl.cloud.tencent.com/document/product/266/33932)を提供しています。その他、 [サーバーAPI](https://www.tencentcloud.com/document/product/266/37566)を呼び出してカスタマイズしたビデオ審査テンプレートを作成し、管理することもできます。

## タスクの開始

オーディオビデオコンテンツ審査タスクの開始には、「サーバーAPIから直接開始」、「コンソールから直接開始」、「アップロード時に実行したいタスクを指定」の3種類の方法があります。詳細内容は、ビデオ処理の[タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。

以下は、各方法のオーディオビデオコンテンツ審査タスク開始についての説明です。

* サーバーAPIによって直接開始します。サーバーAPI [ReviewAudioVideo](https://www.tencentcloud.com/document/product/266/50634)を呼び出してタスクを開始します。
* コンソールから直接開始します。コンソールガイド[オーディオビデオ審査](https://intl.cloud.tencent.com/document/product/266/33897)をご参照ください。
* サーバーからのアップロード時にタスクを指定：サーバーAPI[タスクフローテンプレートの作成](https://www.tencentcloud.com/document/product/266/34167)を呼び出し、タスクフローの中でオーディオビデオ審査タスク(`ReviewAudioVideoTask`)を起動します。[アップロードの申請](https://www.tencentcloud.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0)の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定：サーバーAPI[タスクフローテンプレートの作成](https://www.tencentcloud.com/document/product/266/34167)を呼び出し、タスクフローの中でオーディオビデオ審査タスク(`ReviewAudioVideoTask`)を起動します。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922)の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード：サーバーAPI[タスクフローテンプレートの作成](https://www.tencentcloud.com/document/product/266/34167)を呼び出し、タスクフローの中でオーディオビデオ審査タスク(`ReviewAudioVideoTask`)を起動します。コンソールでビデオをアップロードし、[アップロードと同時にビデオに対する処理操作を実行](https://intl.cloud.tencent.com/document/product/266/33890)を選択して、ビデオのアップロード後にこのタスクフローを実行するよう指定します。

## 結果の取得

ビデオ審査タスクを開始した後、非同期の[オーディオビデオ審査の完了](https://www.tencentcloud.com/document/product/266/50677)を待機するか、同期的に[タスク確認](https://intl.cloud.tencent.com/document/product/266/33931)を実行するという2つの方法によってビデオ審査タスクの実行結果を取得できます。以下は、審査タスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。
```json
{
    "EventType": "ReviewAudioVideoComplete",
    "ReviewAudioVideoCompleteEvent": {
        "TaskId": "125xxxx-ReviewAudioVideo-07edbc78ba20563cdf2362cffbf4aa0ct",
        "Status": "FINISH",
        "ErrCodeExt": "",
        "Message": "SUCCESS",
        "Input":{
            "FileId": "387702130626135215"
        },
        "Output":{
            "Suggestion": "block",
            "Label": "Porn",
            "Form": "Image",
            "SegmentSet":[
                {
                    "StartTimeOffset": 0,
                    "EndTimeOffset": 1,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163480.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:16.039Z"
                },
                {
                    "StartTimeOffset": 1,
                    "EndTimeOffset": 2,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163481.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:17.039Z"
                },
                {
                    "StartTimeOffset": 2,
                    "EndTimeOffset": 3,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163482.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:18.039Z"
                },
                {
                    "StartTimeOffset": 3,
                    "EndTimeOffset": 4,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163483.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:19.039Z"
                },
                {
                    "StartTimeOffset": 4,
                    "EndTimeOffset": 5,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163484.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:20.039Z"
                },
                {
                    "StartTimeOffset": 5,
                    "EndTimeOffset": 6,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163485.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:21.039Z"
                },
                {
                    "StartTimeOffset": 6,
                    "EndTimeOffset": 7,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163486.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:22.039Z"
                },
                {
                    "StartTimeOffset": 7,
                    "EndTimeOffset": 8,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163487.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:23.039Z"
                },
                {
                    "StartTimeOffset": 8,
                    "EndTimeOffset": 9,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163488.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:24.039Z"
                },
                {
                    "StartTimeOffset": 9,
                    "EndTimeOffset": 10,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163489.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:25.039Z"
                }
            ],
            "SegmentSetFileUrl": "http://251000800.vod2.myqcloud.com/a8800b40vodtranssgp251000800/0f9bd2b0-34a8-4642-f481-001894d93019.txt",
            "SegmentSetFileUrlExpireTime": "2022-10-12T07:01:07.695Z"
        },
        "SessionContext": "",
        "SessionId": ""
    }
}
```

コールバック結果の中で、`ReviewAudioVideoCompleteEvent.Output`はオーディオビデオ審査結果のアウトプットであり、`Output.Suggestion`は全体的な審査のアドバイスを表します。ここでは`block`、すなわちそのままブロックすることを推奨しています。`Output.Label=Porn`と`Output.Form=Image`は、違反の内容がビデオ画面に含まれる性的な情報である可能性が最も高いことを示しています。

1つのオーディオビデオに複数の違反部分が存在する可能性があり、`Output.SegmentSet`ではそのうち最初の10部分をリストアップします（全体の違反結果はリンクの有効期間内に`Output.SegmentSetFileUrl`から取得できます）。

各違反部分の`StartTimeOffset`と`EndTimeOffset`は、その部分の元のビデオ内での開始・終了時間を表します。`SubLabel` はその部分の具体的な違反内容を表します。

画面内の文字と音声内の文字の認識：
* `Text`はその部分から認識された完全な文字内容を表します。
* `KeywordSet`はヒットした違反キーワードのリストを表します。

ビデオ画面（人および物体）と画面内の文字の認識：
* `AreaCoordSet`は違反対象のエリア座標を表します。
* `Url`は違反画面のスクリーンキャプチャのリンクです。
* `PicUrlExpireTime`は`Url`の有効期限であり、これを過ぎるとリンクにアクセスできなくなります。
