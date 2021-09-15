
[](id:Billing_items)
## 使用量の統計方法

Tencent Real-Time Communication （TRTC）は[ルーム](https://intl.cloud.tencent.com/document/product/647/37714)内のすべてのユーザーによる**音声時間**から、音声通話サービスの使用量を統計します。

- ユーザーがTRTCルームに滞在する時間を、そのユーザーの音声時間として計算します。
- ユーザーがTRTCルームへの入室に成功後、課金が開始されます。ルーム内に1人のユーザーしかいない場合も、音声時間が計算されます。
- ユーザーは同じルームに何度も出入りすることがありますが、TRTCはその複数の音声時間をリアルタイムでカウントし、合計します。

>!音声時間の統計精度は秒とし、当月の累計秒数を分数に変換してから課金します。1分未満は1分で計算します。

[](id:Fixed_price)
## サービス料金
音声通話サービスの公表価格は下表のとおりです。

|課金項目|単価（米ドル/1000分）|
|---|---|
|音声時間|0.99|

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
  例えば、2021年5月1日に購入したパッケージの有効期間は、2021年5月1日～2022年5月31日となります。

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
>!この課金例は公表価格を採用して計算しています。[一般パッケージを購入](https://buy.cloud.tencent.com/trtc)することにより料金を節約することができます。

ユーザーA、B、Cの3人がTRTCルーム内に30分間連続して同時に滞在したとします。A、B、Cの3人は終始ビデオ画面の受信を行わず、音声に基づいての課金となります。

#### 分析：
- **音声時間のみの料金 = 音声時間単価 × すべてのユーザーの音声時間の合計**
- このTRTCルームで発生した音声時間の**料金総額**は`音声時間単価 × すべてのユーザーの音声時間の合計 = 0.99米ドル/1000分 × (30分 + 30分 + 30分) / 1000 = 0.0891米ドル`です。


[](id:estimate)
## 使用量と料金の見積もり
[TRTC価格計算機](https://buy.intl.cloud.tencent.com/pricing/trtc) を使用して、ご自身の業務で発生する音声通話の使用量と料金を見積もることができます。
1. 業務ニーズに基づき、**音声通話とビデオ通話の推定使用量** に、 **1日あたりの平均通話回数**、**1通話あたりの平均通話人数**、および **1人あたりの平均通話時間**を入力します。
2. 使用タイプで **音声**を選択すると、**月間推定使用量**を計算することができます。
![](https://main.qcloudimg.com/raw/871d7e1d43e83674f82a3960a079ff7c.png)
3. **料金見積もり**で、 **一般パッケージ消費量**、後払い方式と前払い方式を用いた場合の見積もり料金を計算することができます。
![](https://main.qcloudimg.com/raw/6bcfdbe34129fcc143e8cb4bd49ff07e.png)


## 関連ドキュメント
- [課金概要](https://intl.cloud.tencent.com/document/product/647/34610)
- [無料試用](https://intl.cloud.tencent.com/document/product/647/39784)
- [ボイス・インタラクティブストリーミング課金説明](https://intl.cloud.tencent.com/document/product/647/39785)
- [ビデオ・インタラクティブストリーミング課金説明](https://intl.cloud.tencent.com/document/product/647/39786)
- [ビデオ通話課金説明](https://intl.cloud.tencent.com/document/product/647/39788)
- [クラウドレコーディング課金説明](https://intl.cloud.tencent.com/document/product/647/38385)
- [Cloud MixTranscoding課金説明](https://intl.cloud.tencent.com/document/product/647/38929)
- [購入ガイドライン](https://intl.cloud.tencent.com/document/product/647/35440)
- [課金に関するよくあるご質問](https://intl.cloud.tencent.com/document/product/647/39789)
