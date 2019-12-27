## CBS 이용 제한
<table>
<tr>
		<th width="22%">제한 유형</th>
		<th>제한 사항 설명</th>
	</tr>
	<tr>
		<td>엘라스틱 CBS 성능</td>
		<td> 2018년 5월부터 CVM과 함께 구매한 데이터 디스크는 모두 엘라스틱 CBS가 됨에 따라, CVM에서 언마운트 및 리마운트를 지원합니다. 이 기능은 모든 가용존에서 지원됩니다. 자세한 내용은 <ahref="https://cloud.tencent.com/document/api/213/15707">쿼리 가용 영역 목록을 참조하십시오.</a></td>
	</tr>
	<tr>
		<td>CBS 성능 제한 사항</td>
		<td> I/O 성능이 동시에 적용됩니다. <br/>예를 들어 1TB의 SSD CBS가 최대 임의 IOPS 26,000에 도달한다는 것은 읽기 IOPS와 쓰기IOPS 모두 해당 값에 도달할 수 있다는 것을 의미합니다. 동시에 여러 성능 제한으로 인하여 해당 예시의 block size가 4KB/8KB 인 I/O는 IOPS는 최대치에 도달할 수 있지만, block size가 16KB인 I/O를 사용하면 IOPS 최대치에 도달할 수 없습니다(처리량은 260MB/s의 제한에 도달함).</td>
	</tr>
		<tr>
	<td>단일 CVM는 엘라스틱 CBS 마운트 가능한 수량</td>
	<td>최대 20개</td>
	</tr>
		<tr>
	<td>CBS 마운트 가능한 CVM 제한 사항</td>
	<td>CVM과 CBS는 반드시 동일한 가용존에 있어야 합니다.</td>
	</tr>
	<tr>
		<td>CBS 연체 회수</td>
		<td>만약 정액 요금제인 엘라스틱 CBS가 만료된 후 7일 이내에 연장하지 않으면, 시스템은 강제로 해당 CBS와 CVM의 마운트 관계를 해제하여 휴지통으로 회수합니다. 자세한 회수 시스템은<ahref="https://cloud.tencent.com/document/product/362/3064">연체 설명</a>을 참조하십시오. <br>현재,<ahref="https://cloud.tencent.com/document/product/362/5745">CBS 마운트</a>가 정액 요금제 엘라스틱 CBS일 때 사용자는 실제 요구사항에 따라 아래의 연장 방법을 선택할 수 있습니다.
			<ul style="margin-bottom:0;">
			<li>CVM 만료 시간을 설정합니다.</li>
			<li>CBS 만료 후 매월 연장 갱신합니다.</li>
			<li>직접 마운트하고 연장을 진행하지 않습니다</li>
			</ul>
		</td>
	</tr>
</table>

## 스냅샷 이용 제한
<table>
<tr>
		<th width="22%">제한 유형</th>
		<th>제한 사항 설명</th>
	</tr>
		<tr>
		<td>스냅샷 CBS 생성 유형 제한 사항</td>
		<td>데이터 디스크 스냅샷은 새로운 엘라스틱 CBS만을 생성할 수 있습니다. 시스템 디스크 스냅샷은 사용자 정의 이미지만을 생성할 수 있습니다.</td>
	</tr>
		<tr>
	<td>스냅샷으로 CBS 생성 크기 제한 사항</td>
	<td>스냅샷을 이용하여 생성된 새로운 CBS 용량은 반드시 스냅샷 원본 CBS의 용량보다 크거나 같아야 합니다.</td>
	</tr>
			<tr>
			<td>스냅샷 롤백 제한 사항</td>
			<td>스냅샷은 스냅샷이 생성된 원본 CBS로만 롤백할 수 있습니다. 만약 기존 스냅샷을 이용하여 새로운 CBS를 생성하려면,<ahref="https://intl.cloud.tencent.com/document/product/362/5757">스냅샷으로 CBS 생성<a>을 참조하십시오.
		</td>
	</tr>
	<tr>
		<td>스냅샷 총 용량</td>
		<td>무제한</td>
	</tr>
	<tr>
		<td>단일 리전 스냅샷 할당량</td>
		<td>64+리전 내 CBS 수량*64(개)</td>
	</tr>
</table>

## 정기 스냅샷 정책 이용 제한
<table>
<tr>
		<th width="40%">제한 유형</th>
		<th>제한 사항 설명</th>
	</tr>
	<tr>
		<td>단일 리전 정기 스냅샷 정책 할당량</td>
		<td>단일 계정 최대 30개</td>
	</tr>
	<tr>
		<td>단일 CBS의 정기 스냅샷 정책 적용에 대한 제한 사항</td>
		<td>CBS가 속한 리전의 정기 스냅샷에만 정책을 적용할 수 있으며 최대 10개까지 가능합니다.</td>
	</tr>
	<tr>
		<td>단일 정기 스냅샷의 CBS 정책 적용에 대한 제한 사항￼</td>
		<td>기 스냅샷이 속한 리전의 CBS에만 정책을 적용할 수 있으며 최대 200까지 지원 가능합니다.</td>
	</tr>
</table>
