## 과금 방식

TencentDB for MySQL 글로벌 사이트에 정액 과금제 방식이 새롭게 추가되었습니다. 기존 글로벌 사이트 종량제 가격은 변동 없이 유지됩니다.



TencentDB for MySQL은 메모리와 디스크의 가격을 개별 과금하는 방식을 지원하며 사용자가 효율적으로 조합하여 사용할 수 있도록 더 다양한 과금제를 제공합니다.

인스턴스 가격 계산 공식: 인스턴스 가격=메모리 사양 요금+스토리지 용량 요금



## 인스턴스 사양(메모리 용량) 가격
>? 해당 제품의 정액 과금제 방식은 현재 베타 서비스 중입니다. 가격 문서는 참조용이며, 최종 가격은 청구서를 기준으로 적용됩니다. 사용을 원하시면 [영업팀에 문의](https://intl.cloud.tencent.com/contact-sales) 바랍니다.
>
### 정액 과금제 가격

<table>
<thead>
<tr>
<th colspan="3" style="text-align: center;">TencentDB for MySQL</th>
<th colspan="4"  style="text-align:center;">월정액 가격(단위: 달러/월)</th>
</tr>
</thead>
<tbody><tr>
<td>구성 유형</td>
<td>데이터베이스 유형</td>
<td>인스턴스 사양</td>
<td align="center">상하이, 광저우, 베이징, 난징, 칭위안</td>
<td>청두, 충칭</td>
<td>싱가포르, 중국홍콩, 타이베이, 토론토, 뭄바이</td>
<td>도쿄, 서울, 러시아, 방콕, 프랑크푸르트, 실리콘밸리, 버지니아주</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>1코어 1000MB 메모리</td>
<td align="center">14.37</td>
<td>10</td>
<td>24.08</td>
<td>18.59</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>1코어 2000MB 메모리</td>
<td align="center">28.73</td>
<td>20</td>
<td>48.17</td>
<td>37.18</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>2코어 4000MB 메모리</td>
<td align="center">57.46</td>
<td>40</td>
<td>96.34</td>
<td>74.37</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>4코어 8000MB 메모리</td>
<td align="center">114.93</td>
<td>80</td>
<td>192.68</td>
<td>148.73</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>4코어 16000MB 메모리</td>
<td align="center">229.86</td>
<td>160</td>
<td>385.35</td>
<td>297.46</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>8코어 32000MB 메모리</td>
<td align="center">459.72</td>
<td>320</td>
<td>770.7</td>
<td>594.93</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>16코어 64000MB 메모리</td>
<td align="center">919.44</td>
<td>640</td>
<td>1541.41</td>
<td>1189.86</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>16코어 96000MB 메모리</td>
<td align="center">1223.1</td>
<td>960</td>
<td>2312.11</td>
<td>1784.79</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>16코어 128000MB 메모리</td>
<td align="center">1838.87</td>
<td>1280</td>
<td>3082.82</td>
<td>2379.72</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>24코어 244000MB 메모리</td>
<td align="center">3505.35</td>
<td>2440</td>
<td>5876.62</td>
<td>4536.34</td>
</tr>
<tr>
<td>고가용성 버전-마스터 인스턴스</td>
<td>MySQL 마스터 인스턴스</td>
<td>48코어 488000MB 메모리</td>
<td align="center">7010.7</td>
<td>4880</td>
<td>11753.24</td>
<td>9072.68</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>1코어 1000MB 메모리</td>
<td align="center">7.18</td>
<td>5</td>
<td>12.04</td>
<td>9.30</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>1코어 2000MB 메모리</td>
<td align="center">14.37</td>
<td>10</td>
<td>24.08</td>
<td>18.59</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>2코어 4000MB 메모리</td>
<td align="center">28.73</td>
<td>20</td>
<td>48.17</td>
<td>37.18</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>4코어 8000MB 메모리</td>
<td align="center">57.46</td>
<td>40</td>
<td>96.34</td>
<td>74.37</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>4코어 16000MB 메모리</td>
<td align="center">114.93</td>
<td>80</td>
<td>192.68</td>
<td>148.73</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>8코어 32000MB 메모리</td>
<td align="center">229.86</td>
<td>160</td>
<td>385.35</td>
<td>297.46</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>16코어 64000MB 메모리</td>
<td align="center">459.72</td>
<td>320</td>
<td>770.70</td>
<td>594.93</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>16코어 96000MB 메모리</td>
<td align="center">611.55</td>
<td>480</td>
<td>1156.06</td>
<td>892.39</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>16코어 128000MB 메모리</td>
<td align="center">919.44</td>
<td>640</td>
<td>1541.41</td>
<td>1189.86</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>24코어 244000MB 메모리</td>
<td align="center">1752.68</td>
<td>1220</td>
<td>2938.31</td>
<td>2268.17</td>
</tr>
<tr>
<td>단일 노드 고IO 버전</td>
<td>MySQL 읽기 전용 인스턴스</td>
<td>48코어 488000MB 메모리</td>
<td align="center">3505.35</td>
<td>2440</td>
<td>5876.62</td>
<td>4536.34</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>1코어 1000MB 메모리</td>
<td align="center">21.55</td>
<td>15</td>
<td>36.12676056</td>
<td>27.89</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>1코어 2000MB 메모리</td>
<td align="center">43.10</td>
<td>30</td>
<td>72.25352113</td>
<td>55.77</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>2코어 4000MB 메모리</td>
<td align="center">86.20</td>
<td>60</td>
<td>144.5070423</td>
<td>111.55</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>4코어 8000MB 메모리</td>
<td align="center">172.39</td>
<td>120</td>
<td>289.0140845</td>
<td>223.10</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>4코어 16000MB 메모리</td>
<td align="center">344.79</td>
<td>240</td>
<td>578.028169</td>
<td>446.20</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>8코어 32000MB 메모리</td>
<td align="center">689.58</td>
<td>480</td>
<td>1156.056338</td>
<td>892.39</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>16코어 64000MB 메모리</td>
<td align="center">1379.15</td>
<td>960</td>
<td>2312.112676</td>
<td>1784.79</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>16코어 96000MB 메모리</td>
<td align="center">1834.65</td>
<td>1440</td>
<td>3468.169014</td>
<td>2677.18</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>16코어 128000MB 메모리</td>
<td align="center">2758.31</td>
<td>1920</td>
<td>4624.225352</td>
<td>3569.58</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>24코어 244000MB 메모리</td>
<td align="center">5258.03</td>
<td>3660</td>
<td>8814.929577</td>
<td>6804.51</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전</td>
<td>MySQL 3중 노드</td>
<td>48코어 488000MB 메모리</td>
<td align="center">10516.06</td>
<td>7320</td>
<td>17629.85915</td>
<td>13609.01</td>
</tr>
</tbody></table>



**주의사항**

1. 상기 가격은 인스턴스 사양의 구성 비용이며, 스토리지 용량, 백업 용량 및 대역폭 요금은 포함되지 않습니다.
3. 본 테이블에 있는 모든 가격은 구매 가격이며 연장, 설정 변경 시의 가격은 이와 다를 수 있습니다.
4. 공식 홈페이지의 가격은 상황에 따라 달라질 수 있으며, 구체적인 가격은 공식 홈페이지를 참고하시고 장기적으로 유효한 데이터가 아님을 알아두시기 바랍니다.



## 스토리지 용량(디스크 용량) 가격

### 정액 과금제 가격

<table>
<thead>
<tr>
<th style="text-align: center;">TencentDB for MySQL</th>
<th colspan="5"  style="text-align:center;">월정액 가격(단위: 달러/GB/월)</th>
</tr>
</thead>
<tbody><tr>
<td>데이터베이스 유형</td>
<td>상하이, 광저우, 베이징, 난징, 칭위안</td>
<td>청두, 충칭</td>
<td>중국홍콩, 타이베이, 싱가포르, 서울, 토론토, 뭄바이, 방콕</td>
<td>프랑크푸르트, 실리콘밸리, 버지니아주</td>
<td>도쿄, 모스크바</td>
</tr>
<tr>
<td>고가용성 버전 인스턴스</td>
<td>0.101408451</td>
<td>0.101408451</td>
<td>0.169014085</td>
<td>0.112676056</td>
<td>0.211267606</td>
</tr>
<tr>
<td>3중 노드 파이낸스 버전 인스턴스</td>
<td>0.152112676</td>
<td>0.152112676</td>
<td>0.253521127</td>
<td>0.169014085</td>
<td>0.316901408</td>
</tr>
<tr>
<td>읽기 전용 인스턴스</td>
<td>0.050704225</td>
<td>0.050704225</td>
<td>0.084507042</td>
<td>0.056338028</td>
<td>0.105633803</td>
</tr>
</tbody></table>

**주의사항**

1. 상기 가격은 스토리지 용량에 대한 요금이며, 인스턴스 사양 및 대역폭 요금은 포함되지 않습니다.
2.  본 테이블에 있는 모든 가격은 구매 가격이며 연장, 설정 변경 시의 가격은 이와 다를 수 있습니다.
3. 공식 홈페이지의 가격은 상황에 따라 달라질 수 있으며, 구체적인 가격은 공식 홈페이지를 참조하시고 장기적으로 유효한 데이터가 아님을 알아두시기 바랍니다.



## 고급 기능

### 백업 용량

백업 용량은 정액 과금제를 지원하지 않음므로 종량제 과금을 참조 바랍니다.

**인스턴스 구독 연장 관리**

구독 연장 관리 페이지에서는 인스턴스에 대한 일괄 구독 연장, 자동 연장, 만료일 통일, 구독 연장 안 함 표기 등의 기능을 제공합니다.



**인스턴스 업그레이드 알고리즘**

인스턴스의 만료 기간이 T일이고, 업그레이드한 타깃 구성과 기존 구성의 월간 선불금 차액이 C라고 했을 때, 업그레이드 총비용의 계산 공식은 T/30C입니다.

예시, 만료 기간이 15일 남아 있는 1코어 1000MB 메모리 100G 디스크 인스턴스(선불금 24.511달러/월)를 1코어 1000MB 메모리 200G 디스크(선불금 34.653달러/월)로 업그레이드하는 경우, 총비용은 15/30(34.653-24.511)=5.071달러입니다.



**인스턴스 디스크 용량 제한 초과 설명**

비즈니스의 정상적인 수행을 유지하기 위해 디스크 용량을 모두 사용하기 전에 미리 데이터베이스 인스턴스 사양을 업그레이드하거나 디스크 용량을 구매하시기 바랍니다.

인스턴스 스토리지의 데이터양이 인스턴스를 초과하면 인스턴스가 잠겨 데이터를 읽을 수만 있고 입력할 수 있게 되므로, 스케일 업 하거나 콘솔에서 일부 데이터베이스 테이블을 삭제하여 읽기 전용 모드를 해제할 수 있습니다.

데이터베이스가 잠기는 현상이 반복되지 않도록 하려면, 인스턴스의 남은 용량이 20% 이상 혹은 50G 이상(둘 중 하나만 해당하면 됨)으로 유지하면 인스턴스의 잠금 상태가 해제되고, 정상적인 읽기 및 쓰기 기능으로 복구할 수 있습니다.



**재해 복구 인스턴스 동기화 트래픽 요금**

프로모션 기간에는 TencentDB for MySQL 재해 복구 동기화 트래픽 요금을 받지 않습니다.

상용화 후 요금 부과 시 별도로 공지합니다.

## 종량제

종량제는 사용한 시간에 따라 총 세 단계로 구분합니다.

| 사용 시간 | 차등 가격 |
|---------|---------|
| 0시간＜사용 시간 ≤ 96시간 | 종량제 1단계 가격 |
| 96시간＜사용 시간 ≤ 360시간 | 종량제 2단계 가격 |
| 사용 시간＞360시간 | 종량제 3단계 가격 |

### 인스턴스 가격

### 과금 공식
**총비용 = 메모리 사양 요금 + 스토리지 용량 요금 + 백업 용량 요금 + 트래픽 요금**

### 과금 항목
<table>
<thead>
<tr>
<th width="15%">과금 항목</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>메모리 사양 요금<br></td>
<td>구매 페이지에서 선택한 인스턴스 사양의 요금은 종량제 차등 가격제를 지원합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">제품 가격</a>을 참조 바랍니다.</td>
</tr>
<tr>
<td>스토리지 용량 요금</td>
<td>구매 페이지에서 선택한 디스크 크기의 요금은 종량제 차등 가격제를 지원합니다. 자세한 내용은 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">제품 가격</a>을 참조 바랍니다.</td>
</tr>
<tr>
<td>백업 용량 요금</td>
<td>TencentDB for MySQL은 리전에 따라 일정 금액의 무료 백업 용량을 제공합니다. 무료 백업 용량의 크기는 상응하는 리전에 있는 모든 고가용 인스턴스(마스터 인스턴스, 재해 복구 인스턴스 포함) 스토리지 용량의 합입니다.<br>무료 백업 용량에서 초과한 부분의 요금은 <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">백업 용량 요금 설명</a>을 참조 바랍니다.</td>
</tr>
<tr>
<td>트래픽 요금</td>
<td>공용 네트워크 트래픽 요금은 현재 무료입니다.</td>
</tr>
</tbody></table>

#### 종량제 가격

##### 고가용성 버전
<table >
  <td rowspan=2>리전</td>
  <td colspan=3 >메모리 가격(달러/GB/시간)</td>
  <td rowspan=2 >디스크(달러/GB/시간)</td>
 </tr>
 <tr >
  <td >1단계</td>
  <td>2단계</td>
  <td>3단계</td>
 </tr>
 <tr >
  <td >광저우</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>칭위안</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>상하이</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>베이징</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>청두</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>충칭</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>중국홍콩</td>
  <td class=xl66 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>타이베이</td>
  <td class=xl65 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>싱가포르</td>
  <td class=xl65 align=right>0.0705</td>
  <td class=xl65 align=right>0.0528</td>
  <td class=xl65 align=right>0.0352</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>방콕</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>뭄바이</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>서울</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>도쿄</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>실리콘밸리</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>버지니아주</td>
  <td class=xl65 align=right>0.0444</td>
  <td class=xl65 align=right>0.0333</td>
  <td class=xl65 align=right>0.0222</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>토론토</td>
  <td class=xl65 align=right>0.0265</td>
  <td class=xl65 align=right>0.0199</td>
  <td class=xl65 align=right>0.0133</td>
  <td class=xl65 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>프랑크푸르트</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>모스크바</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 </tr>
</table>

##### 읽기 전용 인스턴스

<table>
  <td rowspan=2>리전</td>
  <td colspan=3 >메모리 가격(달러/GB/시간)</td>
  <td rowspan=2 >디스크(달러/GB/시간)</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>1단계</td>
  <td class=xl1529815>2단계</td>
  <td class=xl1529815>3단계</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>광저우</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>칭위안</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>상하이</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>베이징</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>청두</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>충칭</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>중국홍콩</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>타이베이</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>싱가포르</td>
  <td class=xl6529815 align=right>0.0352</td>
  <td class=xl6529815 align=right>0.0264</td>
  <td class=xl6529815 align=right>0.0176</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>방콕</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>뭄바이</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>서울</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>도쿄</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>실리콘밸리</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>버지니아주</td>
  <td class=xl6529815 align=right>0.0222</td>
  <td class=xl6529815 align=right>0.0167</td>
  <td class=xl6529815 align=right>0.0111</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>토론토</td>
  <td class=xl6529815 align=right>0.0133</td>
  <td class=xl6529815 align=right>0.0099</td>
  <td class=xl6529815 align=right>0.0066</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>프랑크푸르트</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>모스크바</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
</table>


## 과금 예시
[정액 과금제 예시]: 광저우 리전에서 4코어 8000MB 메모리, 500GB 디스크의 TencentDB for MySQL 인스턴스 1개를 정액 과금제로 1달간 구매한 경우.
당월 요금 계산은 아래와 같습니다.
인스턴스 가격 = 메모리 사양 요금 + 스토리지 용량 요금 = (114.93달러/월 + 500GB × 0.1014달러/GB/월 ) × 1개월 = 165.63달러
[종량제 예시]: 광저우 리전에서 4코어 8000MB 메모리, 500GB 디스크의 TencentDB for MySQL 인스턴스 1개를 종량제로 400시간 구매한 경우.
1단계 요금: (0.0250달러/GB/시간×8GB+500GB × 0.0003)×96시간=33.6달러
2단계 요금: (0.0200달러/GB/시간×8GB+500GB × 0.0003)×264시간=81.84달러
3단계 요금: (0.0150달러/GB/시간×8GB+500GB × 0.0003)×40시간=10.8달러
인스턴스 요금 = 1단계 요금 + 2단계 요금 + 3단계 요금 = 126.24달러
