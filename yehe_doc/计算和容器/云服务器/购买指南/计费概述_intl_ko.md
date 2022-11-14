[CVM 가격 계산기](https://buy.intl.cloud.tencent.com/price/cvm/calculator)를 사용하여 필요한 각 제품의 구성과 가격을 확인하고, 예상 리소스 비용을 계산해 볼 수 있습니다. 구매 예산 목록에 원하는 상품을 추가한 뒤 원클릭으로 구입할 수도 있습니다.

<dx-alert infotype="notice" title="">
정확한 계산을 위해 로그인 후 계산기를 이용하십시오.
</dx-alert>



## 과금 방식

Tencent Cloud는 다양한 시나리오의 사용자 요구에 적합한 예약 인스턴스, 종량제 및 스팟 인스턴스의 세 가지 유형의 CVM 구매 방법을 제공합니다. 자세한 내용은 [과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.

## 인스턴스

인스턴스는 인스턴스에 사용하는 호스트의 하드웨어 설정을 결정합니다. Tencent Cloud는 인스턴스 유형별로 서로 다른 컴퓨팅과 스토리지 능력을 제공해 사용자가 제공하는 서비스 규모에 따라 인스턴스 컴퓨팅 능력, 스토리지 용량, 네트워크 액세스 방식을 선택할 수 있습니다.
Tencent Cloud는 현재 기본 하드웨어에 따라 다양한 모델 사양을 제공하고 있으며, 자세한 내용은 [인스턴스 스펙](https://intl.cloud.tencent.com/document/product/213/11518)을 참고하십시오.

인스턴스 유형별 가격은 [과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)을 참고하십시오.

## 스토리지

Tencent Cloud는 CVM 인스턴스에 각 유형별로 유연하고 경제적이며 사용하기 쉬운 데이터 스토리지 디바이스를 제공합니다. 각 스토리지 디바이스별로 서로 다른 성능과 가격을 제공하여 다양한 시나리오에 적용할 수 있습니다. 스토리지는 각 용도에 따라 다음과 같이 분류할 수 있습니다.
- 사용 시나리오에 따라 시스템 디스크와 데이터 디스크로 구분
- 구성 모드에 따라 클라우드 디스크, 로컬 디스크, 객체 스토리지로 구분

Tencent Cloud는 현재 프리미엄 CBS와 SSD CBS의 두 가지 클라우드 디스크 유형을 제공하며, 과금 방식은 종량제입니다.
디스크 가격에 관한 자세한 정보는 [CBS 가격 리스트](https://intl.cloud.tencent.com/document/product/213/2255)를 참고하십시오.

## 네트워크 대역폭

Tencent Cloud가 제공하는 모든 네트워크 유형의 통신사 액세스는 모두 BGP 멀티 라인으로, 라인의 품질을 보장하며 트래픽 과금제와 대역폭 과금제 두 가지 네트워크 과금 방식을 제공합니다.
- 대역폭 과금제: 공용 네트워크 전송 속도(단위: Mbps)에 따라 과금되며, 대역폭 이용률이 10% 이상인 경우 대역폭 과금제 선택을 우선적으로 고려할 수 있습니다.
- 트래픽 과금제: 공용 네트워크의 전송 데이터 총량(단위: GB)에 따라 과금되며, 대역폭 이용률이 10% 미만인 경우 트래픽 과금제 선택을 우선적으로 고려할 수 있습니다.

각종 네트워크의 대역폭 과금 방식에 대한 자세한 정보는 [공용 네트워크 과금 방식](https://intl.cloud.tencent.com/document/product/213/10578)을 참고하십시오.


## 이미지[](id:mirrorBilling)
이미지 사용 시 일정 요금이 발생할 수 있으며, 이미지 유형별 요금은 다음과 같습니다.
<table>
<tr>
<th width="16%">이미지 유형</th><th>설명</th>
</tr>
<tr>
<td>공용 이미지</td>
<td>이 유형에는 오픈 소스 이미지와 상업 이미지가 포함되어 있습니다.
<ul style="margin:0px">
<li>오픈 소스 이미지는 무료입니다.</li>
<li>상업용 이미지를 사용하면 License 비용이 청구됩니다. 요금은 인스턴스 사양 및 리전에 따라 다릅니다. 실제 가격은 <a href="https://buy.intl.cloud.tencent.com/price/cvm/calculator">가격 센터</a>에서 확인하십시오. Windows 이미지가 중국 본토 내 리전에서 사용되는 경우 License 비용이 면제됩니다. 중국 본토 이외의 리전에서 사용하는 경우 License 비용은 인스턴스 비용에 포함됩니다. 자세한 내용은 <a href="#ep">과금 예시</a> 를 참고하십시오.</li>
</ul>
</td>
</tr>
<tr>
<td>사용자 정의 이미지</td>
<td>
과금은 다음 두 부분을 포함합니다.
<ul style="margin:0px">
<li>스냅샷 요금: CBS 스냅샷 서비스는 이미지의 맨 아래 레이어에서 사용되기 때문에 사용자 정의 이미지를 유지하기 위해 일정 스냅샷 요금이 발생합니다. 중국 내 지역은 <a href="https://intl.cloud.tencent.com/document/product/362/32415">Free Tier</a> 80GB를 제공하며, 초과분 이후에는 용량에 따라 과금됩니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/362/32415">Snapshot Billing Overview</a>를 참고하십시오.</li>
<li>이미지 요금: 사용자 정의 이미지의 최종 소스가 유료 이미지이고 사용자 정의 이미지를 사용하는 경우 이미지 요금이 부과됩니다.</li>
</ul>
</td>
</tr>
<tr>
<td>공유 이미지</td>
<td>공유 이미지는 생성된 사용자 정의 이미지를 다른 Tencent Cloud 계정과 공유하는 이미지입니다. 이미지의 최종 소스가 유료 이미지이고 공유 이미지를 사용하는 경우 이미지 요금이 부과됩니다.</td>
</tr>
</table>


#### 과금 예시[](id:ep)

예시: 싱가포르 1존, 스탠다드 S5.MEDIUM2 인스턴스, 종량제 과금 방식.
- Windows 인스턴스 요금은 0.05 USD/시간입니다. ‘이미지’는 무료입니다. 아래 이미지를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/af8b0002847ce5f1542a90a1990e27ce.png)
