## 무료 한도

| 적용 대상 | 무료 기한         | 무료 한도                                                     | 획득 방법                                                     |
| -------- | ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 신규 사용자   | 서비스 활성화 이후 6개월 이내 | COS가 제공하는 표준 스토리지 용량의 무료 이용에 관한 자세한 사항은 [무료 한도](https://intl.cloud.tencent.com/document/product/436/6240) 참조 | COS 서비스 활성화 후 자동 제공, [활성화하기](https://console.cloud.tencent.com/cos5) |

> !무료 한도 이용 기간이라도 표준IA 스토리지/CAS 용량, 요청, 트래픽 등 비 표준 스토리지 용량에 속하는 과금 항목은 무료로 제공되지 않습니다.


## 과금 방식

COS는 종량제 과금 방식을 적용하고 있으며, 관련 사항은 다음과 같습니다.

| 과금 방식                                                     | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [종량제(후불)](https://intl.cloud.tencent.com/document/product/436/32534) | COS의 디폴트 과금 방식, [모든 리전] 적용(https://intl.cloud.tencent.com/document/product/436/6224) |

## 제품 가격

COS 제품은 **종량제 가격**을 적용하며, COS와 관련한 세부 가격은 [제품 가격](https://intl.cloud.tencent.com/document/product/436/6239)을 참조하십시오.


## 과금 항목
COS의 과금 항목은 다음 이미지와 같이 스토리지 용량, 요청, 데이터 검색, 트래픽, 관리 기능이 포함됩니다. 자세한 내용은 [과금 항목](https://intl.cloud.tencent.com/document/product/436/33776)을 참조하십시오.


![](https://main.qcloudimg.com/raw/955512f4606494b557a1e54a633ac3e7.png)





## 과금 주기

COS 각 과금 항목의 과금 주기 및 과금 순서는 다음과 같습니다.

<table>
   <tr>
      <th colspan=2>과금 항목</td>
      <th>과금 주기</td>
      <th>과금 주기 설명</td>
      <th>과금 순서</td>
   </tr>
   <tr>
      <td colspan=2>스토리지 용량 과금</td>
      <td>월</td>
      <td rowspan=4>매월 1일 전달에 발생한 비용 결산 및 차감, 3일부터 5일까지 청구서 생성</td>
      <td>무료 한도 > 종량제, 무료 한도 대상이 아닌 경우 종량제가 적용됩니다.</td>
   </tr>
   <tr>
      <td rowspan=3>요청 과금</td>
      <td>읽기 쓰기 요청 과금</td>
      <td rowspan=3>월</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td>고급 보관 검색 요청 과금</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td>스마트 계층화 객체 모니터링 과금</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td rowspan=3>데이터 검색 과금</td>
      <td>저빈도 데이터 검색 과금</td>
      <td rowspan=2>월</td>
      <td rowspan=2>매월 1일 전달에 발생한 비용 결산 및 차감, 3일부터 5일까지 청구서 생성</td>
      <td rowspan=2>종량제</td>
   </tr>
   <tr>
      <td>보관 데이터 검색 과금</td>
   </tr>
   <tr>
      <td>고급 보관 데이터 검색 과금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td colspan=2>트래픽 과금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td>종량제</td>
   </tr>
   <tr>
      <td rowspan=4>관리 기능 과금</td>
      <td>인벤토리 기능 과금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td> 종량제</td>
   </tr>
   <tr>
      <td>인덱스 기능 과금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td> 종량제</td>
   </tr>
   <tr>
      <td>배치 과금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td> 종량제</td>
   </tr>
   <tr>
      <td>객체 태그 과금</td>
      <td>일</td>
      <td>매일 전날 발생한 비용 결산 및 청구서 생성</td>
      <td> 종량제</td>
   </tr>
</table>





## 링크 관련 사항


1. COS 과금의 자세한 계산법 및 시나리오별 자세한 과금 사항은 [과금 사례](https://intl.cloud.tencent.com/document/product/436/6241)를 참조하십시오.
2. COS 관련 연체로 인한 서비스 중단 정책: 데이터 보관 및 폐기 기간, 과금 관련 설명은 COS [연체 설명](https://intl.cloud.tencent.com/document/product/436/10044)을 참조하십시오.
3. 종량제를 이용하는 사용자는 직접 사용량을 계산할 수 있습니다. COS [가격 계산기(https://buy.cloud.tencent.com/price/cos/calculator)로 자세한 과금 내역을 계산해 보십시오.
4. COS와 관련한 문의사항은 [FAQ](https://intl.cloud.tencent.com/document/product/436/32532)를 참조하십시오.