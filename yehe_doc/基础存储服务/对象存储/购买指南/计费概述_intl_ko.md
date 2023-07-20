본문은 클라우드 Cloud Object Storage(COS)의 과금 방식, 과금 항목, 과금 주기 및 제품 가격에 대해 설명합니다

## 과금 방식

COS는 종량제(후불) 및 리소스 패키지(선불)의 두 가지 과금 방식을 지원합니다.

| 과금 방식                                                     | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 종량제(후불) | COS의 기본 과금 방식입니다. 리소스를 먼저 사용하고 나중에 비용을 지불하며, 각종 과금 항목의 요금은 매일 계산, 정산, 차감 및 과금됩니다. [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)의 모든 리전에서 지원됩니다. 자세한 내용은 [종량제(후불)](https://intl.cloud.tencent.com/document/product/436/32534)을 참고하십시오. |
| 리소스 패키지(선불) | COS는 다양한 과금 항목에 대해 다양한 유형의 선불 리소스 패키지를 제공합니다. 실제 사용량은 리소스 패키지에서 먼저 차감 되며 초과분은 종량제 방식으로 과금됩니다. 리소스 패키지은 퍼블릭 클라우드 리전에서만 사용할 수 있으며 파이낸스 클라우드 리전에서는 사용할 수 없습니다. 자세한 내용은 [리소스 패키지(선불)](https://www.tencentcloud.com/document/product/436/54353)를 참고하십시오. |



## 과금 항목

COS 과금 항목에는 [스토리지 사용량 요금](https://intl.cloud.tencent.com/document/product/436/40099), [요청 요금](https://intl.cloud.tencent.com/document/product/436/40100), [데이터 검색 요금](https://intl.cloud.tencent.com/document/product/436/40097), [트래픽 요금](https://intl.cloud.tencent.com/document/product/436/33776) 및 [관리 요금](https://intl.cloud.tencent.com/document/product/436/40098)이 있습니다. 자세한 내용은 아래와 같습니다.



![](https://qcloudimg.tencent-cloud.cn/raw/f122045a434978ab26cb7c276723fc9d.png)


## 과금 주기

COS 각 과금 항목의 과금 주기 및 과금 순서는 다음과 같습니다.

> ?
>- COS 리소스 패키지 유효 기간 및 사용량 차감에 대한 자세한 내용은 [리소스 패키지(선불)](https://www.tencentcloud.com/document/product/436/54353)를 참고하십시오..
>- 2022년 9월 1일부터 COS 스토리지 사용량, 요청 및 데이터 검색 요금이 매일 정산됩니다. 자세한 내용은 [COS 스토리지 사용량, 요청 및 데이터 검색 일 결산 과금 안내](https://intl.cloud.tencent.com/document/product/436/47593)를 참고하십시오.

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
      <td rowspan=1>매일 전일 발생 비용 결산 및 청구서 생성</td>
      <td>프리 티어 > 리소스 패키지 > 종량제. 프리 티어 및 리소스 패키지가 없는 경우 종량제만 가능</td>
   </tr>
   <tr>
      <td rowspan=3>요청 요금</td>
      <td colspan=1>읽기/쓰기 요청 요금</td>
      <td rowspan=3>일</td>
      <td rowspan=3>매일 전일 발생 비용 결산 및 청구서 생성</td>
      <td>리소스 패키지 > 종량제</td>
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
      <td rowspan=3>일</td>
      <td rowspan=3>매일 전일 발생 비용 결산 및 청구서 생성</td>
      <td rowspan=3>종량제</td>
   </tr>
   <tr>
      <td colspan=1>ARCHIVE 데이터 검색 요금</td>
   </tr>
   <tr>
      <td colspan=1>DEEP ARCHIVE 데이터 검색 요금</td>
   </tr>
   <tr>
      <td colspan=2>트래픽 요금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>리소스 패키지 > 종량제</td>
   </tr>
   <tr>
      <td rowspan=4>관리 기능 요금</td>
      <td colspan=1>인벤토리 기능 요금</td>
      <td rowspan=4>일</td>
      <td rowspan=4>매일 전일 발생 비용 결산 및 청구서 생성</td>
      <td rowspan=4>종량제</td>
   </tr>
   <tr>
      <td colspan=1>인덱스 기능 요금</td>
   </tr>
   <tr>
      <td colspan=1>일괄 처리 요금</td>
   </tr>
   <tr>
      <td colspan=1>객체 태그 요금</td>
   </tr>
</table>


## 제품 가격

COS 과금 항목의 가격은 [가격 | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)에서 확인하실 수 있습니다. 세부 사항은 다음과 같습니다.
- 종량제 가격: 퍼블릭 클라우드 가격은 퍼블릭 클라우드 리전에 적용되고 파이낸스 클라우드 가격은 파이낸스 클라우드 리전에 적용됩니다. 자세한 내용은 [가격 | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)를 참고하십시오.
- 리소스 패키지 가격: 퍼블릭 클라우드 리소스 패키지의 가격은 중국 본토 리전과 중국 본토 외부 리전에 적용됩니다. 자세한 내용은 [가격 | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=) 또는 [리소스 패키지 구매 페이지](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)에서 확인할 수 있습니다.


## 가격 계산기

자신의 비즈니스 필요에 따라 과금 항목의 사용량을 추정한 다음 [가격 계산기](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)를 사용하여 요금을 계산하고 비용 견적을 내보낼 수 있습니다.

## 관련 링크


1. COS 과금: 자세한 계산법 및 시나리오별 과금 세부 사항은 [과금 예시](https://intl.cloud.tencent.com/document/product/436/6241)를 참고하십시오.
2. COS 연체로 인한 서비스 중단 정책: 데이터 보관 및 폐기 기간, 과금 관련 설명은 COS [연체 설명](https://intl.cloud.tencent.com/document/product/436/10044)을 참고하십시오.
3. 리소스 패키지 사용에 대한 자세한 내용은 [COS 리소스 패키지 구매 시 유의 사항](https://www.tencentcloud.com/document/product/436/54353)을 참고하십시오.
4. 과금 주기: 자세한 내용은 [About Billing](https://www.tencentcloud.com/document/product/555/7430?lang=en&pg=)을 참고하십시오.
5. COS 과금에 대해 더 궁금한 사항은 [FAQs](https://intl.cloud.tencent.com/document/product/436/32532)를 참고하시거나 [문의](https://www.tencentcloud.com/contact-us) 주시기 바랍니다.

