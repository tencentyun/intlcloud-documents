Media Processing Serviceでは、よく使われる主要なトランスコードパラメータを組み合わせてパラメータテンプレートとし、利便性を高めています。各パラメータテンプレートは名称とIDで識別され、名称が「LD」、「SD」、「HD」、「FHD」などの一般的なパラメータテンプレートは、トランスコードテンプレートの中でそれぞれ10、20、30、40などのIDで識別されます。タスクの違いにより、パラメータテンプレートは次のタイプに分かれます。
- トランスコードテンプレート
- コンテナテンプレート
- アニメーション画像生成テンプレート
- タイムポイントスクリーンキャプチャテンプレート
- サンプリングスクリーンキャプチャテンプレート
- スプライトイメージテンプレート
- ABSへのトランスコードテンプレート
- ビデオコンテンツのインテリジェント認識テンプレート
- ビデオコンテンツ認識テンプレート
- ビデオコンテンツ分析テンプレート

上記のテンプレートタイプについて、MPSは対応する一般パラメータテンプレートを提供し、それらは「プリセットパラメータテンプレート」と呼ばれています。同時に、新たに各タイプのパラメータテンプレートを作成し、それぞれ異なるパラメータを指定することもでき、「カスタムパラメータテンプレート」と呼ばれます。パラメータテンプレート中の各パラメータの詳細情報は[テンプレートパラメータの説明](https://intl.cloud.tencent.com/document/product/1041/33494)をご参照ください。

## プリセットパラメータテンプレート

以下はテンプレートIDや主要パラメータ設定など、MPSにプリセットされる各タイプのパラメータテンプレート情報を示します。

[](id:transcoding)
### プリセットトランスコードテンプレート
#### トランスコードされたビデオ形式

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">仕様等級</th><th colspan="1" rowspan="2">テンプレートID</th><th colspan="1" rowspan="2">コンテナ形式（Format）</th><th colspan="4">ビデオパラメータ</th><th colspan="4">オーディオパラメータ</th></tr>
<tr><th colspan="1">解像度（Resolution）</th><th colspan="1">ビットレート（Bitrate）</th><th colspan="1">フレームレート（FPS）</th><th colspan="1">コーデック（Codec）</th><th colspan="1">ビットレート（Bitrate）</th><th colspan="1">サンプルレート（SampleRate）</th><th colspan="1">オーディオサウンドチャネル数（SoundSystem）</th><th colspan="1">コーデック（Codec）</th></tr>
<tr><td colspan="1" rowspan="2">LD（FLU ）</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">比例ズーム × 360</td><td colspan="1" rowspan="2">400kbps</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64 kbps</td ><td colspan="1" rowspan="12">44100Hz</td><td colspan="1" rowspan="12">ダブルサウンドチャンネル（Stereo）</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">SD</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">比例ズーム × 540</td><td colspan="1" rowspan="2">1000kbps</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">HD</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">比例ズーム × 720</td><td colspan="1" rowspan="2">1800kbps</td><td colspan="1" rowspan="4">128kbps</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">FHD</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">比例ズーム × 1080</td><td colspan="1" rowspan="2">2500kbps</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">比例ズームグ × 1440</td><td colspan="1" rowspan="2">3000kbps</td><td colspan="1" rowspan="4">160kbps</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">比例ズーム × 2160</td><td colspan="1" rowspan="2">6000kbps</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

#### トランスコードされたオーディオ形式

<table>
    <tr>
        <th rowspan=1>
            テンプレートID                
        </th>
        <th rowspan=1>
            コンテナ形式（Format）
        </th>
        <th>
            オーディオビットレート（Bitrate）
        </th>
        <th>
            コーデック（Codec）
        </th>
        <th>
            サウンドチャンネル数（SoundSystem）
        </th>
        <th>
            サンプルレート（SampleRate）
        </th>
    </tr>
 <tr>
        <td>
            1100
        </td>
        <td rowspan="5">
            M4A
        </td>
        <td>
            24kbps
        </td>
        <td rowspan="5">
            AAC
        </td>
        <td rowspan="7">
            2チャネル（Stereo）
        </td>
        <td rowspan="7">
            44100Hz
        </td>
    </tr>
 <tr>
        <td>
            1110
        </td>
        <td>
            48kbps
        </td>
    </tr>
    <tr>
        <td>
            1120
        </td>
        <td>
            96kbps
        </td>
    </tr>
     <tr>
        <td>
            1130
        </td>
        <td>
            192kbps
        </td>
    </tr>
    <tr>
        <td>
            1140
        </td>
        <td>
            256kbps
        </td>
    </tr>
    <tr>
        <td>
            1010
        </td>
        <td rowspan="2">
            MP3
        </td>
        <td>
            128kbps
        </td>
        <td rowspan="2">
            MP3
        </td>
    </tr>
    <tr>
        <td>
            1020
        </td>
        <td>
            320kbps
        </td>
    </tr>
</table>


### プリセットTESHDテンプレート

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">仕様等級</th><th colspan="1" rowspan="2">テンプレートID</th><th colspan="1" rowspan="2">コンテナ形式（Format）</th><th colspan="4">ビデオパラメータ</th><th colspan="4">オーディオパラメータ</th></tr>
<tr><th colspan="1">解像度（Resolution）</th><th colspan="1">最大ビットレート（Bitrate）</th><th colspan="1">フレームレート（FPS）</th><th colspan="1">コーデック（Codec）</th><th colspan="1">ビットレート（Bitrate）</th><th colspan="1">サンプルレート（SampleRate）</th><th colspan="1">オーディオサウンドチャネル数（SoundSystem）</th><th colspan="1">コーデック（Codec）</th></tr>
<tr><td colspan="1">ソースと同じ（SAME）</td><td colspan="1" rowspan="">100800</td><td colspan="1" rowspan="5">MP4</td><td colspan="1">ソースと同じ</td><td colspan="1" rowspan="5">無制限</td><td colspan="1" rowspan="5">25</td><td colspan="1" rowspan="5">H.264</td><td colspan="1">ソースと同じ</td><td colspan="1" rowspan="5">44100Hz</td><td colspan="1" rowspan="5">ダブルサウンドチャンネル（Stereo）</td><td colspan="1" rowspan="5">AAC</td></tr></tr>
<tr><td colspan="1">LD（FLU）</td><td colspan="1">100810</td><td colspan="1">比例ズーム × 360</td><td colspan="1" rowspan="2">64 kbps</td></tr>
<tr><td colspan="1">SD</td><td colspan="1">100820</td><td colspan="1">比例ズーム × 540</td></tr>
<tr><td colspan="1">HD</td><td colspan="1">100830</td><td colspan="1" rowspan="">比例ズーム × 720</td><td colspan="1" rowspan="2">128kbps</td></tr>
<tr><td colspan="1">FHD</td><td colspan="1">100840</td><td colspan="1">比例ズーム × 1080</td></tr></tbody></table>


### プリセットコンテナテンプレート

| テンプレートID | コンテナ形式（Format） |
| ------- | ------------------------ |
| 875       | MP4                      |
| 876       | HLS                      |

[](id:cinemagraph)
### プリセットアニメーション画像生成テンプレート

| テンプレートID | 画像形式（Format） | 解像度（Resolution） | フレームレート（FPS） |
| ------- | --------- | ----------- | ----------- |
| 20000   | GIF                | ソースと同じ                 | 2           |
| 20001   | WebP               | ソースと同じ                 | 2           |

[](id:screenshot01)
### プリセットタイムポイントスクリーンキャプチャテンプレート

| テンプレートID | 出力形式（Format） | 幅（Width） | 高さ（Height） | 塗りつぶしタイプ（FillType） |
| ------- | --------- | ----- | --------- | -------------- |
| 10      | JPG                | ソースと同じ          | ソースと同じ           | 引きのばし   |

[](id:screenshot02)
### プリセットサンプリングスクリーンキャプチャテンプレート

| テンプレートID &nbsp;| 出力形式（Format） | 幅（Width） | 高さ（Height） | サンプリングタイプ（SampleType） | スクリーンキャプチャ間隔（Interval） | 塗りつぶしタイプ（FillType） |
| ------- | -------- | -- | ----- | ---- | ------- | -------- |
| 10       | JPG    | ソースと同じ   | ソースと同じ     | 百分率比  | 10%   | 引きのばし     |

[](id:screenshot03)
### プリセットスプライトイメージテンプレート

| テンプレートID &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 出力形式（Format） | サブ画像幅（Width） | サブ画像の高さ（Height） | サブ画像の行数（Rows） | サブ画像の列数（Columns） | サンプリングタイプ（SampleType） | スクリーンキャプチャ間隔（Interval） |
| ------- | ----- | ------- | ----- | ---- | ---- | -------- | ------- |
| 10      | JPG   | 142    | 80      | 10       | 10    | インターバルに応じて   | 10秒  |

### プリセットABSテンプレート
#### テンプレート情報

<table border="0" >
 <tr>
  <th>テンプレートID</td>
  <th>パッケージタイプ（PackageType）</td>
  <th>サブストリーム情報（SubstreamInfo）</td>
  <th >「低解像度から高解像度」のフィルタリング （DisableHigherResolution）</td>
 </tr>
 <tr>
  <td>10</td>
  <td>HLS</td>
  <td >「SD」から「4K」まで6つの仕様のサブストリームを含みます</td>
  <td>はい</td>
 </tr>
</table>

#### サブストリーム情報

<table border="0" >
 <tr>
  <th rowspan="2" >サブストリーム仕様</td>
  <th colspan="4" >ビデオパラメータ</td>
  <th colspan="4" >オーディオパラメータ</td>
 </tr>
 <tr>
  <th>解像度（Resolution）</th>
  <th>ビットレート（Bitrate）</th>
  <th >フレームレート（FPS）</th>
  <th >コーデック（Codec）</th>
  <th>ビットレート（Bitrate）</th>
  <th>サンプルレート（SampleRate）</th>
  <th>オーディオサウンドチャネル数（SoundSystem）</th>
  <th>コーデック（Codec）</td>
 </tr>
 <tr>
  <td>LD</td>
  <td>比例ズーム x 240</td>
  <td>256kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>ダブルサウンドチャンネル（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>SD</td>
  <td>比例ズーム x 480</td>
  <td>512kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>ダブルサウンドチャンネル（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>HD</td>
  <td>比例ズーム x 720</td>
  <td>512kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>ダブルサウンドチャンネル（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>FHD</td>
  <td>比例ズーム x 1080</td>
  <td>1024kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>ダブルサウンドチャンネル（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>2K</td>
  <td>比例ズーム x 1440</td>
  <td>3072kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>ダブルサウンドチャンネル（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>4K</td>
  <td>比例ズーム x 2160</td>
  <td>6144kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>ダブルサウンドチャンネル（Stero）</td>
  <td>AAC</td>
 </tr>
</table>

### プリセットビデオコンテンツのインテリジェント認識テンプレート

[](id:verify)
<table>
    <tr>
        <th rowspan=2>
            テンプレートID                
        </th>
        <th colspan=3>
            ビデオ画面
        </th>
        <th colspan=2>
            ASRテキスト
        </th>
        <th colspan=2>
            OCRテキスト
        </th>
    </tr>
 <tr>
        <th>
            不快感を与える情報（Porn）
        </th>
        <th>
            安全でない情報（Terrorism）
        </th>
        <th>
            不適切な情報（Political）
        </th>
        <th>
            不快感を与える情報（Asr.Porn）
        </th>
        <th>
            不適切な情報（Asr.Political）
        </th>
        <th>
            不快感を与える情報（Ocr.Porn）
        </th>
        <th>
            不適切な情報（Ocr.Political）
        </th>
    </tr>
    <tr>
        <td>
            10
        </td>
        <td>
            はい
        </td>
        <td>
            はい
        </td>
        <td>
            はい
        </td>
        <td>
            いいえ
        </td>
        <td>
            いいえ
        </td>
        <td>
            いいえ
        </td>
        <td>
            いいえ
        </td>
    </tr>
    <tr>
        <td>
            20
        </td>
        <td>
            はい
        </td>
        <td>
            はい
        </td>
        <td>
            はい
        </td>
        <td>
            はい
        </td>
        <td>
            はい
        </td>
        <td>
            はい
        </td>
        <td>
            はい
        </td>
    </tr>
</table>

### プリセットビデオコンテンツ認識テンプレート

| テンプレートID | テキスト全文認識（OcrFullText） | テキストキーワード認識（OcrWords） | 音声全文認識（AsrFullText） | 音声キーワード認識（AsrWords） |
| -- | -- | -- | -- | -- |
| 10  | いいえ | いいえ | いいえ | いいえ |


### プリセットビデオコンテンツ分析テンプレート

| テンプレートID | インテリジェントクラシフィケーション（Classification） | インテリジェントタグ（Tag） | インテリジェントカバー画像（Cover） | インテリジェントフレームタグ（FrameTag） |
| -- | -- | -- | -- | -- |
| 10 | はい | はい | はい | いいえ |
| 20 | はい | はい | はい | はい |

## カスタムパラメータテンプレート
システムのプリセットパラメータテンプレート以外に、必要に応じてテンプレートパラメータをカスタマイズし、「カスタムパラメータテンプレート」を作成することもできます。コンソールまたはAPI呼び出しによって対応するタイプのパラメータテンプレートを作成でき、このタイプのテンプレートは自分だけが見ることができます。

### コンソールによるカスタムパラメータテンプレート作成

コンソールによるカスタムパラメータテンプレート作成については、[テンプレート設定](https://intl.cloud.tencent.com/document/product/1041/33486)をご参照ください。

### APIによるカスタムパラメータテンプレート作成
次のAPIを使用して、対応するタイプのカスタムパラメータテンプレートを作成することができます。
- [トランスコードテンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/33671)
- [ウォーターマークテンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/33670)
- [サンプリングスクリーンキャプチャテンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/33673)
- [指定タイムポイントスクリーンキャプチャテンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/33672)
- [アニメーション画像生成テンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/33676)
- [スプライトイメージテンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/33674)
- [ABSテンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/37469)
- [ビデオコンテンツのインテリジェント認識テンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/33677)
- [ビデオコンテンツ認識テンプレートの作成]
- [ビデオコンテンツ分析テンプレートの作成](https://intl.cloud.tencent.com/document/product/1041/37470)
