Tencent Cloud는 공식 웹 사이트 구매 및 API 구매의 두 가지 CLB(Cloud Load Balancer) 구매 방식을 제공합니다. 이 섹션에서는 두 가지 구매 방식에 대해 자세히 설명합니다.

## 공식 웹 사이트 구매
[Tencent Cloud 공식 웹사이트](https://buy.cloud.tencent.com/lb)에서 CLB 인스턴스를 구매할 수 있습니다. Tencent Cloud 계정에는 IP별 청구 계정과 CVM별 청구 계정의 두 가지 유형이 있습니다. 2020년 6월 17일 00:00:00 이후에 생성된 계정은 IP별 청구 계정 유형입니다. 그 전에 계정을 만든 경우 계정 유형 확인에 설명된 대로 콘솔에서 [계정 유형을 확인](https://intl.cloud.tencent.com/document/product/684/15246)할 수 있습니다.
### CVM별 청구 계정
사설망 CLB 인스턴스는 무료인 반면 공중망 CLB 인스턴스는 사용한 만큼만 지불하는 시간당 인스턴스 요금을 부과합니다. [CVM](https://intl.cloud.tencent.com/document/product/213/495)에서 공중망을 구입할 수 있습니다. 네트워크 과금 방식에 대한 자세한 내용은 [공용 네트워크 과금 방식](https://intl.cloud.tencent.com/document/product/213/10578)을 참고하십시오.
공식 웹사이트에서 CLB 인스턴스를 구매하려면 다음을 수행하십시오.
1. Tencent Cloud 콘솔에 로그인하여 [CLB 구매 페이지](https://buy.cloud.tencent.com/lb)로 이동합니다.
2. 인스턴스 유형은 ‘CLB’를 권장합니다.
3. 네트워크 유형 및 프로젝트를 포함하여 필요에 따라 속성을 선택합니다. 속성에 대한 자세한 내용은 [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629)을 참고하십시오.
4. 선택한 CLB 인스턴스를 확인하고 결제합니다.
5. 결제가 완료되면 CLB 서비스가 활성화됩니다. 이제 CLB 인스턴스를 구성하고 사용할 수 있습니다.

### IP별 청구 계정
사설망 CLB 인스턴스는 무료입니다. 공중망 CLB 인스턴스는 월간 구독 또는 사용한 만큼 지불하는 방식으로 인스턴스 요금과 공중망 요금을 과금합니다. 월간 구독 공중망은 대역폭으로만 과금되는 반면 종량제 공중망은 대역폭, 트래픽 및 공유 대역폭 패키지별로 과금될 수 있습니다.
공식 웹사이트에서 CLB 인스턴스를 구매하려면 다음을 수행하십시오.
1. Tencent Cloud 콘솔에 로그인하여 [CLB 구매 페이지](https://buy.cloud.tencent.com/lb)로 이동합니다.
2. 인스턴스 유형은 ‘CLB’를 권장합니다.
3. 네트워크 유형, 네트워크 과금 방식 및 프로젝트를 포함하여 필요에 따라 속성을 선택합니다. 속성에 대한 자세한 내용은 [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629)을 참고하십시오.
>?현재 광저우, 상하이, 난징, 지난, 항저우, 푸저우, 베이징, 스자좡, 우한, 창사, 청두, 충칭 리전에서만 지원됩니다. 다른 리전에서의 지원은 콘솔 페이지를 참고하십시오.
>
4. 선택한 CLB 인스턴스를 확인하고 결제합니다.
5. 결제가 완료되면 CLB 서비스가 활성화됩니다. 이제 CLB 인스턴스를 구성하고 사용할 수 있습니다.

## API를 통해 CLB 인스턴스 구매
API를 통해 CLB 인스턴스를 구매하려면 [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/33841)를 참고하십시오.

## 후속 작업
- CLB 인스턴스에 TCP 리스너를 설정하는 방법은 [Configuring TCP Listener](https://intl.cloud.tencent.com/document/product/214/32517)를 참고하십시오.
- CLB 인스턴스에 UDP 리스너를 설정하는 방법은 [Configuring a UDP Listener](https://intl.cloud.tencent.com/document/product/214/32518)를 참고하십시오.
- CLB 인스턴스에 TCP SSL 리스너를 설정하는 방법은 [Configuring TCP SSL Listener](https://intl.cloud.tencent.com/document/product/214/32519)를 참고하십시오.
- CLB 인스턴스에 HTTP 리스너를 설정하는 방법은 [Configuring HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515)를 참고하십시오.
- CLB 인스턴스에 HTTPS 리스너를 설정하는 방법은 [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516)를 참고하십시오.
