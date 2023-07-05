[CVM 가격 계산기](https://buy.tencentcloud.com/price/cvm/calculator)를 사용하여 필요한 모든 제품의 합산 가격을 확인할 수 있으며, 예상 리소스 비용을 계산해 볼 수 있습니다. 필요한 제품을 구매 예산 목록에 추가하고 원클릭으로 구매할 수 있습니다.

<dx-alert infotype="notice" title="">
정확한 계산을 위해 로그인 후 계산기를 이용하십시오.
</dx-alert>

## 과금 방식

Tencent Cloud는 CVM 인스턴스에 대해 RI, 종량제 및 스팟의 세 가지 과금 방식을 제공합니다. 자세한 내용은 [과금 방식](https://www.tencentcloud.com/document/product/213/2180)을 참고하십시오.

## 인스턴스

인스턴스 모델은 호스트의 하드웨어 구성을 결정합니다. 모델마다 컴퓨팅 및 스토리지 용량이 다릅니다. 서비스 규모에 가장 적합한 인스턴스에 대한 컴퓨팅 용량, 스토리지 공간 및 네트워크 액세스 방법을 선택할 수 있습니다.
Tencent Cloud는 하드웨어 사양이 다른 다양한 CVM 모델을 제공합니다. 자세한 내용은 [인스턴스 유형](https://intl.cloud.tencent.com/document/product/213/11518)을 참고하십시오.

인스턴스 가격에 대한 자세한 내용은 [과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.

## 스토리지

Tencent Cloud는 CVM 인스턴스에 유연성, 비용 효율성, 사용 용이성을 갖춘 다양한 데이터 스토리지 장치를 제공합니다. 스토리지 유형에 따라 가격과 성능이 다르며, 다양한 사용 사례에 적합합니다. 스토리지 장치는 다음과 같이 분류됩니다.
- 사용 사례: 시스템 디스크 및 데이터 디스크
- 아키텍처: 클라우드 디스크, 로컬 디스크 및 COS 버킷

Tencent Cloud는 현재 프리미엄 클라우드 디스크와 SSD 클라우드 디스크를 제공합니다. 과금 방식은 종량제입니다.
디스크 가격에 관한 자세한 정보는 [CBS 가격 리스트](https://intl.cloud.tencent.com/document/product/213/2255)를 참고하십시오.

## 네트워크 대역폭

Tencent Cloud는 고품질 멀티라인 BGP 네트워크를 제공하여 최적의 네트워크 경험을 보장합니다. 두 가지 과금 방식(트래픽 과금 및 대역폭 과금)을 선택할 수 있습니다.
- 대역폭 과금: 공중망 전송 속도(단위: Mbps)에 따라 과금되며, 대역폭 이용률이 10% 이상인 경우 적합합니다.
- 트래픽 과금: 총 데이터 전송 크기(단위: GB)에 따라 과금되며, 대역폭 이용률이 10% 미만인 경우 적합합니다.

네트워크의 과금 방식에 대한 자세한 내용는 [공용 네트워크 과금 방식](https://intl.cloud.tencent.com/document/product/213/10578)을 참고하십시오.


## 이미지[](id:mirrorBilling)
이미지 사용 시 일정 요금이 발생할 수 있습니다. 이미지 유형별 요금은 다음을 참고하십시오. [Image Billing Description](https://www.tencentcloud.com/document/product/213/55134).
<table>
<tr>
<th width="16%">이미지 유형</th><th>설명</th>
</tr>
<tr>
<td>공용 이미지</td>
<td>이 유형에는 오픈 소스 이미지와 상업 이미지가 포함되어 있습니다.
<ul style="margin:0px">
<li>오픈 소스 이미지는 무료입니다. </li>
<li>상업용 이미지를 사용하면 License 요금이 청구됩니다.
</li>
</ul>
</td>
</tr>
<tr>
<td>사용자 정의 이미지</td>
<td>
과금은 다음 두 부분을 포함합니다.
<ul style="margin:0px">
<li>스냅샷 요금: 이미지는 CBS 스냅샷 서비스를 사용합니다. 사용자 정의 이미지를 유지하면 스냅샷 요금이 발생합니다. 중국 내 리전은 <a href="https://intl.cloud.tencent.com/document/product/362/32415">Free Tier</a> 80GB를 제공하며, 초과분은 용량에 따라 과금됩니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/362/32415">Snapshot Billing Overview</a>를 참고하십시오. </li>
<li>이미지 요금: 사용자 정의 이미지의 출처가 유료 이미지인 경우 요금이 발생합니다. </li>
</ul>
</td>
</tr>
<tr>
<td>공유 이미지</td>
<td>공유 이미지는 다른 Tencent Cloud 계정과 공유하는 사용자 정의 이미지입니다. 공유 이미지의 출처가 유료 이미지인 경우 요금이 발생합니다. </td>
</tr>
</table>


