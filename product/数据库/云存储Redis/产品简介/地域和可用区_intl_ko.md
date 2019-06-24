
TencentDB for Redis는 중국 대륙 및 이외 여러 지역의 지원을 제공하며, CVM이 지원하는 지역은 모두 지원합니다.

## 네트워크 설명
-  동일 지역의 클라우드 서비스 제품끼리는 사설망으로 서로 연결합니다.
-  다른 지역의 클라우드 서비스 제품끼리는 기본 네트워크 사설망으로 서로 연결할 수 없으며, VPC 간에 피어링 연결을 필요합니다.
 >?TencentDB for Redis, 접근 지연을 감소시킬 수 있도록 CVM과 동일한 지역을 선택하시길 권장합니다.

## 지역과 가용 영역
**중국 대륙 지역**

<table class="table-striped">
<tbody>
	<tr>
		<th>지역</th>
		<th>가용 영역</th>
	</tr>
	<tr>
		<td rowspan="4">화남 지역(광저우)<br> ap-guangzhou</td>
		<td>광저우 1지역(이미 매진)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>광저우 2지역<br> ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>광저우 3지역<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>광저우 4지역<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td rowspan="2">화남 지역(선전 금융)<br>ap-shenzhen-fsi</td>
		<td>선전 금융 1지역<span style="background-color: rgb(249, 249, 249);">(금융 기관과 기업만 티켓 제출하여 개통 신청)<br>ap-shenzhen-fsi-1</span></td>
	</tr>
	<tr>
		<td>선전 금융 2지역<span style="background-color: rgb(249, 249, 249);">(금융 기관과 기업만 티켓 제출하여 개통 신청)<br>ap-shenzhen-fsi-2</span></td>
	</tr>
	<tr>
		<td rowspan="4">화동 지역(상하이)<br>ap-shanghai</td>
		<td>상하이 1지역<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>상하이 2지역<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>상하이 3지역<br>ap-shanghai-3</td>
	</tr>
		<tr>
		<td>상하이 4지역<br>ap-shanghai-4</td>
	</tr>
	<tr>
			<td rowspan="3">화동 지역(상하이 금융)<br>ap-shanghai-fsi</td>
			<td>상하이 금융 1지역(금융 기관과 기업만 티켓 제출하여 개통 신청)<br>ap-shanghai-fsi-1</td>
	</tr>
	<tr>
			<td>상하이 금융 2지역(금융 기관과 기업만 티켓 제출하여 개통 신청)<br>ap-shanghai-fsi-2</td>
	</tr>
		<tr>
			<td>상하이 금융 3지역(금융 기관과 기업만 티켓 제출하여 개통 신청)<br>ap-shanghai-fsi-3</td>
	</tr>
	<tr>
			<td rowspan="4">화북 지역(베이징)<br>ap-beijing</td>
			<td>베이징 1지역<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>베이징 2지역<br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>베이징 3지역<br>ap-beijing-3</td>
	</tr>
		<tr>
			<td>베이징 4지역<br>ap-beijing-4</td>
	</tr>
	<tr>
		<td rowspan="2">서남 지역(청두)<br>ap-chengdu</td>
		<td>청두 1지역<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>청두 2지역<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >서남 지역(충칭)<br>ap-chongqing</td>
			<td>충칭 1지역<br>ap-chongqing-1</td>
	</tr>
</tbody>
</table>	


**중국 대륙 이외 지역**

<table class="table-striped">
	<tbody>
	<tr>
			<th>지역</th>
			<th>가용 영역</th>
		</tr>
		<tr>
			<td rowspan="2">동남아 지역(중국 홍콩)<br>ap-hongkong</td>
			<td>홍콩 1지역(중국 홍콩 노드는 동남아 지역 커버 가능)<br>ap-hongkong-1</td>
		</tr>
<tr>
			<td>홍콩 2지역(중국 홍콩 노드는 동남아 지역 커버 가능)<br>ap-hongkong-2</td>
		   </tr>
		<tr>
			<td>동남아 지역(싱가포르)<br>ap-singapore</td>
			<td>싱가포르 1지역(싱가포르 노드는 동남아 지역 커버 가능)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td >아시아 태평양 지역(서울)<br>ap-seoul</td>
			<td>서울 1지역(서울 노드는 동북아 지역 커버 가능)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >아시아 태평양 지역(도쿄)<br>ap-tokyo</td>
			<td>도쿄 1지역(도쿄 노드는 동북아 지역 커버 가능)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td >아시아 태평양 지역(뭄바이)<br>ap-mumbai</td>
			<td>뭄바이 1지역(뭄바이 노드는 아시아 태평양 남부 지역 커버 가능)<br>ap-mumbai-1</td>
		</tr>
		<tr>
		  	<td >아시아 태평양 지역(태국)<br>ap-bangkok </td>
				 <td >방콕 1지역(방콕 노드는 아시아 태평양 동남부 지역 커버 가능)<br>ap-bangkok-1</td>
		<tr>
			<td>북미 지역(토론토)<br>na-toronto</td>
			<td>토론토 1지역(토론토 노드는 북미 지역 커버 가능)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="1">미국 서부(실리콘 밸리)<br>na-siliconvalley</td>
			<td>실리콘 밸리 1지역(실리콘 밸리 노드는 미국 서부 커버 가능)<br>na-siliconvalley-1</td>
		</tr>
		<tr>
		<tr>
			<td>미국 동부(버지니아)<br>na-ashburn</td>
			<td>버지니아 1지역(버지니아 노드는 미국 동부 지역 커버 가능)<br>na-ashburn-1</td>
		</tr>
			<td>유럽 지역(프랑크푸르트)<br>eu-frankfurt</td>
			<td>프랑크푸르트 1지역(프랑크푸르트 노드는 유럽 지역 커버 가능)<br>eu-frankfurt-1</td>
		</tr>
		<td >유럽 지역(모스크바)<br>eu-moscow</td>
		<td>모스크바 1지역(모스크바 노드는 유럽 지역 커버 가능)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## 특별 지역 설명
화남 지역(선전 금융), 화동 지역(상하이 금융)은 [티켓 제출](https://console.cloud.tencent.com/workorder/category/create?level1_id=10&level2_id=103&level1_name=%E6%95%B0%E6%8D%AE%E5%BA%93&level2_name=%E4%BA%91%E5%AD%98%E5%82%A8Redis%20CRS)하여 신청해야 합니다.

