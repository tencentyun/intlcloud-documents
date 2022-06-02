[](id:senderConfig)
## 발신자 구성 옵션
SES(Simple Email Service)는 SES 콘솔, SES API 및 SES SMTP의 세 가지 이메일 전송 방법을 제공합니다. SES 명령 라인 인터페이스(SES CLI) 또는 [API Category](https://intl.cloud.tencent.com/document/product/1084/39387)를 사용하거나 SMTP API를 호출하여 이메일을 보낼 수 있습니다.

이메일을 보내려면 [Console Guide > Email Sending](https://intl.cloud.tencent.com/document/product/1084/40178)을 참고하십시오.
## 유연한 배포 옵션
### 공유  P  주소
일반적으로 SES는 기본적으로 공유 IP 풀의 공유 IP 주소에서 이메일을 보냅니다. 공유 주소는 설정된 IP로 즉시 전송을 시작하려는 사용자를 위한 빠르고 사용하기 쉬운 옵션입니다. Tencent Cloud는 공유 IP의 품질과 높은 전달률을 보장합니다.
### 전용  IP  주소
전용 IP는 이메일 전송을 위해 Tencent Cloud에서 특별히 할당한 IP입니다. 일반적으로 이메일 전송에 사용된 적이 없거나 평판이 좋기 때문에 스팸 방지 조직에서 스팸 IP로 표시하지 않습니다. 전송량에 따라 전용 IP를 신청할 수 있습니다. 대량의 이메일을 보내야 하는 경우 영업 담당자에게 문의하여 전용 IP를 신청하십시오.


## 발신자 ID 관리 및 보안
이메일을 수신하면 ISP(인터넷 서비스 제공업체)에서 이메일을 받는 사람에게 전달하기 전에 인증 여부를 확인합니다. 인증은 귀하가 보내는 이메일 주소의 소유자임을 ISP에 증명합니다. SES는 SPF(Sender Policy Framework), DKIM(Domain Keys Identified Mail) 및 도메인 기반 메시지 인증을 비롯한 모든 산업 표준 인증 메커니즘을 지원합니다. 이메일이 ISP 검사를 통과하고 수신자에게 성공적으로 전달되었는지 확인할 수 있습니다.
## 통계 보내기
SES는 이메일 전송 활동을 모니터링하는 다양한 방법을 제공합니다. 예를 들어 전체 이메일 응답 퍼널에 대한 정보(전달률, 오픈율, 클릭률, 반송 횟수 등)를 캡처하고 정확한 데이터 분석을 제공할 수 있습니다. 또한 [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502)를 호출하여 이메일 전송 정책을 조정하여 특정 이메일의 전송 상태를 확인할 수 있습니다.

[](id:warmUp)
## 자동 warm up 
### 제품 특징
이메일 전달 프로세스는 매우 복잡할 수 있습니다. IP/도메인의 평판은 전달 가능성을 높이는 데 매우 중요합니다. warm up은 전송 평판을 구축하는 과정입니다. 이메일 발송량은 매일 점차적으로 증가해야 하며 한 번에 원하는 수준에 도달할 수 없습니다. warm up은 ISP에서 좋은 평판을 얻는 데 도움이 됩니다.
>?자동 warm up은 프로세스 전반에 걸쳐 수동 개입 없이 IP 주소 또는 발신자 도메인을 자동으로 warm up하는 것을 말합니다.
### 기능 설명
자동 warm up은 [표준 규칙(기본값)](#default) 및 [업그레이드된 규칙](#customize)의 두 가지 범주로 나뉩니다.

#### 기본 규칙:
일괄 전송 모드에서는 기본적으로 표준 warm up 규칙이 적용됩니다. 백엔드는 일련의 정책을 기반으로 warm up 진행 상황을 결정하고 일일 전송 할당량을 자동으로 할당합니다. 전체 프로세스는 완전히 자동입니다. 하루에 보낼 수 있는 최대 이메일 수에 도달하면 이메일 전송이 중지되고 추가 이메일이 캐시 대기열에 들어가 24시간 후에 전송됩니다. 표준 warm up 계획은 다음과 같습니다.[](id:default)

<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">Day</td>
      <th width="0px" style="text-align:center">전송량/일</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1일</td>
		<td style="text-align:center">500</td>
	</tr>
	<tr>
		<td style="text-align:center">2일</td>
		<td style="text-align:center"sdval="200" >1000</td>
	</tr>
	<tr>
		<td style="text-align:center">3일</td>
		<td style="text-align:center"sdval="500" >2000</td>
	</tr>
	<tr>
		<td style="text-align:center">4일</td>
		<td style="text-align:center"sdval="1000" >5000</td>
	</tr>
	<tr>
		<td style="text-align:center">5일</td>
		<td style="text-align:center"sdval="2000" >10000</td>
	</tr>
	<tr>
		<td style="text-align:center">6일</td>
		<td style="text-align:center"sdval="5000" >20000</td>
	</tr>
	<tr>
		<td style="text-align:center">7일</td>
		<td style="text-align:center"sdval="10000" >40000</td>
	</tr>
	<tr>
		<td style="text-align:center">8일</td>
		<td style="text-align:center"sdval="20000" >60000</td>
	</tr>
	<tr>
		<td style="text-align:center">9일</td>
		<td style="text-align:center"sdval="30000" >80000</td>
	</tr>
	<tr>
		<td style="text-align:center">10일</td>
		<td style="text-align:center"sdval="40000" >100000</td>
	</tr>
	<tr>
		<td style="text-align:center">11일</td>
		<td style="text-align:center"sdval="60000" >150000</td>
	</tr>
	<tr>
		<td style="text-align:center">12일</td>
		<td style="text-align:center"sdval="80000" >200000</td>
	</tr>
	<tr>
		<td style="text-align:center">13일</td>
		<td style="text-align:center"sdval="100000" >300000</td>
	</tr>
	<tr>
		<td style="text-align:center">14일</td>
		<td style="text-align:center"sdval="120000" >400000</td>
	</tr>
	<tr>
		<td style="text-align:center">15일</td>
		<td style="text-align:center"sdval="150000" >500000</td>
	</tr>
	<tr>
		<td style="text-align:center">16일</td>
		<td style="text-align:center"sdval="200000" >600000</td>
	</tr>
	<tr>
		<td style="text-align:center">17일</td>
		<td style="text-align:center"sdval="400000" >700000</td>
	</tr>
	<tr>
		<td style="text-align:center">18일</td>
		<td style="text-align:center"sdval="600000" >800000</td>
	</tr>
	<tr>
		<td style="text-align:center">19일</td>
		<td style="text-align:center"sdval="800000" >900000</td>
	</tr>
		<tr>
		<td style="text-align:center">20일</td>
		<td style="text-align:center"sdval="800000" >1000000</td>
	</tr>
</table>

[](id:customize)
#### 사용자 정의 규칙:
고품질 이메일의 경우 표준 warm up 계획이 귀하의 요구를 충족시킬 수 없는 경우 업그레이드된  warm up 계획을 신청할 수 있습니다. 자세한 내용은 영업 담당자에게 문의하여 신청하십시오.
[](id:batch)
## 일괄 기능 세트
마케팅 또는 알림 이메일의 일괄 발송에 적합합니다. 트리거 기반 이메일(예: 인증 및 트랜잭션 이메일)을 보내려면 API-SendEmail을 호출하는 것이 좋습니다.
### 제품 특징
다음 방법 중 하나로 SES 일괄 전송 기능을 사용할 수 있습니다.
•콘솔: 템플릿이 필요하며 이메일 크기는 10MB를 넘지 않아야 하고 첨부파일은 지원되지 않습니다.
•API: 템플릿이 필요하며 이메일 크기는 10MB를 넘지 않아야 하고 첨부파일이 지원됩니다.

### 기능 설명
콘솔의 **이메일 전송** > **수신자 그룹 목록** 페이지에서 발신자 주소를 관리할 수 있습니다.

일괄 전송 기능은 표준 warm up 계획을 사용하도록 설정됩니다. 계획은 IP/도메인의 평판을 자동으로 식별하고, 일일 전송 할당량을 할당하고, 총 전송량이 하루에 허용되는 최대 수를 초과하는지 여부를 결정합니다. 그렇다면 이메일 전송이 중지되고 추가 이메일이 캐시 대기열에 들어가고 24시간 후에 전송됩니다.

## 일괄 전송
이메일을 일괄적으로 보내려면 콘솔에서 전송 작업을 생성하고 작업 유형에 대해 일괄 처리를 선택한 다음 작업에 필요한 모든 필드를 설정합니다.
## 예약 전송
이메일은 예약된 시간에 보낼 수 있습니다. 작업의 시작 시간을 선택하면 지정된 시간에 이메일이 자동으로 전송됩니다.
## 반복 전송
시작 시간 및 반복을 포함한 작업 필드를 지정하여 콘솔에서 반복 이메일을 설정할 수 있습니다. 콘솔은 지정된 반복 빈도에 따라 자동으로 이메일을 보냅니다.
