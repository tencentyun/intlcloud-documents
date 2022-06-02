[](id:que1) 
### 몇 가지 간단한 방법으로 이메일 전송을 테스트하려면 어떻게 해야 합니까?
테스트를 위해 자신의 계정을 사용할 수 있습니다. SES는 현재 1000개 이메일의 프리 티어를 제공하지만 테스트 계정은 제공하지 않습니다.

[](id:que5) 
### 처음부터 많은 수의 이메일을 보낼 수 있습니까?
아니요. 발송량은 날마다 점차적으로 늘려야 하며 한 번에 원하는 수준으로 올릴 수 없습니다. ISP에서 좋은 평판을 얻으려면 이메일을 보내기 전에 자동 warm up이 필요합니다. 일괄 전송 모드에서는 기본적으로 표준 warm up 규칙이 적용됩니다. [Features](https://intl.cloud.tencent.com/document/product/1084/43285)를 참고하십시오.

[](id:que6) 
### warm up이란?
warm up은 새로운 IP에 대한 평판을 구축하는 방법입니다. 일반적으로 모든 이메일 서비스 제공업체는 IP에서 보내는 일일 이메일 수에 제한이 있습니다. 적은 수의 이메일로 시작하여 점차적으로 매일 그 수를 늘려야 합니다.

[](id:que7) 
일괄 전송 모드에서는 기본적으로 표준 warm up 규칙이 적용됩니다. 백엔드는 일련의 정책을 기반으로 warm up 진행 상황을 결정하고 일일 전송 할당량을 자동으로 할당합니다. 전체 프로세스는 완전히 자동입니다. 하루에 보낼 수 있는 최대 이메일 수에 도달하면 이메일 전송이 중지되고 추가 이메일이 캐시 대기열에 들어가 24시간 후에 전송됩니다. 표준 warm up 계획은 다음과 같습니다.
<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">Day</td>
      <th width="0px" style="text-align:center">발신량/일</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1일</td>
		<td style="text-align:center">100</td>
	</tr>
	<tr>
		<td style="text-align:center">2일</td>
		<td style="text-align:center"sdval="200" >200</td>
	</tr>
	<tr>
		<td style="text-align:center">3일</td>
		<td style="text-align:center"sdval="500" >500</td>
	</tr>
	<tr>
		<td style="text-align:center">4일</td>
		<td style="text-align:center"sdval="1000" >1000</td>
	</tr>
	<tr>
		<td style="text-align:center">5일</td>
		<td style="text-align:center"sdval="2000" >2000</td>
	</tr>
	<tr>
		<td style="text-align:center">6일</td>
		<td style="text-align:center"sdval="5000" >5000</td>
	</tr>
	<tr>
		<td style="text-align:center">7일</td>
		<td style="text-align:center"sdval="10000" >10000</td>
	</tr>
	<tr>
		<td style="text-align:center">8일</td>
		<td style="text-align:center"sdval="20000" >20000</td>
	</tr>
	<tr>
		<td style="text-align:center">9일</td>
		<td style="text-align:center"sdval="30000" >30000</td>
	</tr>
	<tr>
		<td style="text-align:center">10일</td>
		<td style="text-align:center"sdval="40000" >40000</td>
	</tr>
	<tr>
		<td style="text-align:center">11일</td>
		<td style="text-align:center"sdval="60000" >60000</td>
	</tr>
	<tr>
		<td style="text-align:center">12일</td>
		<td style="text-align:center"sdval="80000" >80000</td>
	</tr>
	<tr>
		<td style="text-align:center">13일</td>
		<td style="text-align:center"sdval="100000" >100000</td>
	</tr>
	<tr>
		<td style="text-align:center">14일</td>
		<td style="text-align:center"sdval="120000" >120000</td>
	</tr>
	<tr>
		<td style="text-align:center">15일</td>
		<td style="text-align:center"sdval="150000" >150000</td>
	</tr>
	<tr>
		<td style="text-align:center">16일</td>
		<td style="text-align:center"sdval="200000" >200000</td>
	</tr>
	<tr>
		<td style="text-align:center">17일</td>
		<td style="text-align:center"sdval="400000" >400000</td>
	</tr>
	<tr>
		<td style="text-align:center">18일</td>
		<td style="text-align:center"sdval="600000" >600000</td>
	</tr>
	<tr>
		<td style="text-align:center">19일</td>
		<td style="text-align:center"sdval="800000" >800000</td>
	</tr>
		<tr>
		<td style="text-align:center">20일</td>
		<td style="text-align:center"sdval="800000" >1000000</td>
	</tr>
</table>

사용자 정의 규칙:

고품질 이메일의 경우 표준 warm up 계획이 요구 사항을 충족할 수 없는 경우 사용자 정의 warm up 계획을 수립할 수 있습니다. 자세한 내용은 영업 담당자에게 문의하여 신청하십시오.
