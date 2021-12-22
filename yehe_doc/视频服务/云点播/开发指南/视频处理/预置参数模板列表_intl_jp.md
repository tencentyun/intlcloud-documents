VODでは、ビデオ処理を開始するための複雑なパラメータセットの代わりにパラメータテンプレートを使用できます。各種ビデオ処理のシチュエーションに応じて、さまざまなプリセットパラメータテンプレートを提供します。

## ビデオ変換

ビデオ変換用のプリセットパラメータテンプレートには、次のタイプが含まれます。
- プリセットトランスコードテンプレート
- プリセットコンテナテンプレート
- プリセットアニメーション画像生成テンプレート
- プリセットタイムポイントスクリーンキャプチャテンプレート
- プリセットサンプリングスクリーンキャプチャテンプレート
- プリセットスプライトイメージテンプレート
- プリセットABSテンプレート

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

#### トランスコードされたオーディオ形式[](id:music)

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
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | ソースと同じ                 | 2           |
| 20001   | WEBP                | ソースと同じ                 | 2           |

[](id:screenshot01)
### プリセットタイムポイントスクリーンキャプチャテンプレート

| テンプレートID | 出力形式（Format） | 幅（Width） | 高さ（Height） | 塗りつぶしタイプ（FillType） |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | ソースと同じ          | ソースと同じ           | 引きのばし                 |

[](id:screenshot02)
### プリセットサンプリングスクリーンキャプチャテンプレート

| テンプレートID | 出力形式（Format） | 幅（Width） | 高さ（Height） | サンプリングタイプ（SampleType） | スクリーンキャプチャ間隔（Interval） | 塗りつぶしタイプ（FillType） |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG                | ソースと同じ          | ソースと同じ           | 百分率比               | 10%                  | 引きのばし                 |

[](id:screenshot03)
### プリセットスプライトイメージテンプレート

| テンプレートID | 出力形式（Format） | サブ画像幅（Width） | サブ画像の高さ（Height） | サブ画像の行数（Rows） | サブ画像の列数（Columns） | サンプリングタイプ（SampleType） | スクリーンキャプチャ間隔（Interval） |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80                 | 10               | 10                  | 時間間隔に応じて             | 10秒                 |

### プリセットABSテンプレート
#### テンプレート情報

<table border="0" >
 <tr>
  <th>テンプレートID</td>
  <th>パッケージタイプ（PackageType）</td>
  <th>暗号化タイプ（EncryptionType）</td>
  <th>サブストリーム情報（SubstreamInfo）</td>
  <th >「低解像度から高解像度」のフィルタリング （DisableHigherResolution）</td>
 </tr>
 <tr>
  <td>10</td>
  <td>HLS</td>
  <td>暗号化しない</td>
  <td >「LD」から「4K」まで計6つの仕様のサブストリームを含みます</td>
  <td>はい</td>
 </tr>
 <tr>
  <td>12</td>
  <td>HLS</td>
  <td>SimpleAES</td>
  <td >「LD」から「4K」まで計6つの仕様のサブストリームを含みます</td>
  <td>はい</td>
 </tr>
  <tr>
  <td>20</td>
  <td>MPEG-DASH</td>
  <td>暗号化なし</td>
  <td >「LD」から「4K」まで計6つの仕様のサブストリームを含みます</td>
  <td>いいえ</td>
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


## ビデオAI

ビデオAI用のプリセットパラメータテンプレートには、次のタイプが含まれます。

* プリセットビデオコンテンツ審査テンプレート
* プリセットビデオコンテンツ分析テンプレート
* プリセットビデオコンテンツ認識テンプレート

### プリセットビデオコンテンツ審査テンプレート


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

### プリセットビデオコンテンツ分析テンプレート

| テンプレートID | インテリジェントクラシフィケーション（Classification） | インテリジェントタグ（Tag） | インテリジェントカバー画像（Cover） | インテリジェントフレームタグ（FrameTag） |
| -- | -- | -- | -- | -- |
| 10 | はい | はい | はい | いいえ |
| 20 | はい | はい | はい | はい |

### プリセットビデオコンテンツ認識テンプレート

| テンプレートID  | 顔認証（Face） | テキスト全文認識（OcrFullText） | テキストキーワード認識（OcrWords） | 音声全文認識（AsrFullText） | 音声キーワード認識（AsrWords） |
| -- | -- | -- | -- | -- | -- |
| 10 | はい（デフォルトで人物データベースを使用） | いいえ | いいえ | いいえ| いいえ |




## 過去のトランスコード

### 過去のプリセットトランスコードテンプレート

#### トランスコードされたビデオ形式

<table>
    <tr>
        <th rowspan=2>
            仕様等級                
        </th>
        <th rowspan=2>
            テンプレートID                
        </th>
        <th rowspan=2>
            コンテナ形式（Format）
        </th>
        <th colspan=4>    
            ビデオパラメータ
        </th>
        <th colspan=1>    
            オーディオパラメータ
        </th>
    </tr>
    <tr>
        <th>
            解像度（Resolution）
        </th>
        <th>
            ビットレート（Bitrate）
        </th>
        <th>
            フレームレート（FPS）
        </th>
        <th>
            コーデック（Codec）
        </th>
        <th>
            コーデック（Codec）
        </th>
    </tr>
    <tr>
        <td  rowspan=6>
            滑らかさ（FLU）
        </td>
        <td>
            10
        </td>
        <td>
            MP4
        </td>
        <td>
            320 × 比例ズーム
        </td>
        <td>
            256kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            510
        </td>
        <td>
            MP4
        </td>
        <td>
            比例ズーム × 240
        </td>
        <td>
            250kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            210
        </td>
        <td>
            HLS
        </td>
        <td>
            320 × 比例ズーム
        </td>
        <td>
            256kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            610
        </td>
        <td>
            HLS
        </td>
        <td>
            比例ズーム × 240
        </td>
        <td>
            250kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10046
        </td>
        <td>
            FLV
        </td>
        <td>
            320 × 比例ズーム
        </td>
        <td>
            256kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            710
        </td>
        <td>
            FLV
        </td>
        <td>
            比例ズーム × 240
        </td>
        <td>
            250kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            SD
        </td>
        <td>
            20
        </td>
        <td>
            MP4
        </td>
        <td>
            640 × 比例ズーム
        </td>
        <td>
            512kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            520
        </td>
        <td>
            MP4
        </td>
        <td>
            比例ズーム × 480
        </td>
        <td>
            600kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            220
        </td>
        <td>
            HLS
        </td>
        <td>
            640 × 比例ズーム
        </td>
        <td>
            512kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            620
        </td>
        <td>
            HLS
        </td>
        <td>
            比例ズーム × 480
        </td>
        <td>
            600kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10047
        </td>
        <td>
            FLV
        </td>
        <td>
            640 × 比例ズーム
        </td>
        <td>
            512kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            720
        </td>
        <td>
            FLV
        </td>
        <td>
            比例ズーム × 480
        </td>
        <td>
            600kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            HD
        </td>
        <td>
            30
        </td>
        <td>
            MP4
        </td>
        <td>
            1280 × 比例ズーム
        </td>
        <td>
            1024kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            530
        </td>
        <td>
            MP4
        </td>
        <td>
            比例ズーム × 720
        </td>
        <td>
            800kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            230
        </td>
        <td>
            HLS
        </td>
        <td>
            1280 × 比例ズーム
        </td>
        <td>
            1024kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            630
        </td>
        <td>
            HLS
        </td>
        <td>
            比例ズーム × 720
        </td>
        <td>
            800kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10048
        </td>
        <td>
            FLV
        </td>
        <td>
            1280 × 比例ズーム
        </td>
        <td>
            1024kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            730
        </td>
        <td>
            FLV
        </td>
        <td>
            比例ズーム × 720
        </td>
        <td>
            800kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            FHD
        </td>
        <td>
            40
        </td>
        <td>
            MP4
        </td>
        <td>
            1920 × 比例ズーム
        </td>
        <td>
            2500kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            540
        </td>
        <td>
            MP4
        </td>
        <td>
            比例ズーム × 1080
        </td>
        <td>
            1400kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            240
        </td>
        <td>
            HLS
        </td>
        <td>
            1920 × 比例ズーム
        </td>
        <td>
            2500kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            640
        </td>
        <td>
            HLS
        </td>
        <td>
            比例ズーム × 1080
        </td>
        <td>
            1400kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10049
        </td>
        <td>
            FLV
        </td>
        <td>
            1920 × 比例ズーム
        </td>
        <td>
            2500kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            740
        </td>
        <td>
            FLV
        </td>
        <td>
            比例ズーム × 1080
        </td>
        <td>
            1400kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            2K
        </td>
        <td>
            70
        </td>
        <td>
            MP4
        </td>
        <td>
            比例ズーム × 1440
        </td>
        <td>
            3072kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            570
        </td>
        <td>
            MP4
        </td>
        <td>
            比例ズーム × 1440
        </td>
        <td>
            2048kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            270
        </td>
        <td>
            HLS
        </td>
        <td>
            比例ズーム × 1440
        </td>
        <td>
            3072kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            670
        </td>
        <td>
            HLS
        </td>
        <td>
            比例ズーム × 1440
        </td>
        <td>
            2048kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            370
        </td>
        <td>
            FLV
        </td>
        <td>
            比例ズーム × 1440
        </td>
        <td>
            3072kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            770
        </td>
        <td>
            FLV
        </td>
        <td>
            比例ズーム × 1440
        </td>
        <td>
            2048kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            4K
        </td>
        <td>
            80
        </td>
        <td>
            MP4
        </td>
        <td>
            比例ズーム × 2160
        </td>
        <td>
            6144kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            580
        </td>
        <td>
            MP4
        </td>
        <td>
            比例ズーム × 2160
        </td>
        <td>
            4096kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            280
        </td>
        <td>
            HLS
        </td>
        <td>
            比例ズーム × 2160
        </td>
        <td>
            6144kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            680
        </td>
        <td>
            HLS
        </td>
        <td>
            比例ズーム × 2160
        </td>
        <td>
            4096kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            380
        </td>
        <td>
            FLV
        </td>
        <td>
            比例ズーム × 2160
        </td>
        <td>
            6144kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            780
        </td>
        <td>
            FLV
        </td>
        <td>
            比例ズーム × 2160
        </td>
        <td>
            4096kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
</table>

以上のビデオ変換テンプレートに記載されていないパラメータはすべて同一で、それぞれ次のとおりです。

<table>
    <tr>
        <th style="width:18%">
            タイプ               
        </th>
        <th style="width:22%">
            パラメータ/機能項目
        </th>
        <th>
            説明
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            ビデオパラメータ
        </td>
        <td>
            プロファイル
        </td>
        <td>
				    <ul>
				       <li>H.264 コード使用時のプロファイルはHighです</li>
						   <li>H.265 コード使用時のプロファイルはMainです</li>
				    </ul>
        </td>
    </tr>
    <tr>
        <td>
            GOP 長さ
        </td>
        <td>
            240フレーム
        </td>
    </tr>
    <tr>
        <td>
            カラースペース
        </td>
        <td>
            YUV420P
        </td>
    </tr>
    <tr>
        <td>
            ビットレート制御方法
        </td>
        <td>
            動的ビットレートコード（VBR）
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            オーディオパラメータ
        </td>
        <td>
            サンプルレート
        </td>
        <td>
            44100Hz
        </td>
    </tr>
    <tr>
        <td>
            ビットレート
        </td>
        <td>
            48kbps
        </td>
    </tr>
    <tr>
        <td>
            サウンドチャンネル
        </td>
        <td>
            2チャネル（Stereo）
        </td>
    </tr>
</table>
