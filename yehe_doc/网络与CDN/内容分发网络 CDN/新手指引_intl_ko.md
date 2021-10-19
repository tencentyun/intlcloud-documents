본 문서에서는 CDN의 신규 사용자를 위한 학습 경로를 제공합니다.

## 1. CDN 기본 지식 숙지

- [CDN은 어떤 작업인가요?](https://intl.cloud.tencent.com/document/product/228/2939)
- [왜 Tencent Cloud CDN을 선택해야 할까요?](https://intl.cloud.tencent.com/document/product/228/2941)
- [CDN의 응용 시나리오 소개](https://intl.cloud.tencent.com/document/product/228/32980)
- [Tencent Cloud CDN 사용 시 어떤 제한 사항이 있나요?](https://intl.cloud.tencent.com/document/product/228/32981)
- [CDN의 일반적 개념](https://intl.cloud.tencent.com/document/product/228/36183)



## 2. CDN의 과금 방식

Tencent Cloud CDN의 과금 방식에는 **대역폭 과금 방식**과 **트래픽 과금 방식**이 있습니다. CDN 과금 방식을 완벽히 이해하면 가장 유리한 과금 방식을 선택할 수 있습니다. [과금 설명](https://intl.cloud.tencent.com/document/product/228/2949)을 참조하십시오.






## 3. 신규 사용자

#### 3.1 서비스 활성화 및 과금 방식 선택

Tencent Cloud CDN을 사용하려면 우선 Tencent Cloud 계정에 가입하고 CDN 서비스를 활성화해야 합니다. [CDN 처음부터 설정 시작하기](https://intl.cloud.tencent.com/document/product/228/32978)를 참조하십시오.

#### 3.2 도메인 엑세스

가속 작업을 위해서는 가속 도메인에 연결해야 합니다. CDN이 가속 도메인을 통해 원본 서버 리소스를 CDN 가속 노드에 캐싱하면 사용자가 가까운 곳에서 필요한 리소스를 가져와 리소스 액세스 가속을 실현할 수 있습니다. 자세한 내용은 [도메인 엑세스](https://intl.cloud.tencent.com/document/product/228/5734)를 참조하십시오.

#### 3.3 CNAME 설정

액세스가 완료되면 Tencent Cloud CDN에서 해당 CNAME 주소를 할당하므로 CDN 서비스를 적용하려면 CNAME 설정을 완료해야 합니다. 자세한 내용은 [CNAME 설정](https://intl.cloud.tencent.com/document/product/228/3121)을 참조하십시오.

>? 다음의 모범 사례를 참조해 Tencent Cloud CDN 사용을 시작하여 도메인을 가속화할 수 있습니다.
>- [Tencent Cloud CDN 가속 클라우드 서버 CVM의 인스턴스.](https://intl.cloud.tencent.com/document/product/228/34035)
>- [Tencent Cloud CDN 객체 스토리지 COS의 인스턴스.](https://intl.cloud.tencent.com/document/product/228/34036)




## 4. 콘솔 인터페이스

다음은 CDN 콘솔의 총람 페이지입니다.
![](https://main.qcloudimg.com/raw/95fff730b132974403698b512260f3fb.png)




## 5. 콘솔 기능 개요

<table>
<thead>
<tr>
<th>희망 작업 유형</th>
<th>참고 자료</th>
</tr>
</thead>
<tbody><tr>
<td>액세스한 도메인을 조회하거나 활성화 또는 비활성화. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/5736" target="_blank">도메인 작업</a></td>
</tr>
<tr>
<td>리스트를 필터링 조회하거나 클라우드 리소스를 태그, 프로젝트별로 관리. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32913" target="_blank">도메인 검색</a></td>
</tr>
<tr>
<td>CDN 가속 효과를 극대화하여 CDN에서 여러 항목의 사용자 정의 설정 지원. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6288" target="_blank">설정 개요</a></td>
</tr>
<tr>
<td>콘솔 기능과 Action의 매핑 관계 조회. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35229" target="_blank">콘솔 권한 설명</a></td>
</tr>
<tr>
<td>사용자 정의 정책을 통한 도메인 수준의 권한 부여. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35228" target="_blank">정책 생성</a></td>
</tr>
<tr>
<td>프로젝트 수준에 대한 권한 부여 작업 세분화. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35743" target="_blank">프로젝트별 권한 설명</a></td>
</tr>
<tr>
<td>실시간 모니터링 데이터를 바탕으로 운영 상황 분석. </td>
<td>실시간 모니터링</a></td>
</tr>
<tr>
<td>사용자 출처와 분포, 사용 현황 분석. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32923" target="_blank">데이터 분석</a></td>
</tr>
<tr>
<td>주기적으로 노드 캐시 리소스를 정리하고 원본 서버에서 최신 리소스를 불러와 다시 캐싱. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6299" target="_blank">캐시 퍼지</a></td>
</tr>
<tr>
<td>지정된 리소스를 미리 가속 노드에 로딩. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/39000" target="_blank">캐시 프리패치</a></td>
</tr>
<tr>
<td>액세스 로그를 다운로드하여 니즈에 따라 인기 리소스와 활성 사용자 등을 분석. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6316" target="_blank">로그 다운로드</a></td>
</tr>
<tr>
<td>로그 데이터를 빠르게 검색하고 분석. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35380" target="_blank">실시간 로그</a></td>
</tr>
<tr>
<td>전체 네트워크의 실시간 상태 개요 및 세부 사항 점검. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6311" target="_blank">전체 네트워크 상태 모니터링</a></td>
</tr>
<tr>
<td>사용자가 서비스 상태를 분석할 수 있도록 서비스 상태를 다양한 범주의 리포트 형식으로 표시. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6312" target="_blank">운영 리포트</a></td>
</tr>
<tr>
<td>CDN 콘솔에서 중국 내 트래픽 패키지 사용 현황 조회. </td>
<td>트래픽 패키지 관리</a></td>
</tr>
<tr>
<td>지정된 IP가 Tencent Cloud의 CDN 노드인지 확인. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/10747" target="_blank">Tencent Cloud CDN IP 확인</a></td>
</tr>
<tr>
<td>액세스 오류가 발생한 URL을 진단하여 문제를 신속히 진단. </td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6304" target="_blank">자가 진단 툴</a></td>
</tr>
<tr>
<td>DDoS, CC, WAF 공격 완벽 차단 및 모니터링. </td>
<td>SCDN</a></td>
</tr>
<tr>
<td>Tencent Cloud CDN을 통한 이미지 대량 배포. </td>
<td>이미지 최적화</a></td>
</tr>
</tbody></table>


## 6. 신규 사용자 FAQ
#### 과금 관련 문제
- [CDN 청구서는 어떻게 조회하나요?](https://intl.cloud.tencent.com/document/product/228/31479)
- [구매한 CDN 중국 내 트래픽 패키지가 필요 없어진 경우 환불받을 수 있나요?](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN은 요청 횟수에 따른 과금 방식을 지원하나요?](https://intl.cloud.tencent.com/document/product/228/31479)
- [원본 서버가 COS를 사용할 경우, CDN이 COS에 원본을 요청할 때 발생하는 트래픽에 대해서도 과금되나요?](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN 비활성화(CDN 서비스 종료) 후에도 트래픽이나 요금이 발생하나요?](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN 과금 방식을 변경할 수 있나요?](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN 중국 내 트래픽 패키지 사용 관리](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN 과금 시 다운스트림 트래픽에만 비용이 청구되나요?](https://intl.cloud.tencent.com/document/product/228/31479)

#### 도메인 엑세스 관련 문제

- [CDN은 와일드카드 서브도메인 액세스를 지원하나요?](https://intl.cloud.tencent.com/document/product/228/31476)
- [ICP 비안 등록이 완료된 도메인임에도 불구하고 CDN 가속 도메인 추가 시 ICP 비안 미등록이라고 뜨는 이유는 무엇인가요?](https://intl.cloud.tencent.com/document/product/228/31476)
- [CDN을 설정하는 데 시간이 얼마나 걸리나요?](https://intl.cloud.tencent.com/document/product/228/31476)
- [원본 서버 IP를 여러 개 설정할 수 있나요?](https://intl.cloud.tencent.com/document/product/228/31476)
- [CDN이 적용되었는지 어떻게 확인하나요?](https://intl.cloud.tencent.com/document/product/228/31476)
- [도메인이 비활성화만 가능하고, 삭제는 불가능한 이유는 무엇인가요?](https://intl.cloud.tencent.com/document/product/228/31476)
- [가속 서비스를 비활성화하려면 어떻게 해야 하나요?](https://intl.cloud.tencent.com/document/product/228/31476)
- [가속 도메인은 어떻게 삭제하나요?](https://intl.cloud.tencent.com/document/product/228/31476)
- [가속 도메인 / 원본 서버에서 포트를 설정할 수 있나요?](https://intl.cloud.tencent.com/document/product/228/31476)
-[CDN 파일을 다운로드할 수 없습니다](https://intl.cloud.tencent.com/document/product/228/31476)



## 7. 피드백 및 의견
Tencent Cloud CDN 제품 및 서비스 사용 중 문의사항 또는 의견이 있는 경우 다음 채널을 통해 피드백을 보내주십시오. 전문가가 문제를 해결해 드립니다.
- 링크, 내용, API 오류 등 제품 문서에 문제가 발생하는 경우 문서 페이지 오른쪽 [문서 피드백]을 클릭하거나 문제가 있는 내용을 선택하여 피드백을 보낼 수 있습니다.
- 제품 관련 문제가 발생한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청할 수 있습니다.

