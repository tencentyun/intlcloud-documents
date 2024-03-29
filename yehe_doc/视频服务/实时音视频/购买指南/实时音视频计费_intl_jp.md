ここでは、TRTCが[音声通話](https://intl.cloud.tencent.com/document/product/647/36066)、[ビデオ通話](https://intl.cloud.tencent.com/document/product/647/36066)、[オーディオビデオインタラクティブストリーミング](https://intl.cloud.tencent.com/document/product/647/37286)の使用料金を月次集計する方法についてご紹介します。

ビジネス費用の見積もりが必要な場合、[TRTC価格計算ツール](https://intl.cloud.tencent.com/pricing/trtc/calculator)を使用してください。

当社と販売契約を結んでいる場合、実際の課金情報は契約書のとおりです。

>? 2021年10月27日以降、初めてTRTCコンソールで[アプリケーション](https://intl.cloud.tencent.com/zh/document/product/647/37714) を作成したアカウントについては、本ドキュメント内の「サブスクライブするビデオの総解像度」方式で従量課金を開始します。



## 料金の計算

TRTCは月末に、[Tencent Cloudアカウント](https://console.intl.cloud.tencent.com/trtc)におけるすべてのプロジェクトによって発生したオーディオとビデオの時間使用量（単位は分）を集計します。ビデオの時間使用量は、「サブスクライブするビデオの総解像度」に応じて4つのグレードに分けられ、グレード別に価格が異なりますので、ご注意ください。TRTCがそれぞれの開発者アカウントに提供する[月間無料分数10000分](https://intl.cloud.tencent.com/document/product/647/42735)を差し引いた後、TRTCは残りのオーディオ時間使用量とビデオ時間使用量を対応する単価で乗じた後に合算し、その月の合計料金を算出します。

### ステップ1：基本の課金計算式を理解します：

**月額料金** = **オーディオ時間使用量** × **オーディオ単価** + **各グレードのビデオ時間使用量** × **対応するビデオ単価**

### ステップ2：オーディオ時間使用量とビデオ時間使用量を計算します：

各セッションの時間使用量は、このセッションの**すべてのユーザーに発生した時間使用量の総和**です。

-   **ビデオ時間使用量**：ユーザーがビデオストリームのサブスクリプションに成功すると、ビデオ時間使用量が発生します。オーディオストリームとビデオストリームを同時にサブスクリプションする場合、ビデオ使用量のみが計算されるので、ご注意ください。
-   **オーディオ時間使用量**：ユーザーがビデオストリームをサブスクリプションしていない場合、オーディオストリームをサブスクリプションするか否かにかかわらず、オーディオ時間使用量が発生します。すなわち、ユーザーがルームに参加した後、ビデオストリームをサブスクリプションした場合、ビデオ使用量のみが計算されるが、ビデオまたはオーディオストリームをサブスクリプションしていない場合は、ルームに滞在する時間が計算され、オーディオ使用量とします。

### ステップ3：各グレードの単価。

| 使用量のタイプ          | 単価（米ドル/1000分） | ユーザーがサブスクリプションしたビデオの総解像度                                     |
| :---------------- | :------------------ | ------------------------------------------------------------ |
| オーディオ              | 0.99                | -                                                            |
| ハイビジョン（HD）        | 3.99                | 解像度 ≤ 921,600（1280x720）                                 |
| フルハイビジョン（Full HD） | 8.99                | 921,600（1280 × 720）＜ 解像度 ≤ 2,073,600（1920 × 1080）    |
| ビデオ2K                | 15.99               | 2,073,600 (1920 × 1080) ＜ 解像度 ≤ 3,686,400 （2560 × 1440） |
| ビデオ4K               | 35.99               | 3,686,400 （2560 × 1440）＜ 解像度 ≤ 8,847,360 （4096 × 2160） |

例えば、ユーザーAが960×720の解像度で2つのビデオストリームを同時にサブスクリプションする場合、このユーザーが受信するビデオの総解像度は960×720+960×720=1,382,400となり、そのビデオ使用量はFHDタイプの単価で課金されます。



## 課金の例1

本節では、TRTCの費用計算について説明します。

6人のユーザーが同時に1つのチャンネルに加入し、60分間のビデオインタラクティブライブライブストリーミングを行ったとします。

ビデオインタラクティブストリーミングにはキャスター3名（キャスターA、B、C）がおり、キャスターAのビデオ解像度は960×720、キャスターBとCのビデオ解像度は640×480です。視聴者2名がすべてのキャスターのビデオストリームをサブスクリプションしたが、もう1人の視聴者がビデオストリームでなくオーディオストリームだけをサブスクリプションしたとします。さらに、キャスターAは、チャンネル内の他のすべてのユーザーと画面を共有しました。この場合、送受信される画面共有ストリームの解像度は1920×1080となります。

### ステップ1：各ユーザーがサブスクリプションしたビデオ総解像度および時間使用量を計算します

下表は、各ユーザーが受信するビデオストリームの総解像度を計算して、各ユーザーのビデオ使用量のグレードおよび対応する単価を得る方法について示します：

| ユーザー              | サブスクリプションしたビデオストリーム                            | ビデオの解像度                                  | 総解像度  | 総解像度のグレード | 時間（分） |
| :---------------- | :-------------------------------------- | :-------------------------------------------- | :-------- | :----------- | ------------ |
| キャスターA + 画面共有 | キャスターB+キャスターCのビデオストリーム                     | 640 × 480 × 2                                 | 614,400   | ハイビジョン (HD)    | 60           |
| キャスターB            | キャスターA + キャスターC + キャスター Aが共有した画面ビデオストリーム | (960 × 720) + (640 × 480) + (1920 × 1080)     | 3,072,000 | ビデオ2K       | 60           |
| キャスター C            | キャスターA +キャスターB + キャスターAが共有した画面ビデオストリーム  | (960 × 720) + (640 × 480) + (1920 × 1080)     | 3,072,000 | ビデオ2K       | 60           |
| 視聴者1            | キャスター3名+キャスターAが共有した画面 | (960 × 720) + (640 × 480 × 2) + (1920 × 1080) | 3,379,200 | ビデオ2K       | 60           |
| 視聴者2            | キャスター3名+キャスターAが共有した画面 | (960 × 720) + (640 × 480 × 2) + (1920 × 1080) | 3,379,200 | ビデオ2K       | 60           |
| 視聴者3            | ビデオストリームでなく、オーディオストリームだけをサブスクリプションします              | -                                             | -         | オーディオ         | 60           |

図例：

![課金説明例 -2@2x](https://qcloudimg.tencent-cloud.cn/raw/b9284fc7114058229815f4ce13168aa3.png)

### ステップ2：対応するグレードの単価を検索し、計算式により費用を計算します

**月額料金** = **オーディオ時間使用量** × **オーディオ単価** + **各グレードのビデオ時間使用量** × **対応するビデオ単価**で上記シーンの費用を計算します：

<table>
     <tr>
         <th style="text-align:center">有料サービス（ビデオ解像度のグレード）</th>
         <th style="text-align:center">合計使用量（分） = 各ユーザーの使用量の総和</th>
         <th style="text-align:center">単価（米ドル/1000分）</th>
         <th style="text-align:center">各サービス料金（米ドル）</th>
         <th style="text-align:center">合計料金（米ドル）（小数点第2位を四捨五入）</th>
     </tr>
     <tr>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">60 × 1 = 60</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(60/1000) × 3.99 = 0.2394</td>
         <td style="text-align:center" rowspan="3">4.14</td>
     </tr>
     <tr>
         <td style="text-align:center">ビデオ2K</td>
         <td style="text-align:center">60 × 4 = 240</td>
         <td style="text-align:center">15.99</td>
         <td style="text-align:center">(240/1000) × 15.99 = 3.8376</td>
     </tr>
 		 <tr>
         <td style="text-align:center">オーディオ</td>
         <td style="text-align:center">60 × 1 = 60</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">(60/1000) × 0.99 = 0.0594</td>
     </tr>
</table>


## 課金の例2

本節では、TRTCの費用計算について説明します。
6人のユーザーが同時に1つのチャンネルに加入し、60分間のビデオインタラクティブライブライブストリーミングを行ったとします。
ビデオインタラクティブストリーミングにはキャスター4名（キャスターA、B、C、D）がおり、キャスターA・B・Cが設定するライブストリーミングのビデオ解像度は480 × 480、キャスターDはオーディオストリームだけをプッシュします。視聴者1名がすべてのキャスターのビデオストリームをサブスクリプションし、もう1人の視聴者がビデオストリームでなくオーディオストリームだけをサブスクリプションしたとします。

### ステップ1：各ユーザーがサブスクリプションしたビデオ総解像度および時間使用量を計算します

下表は、各ユーザーが受信するビデオストリームの総解像度を計算して、各ユーザーのビデオ使用量のグレードおよび対応する単価を得る方法について示します：

| ユーザー   | サブスクリプションしたビデオストリーム                                  | ビデオの解像度  | 解像度の和 | ビデオ総解像度のグレード | 時間（分） |
| ------ | --------------------------------------------- | ------------- | ---------- | ---------------- | ------------ |
| キャスターA | キャスターB + キャスターCのビデオストリーム + キャスターDのオーディオストリーム         | 480× 480 × 2  | 460,800    | ハイビジョン (HD)        | 60           |
| キャスターB | キャスターA + キャスターCのビデオストリーム + キャスターDのオーディオストリーム         | 480× 480 × 2  | 460,800    | ハイビジョン (HD)        | 60           |
| キャスターC | キャスターA + キャスターBのビデオストリーム + キャスターDのオーディオストリーム         | 480× 480 × 2  | 460,800    | ハイビジョン (HD)        | 60           |
| キャスターD | キャスターA + キャスターB + キャスターCのビデオストリーム                 | 480 × 480 × 3 | 691,200    | ハイビジョン (HD)        | 60           |
| 視聴者1 | キャスターA + キャスターB + キャスターCのビデオストリーム + キャスターDのオーディオストリーム | 480 × 480 × 3 | 691,200    | ハイビジョン (HD)        | 60           |
| 視聴者2 | ビデオストリームでなく、オーディオストリームだけをサブスクリプションしました                    | -             | -          | オーディオ             | 60           |

### ステップ2：対応するグレードの単価を検索し、計算式により費用を計算します。

**月額料金** = **オーディオ時間使用量** × **オーディオ単価** + **各グレードのビデオ時間使用量** × **対応するビデオ単価**で上記シーンの費用を計算します：

<table>
     <tr>
         <th style="text-align:center">有料サービス（ビデオ解像度のグレード）</th>
         <th style="text-align:center">合計使用量（分） = 各ユーザーの使用量の総和</th>
         <th style="text-align:center">単価（米ドル/1000分）</th>
         <th style="text-align:center">各サービス料金（米ドル）</th>
         <th style="text-align:center">合計料金（米ドル）（小数点第2位を四捨五入）</th>
     </tr>
     <tr>
         <td style="text-align:center">HD</td>
         <td style="text-align:center">60 × 5 = 300</td>
         <td style="text-align:center">3.99</td>
         <td style="text-align:center">(300/1000) × 3.99 = 1.197</td>
         <td style="text-align:center" rowspan="3">1.26</td>
     </tr>
 		 <tr>
         <td style="text-align:center">オーディオ</td>
         <td style="text-align:center">60 × 1 = 60</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">(60/1000) × 0.99 = 0.0594</td>
     </tr>
</table>


## 注意事項

ここでは参考として、詳細な注意事項についてご説明します。

### 価格計算ツール

[TRTC価格計算ツール](https://intl.cloud.tencent.com/pricing/trtc/calculator)を確認してください。

### 時間使用量の精度

TRTCは、時間の集計精度は秒とし、その月の累計秒数を分数に変換した上で課金します。毎月の使用量が各月末に決済されると、TRTCはその月に発生したオーディオと各タイプのビデオ使用量（単位は秒）を合算し、60で除してオーディオの分数と各タイプのビデオの分数を算出し、最後に**切り上げ**ます。例えば、1か月に59秒のオーディオ時間使用量が発生した場合、オーディオ使用量データは1分としてカウントされます。61秒のビデオ時間使用量が発生した場合、ビデオ使用量データは2分としてカウントされます。月間使用量の誤差は1分以内です。

### デュアルストリーム解像度

デュアルストリームモードでは、ユーザーの解像度の計算方法は次のとおりです：

-   高画質ストリームをサブスクリプションする場合、ユーザーの総解像度は、送信者が設定した高画質ストリームの解像度に基づいて計算されます。
-   低画質ストリームをサブスクリプションする場合、ユーザーの総解像度は、ユーザーが実際に受信した解像度に基づいて計算されます。

### 画面共有ストリームの解像度

お客様のシナリオに画面共有が含まれる場合、画面共有ストリームのビデオ単価は、`TRTCVideoEncParam`で設定したビデオ解像度に基づきます。設定方法については、次の説明をご参照ください：

-   フルプラットフォームC++:[startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd)
-   iOS: [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4)
-   macOS: [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)
-   Android:[startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f)

Web端末では、デバイスとブラウザの制限により、一部のブラウザは設定された画面プロパティに完全に適応できない場合があります。この場合、ブラウザが自動的に解像度を調整し、実際の解像度に応じて料金が計算されます。詳細については、[setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile)をご参照ください。

### その他の製品またはサービスの料金

お客様のシナリオが、オーディオ・ビデオ通話やインタラクティブライブストリーミングだけでなく、[クラウドレコーディング](https://intl.cloud.tencent.com/document/product/647/45176)などその他のTRTC製品またはサービスにも関連する場合、追加料金がかかります。詳細は、各TRTC製品またはサービスの課金説明をご参照ください。
