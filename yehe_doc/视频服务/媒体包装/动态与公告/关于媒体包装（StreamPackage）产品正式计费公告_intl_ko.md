StreamPackage는 **2022년 10월 7일** 베타 테스트를 중단하고 **2022년 10월 8일 00:00**부터 유료 서비스가 됩니다. 그 때까지는 계속 무료로 서비스를 이용하실 수 있습니다. 수수료 발생을 원하지 않으시면 10월 8일 이전에 서비스 이용을 중단하시기 바랍니다.

StreamPackage는 일 결산 후불 방식으로 매일 과금됩니다. 매일 수수료는 다음 날 계정 잔액에서 차감됩니다. 연체된 결제는 서비스가 중단됩니다. 이를 방지하려면 계정에 사용 가능한 잔액이 충분한지 확인하십시오. 제품의 과금 세부 정보는 다음과 같습니다.

## 과금 개요
<table class="table-striped">
<tbody>
	<tr>
		<th>과금 항목</th>
		<th>과금 관련 설명</th>
		<th>결제 방식</th>
	</tr>
	<tr>
		<td>아웃바운드 트래픽</td>
		<td>StreamPackage를 사용하여 라이브 스트림을 제공하면 아웃바운드 트래픽 요금이 발생합니다. 가격은 리전에 따라 다르며 차등 구간별 단가를 기반으로 합니다.</td>
		<td>후불-일 결산</td>
	</tr>
	<tr>
		<td>인바운드 트래픽</td>
		<td>StreamPackage를 사용하여 라이브 스트림을 수신하면 인바운드 트래픽 요금이 발생합니다. 가격은 리전에 따라 다르며 차등 구간별 단가를 기반으로 합니다.</td>
		<td>후불-일 결산</td>
	</tr>	
	<tr>
		<td>패키징</td>
		<td>StreamPackage를 사용하여 라이브 스트림을 패키징하면 패키징된 스트림의 트래픽 볼륨을 기반으로 하는 패키징 요금이 발생합니다.</td>
		<td>후불-일 결산</td>
	</tr>	
</tbody>
</table>


## 아웃바운드 트래픽 요금
StreamPackage를 사용하여 라이브 스트림을 제공하면 아웃바운드 트래픽 요금이 발생합니다. 가격은 리전에 따라 다르며 차등 구간별 단가를 기반으로 합니다.
#### 주의사항
- 과금 방식: 종량제 후불.
- 과금 주기: 아웃바운드 트래픽은 매일 과금되며 청구서가 생성된 다음 날 00:00~24:00(UTC+8) 사이에 매일 발생한 요금이 계정 잔액에서 차감됩니다. 실제 차감 및 과금 시간은 청구서를 참고하십시오.
- CSS를 사용하여 원본 서버에서 스트림을 가져온 다음 스트림을 전달하면 StreamPackage 아웃바운드 트래픽 요금이 면제됩니다. CSS의 과금 세부 정보는 [가격 리스트](https://www.tencentcloud.com/document/product/267/2819)를 참고하십시오.

#### 과금 가격
아웃바운드 트래픽 요금은 차등 단가 모델을 기반으로 합니다. 소비된 트래픽량에 각 가격 책정 구간의 단가를 곱하고 그 결과를 합산합니다.
<table class="table-striped">
<tbody>
	<tr>
		<th>리전</th>
		<th>트래픽 구간</th>
		<th>정가(USD/GB/일)</th>
	</tr>
	<tr>
		<td rowspan="4">인도</td>
		<td>0 - 300GB</td>
		<td>0.1093</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.080</td>
	</tr>
	<tr>
		<td rowspan="4">태국</td>
		<td>0 - 300GB</td>
		<td>0.1093</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.080</td>
	</tr>
	<tr>
		<td rowspan="4">서울</td>
		<td>0 - 300GB</td>
		<td>0.126</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.122</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.117</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.108</td>
	</tr>
    <tr>
		<td rowspan="4">일본</td>
		<td>0 - 300GB</td>
		<td>0.1368</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.1068</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.1032</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.1008</td>
	</tr>
    <tr>
		<td rowspan="4">프랑크푸르트</td>
		<td>0 - 300GB</td>
		<td>0.09</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.07</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.05</td>
	</tr>
    <tr>
		<td rowspan="4">싱가포르</td>
		<td>0 - 300GB</td>
		<td>0.12</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.08</td>
	</tr>	
    <tr>
		<td rowspan="4">기타</td>
		<td>0 - 300GB</td>
		<td>0.15</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.138</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.126</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.114</td>
	</tr>		
</tbody>
</table>

#### 과금 공식
각 구간별 아웃바운드 트래픽 요금 = 아웃바운드 트래픽 x 구간 단가. 총 아웃바운드 트래픽 요금은 각 구간의 요금을 합한 요금입니다.
#### 과금 예시
2022년 12월 1일에 StreamPackage의 싱가포르 서비스를 사용하여 1.8T의 라이브 스트림을 제공했다고 가정합니다. 발생하는 아웃바운드 트래픽 요금은 다음과 같습니다.
300 x 0.12 + 1200 x 0.085 + 300 x 0.082 = 162.6 USD.



## 인바운드 트래픽 요금
StreamPackage를 사용하여 라이브 스트림을 수신하면 인바운드 트래픽 요금이 발생합니다.
#### 주의사항
- 과금 방식: 종량제 후불.
- 과금 주기: 인바운드 트래픽은 매일 과금되며 청구서가 생성된 다음 날 00:00 ~ 24:00(UTC+8) 사이에 발생한 요금이 계정 잔액에서 차감됩니다. 실제 차감 및 과금 시간은 청구서를 참고하십시오.

#### 과금 가격
인바운드 트래픽 요금은 차등 가격 책정 모델을 기반으로 합니다. 소비된 트래픽량에 각 가격 책정 구간의 단가를 곱하고 그 결과를 합산합니다.
<table class="table-striped">
<table class="table-striped">
<tbody>
	<tr>
		<th>리전</th>
		<th>트래픽 구간</th>
		<th>정가(USD/GB/일)</th>
	</tr>
	<tr>
		<td rowspan="4">인도</td>
		<td>0 - 300GB</td>
		<td>0.0273</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.02</td>
	</tr>
	<tr>
		<td rowspan="4">태국</td>
		<td>0 - 300GB</td>
		<td>0.0273</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.02</td>
	</tr>
	<tr>
		<td rowspan="4">서울</td>
		<td>0 - 300GB</td>
		<td>0.0315</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0305</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0293</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.027</td>
	</tr>
    <tr>
		<td rowspan="4">일본</td>
		<td>0 - 300GB</td>
		<td>0.0342</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0267</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0258</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.0252</td>
	</tr>
    <tr>
		<td rowspan="4">프랑크푸르트</td>
		<td>0 - 300GB</td>
		<td>0.0225 </td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0175</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.0125</td>
	</tr>
    <tr>
		<td rowspan="4">싱가포르</td>
		<td>0 - 300GB</td>
		<td>0.03</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.02</td>
	</tr>	
    <tr>
		<td rowspan="4">기타</td>
		<td>0 - 300GB</td>
		<td>0.0375</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0345</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0315</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.0285</td>
	</tr>		
</tbody>
</table>

#### 과금 공식
각 구간별 인바운드 트래픽 요금 = 인바운드 트래픽 x 구간 단가. 총 인바운드 트래픽 요금은 각 구간의 요금을 합한 요금입니다.

#### 과금 예시
2022년 12월 1일에 StreamPackage의 싱가포르 서비스를 사용하여 1.8T의 라이브 스트림을 수신했다고 가정합니다. 발생하는 인바운드 트래픽 요금은 다음과 같습니다.
300 x 0.03 + 1200 x 0.0213 + 300 x 0.0205 = 40.71 USD.

## 패키징 요금
StreamPackage는 클라우드에서 들어오는 스트림을 다양한 시나리오에서 재생할 수 있도록 다양한 형식으로 패키징합니다. 패키징 요금은 패키징된 스트림의 트래픽량을 기준으로 합니다.
#### 과금 가격
<table class="table-striped">
<table class="table-striped">
<tbody>
	<tr>
		<th>과금 항목</th>
		<th>과금 방식</th>
		<th>가격</th>
	</tr>
	<tr>
		<td>패키징</td>
		<td>패키지된 스트림의 트래픽량</td>
		<td>0.1024 USD/GB/일</td>
	</tr>
</tbody>
</table>	

#### 과금 공식
패키징 요금 = 트래픽량 x 단가
일일 패키징 요금은 하루에 패키징된 스트림의 총 트래픽량에 패키징 단가를 곱한 값입니다.

#### 과금 예시
2022년 12월 01일에 StreamPackage를 사용하여 200GB의 라이브 스트림을 패키징했다고 가정합니다. 2022년 12월 02일에 다음 패키징 요금이 계정 잔액에서 공제됩니다.
200(GB) x 0.1024(USD/GB/일) = 20.48 USD



상기 StreamPackage 과금 규칙은 **2022년 10월 8일 00:00부터** 적용됩니다. 10월 8일 사용량에 대해서는 10월 9일에 과금됩니다. 계정 잔액에 주의하고, 필요하다고 생각되는 변경 사항이 있으면 제 때에 변경하시기 바랍니다. 문의 사항이 있으시면 언제든지 저희에게 연락해 주십시오.

2022-09-01
Tencent Cloud팀