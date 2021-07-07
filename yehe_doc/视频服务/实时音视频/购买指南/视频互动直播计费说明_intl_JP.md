>! このドキュメントは、TRTC低遅延ライブストリーミングルーム内の課金に対しての関連説明のみを行っています。TRTCルーム内のオーディオ・ビデオストリーミングをCSSシステムにバイパスし、視聴者がライブCDNで視聴した場合、追加料金が発生します。詳細については、[CDN relayed live streaming≻関連費用]】(https://intl.cloud.tencent.com/document/product/647/35242)をご参照ください。


<span id="Billing_items"></span>
## 使用量の統計方法

Tencent Real-Time Communication （TRTC）は[ルーム](https://intl.cloud.tencent.com/document/product/647/37714)内のすべてのユーザーによる[ビデオ時間](#v_duration)と[音声時間](#s_duration)から、ビデオ・インタラクティブストリーミングサービスの使用量を統計します。

>!時間の統計精度は秒とし、当月の累計秒数を分数に変換してから課金します。1分未満は1分で計算します。


<span id="v_duration"></span>
### ビデオ時間
ビデオ時間とは、ユーザーがTRTCルームに入った後、オーディオ・ビデオストリーミングを購読し、ビデオ画面の受信に成功した時間を指します。TRTCはユーザーが**実際に受信するビデオ解像度**によってビデオのグレードを区分し、異なるグレードに対するビデオ時間に対してそれぞれ課金します。
ビデオのグレードと解像度の対応関係は下表のとおりです。

|ビデオのグレード|実際に受信した解像度|
|-------|--------|
|標準SD|640 × 480（480を含む）以下|
|高精細度HD|640 × 480 - 1280 × 720（720を含む）|
|超高精細度HD+|1280 × 720より上|

- ユーザーがビデオを購読する場合、そのビデオにオーディオが含まれているかどうかに関わらず、ビデオ時間のみを1回カウントし、音声時間を重複して計算することはありません。
- 1人のユーザーが同時に複数のビデオを購読する場合、その購読する各ビデオ時間を別々にカウントし、合計します。
- TRTCプラットフォーム全体のSDKが、ビデオの解像度を制限することはありません。実際のビジネスニーズに応じて[画質の設定]」(https://intl.cloud.tencent.com/document/product/647/35153)を自分で行うことができます。


<span id="s_duration"></span>
### 音声時間
ビデオ・インタラクティブストリーミングシーンの音声時間 = ユーザーがTRTCルームにいる総滞在時間 - ビデオ画面受信時の滞在時間。
例えば、某ユーザーが00:00にTRTCルームに入り、00:50にルームを退出する場合、ルーム内の滞在状況は下図のとおりです。
![](https://main.qcloudimg.com/raw/ff9f19240d4345825f6b53c03e088e26.png)
図中の青色の部分はそのユーザーの音声時間を記しています。`総滞在時間 - ビデオ画面受信時の滞在時間 = 50分 - 15分 = 35分`。


- ユーザーがビデオを購読していない場合のみ、音声時間がカウントされます。
- ユーザーがTRTCルームへの入室に成功した後、ビデオの購読がない場合は、アップストリームフローがなくても音声時間がカウントされます。
- ユーザーは同じルームに何度も出入りすることがありますが、TRTCはその複数の音声時間をリアルタイムでカウントし、合計します。


<span id="Fixed_price"></span>
## サービス料金

ビデオ・インタラクティブストリーミングサービスの公表価格は下表のとおりです。

|課金項目|単価（米ドル/1000分）|
|---|---|
|音声|0.99|
|標準SD|1.99|
|高精細度HD|3.99|
|超高精細度HD+|14.99|

<span id="Billing_method"></span>
## 課金方式
お支払い方法として、TRTCは**前払いパッケージ**と**後払い**をサポートしています。デフォルトでは前払いパッケージを採用し、後払いは購入したパッケージを消費したり、期限切れになったりした後に自動的に開始され、直接開始することはできません。

<span id="pre-payment"></span>
### 前払いパッケージ

TRTCはオーディオビデオ一般パッケージを提供します。**1:2:4:15**の割合で、それぞれ音声、標準SD、高精細度HD、超高精細度HD+の時間を差し引きます。例えば、HDビデオ時間1分間は、一般パッケージから4分間差し引かれます。
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
         <td style="text-align:center">50</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.941</td>
         <td style="text-align:center">47</td>   
         <td style="text-align:center"><95%</td>     
     </tr> 
     <tr>
         <td style="text-align:center">300 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.891</td>
         <td style="text-align:center">267</td>   
         <td style="text-align:center"><90%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.842</td>
         <td style="text-align:center">841</td>   
         <td style="text-align:center"><85%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.792</td>
         <td style="text-align:center">2376</td>   
         <td style="text-align:center">80%</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">カスタマイズパッケージ</td>   
         <td style="text-align:center">0 < T < 50</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">パッケージ内単価*パッケージ時間 T</td>   
         <td style="text-align:center">100%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">50 ≤ T ＜ 300</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.941</td>
         <td style="text-align:center">95%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">300 ≤ T ＜ 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.891</td>
         <td style="text-align:center">90%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T ＜ 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.842</td>
         <td style="text-align:center">85%</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.792</td>
         <td style="text-align:center">80%</td>   
     </tr> 
</table>


>?表中のパッケージ内単価は1000分ごとの単価を小数点以下3桁まで切り上げ、実際の課金額は1分ごとの単価を小数点以下8桁にします。

一般パッケージの説明：
- 一般パッケージの有効期間は購入当日から翌年の同月末とします。
 例えば、2020年05月01日に購入したパッケージの有効期間は、2020年05月01日～2021年05月31日となります。
- 一般パッケージは重複して購入でき、各タイプの使用量で実際に生じた時間に応じて、一般パッケージから対応する分数が差し引かれます。先に期限切れとなるパッケージから優先的に差し引かれます。
- 新規購入パッケージの支払い成功後、5分前後で有効となります。** 新規購入パッケージが有効になると、新パッケージ購入当日の0時から生じた分で、その他のパッケージから差し引かれていない使用量がすぐに控除されます**。
- ユーザーのオンライン業務の正常な運営に影響を与えないように、**一般パッケージを使い切ったり、期限切れとなったりしても自動的にサービス停止にはならず**、パッケージ分を超えた使用量には[後払い](#post-payment)の課金方式が採用されます。
- すべての一般パッケージが期限切れになると、未使用の分数は自動的にリセットされ、元に戻すことはできません。


<span id="post-payment"></span>
### 後払い
サービス使用量に対して差し引き可能なパッケージがない、またはパッケージの残高を超えたという場合は、後払い方式を採用し、[公表価格](#Fixed_price)で課金します。
TRTC後払いには[日次決済](#daily)と[月次決済](#monthly)の2つの決済サイクルがあります。

#### 日次決済後払い<span id="daily)
2020年09月01日以降に初めてTRTCコンソールで[アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)を作成したユーザーは、後払いの効力発生後、デフォルトで**日次決済**の決算方式が選択されます。日ごとに課金され、毎日午前10時に、前日に発生した料金が引き落とされます。


<span id="monthly"></span>
#### 月次決済後払い
2020年08月31日およびそれより前に初めてTRTCコンソールで[アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)を作成したユーザーは、後払いの効力発生後、デフォルトで**月次決済**の決算方式が採用されます。月ごとに課金され、毎月01日 - 05日に、アカウントの残高から前月に発生した料金が引き落とされます。詳細については、[アカウント請求書](https://intl.cloud.tencent.com/document/product/555/7432)を基準とします。
>!
- 後払いは先にパッケージを購入し、購入したすべてのパッケージが消費されるか、または期限切れになった後に自動的に開始され、直接開始することはできません。
- 決済サイクルは自分で変更できません。月次決済を日次決済に変更したい場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してサポートを受けることができます。
- アカウントの残高が不足し、請求書料金を差し引くことができない時は、その他のTencent Cloudサービスも、アカウントの料金不足により自動的にサービス停止となることがあります。例えば、クラウドレコーディングは**Cloud Streaming Services**と**Video on Demand**に依存し、Tencent Cloudアカウントが料金不足の場合、クラウドレコーディングが失敗する恐れがあります。

<span id="Billing_examples"></span>
## 課金の例
>!この課金例は公表価格を採用して計算しています。[パッケージを購入](https://buy.cloud.tencent.com/trtc)の方式により料金を節約することができます。

### 音声時間のみの例
ユーザーA、B、Cの3人がTRTCルーム内に30分間連続して同時に滞在したとします。A、B、Cの3人は終始ビデオ画面の受信を行いませんでした。
このTRTCルームで発生した音声時間の**料金総額**は`音声時間単価 × すべてのユーザーの音声時間の合計 = 0.99米ドル/1000分 × (30分 + 30分 + 30分) / 1000 = 0.0891米ドル`です。

### ビデオ時間のみの例

ユーザーA、BがTRTCルーム内に45分間連続して同時に滞在したとします。A、Bともに相手のビデオストリームを終始受信しました。A、Bが実際に受信したビデオ解像度は下表のとおりです。

<table>
     <tr>
         <th style="text-align:center">時間</th>  
         <th style="text-align:center"> AがBを受信した解像度</th> 
         <th style="text-align:center"> BがAを受信した解像度</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="1">前半30分</td>   
         <td style="text-align:center">1280 × 720（HD）</td>
         <td style="text-align:center">1920 × 1080（FHD）</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="1">後半15分</td>   
         <td style="text-align:center">640 × 360（SD）</td> 
         <td style="text-align:center">640 × 360（SD）</td>
     </tr> 
</table>

**分析：**
- Aによる使用量および料金：
  - AがBを受信した解像度は、前半30分がHDグレード、後半15分がSDグレード。
  - Aによる料金は ` HDビデオ時間単価 × HDビデオ時間 + SDビデオ時間単価 × SDビデオ時間 = 3.99米ドル/1000分 × (30分 / 1000) + 1.99米ドル/1000分 × (15分 / 1000）= 0.14955米ドル`。
- Bによる使用量および料金：
  - BがAを受信した解像度は、前半30分がFHDグレード、後半15分がSDグレード。
  - Bによる料金は ` FHDビデオ時間単価 × FHDビデオ時間 + SDビデオ時間単価 × SDビデオ時間 = 14.99米ドル/1000分 × (30分 / 1000) + 1.99米ドル/1000分 × (15分 / 1000）= 0.47955米ドル`。

このTRTCルームで発生した**料金総額**は `ユーザーAによる料金 + ユーザーBによる料金 = 0.6291米ドル `です。

### 音声時間とビデオ時間の混合例

ユーザーA、BがTRTCルーム内に45分間連続して同時に滞在したとします。AはBのビデオストリームを終始受信しました。Bは前半30分はAのビデオストリームを受信し、後半15分はAのビデオストリームを受信しませんでした。A、Bが実際に受信したビデオ解像度は下表のとおりです。

<table>
     <tr>
         <th style="text-align:center">時間</th>  
         <th style="text-align:center">AがBを受信した解像度</th> 
         <th style="text-align:center">BがAを受信した解像度</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="1">前半30分</td>   
         <td style="text-align:center">1280 × 720（HD）</td>
         <td style="text-align:center">1920 × 1080（FHD）</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="1">後半15分</td>   
         <td style="text-align:center">640 × 360（SD）</td> 
         <td style="text-align:center">音声（ビデオなし）</td>
     </tr> 
</table>


**分析：**
- Aによる使用量および料金：
  - AがBを受信した解像度は、前半30分がHDグレード、後半15分がSDグレード。
  - Aによる料金は ` HDビデオ時間単価 × HDビデオ時間 + SDビデオ時間単価 × SDビデオ時間 = 3.99米ドル/1000分 × (30分 / 1000) + 1.99米ドル/1000分 × (15分 / 1000)= 0.14955米ドル`。
- Bによる使用量および料金：
  - BがAを受信した解像度は、前半30分がFHDグレード、後半15分はAのビデオストリームを受信せず。
  - Bによる料金は `FHDビデオ時間単価 × FHDビデオ時間 + 音声時間単価 × 音声時間 = 14.99米ドル/1000分 × (30分 / 1000) + 0.99米ドル/1000分 × (15分 / 1000）= 0.46455米ドル`。

このTRTCルームで発生した**料金総額**は `ユーザーAによる料金 + ユーザーBによる料金 = 0.6141米ドル `です。



## 関連ドキュメント
- [課金概要](https://intl.cloud.tencent.com/document/product/647/34610)
- [無料試用](https://intl.cloud.tencent.com/document/product/647/39784)
- [ボイス・インタラクティブストリーミング課金説明](https://intl.cloud.tencent.com/document/product/647/39785)
- [音声通話課金説明](https://intl.cloud.tencent.com/document/product/647/39787)
- [ビデオ通話課金説明](https://intl.cloud.tencent.com/document/product/647/39788)
- [クラウドレコーディング課金説明](https://intl.cloud.tencent.com/document/product/647/38385)
- [Cloud MixTranscoding課金説明](https://intl.cloud.tencent.com/document/product/647/38929)
- [購入ガイドライン](https://intl.cloud.tencent.com/document/product/647/35440)
- [課金に関するよくあるご質問](https://intl.cloud.tencent.com/document/product/647/39789)
