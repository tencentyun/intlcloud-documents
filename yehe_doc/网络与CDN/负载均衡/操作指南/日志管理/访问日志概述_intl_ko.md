CLB(Cloud Load Balancer) 액세스 로그는 요청 시간, 요청 경로, 클라이언트 IP 및 포트, 반환 코드, 응답 시간과 같은 각 클라이언트 요청의 세부 정보를 수집하고 기록합니다. 이 기능은 클라이언트 요청을 더 잘 이해하고, 문제를 해결하고, 사용자 행동을 분석하는 데 도움이 될 수 있습니다.
>?
>- 레이어 7 CLB만 액세스 로그 구성을 지원합니다.
>- 현재 일부 리전에서만 액세스 로그 구성을 지원합니다. 자세한 내용은 CLS의 <a href="https://cloud.tencent.com/document/product/614/18940">가용 리전</a>을 참고하십시오.

## 스토리지 메소드
CLB 액세스 로그는 [Cloud Log Service(CLS)](https://intl.cloud.tencent.com/document/product/614)에 저장 가능: CLS는 로그 수집, 저장, 검색, 분석, 실시간 내보내기, 배송 등 다양한 로그 서비스를 제공하는 원스톱 로그 서비스 플랫폼입니다. 비즈니스 운영, 보안 모니터링, 로그 감사 및 로그 분석을 구현하는 데 도움이 됩니다.

<table class="table">
<thead>
<tr>
<th>기능</th>
<th>CLS에 액세스 로그 저장</th>
</tr>
</thead>
<tbody>
<tr>
<td>로그 획득을 위한 시간 세분성 </td>
<td> 분</td>
</tr>
<tr>
<td>온라인 검색 </td>
<td> 지원</td>
</tr>
<tr>
<td>검색 구문 </td>
<td>전체 텍스트 검색, 키-값 검색, 퍼지 키워드 검색 등 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/614/37882">검색 규칙</a>을 참고하십시오.</td>
</tr>
<tr>
<td>지원 리전 </td>
<td>CLS 사용 가능한 리전에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/zh/document/product/614/18940">가용 리전</a>을 참고하십시오.</td>
</tr>
<tr>
<td>지원되는 CLB 유형 </td>
<td> 공중망/사설망 CLB</td>
</tr>
<tr>
<td>업스트림/다운스트림 링크 </td>
<td> CLS 로그는 COS로 배송되고 추가 처리를 위해 CKafka로 내보낼 수 있습니다.</td>
</tr> 
<tr>
<td>로그 저장 </td>
<td>Tencent Cloud는 기본적으로 액세스 로그를 저장하지 않습니다. 필요에 따라 스토리지 기능을 구성할 수 있습니다.</td>
</tr>
</tbody></table>

## 관련 작업
- [Storing CLB access logs to CLS](https://intl.cloud.tencent.com/document/product/214/35063)
