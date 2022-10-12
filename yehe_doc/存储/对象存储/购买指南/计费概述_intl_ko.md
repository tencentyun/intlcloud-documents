본문은 클라우드 Cloud Object Storage(COS)의 과금 방식, 과금 항목, 과금 주기 및 제품 가격에 대해 설명합니다

## 과금 방식

COS는 종량제 과금 방식을 적용하고 있으며, 관련 사항은 다음과 같습니다.

| 과금 방식                                                     | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 종량제(후불) | COS의 기본 과금 방식입니다. 리소스를 먼저 사용하고 나중에 비용을 지불하며, 각종 과금 항목의 요금은 매일 계산, 정산, 차감 및 과금됩니다. [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)의 모든 리전에서 지원됩니다. 자세한 내용은 [종량제(후불)](https://intl.cloud.tencent.com/document/product/436/32534)을 참고하십시오. |




## 과금 항목

COS의 과금 항목은 다음 이미지와 같이 스토리지 사용량, 요청, 데이터 검색, 트래픽, 관리 기능이 포함됩니다. 자세한 내용은 [트래픽 요금](https://intl.cloud.tencent.com/document/product/436/33776)을 참고하십시오.


![](https://qcloudimg.tencent-cloud.cn/raw/f122045a434978ab26cb7c276723fc9d.png)





## 과금 주기

COS 각 과금 항목의 과금 주기 및 과금 순서는 다음과 같습니다.

> ?
>2022년 9월 1일부터 COS 스토리지 사용량, 요청 및 데이터 검색 요금이 매일 정산됩니다. 자세한 내용은 [COS 스토리지 사용량, 요청 및 데이터 검색 일별 과금 안내](https://intl.cloud.tencent.com/document/product/436/47593)를 참고하십시오.

<table>
   <tr>
      <th colspan=2>과금 항목</td>
      <th>과금 주기</td>
      <th>과금 주기 설명</td>
      <th>과금 순서</td>
   </tr>
   <tr>
      <td colspan=2>스토리지 사용 요금</td>
      <td>일</td>
      <td rowspan=4>매일 전일 발생 비용 결산 및 청구서 생성</td>
      <td>프리 티어 > 종량제; 프리 티어 대상이 아닌 경우 종량제가 적용됩니다.</td>
   </tr>
   <tr>
      <td rowspan=3>요청 요금</td>
      <td colspan=1>읽기/쓰기 요청 요금</td>
      <td rowspan=3>일</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td colspan=1>DEEP ARCHIVE 데이터 검색 요청 요금</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td colspan=1>INTELLIGENT TIERING 객체 모니터링 요금</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td rowspan=3>데이터 검색 요금</td>
      <td colspan=1>STANDARD_IA 데이터 검색 요금</td>
      <td rowspan=2>일</td>
      <td rowspan=2>매일 전일 발생 비용 결산 및 청구서 생성</td>
      <td rowspan=2>종량제</td>
   </tr>
   <tr>
      <td colspan=1>ARCHIVE 데이터 검색 요금</td>
   </tr>
   <tr>
      <td colspan=1>DEEP ARCHIVE 데이터 검색 요금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td colspan=2>트래픽 요금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td rowspan=4>관리 기능 요금</td>
      <td colspan=1>인벤토리 기능 요금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td colspan=1>인덱스 기능 요금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td colspan=1>일괄 처리 요금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td colspan=1>객체 태그 요금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>종량제</td>
   </tr>
</table>


## 제품 가격

COS 과금 항목의 가격은 [제품 가격](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)에서 확인하실 수 있습니다.


## 관련 링크


1. COS 과금: 자세한 계산법 및 시나리오별 과금 세부 사항은 [과금 예시](https://intl.cloud.tencent.com/document/product/436/6241)를 참고하십시오.
2. COS 연체로 인한 서비스 중단 정책: 데이터 보관 및 폐기 기간, 과금 관련 설명은 COS [연체 설명](https://intl.cloud.tencent.com/document/product/436/10044)을 참고하십시오.
3. 과금 주기: 자세한 내용은 [About Billing](https://www.tencentcloud.com/document/product/555/7430?lang=en&pg=)을 참고하십시오.
4. COS 과금에 대해 더 궁금한 사항은 [FAQs](https://intl.cloud.tencent.com/document/product/436/32532)를 참고하시거나 [문의](https://www.tencentcloud.com/contact-us) 주시기 바랍니다.

