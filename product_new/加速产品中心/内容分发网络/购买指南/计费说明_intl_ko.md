CDN은 **대역폭 청구** 와 **트래픽 청구** 두 가지 청구 방식을 제공합니다. 모두 **후불 일일 정산** 방식을 사용하며 전날 00:00:00 - 23:59:59 사이에 발생한 총 소모량은 둘째 날에 과금합니다.

## 대역폭 청구
### 차등 가격제
CDN 대역폭 청구는 차등 도달 모드를 사용합니다. 차등 가격은 아래 참조하십시오.
<table  style="width:494px">
	<thead>
		<tr>
			<th scope="col" style="width: 145px;">청구 모드</th>
			<th scope="col" style="width: 154px;">대역폭 차등</th>
			<th scope="col" style="width: 180px;">단가(달러/Mbps/일)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="1" rowspan="4" style="text-align: center; width: 145px;">대역폭 피크값</td>
			<td style="text-align: center; width: 154px;">0-500Mbps</td>
			<td style="text-align: center; width: 180px;">0.094</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">500Mbps-5Gbps</td>
			<td style="text-align: center; width: 180px;">0.092</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">5Gbps-50Gbps</td>
			<td style="text-align: center; width: 180px;">0.086</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">50Gbps보다 크거나 같음</td>
			<td style="text-align: center; width: 180px;">0.084 또는 계약서 가격 기준으로 오프라인</td>
		</tr>
	</tbody>
</table>


### 계산 방식
전날 CDN의 대역폭 피크값이 X라고 가정하면 차등 계산 방식은 다음과 같습니다.
1. X<500Mbps인 경우, 청구서 요금은 X\*0.094
2. 500Mbps<=X<5000Mbps인 경우, 청구서 요금은 X\*0.092
3. 5000Mbps<=X<50000Mbps인 경우, 청구서 요금은 X\*0.086
4. X >= 50000Mbps인 경우, 오프라인 계약으로 더 많은 혜택을 제공해드립니다.



## 트래픽 청구
### 차등 가격제
CDN 트래픽 청구는 월간 단위 누적 청구 방식을 사용합니다. 아래의 표 참조하십시오.
<table  style="width:494px">
	<thead>
		<tr>
			<th scope="col" style="width:98px">청구 모드</th>
			<th scope="col" style="width: 170px;">트래픽 차등</th>
			<th scope="col" style="width: 189px;">단가(달러/GB)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="1" rowspan="5" style="text-align:center; width:98px">월간 트래픽</td>
			<td style="text-align: center; width: 170px;">0GB-2TB</td>
			<td style="text-align: center; width: 189px;">0.037</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 170px;">2TB-10TB</td>
			<td style="text-align: center; width: 189px;">0.035</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 170px;">10TB-50TB</td>
			<td style="text-align: center; width: 189px;">0.032</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 170px;">50TB-100TB</td>
			<td style="text-align: center; width: 189px;">0.026</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 170px;">100TB보다 크거나 같음</td>
			<td style="text-align: center; width: 189px;">0.020또는 계약서 가격 기준으로 오프라인 협상</td>
		</tr>
	</tbody>
</table>


### 계산 방식
트래픽 청구는 대역폭 청구와 달리 월간 트래픽에 따른 차등 누진으로 정산되며, 계산 방식은 다음과 같습니다.
+ 발생한 트래픽이 3TB인 경우, 아래 그림 참조하십시오. 그림에서 회색은 실제 청구 차등이고 녹색은 1월 1일에 발생한 트래픽이며 2TB는 0TB-2TB 청구 차등 및 1TB는 2TB-10TB 청구 차등에 속하므로 1월 1일 실제 요금은 2 \* 1000 \* 0.037 + 1 \* 1000 \*입니다.
  ![](https://mc.qcloudimg.com/static/img/bfdae242f6cca57421a65e46a96b0c67/image.png)

+1월2일에 발생한 트래픽이 3TB의 경우,아래 그림 참조하십시오. 트래픽 청구는 월간 누적으로 정산하므로 1월 2일에 발생한 트래픽은 2TB-10TB 청구 차등에 속하기 때문에 1월 2일의 실제 요금은 3 \* 1000 \* 0.035입니다.
  ![](https://mc.qcloudimg.com/static/img/f62d1056c1c2cab249cec62ad6e74ddc/image.png)

+ 1월3일에 발생한 트래픽이 7TB인 경우, 아래 그림 참조하십시오. 이때 3번의 7TB에서 4TB는 2TB-10TB 청구 차등 및 3TB는 10TB-50TB 청구 차등에 속하기 때문에 1월 3일의 실제 요금은 4 \* 1000 \* 0.035 + 3 \* 1000 \* 0.032입니다.
  ![](https://mc.qcloudimg.com/static/img/954e2d483e31afd411f9a91ebd7f66c8/image.png)

이와 같은 방법으로 월별 일일 비용을 계산하고 2월1일부터 청구가 시작되면 모든 것이 다시 0부터 누적됩니다.

## 대규모 고객 청구 설명
Tencent Cloud에서 이미 사용하고 있거나 월 2만 달러 이상 소모를 예상할 경우, 서비스 상담을 통해 할인된 가격 및 월별 정산 등 유연한 청구 방식을 활용할 수 있습니다.

+ **일일 피크 대역폭은 월평균으로 계산**: CDN 일일 대역폭 통계 포인트는 총 288개로 각각의 유효일의 피크값을 평균으로 청구 대역폭으로 계산한 후 비즈니스팀과 계약한 가격에 따라 계산합니다.
> 계산 예시:
> 고객이 2017년 2월 1일에 본격적으로 청구 시작하며 계약서 가격은 P USD/Mbps/월입니다.
> 유효 날짜: 발생한 소모량이 1Kbps보다 큰 경우 유효한 날짜로 기록됩니다.
>고객이 2월에 14일 동안 발생한 소모량이 1Kbps보다 크다고 가정할 경우, 14일 동안 일일 288개 통계 포인트의 최댓값이 Max_1, Max_2, Max_3... Max_14이고 청구 대역폭은 평균(Max_1, Max_2, ..., Max_14)이므로 2월 요금은 평균(Max_1, Max_2, ..., Max_14)xPx14/28입니다.

+**월간 대역폭 95% 청구**: CDN 일일 대역폭 통계 포인트는 총 288개이고 매달 1일부터 유효일(소모 발생)의 모든 통계 포인트를 정렬하며 처음 5% 통계 포인트는 제거합니다. 나머지 가장 큰 통계 포인트는 계약서 가격을 기준으로 대역폭 청구 방식으로 과금합니다.
> 계산 예시:
> 고객이 2017년 2월 1일에 본격적으로 청구하며 계약서 가격은 P USD/Mbps/월입니다.
> 유효일: 발생한 소모량이 1Kbps보다 큰 경우 유효일로 기록됩니다.
> 고객이 2월에 14일 동안 발생한 소모량이 1Kbps보다 크다고 가정할 경우, 청구 대역폭은 14일 모든 통계 포인트는 14\*288이고 최고 5%의 포인트를 제거한 나머지 통계 포인트 중 가장 높은 것은 Max95이므로 2월 요금은 Max95xPx14/28입니다.

+**월간 트래픽**: 월간 누적 사용된 모든 트래픽 합계는 계약서 가격을 기준으로 계산됩니다.

[티켓 제출](https://console.cloud.tencent.com/workorder/category/create?level1_id=83&level2_id=85&level1_name=%E5%AD%98%E5%82%A8%E4%B8%8ECDN&level2_name=%E5%86%85%E5%AE%B9%E5%88%86%E5%8F%91%E7%BD%91%E7%BB%9C%20%20CDN)을 통해 상세 정보를 문의하십시오.

## 청구 모드 선택
CDN은 **대역폭 청구** 및 **트래픽 청구** 두 가지 청구 모드를 제공하고 서비스 형태에 따라 적합한 청구 모드를 선택할 수 있습니다. 청구 대역폭 활용률을 통해 적합한 청구 모드를 선택할 수 있으며 청구 대역폭 사용률 계산 방식은 다음과 같습니다.
전날 00:00~24:00에 소모한 트래픽이 200GB라고 가정할 경우, 곡선 그래프는 아래와 같이 표시되며 곡선이 차지하는 영역을 트래픽 소모량으로 이해하면 됩니다.
![](https://mc.qcloudimg.com/static/img/3ecfe86a031782ebeaf0b1f7595cc69f/image.png)
전날 00:00~24:00의 대역폭 피크값은 40Mbps이고 1일을 86400초로 가정할 경우, 1일 트래픽은  40 \* 1000 \* 86400이고 단위는 GB(432GB)로 환산됩니다. 그림에서 직사각형이 차지하는 영역으로 이해하면 됩니다.
![](https://mc.qcloudimg.com/static/img/b80d043b6e7f461d62fd2d87abf67005/image.png)
대역폭 활용률은 200GB/432GB*100%=46%입니다.

**선택 방식**
+ 대역폭 활용률이 50% 이상이면 서비스 곡선이 비교적 안정적임을 나타내므로 대역폭 청구 방식을 제안합니다.
+ 대역폭 활용률이 50% 미만이면 서비스 곡선 파동이 크다는 것을 나타내므로 트래픽 청구 방식을 제안합니다.
