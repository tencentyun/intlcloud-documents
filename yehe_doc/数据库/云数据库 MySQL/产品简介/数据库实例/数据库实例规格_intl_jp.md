このドキュメントでは、TencentDB for MySQLのインスタンス仕様について説明し、MySQLインスタンスの最新仕様を理解することができます。このドキュメントを参照して、各仕様の具体的な設定を確認できます。

## 2ノード/3ノード（ローカルSSDディスク）
マスターインスタンス（2ノード/3ノード構造）、読取専用インスタンス、ディザスタリカバリインスタンスの仕様情報については、この表を参照できます。
<table class="table-striped">
<tbody>
<tr><th>隔離ポリシー</th><th>CPU とメモリ</th><th>最大 IOPS</th><th>ストレージ容量</th></tr>
<tr>
<td rowspan="14">汎用型</td>
<td>1コア 1000MB</td><td>1200</td><td rowspan="4">25GB - 3000GB</td></tr>        
<tr>
<td>1コア 2000MB</td><td>2000</td></tr>
<tr>
<td>2コア 4000MB</td><td>4000</td></tr>
<tr>
<td>4コア 8000MB</td><td>8000</td></tr>
<tr>
<td>4コア 16000MB</td><td>14000</td><td rowspan="6">25GB - 4000GB</td></tr>
<tr>
<td>8コア 16000MB</td><td>20000</td></tr>
<tr>
<td>8コア 32000MB</td><td>28000</td></tr>
<tr>
<td>16コア 32000MB</td><td>32000</td></tr>
<tr>
<td>16コア 64000MB</td><td>40000</td></tr>
<tr>
<td>16コア 96000MB</td><td>40000</td></tr>
<tr>
<td>16コア 128000MB</td><td>40000</td><td rowspan="3">25GB - 8000GB</td></tr>
<tr>
<td>24コア 244000MB</td><td>60000</td></tr>
<tr>
<td>32コア 256000MB</td><td>80000</td></tr>
<tr>
<td>48コア 488000MB</td><td>120000</td><td rowspan="1">25GB - 12000GB</td></tr>
<tr>
<td rowspan="26">独占型</td>
<td>2コア 16000MB</td><td>8000</td><td rowspan="7">25GB - 3000GB</td></tr>        
<tr>
<td>4コア 16000MB</td><td>10000</td></tr>
<tr>
<td>4コア 24000MB</td><td>13000</td></tr>
<tr>
<td>4コア 32000MB</td><td>16000</td></tr>
<tr>
<td>8コア 32000MB</td><td>32000</td></tr>
<tr>
<td>8コア 48000MB</td><td>36000</td></tr>
<tr>
<td>8コア 64000MB</td><td>40000</td></tr>
<tr>
<td>12コア 48000MB</td><td>36000</td><td rowspan="15">25GB - 6000GB</td></tr>
<tr>
<td>16コア 64000MB</td><td>60000</td></tr>
<tr>
<td>12コア 72000MB</td><td>40000</td></tr>
<tr>
<td>12コア 96000MB</td><td>48000</td></tr>
<tr>
<td>16コア 96000MB</td><td>60000</td></tr>
<tr>
<td>24コア 96000MB</td><td>72000</td></tr>
<tr>
<td>16コア 128000MB</td><td>60000</td></tr>
<tr>
<td>32コア 128000MB</td><td>80000</td></tr>
<tr>
<td>24コア 144000MB</td><td>76000</td></tr>
<tr>
<td>24コア 192000MB</td><td>80000</td></tr>
<tr>
<td>32コア 192000MB</td><td>90000</td></tr>
<tr>
<td>48コア 192000MB</td><td>120000</td></tr>
<tr>
<td>32コア 256000MB</td><td>100000</td></tr>
<tr>
<td>48コア 288000MB</td><td>140000</td></tr>
<tr>
<td>48コア 384000MB</td><td>140000</td></tr>
<tr>
<td>64コア 256000MB</td><td>150000</td><td rowspan="2">25GB - 9000GB</td></tr>
<tr>
<td>64コア 384000MB</td><td>150000</td></tr>
<tr>
<td>64コア 512000MB</td><td>150000</td><td rowspan="2">25GB - 12000GB</td></tr>
<tr>
<td>90コア 720000MB</td><td>150000</td></tr>
</tbody></table>        

>?ストレージ容量の上限は、地域ごとにインスタンスの仕様によって異なる場合があります。実際の購入ページをご参照ください。

## シングルノード（SSD Cloud Block Storage）
<table class="table-striped">
<thead><tr><th>隔離ポリシー</th><th>CPUとメモリ</th><th>最大IOPS</th><th>最大スループット</th><th>ストレージ容量</th></tr></thead>
<tbody>
<tr>
<td rowspan="8">基本タイプ</td>
<td>1コア1000MB</td><td rowspan="8">ランダムIOPS性能計算式：ランダムIOPS = min{1800 + 30 × 容量（GB）, 26000}<br>最大IOPS：26000</td><td rowspan="8">スループット性能計算式(MB/s)：スループット = min{120 + 0.2 × 容量（GB）, 260}<br>最大スループット(MB/s)：260MB/s</td><td rowspan="8">20GB - 32000GB</td></tr>
<tr>
<td>1コア2000MB</td></tr>
<tr>
<td>2コア4000MB</td></tr>
<tr>
<td>2コア8000MB</td></tr>
<tr>
<td>4コア8000MB</td></tr>
<tr>
<td>4コア16000MB</td></tr>
<tr>
<td>8コア16000MB</td></tr>
<tr>
<td>8コア32000MB</td></tr>
</tbody></table>

## シングルノード（強化型SSD CBS）
<table class="table-striped">
<thead><tr><th>隔離ポリシー</th><th>CPUとメモリ</th><th>最大IOPS</th><th>最大スループット</th><th>ストレージ容量</th></tr></thead>
<tbody>
<tr>
<td rowspan="8">基本タイプ</td>
<td>1コア1000MB</td><td rowspan="8">ランダムIOPS性能計算式：ランダムIOPS = min{1800 + 50 × 容量(GB), 50000}<br>最大IOPS：50000</td><td rowspan="8">スループット性能計算式（MB/s）：スループット = min{120 + 0.5 × 容量(GB), 350}<br>最大スループット（MB/s）：350MB/s</td><td rowspan="8">20GB - 32000GB</td></tr>
<tr>
<td>1コア2000MB</td></tr>
<tr>
<td>2コア4000MB</td></tr>
<tr>
<td>2コア8000MB</td></tr>
<tr>
<td>4コア8000MB</td></tr>
<tr>
<td>4コア16000MB</td></tr>
<tr>
<td>8コア16000MB</td></tr>
<tr>
<td>8コア32000MB</td></tr>
</tbody></table>
