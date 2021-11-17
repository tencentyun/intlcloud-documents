トランスコードは、特定のビデオストリームを別のビデオストリームに変換するオフラインタスクです。コーデック、解像度、ビットレートなどの元のビットストリームのパラメータを変更して、さまざまなデバイスやネットワーク環境での再生に適応させます。トランスコードを使用して以下の機能を実現できます。
- 多様な端末に適応：元のビデオを端末適応性の高い形式（例：MP4）にトランスコードして、ビデオリソースをより多くのデバイスで再生できるようにします。
- さまざまな帯域幅に適応：ビデオをLD、SD、HD、またはFHD出力にスムーズに変換します。ユーザーは、現在のネットワーク環境に応じて、ビデオ再生に適したビットレートを選択できます。
- 再生効率を改善：トランスコードによってMP4の末尾にあるソース情報MOOVを事前に先頭にもってきますので、プレーヤーは完全なビデオをダウンロードせずに、すぐに再生することができます。
- ビデオにウォーターマークを刻印：ビデオにウォーターマークを刻印してビデオの帰属または版権を標識します。詳しい情報については、[ウォーターマーク](https://intl.cloud.tencent.com/document/product/266/33939)をご参照ください。
- 帯域幅の削減：より高度なコーデック（例：H.265）を使用してトランスコードすることで、元の画質が低下しない前提で、ビットレートを大幅に削減し、再生帯域幅を削減できます。

ビデオトランスコーディングした後、[結果の取得](#jghq)をもとに、トランスコード後のビデオ再生URLを取得できます。ご自身のプレーヤーまたはサードパーティプレーヤーを使用して、トランスコード後のビデオを再生することができます。

>!トランスコーディング機能は主に**ショート動画（UGSV）**のシナリオに適用します。**ロング動画**（動画サイト、eラーニングなど）に対しては、 [アダプティブビットレートストリーミングへのトランスコード](https://intl.cloud.tencent.com/document/product/266/33942) を使用すれば、お客様のユーザーに対しより素晴らしい体験をもたらすことができます。
<span id="zm"></span>
## トランスコードテンプレート

トランスコードの目標仕様には、エンコード形式、解像度、ビットレートなどのパラメータがあります。VODではトランスコードテンプレートを使用してトランスコードのパラメータグループを表します。トランスコードテンプレートによって、以下のトランスコード関連パラメータを指定することができます。
>?その他のオーディオビデオトランスコーディング形式については、[トランスコーディングのサポート形式](https://intl.cloud.tencent.com/document/product/266/7898)をご参照ください。
<table>
    <tr>
        <th style="width:18%">
            タイプ
        </th>
        <th style="width:22%">
            パラメータ
        </th>
        <th>
            説明
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            コンテナ
        </td>
    </tr>
    <tr>
        <td>
            コンテナ形式
        </td>
        <td>
			以下のビデオおよび純音声コンテナ形式への変換が可能です
            <li>ビデオ：MP4、TS、HLS、FLV</li>
            <li>純音声：MP3、M4A、FLAC、OGG</li>
        </td>
    </tr>
    <tr>
        <td>
            ビデオストリームの削除
        </td>
        <td>
            「ビデオストリームの削除」を有効にすると、トランスコードしたビデオにはビデオストリームが含まれません（オーディオストリームのみ残ります）
        </td>
    </tr>
    <tr>
        <td>
            オーディオストリームの削除
        </td>
        <td>
            「オーディオストリームの削除」を有効にすると、トランスコードしたビデオにはオーディオストリームが含まれません（ビデオストリームのみ残ります）
        </td>
    </tr>
    <tr>
        <td rowspan=7>
            ビデオコーデック
        </td>
        <td>
            コーデック（Codec）
        </td>
        <td>
            H.264とH.265の2種類のコーデックをサポートしています
        </td>
    </tr>
    <tr>
        <td>
            ビットレート（Bitrate）
        </td>
        <td>
            サポートするビデオビットレートの範囲：10kbps～35Mbps
        </td>
    </tr>
    <tr>
        <td>
            フレームレート（Frame Rate）
        </td>
        <td>
            サポートするフレームレートの範囲：1fps～60fps。一般的なフレームレートは24fps、25fps、30fps
        </td>
    </tr>
    <tr>
        <td>
            解像度（Resolution）
        </td>
        <td>
            <li>サポートする幅の範囲：128px～4096px</li>
            <li>サポートする高さの範囲：128px～4096px</li>
        </td>
    </tr>
    <tr>
        <td>
            GOP 長さ
        </td>
        <td>
            サポートするGOP長さの範囲：1秒～10秒
        </td>
    </tr>
    <tr>
        <td>
            プロファイル（Profile）
        </td>
        <td>
            <li>ビデオコーデックがH.264の時は、Baseline、Main、Highのプロファイルをサポートします</li>
            <li>ビデオコーデックがH.265の時は、Mainのプロファイルをサポートします</li>
        </td>
    </tr>
    <tr>
        <td>
            カラースペース（Color Space）
        </td>
        <td>
            YUV420Pをサポートします
        </td>
    </tr>
    <tr>
        <td rowspan=4>
            オーディオコーデックパラメータ
        </td>
        <td>
            コーデック（Codec）
        </td>
        <td>
            MP3、AAC、AC3 、FLACのコーデックをサポートします
        </td>
    </tr>
    <tr>
        <td>
            サンプルレート（Sample Rate）
        </td>
        <td>
            以下のオーディオサンプルレートをサポートします。
            <li>34000Hz</li>
            <li>44100Hz</li>
            <li>48000Hz</li>
        </td>
    </tr>
    <tr>
        <td>
            ビットレート（Bitrate）
        </td>
        <td>
            サポートするビットレートは26kbps～256kbps。これには以下が含まれます。
            <li>48kbps</li>
            <li>64kbps</li>
            <li>128kbps</li>
        </td>
    </tr>
    <tr>
        <td>
            サウンドチャンネル（Channel）
        </td>
        <td>
        	<li>シングルサウンドチャンネル</li>
			    <li>ダブルサウンドチャンネル</li>
			    <li>ステレオ</li>
        </td>
    </tr>
</table>

一般的なトランスコードの仕様を対象に、VODでは、[プリセットトランスコードテンプレート](https://intl.cloud.tencent.com/document/product/266/33932)を用意しています。その外、コンソールを介して（具体的な操作は [テンプレート設定](https://intl.cloud.tencent.com/document/product/266/14059)を参照）または [サーバーAPI](https://intl.cloud.tencent.com/document/product/266/34164) を呼び出して、トランスコーディングのカスタマイズテンプレートを作成し、管理することができます。

## タスクの開始

トランスコードタスクの開始には、「サーバーAPIから直接開始」、「コンソールから直接開始」、「アップロード時に実行したいタスクを指定」の3種類の方法があります。詳細内容は、ビデオ処理の [タスクの開始](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。

以下は、各種方式のトランスコーディングタスク開始についての説明です。

* サーバーAPI[ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) の呼び出しによるタスク開始：リクエストの中の`MediaProcessTask.TranscodeTaskSet`パラメータで [トランスコードテンプレート](#sh) のテンプレートIDを指定します。
* コンソールでのビデオに対するタスクの開始：コンソールで[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でトランスコーディングの目標仕様を設定します。コンソールでこのタスクフローを使用して[ビデオ処理を開始](https://intl.cloud.tencent.com/document/product/266/33892)します。
* サーバーからのアップロード時にタスクを指定：コンソールで[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でトランスコーディングの目標仕様を設定します。[アップロードの申請](https://intl.cloud.tencent.com/document/product/266/34120)の中の`procedure`パラメータでこのタスクフローを指定します。
* クライアントからのアップロード時にタスクを指定：コンソール で[タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でトランスコーディングの目標仕様を設定します。[クライアントからのアップロード署名](https://intl.cloud.tencent.com/document/product/266/33922) の中の`procedure`でこのタスクフローを指定します。
* コンソールからのアップロード：コンソールで [タスクフローを追加](https://intl.cloud.tencent.com/document/product/266/14058)し、タスクフローの中でトランスコーディングの目標仕様を設定します。コンソールを介してビデオをアップロードし、[アップロードと同時にビデオに対する処理操作を実行](https://intl.cloud.tencent.com/document/product/266/33890)を選択して、ビデオアップロード後にこのタスクフローの実行を指定します。
<span id="jghq"></span>
## 結果の取得

トランスコードタスクの開始後、非同期の[結果通知](https://intl.cloud.tencent.com/document/product/266/33931) または同期の [タスクの確認](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) の2種類の方式でトランスコードの実行結果を取得できます。以下は、トランスコードタスクの開始後、通常のコールバック方式での結果通知の例となります（値がnullのフィールドは省略）。

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
                "Type":"Transcode",
                "TranscodeTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":220
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20.m3u8",
                        "Size":63120997,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Height":480,
                        "Width":640,
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

コールバックの結果の中で、`ProcedureStateChangeEvent.MediaProcessResultSet`に`Type`がTranscode`となる結果が1つあり、`Definition`が220となっています。
