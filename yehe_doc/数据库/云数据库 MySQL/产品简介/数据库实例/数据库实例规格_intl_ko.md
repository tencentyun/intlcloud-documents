본문은 TencentDB for MySQL의 최신 사양을 설명합니다.

## 2노드/3노드(로컬 SSD 디스크)
다음 표에는 소스 인스턴스(2노드/3노드), 읽기 전용 인스턴스 및 재해 복구 인스턴스의 사양이 나와 있습니다.
<table class="table-striped">
<tbody>
<tr><th>격리 정책</th><th>CPU 및 메모리</th><th>최대 IOPS</th><th>스토리지 공간</th></tr>
<tr>
<td rowspan="14">일반형</td>
<td>1코어 1000MB</td><td>1200</td><td rowspan="4">25GB - 3000GB</td></tr>        
<tr>
<td>1코어 2000MB</td><td>2000</td></tr>
<tr>
<td>2코어 4000MB</td><td>4000</td></tr>
<tr>
<td>4코어 8000MB</td><td>8000</td></tr>
<tr>
<td>4코어 16000MB</td><td>14000</td><td rowspan="6">25GB - 4000GB</td></tr>
<tr>
<td>8코어 16000MB</td><td>20000</td></tr>
<tr>
<td>8코어 32000MB</td><td>28000</td></tr>
<tr>
<td>16코어 32000MB</td><td>32000</td></tr>
<tr>
<td>16코어 64000MB</td><td>40000</td></tr>
<tr>
<td>16코어 96000MB</td><td>40000</td></tr>
<tr>
<td>16코어 128000MB</td><td>40000</td><td rowspan="3">25GB - 8000GB</td></tr>
<tr>
<td>24코어 244000MB</td><td>60000</td></tr>
<tr>
<td>32코어 256000MB</td><td>80000</td></tr>
<tr>
<td>48코어 488000MB</td><td>120000</td><td rowspan="1">25GB - 12000GB</td></tr>
<tr>
<td rowspan="26">전용형</td>
<td>2코어 16000MB</td><td>8000</td><td rowspan="7">25GB - 3000GB</td></tr>        
<tr>
<td>4코어 16000MB</td><td>10000</td></tr>
<tr>
<td>4코어 24000MB</td><td>13000</td></tr>
<tr>
<td>4코어 32000MB</td><td>16000</td></tr>
<tr>
<td>8코어 32000MB</td><td>32000</td></tr>
<tr>
<td>8코어 48000MB</td><td>36000</td></tr>
<tr>
<td>8코어 64000MB</td><td>40000</td></tr>
<tr>
<td>12코어 48000MB</td><td>36000</td><td rowspan="15">25GB - 6000GB</td></tr>
<tr>
<td>16코어 64000MB</td><td>60000</td></tr>
<tr>
<td>12코어 72000MB</td><td>40000</td></tr>
<tr>
<td>12코어 96000MB</td><td>48000</td></tr>
<tr>
<td>16코어 96000MB</td><td>60000</td></tr>
<tr>
<td>24코어 96000MB</td><td>72000</td></tr>
<tr>
<td>16코어 128000MB</td><td>60000</td></tr>
<tr>
<td>32코어 128000MB</td><td>80000</td></tr>
<tr>
<td>24코어 144000MB</td><td>76000</td></tr>
<tr>
<td>24코어 192000MB</td><td>80000</td></tr>
<tr>
<td>32코어 192000MB</td><td>90000</td></tr>
<tr>
<td>48코어 192000MB</td><td>120000</td></tr>
<tr>
<td>32코어 256000MB</td><td>100000</td></tr>
<tr>
<td>48코어 288000MB</td><td>140000</td></tr>
<tr>
<td>48코어 384000MB</td><td>140000</td></tr>
<tr>
<td>64코어 256000MB</td><td>150000</td><td rowspan="2">25GB - 9000GB</td></tr>
<tr>
<td>64코어 384000MB</td><td>150000</td></tr>
<tr>
<td>64코어 512000MB</td><td>150000</td><td rowspan="2">25GB - 12000GB</td></tr>
<tr>
<td>90코어 720000MB</td><td>150000</td></tr>
</tbody></table>        

>?각 리전의 인스턴스 사양에 따라 스토리지 공간 최댓값이 다를 수 있습니다. 실제 구매 페이지의 정보를 참고하십시오.

## 단일 노드(SSD 클라우드 디스크)
<table class="table-striped">
<thead><tr><th>격리 정책</th><th>CPU 및 메모리</th><th>최대 IOPS</th><th>최대 처리량</th><th>스토리지 공간</th></tr></thead>
<tbody>
<tr>
<td rowspan="8">기본형</td>
<td>1코어 1000MB</td><td rowspan="8">임의 IOPS 공식: 임의 IOPS = min{1800 + 30 × 용량(GB), 26000}<br>최대 IOPS: 26000</td><td rowspan="8">처리량 공식(MB/s): 처리량 = min{120 + 0.2 × 용량(GB), 260}<br>최대 처리량(MB/s): 260MB/s</td><td rowspan="8">20GB - 32000GB</td></tr>
<tr>
<td>1코어 2000MB</td></tr>
<tr>
<td>2코어 4000MB</td></tr>
<tr>
<td>2코어 8000MB</td></tr>
<tr>
<td>4코어 8000MB</td></tr>
<tr>
<td>4코어 16000MB</td></tr>
<tr>
<td>8코어 16000MB</td></tr>
<tr>
<td>8코어 32000MB</td></tr>
</tbody></table>

## 단일 노드(향상된 SSD 클라우드 디스크)
<table class="table-striped">
<thead><tr><th>격리 정책</th><th>CPU 및 메모리</th><th>최대 IOPS</th><th>최대 처리량</th><th>스토리지 공간</th></tr></thead>
<tbody>
<tr>
<td rowspan="8">기본형</td>
<td>1코어 1000MB</td><td rowspan="8">임의 IOPS 공식: 임의 IOPS = min{1800 + 50 × 용량(GB), 50000}<br>최대 IOPS：50000</td><td rowspan="8">처리량 공식(MB/s): 처리량 = min{120 + 0.5 × 용량(GB), 350}<br>최대 처리량(MB/s): 350MB/s</td><td rowspan="8">20GB - 32000GB</td></tr>
<tr>
<td>1코어 2000MB</td></tr>
<tr>
<td>2코어 4000MB</td></tr>
<tr>
<td>2코어 8000MB</td></tr>
<tr>
<td>4코어 8000MB</td></tr>
<tr>
<td>4코어 16000MB</td></tr>
<tr>
<td>8코어 16000MB</td></tr>
<tr>
<td>8코어 32000MB</td></tr>
</tbody></table>
