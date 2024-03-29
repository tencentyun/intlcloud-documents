## 1\. 배경
이 모듈은 IoT 허브 (“**기능**”)을 사용하는 경우 적용됩니다. 이 모듈은  (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)")에 있는 데이터 개인정보 보호 및 보안 계약에 통합됩니다. 이 모듈에서 사용되었지만 정의되지 않은 용어는 DPSA에 정의된 것과 같은 의미를 갖습니다. DPSA와 이 모듈 간에 상충이 있는 경우, 이 모듈은 상충되지 않는 범위 내에서 적용됩니다.

## 2\. 처리
당사는 기능과 관련하여 다음과 같은 데이터를 처리합니다.

<table>
<thead>
<tr>
<th><b>개인 정보</b></th>
<th><b>이용</b></th>
</tr>
</thead>
<tbody>
<tr>
<td><b>로그 데이터</b>: 장치 로그(이 데이터의 수집을 활성화하는 경우) </td>
<td>당사는 귀하의 구성에 따라 사용자의 디버깅 또는 문제 해결을 용이하게 하기 위해서만 이 데이터를 처리합니다.
이 데이터는 당사 Elasticsearch 서비스 기능과 함께 저장 및 백업된다는 점을 유의하십시오. 또한 Cloud Log Dump 기능을 사용하여 데이터를 저장하고 분석할 수도 있습니다.
</td>
</tr>
<tr>
<td><b>구성 데이터</b>: 제품 설정(제품 명, 제품 ID), 장치(장치 명, 장치 키/인증서) 및 규칙(SQL 문)</td>
<td>당사는 귀하가 제품 또는 장치 식별 및 관리를 용이하게 하기 위해 이 데이터를 처리합니다.
이 데이터는 당사의 MySQL 기능용 TencentDB와 함께 저장 및 백업된다는 점에 유의하십시오.
</td>
</tr>
<tr>
<td><b>모니터링 데이터</b>: 온라인 장치, 장치 메시지, 장치 섀도우, 규칙 및 펌웨어에 대한 통계</td>
<td>사용자에게 기능 사용에 대한 통계를 제공하기 위해서만 이 데이터를 처리합니다.
이 데이터는 클라우드 모니터 기능과 함께 저장 및 관리된다는 점에 유의하십시오. 이 데이터는 MySQL 기능용 TencentDB와 함께 저장됩니다.
</td>
</tr>
<tr>
<td><b>리소스 데이터</b>: 귀하가 업로드한 플랫폼과 장치와 관련된 리소스(귀하가 그러한 리소스에 개인 데이터를 포함한 경우)</td>
<td>귀하가 최종 사용자에게 이러한 데이터를 제공하기 위해서만 이 데이터를 처리합니다.
이 데이터는 Cloud Object Storage 기능과 함께 저장 및 백업된다는 점에 유의하십시오.
</td>
</tr>
<tr>
<td><b>게시된 장치 데이터</b>: 장치 유형, 장치 상태, SQL 문으로 해당 장치를 통제하는 규칙 및 명령</td>
<td>당사는 귀하가 지시한 대로 장치 확인 및 메시지 전달을 위해서만 이 데이터를 처리합니다.
이 데이터에 액세스할 수 없습니다. 이 데이터는 귀하가 지시한 대로 다른 서비스로 전송됩니다.
</td>
</tr>
<tr>
<td><b>가입자 장치 데이터 </b>: 장치 명령 메시지 </td>
<td>귀하와 최종 사용자가 장치 제어를 용이하게 하기 위해서만 이 데이터를 처리합니다.
이 데이터에 액세스할 수 없습니다. 이 데이터는 귀하가 지시한 대로 다른 서비스로 전송됩니다. 
</td>
</tbody></table>

## 3\. 서비스 지역
DPSA에 명시된 바와 같습니다.
## 4\. 하위 프로세서
DPSA에 명시된 바와 같습니다.
## 5\. 데이터 보존
당사는 다음과 같이 기능과 관련하여 처리된 개인 데이터를 보관합니다.

<table>
<thead>
<tr>
<th><b>개인 정보</b></th>
<th><b>보존 정책</b></th>
</tr>
</thead>
<tbody>
<tr>
<td><b>로그 데이터</b></td>
<td>Elasticsearch 서비스 기능으로 7일 동안 보관.
또한 Cloud Log Dump 기능과 함께 귀하가 지정한 기간 동안 데이터를 저장할 수도 있습니다.</td>
</tr>
<tr>
<td><b>구성 데이터</b></td>
<td>귀하가 계정 삭제를 요청할 때까지 저장되며, 삭제 요청이 있으면 데이터는 30일 이내에 삭제됩니다. 삭제를 요청하지 않는 경우, 이러한 데이터는 연체 금액이 귀하의 계정에서 지불 가능하게 된 일자, 이 기능의 사용 권리 종료, 또는 이 기능의 서비스 중단 일자 중 가장 빨리 도래하는 날로부터 30일 이내에 삭제됩니다.</td>
</tr>
<tr>
<td><b>리소스 데이터</b></td>
<td>귀하가 계정 삭제를 요청할 때까지 저장되며, 삭제 요청이 있으면 데이터는 30일 이내에 삭제됩니다. 삭제를 요청하지 않는 경우, 이러한 데이터는 연체 금액이 귀하의 계정에서 지불 가능하게 된 일자, 이 기능의 사용 권리 종료, 귀하의 기능 구독 만료, 또는 이 기능의 서비스 중단 일자 중 가장 빨리 도래하는 날로부터 30일 이내에 삭제됩니다.</td>
</tr>
<tr>
<td><b>모니터링 데이터</b></td>
<td>7일 동안 보관됩니다.</td>
</tr>
<tr>
<td><b>게시된 장치 데이터</b></td>
<td>저장되지 않습니다.</td>
</tr>
<tr>
<td><b>가입자 장치 데이터</b></td>
<td>저장되지 않습니다. </td>
</tbody></table>

DPSA에 따라 이러한 개인 데이터의 삭제를 요청할 수 있습니다.

## 6\. 특수 조건
개인 데이터 처리에 동의할 수 있는 최소 연령을 만족하는 최종 사용자만 이 기능을 사용할 수 있습니다. 이는 최종 사용자의 해당 지역에 따라 다를 수 있습니다.
