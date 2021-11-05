> !
>
>-  このドキュメントでは、[TRTCが提供するMCUクラスターによるCloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)を使用することで発生するバイパストランスコード料金についてのみ説明しています。TRTCのオーディオビデオストリーミングをCSSにRelayed Pushした後、[CSSの提供するクラウドミクスストリーミング機能](https://intl.cloud.tencent.com/document/product/267/37665)を使用される場合は、CSSから[CSSトランスコード](https://intl.cloud.tencent.com/document/product/267/39604)の料金が請求されます。
> -   トランスコード後に出力したオーディオビデオストリーミングをCSSシステムに転送し、視聴者に[CDN relayed live streamingの実装](https://intl.cloud.tencent.com/document/product/647/35242)をさせた場合、CSSはお客様に対し、[トラフィック/帯域幅](https://intl.cloud.tencent.com/document/product/267/2818#.E6.B5.81.E9.87.8F.E5.B8.A6.E5.AE.BD) の料金を請求します。
> -   当社と販売契約を結んでいる場合、実際の課金情報は契約書のとおりとなります。

<span id="Billing_items"></span>

## 単価

TRTC Cloud MixTranscodingサービスの単価は次のとおりです。

| コーデック | 課金項目                   | 単価（米ドル/1000分）（小数点以下第3位を四捨五入） |
| -------- | ------------------------ | --------------------------------------------- |
| オーディオトランスコード | バイパストランスコード-音声            | 0.799                                         |
| H.264    | バイパストランスコード-H264-SD    | 2.296                                         |
| H.264    | バイパストランスコード-H264-HD    | 4.643                                         |
| H.264    | バイパストランスコード-H264-FHD | 8.990                                         |

<span id="Billing_method"></span>

## 利用量の統計方法

Tencent Real-Time Communication（TRTC）は、同じ[Tencent Cloudアカウント](https://console.intl.cloud.tencent.com/trtc)内のすべてのアプリケーションがMCUミクスストリーミングトランスコードを経た後に出力された**トランスコード時間**に基づき、バイパストランスコードサービスの使用量を集計します。トランスコード時間はコーデックとトランスコードの結果によって異なり、[ビデオ時間](#m_video) と [オーディオ時間](#m_voice)に分かれます。

> ! 時間の集計精度は秒とし、1日あたりの累計秒数を分数に変換してから課金します。1分未満は1分としてカウントします。

<span id="m_video"></span>

### ビデオ時間

ビデオ時間は、トランスコード結果に含まれるビデオ画面の時間を指します。TRTCは、トランスコード後に出力されるビデオの解像度に応じてビデオのグレードを区分し、その後グレードごとのビデオ時間に対してそれぞれ課金します。ビデオのグレードと解像度の対応関係は下表のとおりとなります。

| ビデオのグレード           | 出力解像度                                                |
| ------------------ | --------------------------------------------------------- |
| SD        | 出力解像度≦307,200（640 × 480）                         |
| HD        | 307,200（640 × 480）＜ 出力解像度≦921,600（1280 × 720） |
| FHD | 921,600（1280 × 720）＜ 出力解像度                        |

-  トランスコード後に出力される同一ストリームの同一時間内にビデオもオーディオも存在する場合は、ビデオ時間のみで集計され、オーディオ時間が重複して計算されることはありません。
-  トランスコード後に出力される同一ストリームの解像度は変化する可能性があります。TRTCではサービス使用量を分割して集計し、通常では60秒に1回更新します。解像度に変化が生じた場合はすぐに報告、更新されます。

<span id="m_voice"></span>

### オーディオ時間

オーディオ時間とは、トランスコード結果の中にオーディオのみが存在する時間を指します。

<span id="Fixed_price"></span>

## 課金の例

お客様が1月1日にTRTCのMCUクラスターを使用してCloud MixTranscodingを行い、H.264コーデックを使用して解像度1920×1080、640×360のビデオを各100分間出力し、同時にオーディオトランスコードを使用して100分間のオーディオを出力したとします。

ユーザーAは1月1日に発生したバイパストランスコード料金を、1月2日に次のとおり支払う必要があります。

<table>
     <tr>
         <th style="text-align:center">出力解像度</th>
         <th style="text-align:center">ビデオのグレード</th>
         <th style="text-align:center">時間（分）</th>
         <th style="text-align:center">単価（米ドル/1000分）</th>
         <th style="text-align:center">各サービス料金（米ドル）</th>
         <th style="text-align:center">合計料金（米ドル）（小数点第2位を四捨五入）</th>
     </tr>
     <tr>
         <td style="text-align:center">1920 × 1080</td>
         <td style="text-align:center">FHD</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">8.990</td>
         <td style="text-align:center" >0.899</td>
         <td style="text-align:center" rowspan="3">1.44</td>
     </tr>
     <tr>
         <td style="text-align:center">640 × 360</td>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">4.643</td>
         <td style="text-align:center">0.464</td>
     </tr>
     <tr>
         <td style="text-align:center">オーディオ</td>
         <td style="text-align:center">オーディオ</td>
         <td style="text-align:center">100</td>
         <td style="text-align:center">0.799</td>
         <td style="text-align:center">0.0799</td>
     </tr>
</table>

## 注意事項

ここでは参考として、詳細な注意事項についてご説明します。

### 日次決済請求書

日次決済の支払い方式です。TRTC Cloud MixTranscodingサービスは**日次決済後払い**方式のみをサポートしています。日ごとに課金し、毎日午前10時に前日に発生した料金を引き落とします。

<span id="Billing_examples"></span>
