### CDN은 요청 횟수에 따른 과금을 지원하나요?
현재 CDN은 요청 횟수에 따른 과금 방식을 지원하지 않습니다.

### CDN 비용이 연체되면 어떻게 되나요?
자세한 내용은 과금 설명 문서의 [과금 설명](https://intl.cloud.tencent.com/document/product/228/2949#.E6.AC.A0.E8.B4.B9.E8.AF.B4.E6.98.8E)을 참조 바랍니다.

### 원본 서버가 COS를 사용할 경우, CDN이 COS에 Origin-pull 할 때 발생하는 트래픽도 요금이 부과되나요?
CDN이 COS에 Origin-pull 할 때 발생하는 트래픽의 경우, CDN에서는 과금되지 않고 COS에서 과금됩니다. 자세한 내용은 [COS를 CDN 원본 서버로 사용](https://intl.cloud.tencent.com/document/product/228/32977)을 참조 바랍니다.

### CDN 비활성화(CDN 서비스 종료) 후에도 트래픽이 발생하거나 과금되는 일이 있나요?
CDN의 도메인 가속 서비스를 비활성화한 후 도메인에 여전히 CNAME이 설정되어 있다면, 노드로부터 리졸브 요청 시 404 상태 코드를 리턴하며, 이에 따라 소량의 트래픽 소모가 발생합니다. 콘솔이 사용자가 이 데이터 레코드를 참고할 수 있도록 보존하므로, 이와 동시에 해당하는 로그 레코드 또한 생성됩니다. 단, 도메인을 비활성화한 상태이기에 이 부분에 대한 실제 트래픽 소모 및 로그 패키지는 비용에 포함되지 않습니다. 가속 서비스를 비활성화하기 전에 먼저 원본 가져오기 리졸브를 수정하세요.

### CDN 과금 방식은 어떻게 변경하나요?

CDN 사용 도중 과금 방식이 실제 비즈니스 상황에 부적합하다고 느끼실 경우(적합 여부는 [과금 방식 선택](https://intl.cloud.tencent.com/document/product/228/2949#.E8.AE.A1.E8.B4.B9.E6.96.B9.E5.BC.8F.E9.80.89.E6.8B.A9)을 참조하여 판단할 수 있습니다), 사용 도중에 과금 방식을 변경하실 수 있습니다. 변경 방법은 아래와 같습니다.
1. Tencent Cloud [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 서비스 개요에 들어간 뒤, 오른쪽의 과금 현황에서 [Change]을 클릭합니다.
![이미지 설명](https://main.qcloudimg.com/raw/38b82d3d166970552437b5525b74c44f.png)
2. 과금 방식을 기존의 **트래픽 과금**에서 **대역폭 과금**으로 변경합니다.
![이미지 설명](https://main.qcloudimg.com/raw/6fd1575557d0c4b7b06be9f1fc30e1da.png)
3. 과금 방식을 **대역폭 과금**으로 변경한 후에는 이튿날에 비용을 결산할 때 전날 소모가 발생한 시간에 적용되어 있던 과금 방식을 기준으로 결산됩니다.

### 원본 서버가 CVM을 사용할 경우, CDN이 CVM에 Origin-pull 할 때 발생하는 트래픽도 과금되나요?

CDN은 해당 트래픽에 대해 추가로 요금을 부과하지 않습니다.

### CDN 대역폭 과금에서, 1Gbps는 몇 Mbps인가요?

CDN에서 사용하는 대역폭 단위는 1Gbps = 1000Mbps, 1Mbps = 1000Kbps, 1Kbps = 1000bps 입니다.

### CDN 과금 시 다운스트림 트래픽에만 비용이 청구되나요?

CDN은 다운스트림 트래픽에만 비용을 청구하며, 업스트림 트래픽은 요금을 부과하지 않습니다.

### 사용하던 CDN이 공격당할 경우, 해당 공격으로 인해 발생한 비용은 면제되나요?

CDN의 주요 기능은 콘텐츠 가속이므로, 해당 요청이 악성 요청인지의 정상적인 요청인지를 식별할 수 없어, 악성 요청을 처리하여 트래픽이 발생하지 않도록 막아내지 못합니다. 따라서 악성 도메인으로 인한 손실 방지를 위해, 도메인이 공격받아 대역폭이 10Gbps를 초과한 경우 [티켓 제출](https://console.qcloud.com/workorder/category)을 통해 문의하시면 Tencent Cloud CDN에서 대역폭이 10Gbps를 초과하는 부분의 비용을 반환해드립니다.

### CDN은 어떤 과금 방식이 있나요?

CDN은 두 가지 과금 방식을 제공합니다. 대역폭 청구와 트래픽 청구(기본)는 모두 후불 일일 결제입니다. 후불제는 일일 결산 방식으로 전날 00:00:00-23:59:59에서 발생한 총 소모량은 둘째 날 18:00 전에 과금합니다. 청구 모드 선택 방법에 대한 정보는 [과금 설명](https://intl.cloud.tencent.com/document/product/228/2949)을 참조하십시오.

### CDN은 언제 비용이 결제되나요?

CDN은 후불 결산 방식입니다(선사용, 후결제). 둘째 날의 결산 방식은 전날의 소모량을 기준으로 청구합니다.

- 당일 과금 방식은 대역폭 과금 방식입니다. 소모량이 발생하지 않았을 때 트래픽 과금 방식으로 전환됩니다. 두번째 날 결산 시 중도에 과금 방식을 수정하지 않았다면 트래픽 과금 방식에 따라 정산됩니다.
- 당일 과금 방식은 대역폭 과금 방식입니다. 트래픽 과금 방식으로 전환했을 때 이미 소모량이 발생합니다. 중도에 과금 방식을 수정하지 않았다면 트래픽 과금 방식에 따라 결산합니다.

CDN 서비스의 월간 소비 금액이 2만 달러 이상이거나 2만 달러를 초과할 것으로 예상된다면, Tencent Cloud CDN에서 저렴한 가격의 월간 과금 방식을 적용할 수 있으니, 티켓 제출을 통해 문의해보시길 바랍니다.

### 월간 대역폭 95% 과금이란 무엇인가요?

대역폭 과금은 대역폭의 피크값을 기준으로 과금됩니다.
월간 대역폭 95%: CDN의 일일 대역폭 통계 포인트는 총 288개로, 당월 1일부터 각 유효일(발생한 소모량이 0byte보다 크면 유효일로 기록)의 모든 통계 포인트를 정렬하여 상위 5%를 제외한 나머지 중 가장 큰 통계 포인트를 계약서의 가격에 따라 대역폭 과금 방식으로 과금합니다.

> 계산 예시:
> 고객은 1월1일부터 본격적으로 청구 시작하며 계약서 가격은 P USD/Mbps/월 입니다.
> 1월에 총 14일의 유효일이 있다고 가정할 경우, 이 14일 동안의 모든 통계 포인트인 14 * 288개에서 상위 5%를 제외한 나머지 중 가장 높은 값인 Max95가 곧 과금 대역폭 기준이 됩니다. 따라서 1월 요금은 Max95 * P * 14 / 31입니다.

### CDN 청구서는 어떻게 확인하나요?

Tencent Cloud [Account Info](https://console.cloud.tencent.com/expense/bill/overview)에서 청구서를 확인할 수 있습니다. 자세한 작업 절차는 [청구서 문의](https://intl.cloud.tencent.com/document/product/228/6071)를 참조하십시오.