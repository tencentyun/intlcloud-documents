

>! このドキュメントは、TRTC低遅延ライブストリーミングルーム内の課金に対しての関連説明のみを行っています。TRTCルーム内のオーディオビデオストリームをCSSシステムにバイパスし、視聴者がライブCDNで視聴した場合、追加料金が発生します。詳細については、[CDN relayed live streaming≻関連費用](https://intl.cloud.tencent.com/document/product/647/35242)をご参照ください。


[](id:Billing_items)
## 使用量の統計方法

Tencent Real-Time Communication （TRTC）は[ルーム](https://intl.cloud.tencent.com/document/product/647/37714)内のすべてのユーザーによる[ビデオ時間](#v_duration)と[音声時間](#s_duration)から、ビデオ・インタラクティブストリーミングサービスの使用量を統計します。

>!時間の統計精度は秒とし、当月の累計秒数を分数に変換してから課金します。1分未満は1分で計算します。


[](id:v_duration)
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
- TRTCの全プラットフォームのSDKはいずれもビデオの解像度に制限を設けていません。実際の業務ニーズに基づいて、ご自身で[画質の設定](https://intl.cloud.tencent.com/document/product/647/35153)を行うことができます。


[](id:s_duration)
### 音声時間
ビデオ・インタラクティブストリーミングシーンの音声時間 = ユーザーがTRTCルームにいる総滞在時間 - ビデオ画面受信時の滞在時間。
例えば、某ユーザーが00:00にTRTCルームに入り、00:50にルームを退出する場合、ルーム内の滞在状況は下図のとおりです。
![](https://main.qcloudimg.com/raw/b127abe248a205842a6216ccbd7c111e.png)
図中の青色の部分はそのユーザーの音声時間を記しています。`総滞在時間 - ビデオ画面受信時の滞在時間 = 50分 - 15分 = 35分`。


- ユーザーがビデオを購読していない場合のみ、音声時間がカウントされます。
- ユーザーがTRTCルームへの入室に成功した後、ビデオの購読がない場合は、アップストリームフローがなくても音声時間がカウントされます。
- ユーザーは同じルームに何度も出入りすることがありますが、TRTCはその複数の音声時間をリアルタイムでカウントし、合計します。


[](id:Fixed_price)
## サービス料金

ビデオ・インタラクティブストリーミングサービスの公表価格は下表のとおりです。

| 課金項目   | 単価（米ドル/1000分） |
|---|---|
| 音声     | 0.99                |
| 標準SD  | 1.99                |
| 高精細度HD  | 3.99                |
| 超高精細度HD+ | 14.99               |

[](id:Billing_method)
## 課金方式
支払い方式。TRTCは**前払いパッケージ**および**後払い**をサポートしており、デフォルトでは前払いパッケージが採用されます。ご自身で後払い方式を開始したい場合は、関連の[ドキュメント](https://intl.cloud.tencent.com/document/product/647/41979)をご参照ください。

[](id:pre-payment)
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
         <td style="text-align:center">25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">24</td>   
         <td style="text-align:center"><97%</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center"><92%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center"><87%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center"><82%</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">カスタマイズパッケージ</td>   
         <td style="text-align:center">0 < T < 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">パッケージ内単価*パッケージ時間 T</td>   
         <td style="text-align:center">100%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ T ＜ 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center"><97%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ T ＜ 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center"><92%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T ＜ 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center"><87%</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center"><82%</td>   
     </tr> 
</table>



>?表中のパッケージ内単価は1000分ごとの単価を小数点以下3桁まで切り上げ、実際の課金額は1分ごとの単価を小数点以下8桁にします。

一般パッケージの説明：

- 一般パッケージの有効期間は購入当日から翌年の同月末とします。
 例えば、2020年5月1日に購入したパッケージの有効期間は、2020年5月1日～2021年5月31日となります。
- 一般パッケージは重複して購入できます。各タイプの使用量は実際に発生した時間に応じて、一般パッケージから対応する分数が差し引かれます。先に期限切れとなるパッケージから優先的に差し引かれます。
- 新規購入パッケージの支払い成功後、5分前後で有効となります。** 新規購入パッケージが有効になると、新パッケージ購入当日の0時から生じた分で、その他のパッケージから差し引かれていない使用量がすぐに控除されます**。
- ユーザーのオンライン業務の正常な運営に影響を与えないように、**一般パッケージを使い切ったり、期限切れとなったりしても自動的にサービス停止にはならず**、パッケージ分を超えた使用量には[後払い](#post-payment)の課金方式が採用されます。
- すべての一般パッケージは期限切れになると、未消費の分数が自動的にリセットされ、元に戻すことはできなくなります。


[](id:post-payment)
### 後払い
サービス使用量に対して差し引き可能なパッケージがない、またはパッケージの残高を超えたという場合は、後払い方式を採用し、[公表価格](#Fixed_price)で課金します。
TRTC後払いには[日次決済](#daily)と[月次決済](#monthly)の2つの決済サイクルがあります。

[](id:daily)
#### 日次決済後払い
2020年9月1日以降に初めてTRTCコンソールで[アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)を作成したユーザーには、後払いの効力発生後、デフォルトで**日次決済**の決算方式が採用されます。日ごとに課金され、毎日午前10時に、前日に発生した料金が引き落とされます。


[](id:monthly)
#### 月次決済後払い
2020年8月31日およびそれ以前に初めてTRTCコンソールで[アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714) を作成したユーザーには、後払いの効力発生後、デフォルトで**月次決済**の決算方式が採用されます。月ごとに課金され、毎月1日から5日の間に、前月に発生した料金がアカウント残高から引き落とされます。詳細については[アカウント請求書](https://intl.cloud.tencent.com/document/product/555/7432) を基準とします。
>!
>- 決済サイクルはご自身で変更できません。月次決済を日次決済に変更したい場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category) してサポートを受けることができます。
>- アカウントの残高が不足し、請求書料金を差し引くことができない時は、その他のTencent Cloudサービスも、アカウントの料金不足により自動的にサービス停止となることがあります。例えば、クラウドレコーディングは**Cloud Streaming Services**と**Video on Demand**に依存し、Tencent Cloudアカウントが料金不足の場合、クラウドレコーディングが失敗する恐れがあります。

[](id:Billing_examples)
## 課金の例
>!この課金例は公表価格を採用して計算しています。[パッケージを購入](https://buy.cloud.tencent.com/trtc)することにより料金を節約することができます。

### 音声のみの例

ユーザーA、B、Cの3人がTRTCルーム内に30分間連続して同時に滞在したとします。A、B、Cの3人は終始ビデオ画面の受信を行わず、音声に基づいての課金となります。

#### 分析：
- **音声時間のみの料金 = 音声時間単価 × すべてのユーザーの音声時間の合計**
- このTRTCルームで発生した音声時間の**料金総額**は`音声時間単価 × すべてのユーザーの音声時間の合計 = 0.99米ドル/1000分 × (30分 + 30分 + 30分) / 1000 = 0.0891米ドル`です。

### 音声/ビデオの混合例

ユーザーA、B、CがTRTCルーム内に30分間連続して同時に滞在したとします。A、B、Cは下表のとおり、互いにオーディオビデオストリーミングを閲覧しました。

<table style="width:715px;">
<style>.markdown-text-box table td, .markdown-text-box table th {text-align: center;}
.tablestyle{position:absolute;width:1px;height:160px;top:0;left:0;background-color: #d9d9d9;transform:rotate(-69deg);transform-origin:top;}
.th1{position:absolute;right:20px;top:10px;}
.th2{position:absolute;right:80px;top:30px)
</style>
<tr>
<th style ="position:relative;width:150px" >
  <div class="tablestyle"></div>
  <div class="th1">送信側</div>
  <div class="th2">受信側</div></th>
  <th>A<br>640 × 360（SD）</th>
  <th>B<br>純粋なオーディオ</th>
  <th>C<br>1920 × 1080（FHD）</th>
</tr><tr>
  <td>A</td>
  <td>-</td>
  <td>&#10003;</td>
  <td>&#10003;</td>
</tr><tr>
  <td>B</td>
  <td>&#10003;</td>
  <td>-</td>
  <td>&#10003;</td>
</tr><tr>
  <td>C</td>
  <td>&#10003;</td>
  <td>&#10003;</td>
  <td>-</td>
</tr></table>


#### 分析：
- Aによる使用量および料金：
  - **Aによる料金 = AがBを受信した料金 + AがCを受信した料金**
  - AがBを受信した料金 = 音声時間単価 × 音声時間 = 0.99米ドル/1000分 × (30分 / 1000)= 0.0297米ドル
  - AがCを受信した料金 = 超高精細度ビデオ時間単価 × 超高精細度ビデオ時間 = 14.99米ドル/1000分 × (30分 / 1000)= 0.4497米ドル
  - Aによる料金は、AがBを受信した料金 + AがCを受信した料金 = 0.0297 + 0.4497 = 0.4794米ドル
- Bによる使用量および料金：
  - **Bによる料金 = BがAを受信した料金 + BがCを受信した料金**
  - BがAを受信した料金 = 標準ビデオ時間 × 標準時間 = 1.99米ドル/1000分 × (30分 / 1000)= 0.0597米ドル
  - BがCを受信した料金 = 超高精細度時間単価 × 超高精細度時間 = 14.99米ドル/1000分 × (30分 / 1000)= 0.4497米ドル
  - Bによる料金は、BがAを受信した料金 + BがCを受信した料金 =0.0597 + 0.4497= 0.5094米ドル

- Cによる使用量および料金：
  -  **Cによる料金 = CがAを受信した料金 + CがBを受信した料金**
  - CがAを受信した料金 = 標準ビデオ時間 × 標準時間 = 1.99米ドル/1000分 × (30分 / 1000)=0.0597米ドル
  - CがBを受信した料金 = 音声時間単価 × 音声時間 = 0.99米ドル/1000分 × (30分 / 1000)= 0.0297米ドル
  - Cによる料金は、CがAを受信した料金 + CがBを受信した料金= 0.0597 + 0.0297 =0.0894米ドル

このTRTCルームで発生した**料金総額**は `ユーザーAによる料金 + ユーザーBによる料金 + ユーザーCによる料金 = 1.0782米ドル `です。

[](id:estimate)
## 使用量と料金の見積もり
[TRTC価格計算機](https://buy.intl.cloud.tencent.com/pricing/trtc) を使用して、ご自身の業務で発生するボイス・インタラクティブストリーミングの使用量と料金を見積もることができます。
1.業務ニーズに基づき、**ボイス・インタラクティブストリーミング、ビデオ・インタラクティブストリーミングの推定使用量** に、 **1日あたりの平均ルーム数**、**ルーム1室あたりの平均キャスター数**、**ルーム1室あたりの平均視聴者数** および **ルーム1室あたり・ライブストリーミング1回あたりの平均時間**を入力します。
2. 使用タイプを **「標準SD」**、**「高精細度HD」** または **「超高精細度HD+」**から選択すると、**月間推定使用量**を計算することができます。
![](https://main.qcloudimg.com/raw/871d7e1d43e83674f82a3960a079ff7c.png)
3. **料金見積もり**で、 **一般パッケージ消費量**、後払い方式と前払い方式を用いた場合の見積もり料金を計算することができます。
![](https://main.qcloudimg.com/raw/6bcfdbe34129fcc143e8cb4bd49ff07e.png)



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