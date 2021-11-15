>?この製品は、動的な価格設定ク​​エリとコスト見積もりをサポートするようになりました。詳細については、[価格設定センター](https://intl.cloud.tencent.com/pricing/cdb)にアクセスして、関連する費用を問い合わせて見積もります。

## 課金モード

TencentDB for MySQLは、サブスクリプション課金モードを提供するようになりました。従量課金制の価格は変わりません。



TencentDB for MySQLは、メモリとディスクの別個課金の販売方式をサポートし、ユーザーの多様な組み合わせにより多くの方法を提供します。

インスタンス価格計算式：インスタンス価格=メモリ仕様費用+ストレージ容量費用。






## 高度な機能

### バックアップ容量

バックアップ容量はサブスクリプション課金モードをサポートしていません。従量課金制の価格をご参照ください。

**インスタンス更新管理**

更新管理ページでインスタンスの一括更新、自動更新、不更新設定などの機能を利用できます。



**インスタンスのアップグレードアルゴリズム**

このインスタンスの有効期間をT日とし、ターゲット構成と既存の構成の間の月前払い費用の差額をCとすれば、アップグレード総費用の計算式はT/30Cとなります。

例えば、1コア、1000MBメモリ、100GBのディスクのインスタンス（前払金：24.511 USD/月）があり、あと15日で有効期限が切れるとします。現在、1コア、1000MBメモリ、200GBのディスク（前払金：34.653 USD /月）にアップグレードする必要がある場合、アップグレート合計料金=15/30(34.653-24.511)=5.071 USDです。



**インスタンスディスク容量制限超過説明**

ビジネス継続性を確保するには、ディスクの空き容量が不足したとき、データベースインスタンス仕様をアップグレードし、またはディスク容量を購入してください。

インスタンスに保存されているデータのサイズが容量制限を超えると、インスタンスはロックされ、データを読み取ることができますが、書き込むことができません。ロックを解除するには、容量を拡張するか、コンソールで一部のデータベーステーブルを削除する必要があります。

データベースがロック状態を繰り返しトリガするのを避けるために、インスタンスの空き領域が20%または50Gを超えた場合（2つ条件の1を満たすだけでよい）、インスタントがロック状態を解除し、通常の読出し /書込み機能を回復します。



**ディザスタリカバリインスタンスのトラフィック同期料金**

プロモーション期間のTencentDB for MySQLディザスタリカバリインスタンスのデータ同期トラフィックは、無料です。

市販化課金時間は別途通知します。

## 従量課金

従量課金は使用期間によって3つの階層に分けられます。

| 使用期間 | 階層価格 |
|---------|---------|
| 0時間＜使用期間 ≤ 96時間 | 従量課金の第1階層価格 |
| 96時間＜使用期間 ≤ 360時間 | 従量課金の第2階層価格 |
| 使用期間＞360時間 | 従量課金の第3階層価格 |

### インスタンス価格

#### 課金計算式
**総費用 = メモリ規格費用 + ストレージ容量費用 + バックアップスペース費用 + トラフィック費用（ 現在無料）**

#### 課金アイテム
<table>
<thead>
<tr>
<th width="15%">課金アイテム</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>メモリ規格費用<br></td>
<td>【購入】ページで選択したインスタンス仕様は、従量課金の階層価格を適用します。価格の詳細については、<a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">製品の価格設定</a>をご参照ください。</td>
</tr>
<tr>
<td>ストレージ容量費用</td>
<td>購入ページで選択したディスク容量は、従量課金の階層価格を適用します。価格の詳細については、<a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">製品の価格設定をご参照ください</a>。<br>ストレージ容量は、TencentDB for MySQLの実行に必要なデータファイル、共有テーブルスペース、エラーログファイル、REDO LOG、UNDO LOG、データディクショナリ、binlogなどを格納するために使用されます。</tr>
<tr>
<td>バックアップスペース費用</td>
<td>TencentDB for MySQLは、リージョンに基づいて一定の無料バックアップスペースを提供します。無料バックアップスペースの大きさはユーザーの所在地域におけるすべての2ノード、3ノードインスタンス（マスターインスタンスを含む）のストレージスペースの合計とします。<br>無料のバックアップスペースを超える場合の費用については、<a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">バックアップスペースの費用に関する説明</a>をご参照ください。</td>
</tr>
<tr>
<td>トラフィック費用</td>
<td>パブリックネットワークのトラフィック費用を指し、現在無料です。</td>
</tr>
</tbody></table>


#### 従量課金制

##### 高可用性エディション
<table >
  <td rowspan=2>リージョン</td>
  <td colspan=3 >メモリ価格（USD/GB/時間）</td>
  <td rowspan=2 >ディスク（USD/GB/時間）</td>
 </tr>
 <tr >
  <td >第1階層</td>
  <td>第2階層</td>
  <td>第3階層</td>
 </tr>
 <tr >
  <td >広州</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>清遠</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>上海</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>北京</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>成都</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>重慶</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>中国香港</td>
  <td class=xl66 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>中国台北</td>
  <td class=xl65 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>シンガポール</td>
  <td class=xl65 align=right>0.0705</td>
  <td class=xl65 align=right>0.0528</td>
  <td class=xl65 align=right>0.0352</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>バンコク</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>ムンバイ</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>ソウル</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>東京</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>シリコンバレー</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>バージニア</td>
  <td class=xl65 align=right>0.0444</td>
  <td class=xl65 align=right>0.0333</td>
  <td class=xl65 align=right>0.0222</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>トロント</td>
  <td class=xl65 align=right>0.0265</td>
  <td class=xl65 align=right>0.0199</td>
  <td class=xl65 align=right>0.0133</td>
  <td class=xl65 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>フランクフルト</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>モスクワ</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 </tr>
</table>

##### 読み取り専用インスタンス

<table>
  <td rowspan=2>リージョン</td>
  <td colspan=3 >メモリ価格（USD/GB/時間）</td>
  <td rowspan=2 >ディスク（USD/GB/時間）</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>第1階層</td>
  <td class=xl1529815>第2階層</td>
  <td class=xl1529815>第3階層</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>広州</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>清遠</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>上海</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>北京</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>成都</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>重慶</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>中国香港</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>中国台北</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>シンガポール</td>
  <td class=xl6529815 align=right>0.0352</td>
  <td class=xl6529815 align=right>0.0264</td>
  <td class=xl6529815 align=right>0.0176</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>バンコク</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>ムンバイ</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>ソウル</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>東京</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>シリコンバレー</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>バージニア</td>
  <td class=xl6529815 align=right>0.0222</td>
  <td class=xl6529815 align=right>0.0167</td>
  <td class=xl6529815 align=right>0.0111</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>トロント</td>
  <td class=xl6529815 align=right>0.0133</td>
  <td class=xl6529815 align=right>0.0099</td>
  <td class=xl6529815 align=right>0.0066</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>フランクフルト</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>モスクワ</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
</table>


## 課金の例
>?下記価格はあくまでも一例です。地域やキャンペーン、ポリシーの調整により具体的な価格が変動する場合があります。詳細な価格については公式サイトをご参照ください。
>

### サブスクリプション
広州地域の場合：
- 広州三区で4コア、8000MBのメモリ、500GBのディスク、有効期間1ヶ月のサブスクリプションTencentDB for MySQLインスタンス（高可用性エディション）を購入しました。
- 広州四区で4コア、8000MBのメモリ、200GBのディスク、有効期間1ヶ月のサブスクリプションTencentDB for MySQLインスタンス（高可用性エディション）を購入しました。

総費用 = メモリ規格費用 + ストレージ容量費用 + バックアップスペース費用

##### メモリ規格費用 + ストレージスペース費用
費用は次のように計算します。
メモリ規格費用 + ストレージスペース費用 = 2 × 114.93USD/月 + (500GB + 200GB) × 0.1014USD/GB/月 × 1か月 = 300.84USDです。

##### バックアップスペース費用
広州三区で稼働している高可用性エディションのインスタンスは、データベースのストレージスペースを毎月500GB購入し、広州4区で稼働している高可用性エディションのインスタンスは、データベースストレージスペースを毎月200GB購入すると、広州地域には毎月700GBの無料バックアップスペースがあります。

顧客は広州地域での合計バックアップストレージスペースが700GBを超えた場合（例えばデータバックアップは800GB、ログバックアップは100GBである）、1時間当りの課金スペース = 800 + 100 - 700 = 200GBとなります。顧客はこの200GBのためにバックアップスペース費用を支払う必要があります。その他はこれによって類推することができます。

バックアップスペース料金（時間）= 200GB（バックアップスペースを超えると実際のシナリオによって変化することがあります）×0.000127USD/GB/時間です。

### 従量課金
広州地域で4コア、8000MBのメモリ、500GBのディスク、有効期限400時間の従量課金TencentDB for MySQLインスタンスを購入しました。
第1階層料金：（0.0250USD/GB/時間×8GB+500GB × 0.0003）×96時間=33.6 USD
第2階層料金：（0.0200USD/GB/時間×8GB+500GB × 0.0003）×264時間=81.84USD
第3階層料金：（0.0150USD/GB/時間×8GB+500GB × 0.0003）×40時間=10.8USD
インスタンス料金=第1階層料金+第2階層料金+第3階層料金=126.24USD

## よくあるご質問
私のインスタンスはサブスクリプション課金モードですが、他の料金がかかっているのはなせですか。
バックアップスペースが無料利用枠を超えているかどうかを確認してください。無料利用枠を超えたバックアップスペースは課金されます。
バックアップスペースの使用情報は、[MySQLコンソール](https://console.cloud.tencent.com/cdb/backup) のデータベースのバックアップページで表示できます。バックアップスペース課金の詳細については、[バックアップスペースの費用に関する説明](https://cloud.tencent.com/document/product/236/36263)をご参照ください。

### 従量課金インスタンスが使用されていない場合、料金はかかりますか。
従量課金インスタンスが使用されなくても、そのまま課金されます。課金されることを避けるためにはタイムリーに廃棄してください。

#### どのようなファイルがストレージスペースに保存されますか。

- データファイル：作成されたテーブル、インデックスなどを含む、データが占めるスペース。
- システムファイル：共有テーブルスペース、エラーログファイル、REDO LOG、UNDO LOG、およびデータディクショナリを含みます。
- binlogファイル：すべてのDDLおよびDMLステートメントが記録されます（select、showなどのデータクエリステートメントを除く）。バイナリログの主な目的は、レプリケーションとデータリカバリです。変更されるデータが多いほど、生成されるbinlogも多くなります。生成された[binlogファイル](https://cloud.tencent.com/document/product/236/53513) はCOSにアップロードされ、ローカルbinlogが占めるスペースを削減します。

## 関連資料
- TencentDB for MySQLインスタンスは、コンソールまたはAPIから購入できます。詳細については、[購入方法](https://intl.cloud.tencent.com/document/product/236/5160)をご覧ください。
- TencentDB for MySQLインスタンスは、有効期限が切れてリソースが解放される前に、アラートメッセージをユーザーに送信します。詳細については、 [支払い延滞の説明](https://intl.cloud.tencent.com/document/product/236/5159)をご覧ください。
- TencentDB for MySQLインスタンスは、コンソールを介して返品・返金の申請をサポートしています。詳細については、 [返金について](https://intl.cloud.tencent.com/document/product/236/14618)をご覧ください。
- TencentDB for MySQLインスタンスの仕様は、アップグレードまたはダウングレードをサポートしています。詳細については、[インスタンスの仕様変更に基づく料金の調整](https://intl.cloud.tencent.com/document/product/236/32345)をご覧ください。
