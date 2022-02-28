# TRTC課金

ここでは、TRTCが[音声通話](https://intl.cloud.tencent.com/document/product/647/36064)、[ビデオ通話](https://intl.cloud.tencent.com/document/product/647/36063)、[オーディオビデオインタラクティブストリーミング](https://intl.cloud.tencent.com/document/product/647/36059)の使用料金を月次集計する方法についてご紹介します。

ビジネス費用の見積もりが必要な場合、[TRTC価格計算ツール](https://intl.cloud.tencent.com/pricing/trtc/calculator)を使用してください。

当社と販売契約を結んでいる場合、実際の課金情報は契約書のとおりとなります。

>? 2021年10月27日以降、初めてTRTCコンソールで[アプリケーション](https://intl.cloud.tencent.com/zh/document/product/647/37714) を作成したアカウントについては、本ドキュメント内の「総解像度」方式で従量課金を開始します。

## 料金の構成

TRTCは月末に、[Tencent Cloudアカウント](https://console.intl.cloud.tencent.com/trtc)におけるすべてのプロジェクトによって発生したその月のオーディオおよびビデオの時間使用量（単位は分）を集計します。ビデオの時間使用量は、総解像度に応じて3つのグレードに分けられ、グレード別に価格が異なりますので、ご注意ください。TRTCがそれぞれの開発者アカウントに提供する[月間無料分数10000分](https://intl.cloud.tencent.com/document/product/647/42735)を差し引いた後、TRTCは残りのオーディオ時間使用量とビデオ時間使用量を対応する単価で乗じた後に合算し、その月の合計料金を算出します。

料金の基本的な公式は次のとおりです。

**月額料金** = **オーディオ時間使用量** × **オーディオ単価** + **各グレードのビデオ時間使用量** × **対応するビデオ単価**

### 時間使用量

各セッションの時間使用量は、このセッションの**すべてのユーザーに発生した時間使用量の総和**です。

-   **ビデオ時間使用量**：ユーザーがビデオストリームのサブスクリプションに成功すると、ビデオ使用量が発生します。オーディオストリームとビデオストリームを同時にサブスクリプションする場合、ビデオ使用量のみが計算されるので、ご注意ください。
-   **オーディオ時間使用量**：ユーザーがビデオストリームをサブスクリプションしていない場合、オーディオストリームをサブスクリプションしているかどうかに関わりなく、オーディオ使用量が発生します。

### 単価

オーディオビデオ時間使用量の単価は次のとおりです。

|使用量タイプ          | 単価（米ドル/1000分） |
| :---------------- | :------------------ |
| オーディオ              | 0.99                |
| SD        | 1.99                |
| HD        | 3.99                |
| FHD | 14.99               |

TRTCは、ユーザーが受信したすべてのビデオの総解像度に応じて、ビデオを次の3つのタイプに分類し、各タイプのビデオ料金を計算します。

| ビデオ使用量タイプ      | ユーザーがサブスクリプションしたビデオの総解像度                                  |
| :---------------- | :-------------------------------------------------------- |
| SD        | 総解像度≦307,200（640 × 480）                         |
| HD        | 307,200（640 × 480）＜ 総解像度≦921,600（1280 × 720） |
| FHD | 921,600（1280 × 720）＜ 総解像度                        |

例えば、ユーザーAが960×720の解像度で2つのビデオストリームを同時にサブスクリプションする場合、このユーザーがサブスクリプションするビデオの総解像度は960×720+960×720=1,382,400となり、そのビデオ使用量はFHDタイプの単価で課金されます。

## 前払いパッケージ

TRTCはオーディオビデオ一般[パッケージ]（https://intl.cloud.tencent.com/document/product/647/42736)を提供します。**1:2:4:15**の割合で、それぞれ音声、SD、HD、FHDの時間を差し引きます。例えば、HDビデオ時間が1分間の場合、一般パッケージから4分間が差し引かれます。

一般パッケージの料金は下表のとおりです。

<table>
     <tr>
         <th style="text-align:center">パッケージタイプ</th>  
         <th style="text-align:center">パッケージ時間（1000分）</th> 
         <th style="text-align:center">公表価格（米ドル/1000分）</th> 
         <th style="text-align:center">パッケージ内単価（米ドル/1000分）</th> 
         <th style="text-align:center">パッケージ価格（米ドル）</th> 
          <th style="text-align:center">割引</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="4">固定パッケージ</td>   
         <td style="text-align:center">25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">24</td>   
         <td style="text-align:center">3% off</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center">8% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center">13.5% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center">18.7% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">カスタマイズパッケージ</td>   
         <td style="text-align:center">0 < T < 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">パッケージ内単価*パッケージ時間 T</td>   
         <td style="text-align:center"> original </td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ T ＜ 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">3% off</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ T ＜ 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">8% off</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T ＜ 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">13.5% off</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">18.7% off</td>   
     </tr> 
</table>

> ?
>-   表中のパッケージ内単価は、1000分ごとの単価を小数点以下3桁まで切り上げています。実際の課金額は、1分ごとの単価に基づいて小数点以下8桁になります。詳細な説明
>-   現在、TRTC前払いサービスのご利用にはホワイトリスト審査が必要です。[お問い合わせ](https://intl.cloud.tencent.com/contact-us)からアクティブ化してください。
>-   お客様の月平均分数が3M分を超え、さらなるサポートと見積もりサービスを受けたい場合、[販売に関するお問い合わせ](https://intl.cloud.tencent.com/contact-us)を行ってください。

## 課金の例

ここでは、TRTCによるビデオの総解像度、各サービスタイプの時間使用量および関連料金の計算方法についてご説明します。

ユーザー5名が同時にチャンネルに参加し、60分間のビデオインタラクティブストリーミングを行っていると仮定します。ビデオインタラクティブストリーミングにはキャスター3名（キャスターA・B・C）がおり、キャスターAのビデオ解像度は960×720、キャスターBとCのビデオ解像度は640×480です。視聴者2名がすべてのキャスターのビデオストリームをサブスクリプションしました。さらに、キャスターAは、チャンネル内の他のすべてのユーザーと画面を共有しました。この場合、送受信される画面共有ストリームの解像度は1920×1080となります。

### ビデオの総解像度の計算

次の表には、各ユーザーがサブスクリプションしたビデオストリームの総解像度を計算して、各ユーザーのビデオ使用量のタイプと単価を決定する方法を示しています。

| ユーザー              | サブスクリプションしたビデオストリーム                 | ビデオの総解像度                              | 総解像度  | ビデオ使用量タイプ |
| :---------------- | :--------------------------- | :-------------------------------------------- | :-------- | :----------- |
| キャスターA+画面共有 | キャスター2名                     | 640 × 480 × 2                                 | 614,400   | HD    |
| キャスターB            | キャスター2名+キャスターAが共有した画面 | (960 × 720) + (640 × 480) + (1920 x 1080)     | 3,072,000 | FHD |
| キャスターC            | キャスター2名+キャスターAが共有した画面 | (960 × 720) + (640 × 480) + (1920 x 1080)     | 3,072,000 | FHD |
| 視聴者1            | キャスター3名+キャスターAが共有した画面 | (960 × 720) + (640 × 480 × 2) + (1920 x 1080) | 3,379,200 | FHD |
| 視聴者2            | キャスター3名+キャスターAが共有した画面 | (960 × 720) + (640 × 480 × 2) + (1920 x 1080) | 3,379,200 | FHD |

### 課金

次の表には、ビデオインタラクティブストリーミングで発生する合計料金の計算方法を示しています。

<table>
     <tr>
         <th style="text-align:center"有料サービス（ビデオ使用量タイプ）</th>
         <th style="text-align:center">合計使用量（分） = 各ユーザーの使用量の総和</th>
         <th style="text-align:center">単価（米ドル/1000分）</th>
         <th style="text-align:center">各サービス料金（米ドル）</th>
         <th style="text-align:center">合計料金（米ドル）（小数点第2位を四捨五入）</th>
     </tr>
     <tr>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">60</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(60/1000) × 3.99 = 0.2394</td>
         <td style="text-align:center" rowspan="2">13.68</td>
     </tr>
     <tr>
         <td style="text-align:center">FHD</td>
         <td style="text-align:center">60 × 4 = 240</td>
         <td style="text-align:center">14.99</td>
         <td style="text-align:center">(240/1000) × 14.99 = 13.44</td>
     </tr>
</table>

## 注意事項

ここでは参考として、詳細な注意事項についてご説明します。

### 価格計算ツール

[TRTC価格計算ツール](https://intl.cloud.tencent.com/pricing/trtc/calculator)を確認してください。

### 時間使用量の精度

TRTCは、時間の集計精度は秒とし、その月の累計秒数を分数に変換した上で課金します。毎月の使用量が各月末に決済されると、TRTCはその月に発生したオーディオと各タイプのビデオ使用量（単位は秒）を合算し、60で除してオーディオの分数と各タイプのビデオの分数を算出し、最後に**切り上げ**ます。例えば、1か月に59秒のオーディオ時間使用量が発生した場合、オーディオ使用量データは1分としてカウントされます。61秒のビデオ時間使用量が発生した場合、ビデオ使用量データは2分としてカウントされます。月間使用量の誤差は1分以内です。

### デュアルストリーム解像度

デュアルストリームモードでは、ユーザーの解像度の計算方法は次のとおりになります。

-   大容量ストリームをサブスクリプションする場合、ユーザーの総解像度は、送信者が設定した大容量ストリームの解像度に基づいて計算されます。
-   小容量ストリームをサブスクリプションする場合、ユーザーの総解像度は、ユーザーが実際に受信した解像度に基づいて計算されます。

### 画面共有ストリームの解像度

お客様のシナリオに画面共有が含まれる場合、画面共有ストリームのビデオ単価は、`TRTCVideoEncParam`で設定したビデオ解像度に基づきます。設定方法については、次の説明をご参照ください。

-   フルプラットフォームC++:[startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd)
-   iOS: [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4)
-   macOS: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)
-   Android:[startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f)

Web端末では、デバイスとブラウザの制限により、一部のブラウザは設定された画面プロパティに完全に適応できない場合があります。この場合、ブラウザが自動的に解像度を調整し、実際の解像度に応じて料金が計算されます。詳細については、[setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile)をご参照ください。

### その他の製品またはサービスの料金

お客様のシナリオが、ビデオ通話やインタラクティブライブストリーミングだけでなく、[Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/38929)などその他のTRTC製品またはサービスにも関連する場合、追加料金がかかります。詳細は、各TRTC製品またはサービスの課金説明をご参照ください。
