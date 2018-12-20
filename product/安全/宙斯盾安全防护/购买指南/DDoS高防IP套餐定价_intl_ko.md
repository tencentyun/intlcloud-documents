## DDoS 고도 방어 IP 세트 설명
### 세트 관련 용어
- **비BGP 3 IP** 
China Telecom, China Mobile, China Unicom 고도 방어 IP 각 1개, 총 3개 고도 방어 IP가 있습니다.
- **비BGP 2 IP**
China Telecom, China Mobile, China Unicom 고도 방어 IP 중의 2개, 총 2개 고도 방어 IP가 있습니다.
- **BGP + 비BGP 3 IP**
BGP, China Telecom, China Mobile, China Unicom 고도 방어 IP 각 1개, 총 4개 고도 방어 IP가 있습니다.
- **BGP + 비BGP 2 IP**
BGP 고도 방어 IP 1개, China Telecom, China Unicom, China Mobile 중의 고도 방어 IP 2개, 총 3개 고도 방어 IP가 있습니다.

### 네트워크 대역폭 최고 피크값

|대역폭 네트워크|China Telecom|China Unicom|China Mobile
|-|-|-|-|
|최저 보장 방어 대역폭의 최고 피크값|400Gbps|400Gbps|200Gbps|
|엘라스틱 방어 대역폭의 최고 피크값|600Gbps|600Gbps|200Gbps|

**예제:**
- 비BGP 3 IP 최저 보장 방어 400Gbps는 China Telecom 최저 보장 방어 400Gbps, China Unicom 최저 보장 방어 400Gbps, China Mobile 최저 보장 방어 200Gbps를 의미합니다.
- 비BGP 3 IP 엘라스틱 방어 500Gbps는 China Telecom 엘라스틱 방어 500Gbps, China Telecom 엘라스틱 방어 500Gbps, China Mobile 엘라스틱 방어 200Gbps를 의미합니다.

>?
>- 사용자가 200Gbps 이상의 최저 보장 방어 피크값을 선택하고 China Mobile 고도 방어 IP를 가지고 있는 경우, China Mobile 고도 방어 IP는 최고 200Gbps로만 구성됩니다.
>- 사용자가 200Gbps 이상의 엘라스틱 대역폭 보장 방어 피크값을 선택하고 China Mobile 고도 방어 IP를 가지고 있는 경우, China Mobile 고도 방어 IP는 최고 200Gbps로만 구성됩니다.



## 연간 특별 세트
|최저 보장 방어|비BGP 3 IP<br>(USD/년)|비BGP 2 IP<br>(USD/년)
|-|-|-|
|피크값 대역폭 150Gbps|70280|61033|
|피크값 대역폭 300Gbps|122682|113435|
|피크값 대역폭 400Gbps|154124|144260|

>!
>- 최저 보장 방어 피크 대역폭은 150Gbps이며 엘라스틱 방어 피크값은 300Gbps까지 구성할 수 있습니다.
>- 최저 보장 방어 피크 대역폭은 300Gbps이며 엘라스틱 방어 피크값은 600Gbps까지 구성할 수 있습니다.
>- 최저 보장 방어 피크 대역폭은 400Gbps이며 엘라스틱 방어 피크값은 800Gbps까지 구성할 수 있습니다.

## 최저 보장 방어 피크값

<table>
<tr>
<th rowspan="2">최저 보장 방어</th>
<th rowspan="2">비BGP 3 IP<br>&nbsp(USD/월)</th>
<th rowspan="2">비BGP 크 2 IP<br>(USD/월)</th>
<th colspan="2">BGP + 비BGP 3 IP(USD/월)
</th>
<th colspan="2">BGP + 비BGP 2 IP(USD/월)</th>
</tr>

<tr>
<th>20 Gbps BGP 최저 보장</th>
<th>30 Gbps BGP 최저 보장</th>
<th>20 Gbps BGP 최저 보장</th>
<th>30 Gbps BGP 최저 보장</th>
</tr>

<tr>
<td>피크값 대역폭 20Gbps</td>
<td>3005&nbsp&nbsp&nbsp&nbsp</td>
<td>2543&nbsp&nbsp&nbsp&nbsp</td>
<td>3853</td>
<td>-</td>
<td>3545</td>
<td>-</td>
</tr>

<tr>
<td>피크값 대역폭 30Gbps</td>
<td>4624</td>
<td>3930</td>
<td>5394</td>
<td>5780</td>
<td>4701</td>
<td>5086</td>
</tr>

<tr>
<td>피크값 대역폭 50Gbps</td>
<td>10789</td>
<td>10018</td>
<td>11559</td>
<td>12099</td>
<td>10789</td>
<td>11328</td>
</tr>

<tr>
<td>피크값 대역폭 60Gbps</td>
<td>14025</td>
<td>13101</td>
<td>14642</td>
<td>15258</td>
<td>13871</td>
<td>14333</td>
</tr>

<tr>
<td>피크값 대역폭 80Gbps</td>
<td>26201</td>
<td>24660</td>
<td>26972</td>
<td>27434</td>
<td>25430</td>
<td>25893</td>
</tr>

<tr>
<td>피크값 대역폭 100Gbps</td>
<td>30825</td>
<td>29283</td>
<td>31595</td>
<td>32058</td>
<td>30054</td>
<td>30516</td>
</tr>

<tr>
<td>피크값 대역폭 150Gbps</td>
<td>40072</td>
<td>36373</td>
<td>40843</td>
<td>41305</td>
<td>37144</td>
<td>37606</td>
</tr>

<tr>
<td>피크값 대역폭 200Gbps</td>
<td>50090</td>
<td>42538</td>
<td>50861</td>
<td>51323</td>
<td>43309</td>
<td>43771</td>
</tr>


<tr>
<td>피크값 대역폭 300Gbps</td>
<td>59338</td>
<td>53943</td>
<td>60108</td>
<td>60571</td>
<td>54714</td>
<td>55176</td>
</tr>

<tr>
<td>피크값 대역폭 400Gbps</td>
<td>66273</td>
<td>63191</td>
<td>67044</td>
<td>67506</td>
<td>63961</td>
<td>64424</td>
</tr>
</table>



**할인 혜택:** 세트는 한번에 1년 이상을 구매하면 15% 할인 혜택을 받을 수 있습니다.

## 엘라스틱 방어 피크값
| 엘라스틱 방어 | 출판 가격(USD/일)|
|---------|---------|
| 0Gbps ＜ 엘라스틱 피크값 ≤  10Gbps |139|
| 10Gbps＜ 엘라스틱 피크값 ≤  20Gbps |308|
| 20Gbps＜ 엘라스틱 피크값 ≤  30Gbps |493|
| 30Gbps＜ 엘라스틱 피크값 ≤  40Gbps |663|
| 40Gbps ＜ 엘라스틱 피크값 ≤  50Gbps |801|
| 50Gbps ＜ 엘라스틱 피크값 ≤  60Gbps |925|
| 60Gbps＜ 엘라스틱 피크값 ≤  70Gbps | 1048|
| 70Gbps ＜ 엘라스틱 피크값 ≤  80Gbps |1171|
| 80Gbps ＜ 엘라스틱 피크값 ≤  100Gbps |1403|
| 100Gbps ＜ 엘라스틱 피크값 ≤ 150Gbps  |1988|
| 150Gbps ＜ 엘라스틱 피크값 ≤ 200Gbps|2558|
|200Gbps ＜ 엘라스틱 피크값 ≤ 250Gbps  |3160|
|250Gbps ＜ 엘라스틱 피크값 ≤ 300Gbps  |3776|
|300Gbps ＜ 엘라스틱 피크값 ≤ 350Gbps  |4932|
| 350Gbps ＜ 엘라스틱 피크값 ≤ 400Gbps |6088|
| 400Gbps ＜ 엘라스틱 피크값 ≤  450Gbps |7090|
|450Gbps ＜ 엘라스틱 피크값 ≤  500Gbps |8014|
|500Gbps ＜ 엘라스틱 피크값 ≤  600Gbps |9093|
|600Gbps ＜ 엘라스틱 피크값 ≤  650Gbps |10172|
|650Gbps ＜ 엘라스틱 피크값 ≤  700Gbps |11174|
|700Gbps ＜ 엘라스틱 피크값 ≤  750Gbps |12022|
|750Gbps ＜ 엘라스틱 피크값 ≤  800Gbps |12792|

## 포워딩 포트 수량(선불식)
|포워딩 포트 수량|출판 가격(USD/개/월)
|-|-|
|포트 수량 ≤ 60|무료|
|포트 수량 > 60|7.7|

## 포워딩 트래픽/대역폭(후불식)
|포워딩 트래픽|BGP|China Telecom/China Unicom/China Mobile|
|-|-|-|
|트래픽 기반 요금제|0.13(USD/GB) |0.06(USD/GB) |
|대역폭 기반 요금제|0.47(USD/Mbps)|0.23(USD/Mbps) |

>!세트에서 포워딩 비즈니스 대역폭은 100Mbps 이하인 경우 무료입니다.

