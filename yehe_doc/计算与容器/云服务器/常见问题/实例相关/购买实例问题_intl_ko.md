### CVM은 어떻게 구매하나요?

모든 사용자는 Tencent Cloud의 공식 홈페이지에서 클라우드 서비스를 구매할 수 있으며, 종량제(초 단위로 청구 및 시간당 결산) 유형의 CVM을 구매하실 수 있습니다. 자세한 내용은 [과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)을 참조 바랍니다.

### CVM에서 현재 제공하는 인스턴스 유형은 무엇인가요?

CVM은 다양한 인스턴스 사양을 제공합니다. 자세한 내용은 [인스턴스 사양](https://intl.cloud.tencent.com/document/product/213/11518)을 참조하여, 사용자의 비즈니스 수요에 맞는 인스턴스 유형을 선택할 수 있습니다.
- 갑작스러운 비즈니스 피크 타임이 발생한다면 종량제 과금 방식을 선택할 수 있습니다. 컴퓨터의 인스턴스를 언제든 활성화/폐기할 수 있으며, 인스턴스 실제 사용량에 따라 요금을 지불합니다. 또한, 초 단위의 정확한 과금을 통해 비용을 최소화할 수 있습니다. 

### Windows Server 2003 CVM을 구매할 수 있나요?

Microsoft에서 2015년 7월 14일부터 Windows Server 2003과 Windows Server 2003 R2에 대한 확장 지원 서비스 제공을 중단함에 따라, Tencent Cloud도 더는 Windows Server 2003 서버를 제공하지 않으므로 구매하실 수 없습니다.


### CVM은 어떤 방식으로 구매할 수 있나요?

CVM은 공식 홈페이지 구매와 API 구매, 두 가지 방식으로 구매할 수 있습니다.

### CVM을 구매하면 얼마 후에 사용할 수 있나요?

구매한 CVM을 시스템에 설치 완료한 후, 서버가 **실행 중** 상태라면 즉시 로그인 및 사용할 수 있습니다.

### 어떤 리전 또는 가용존에서 인스턴스를 구매할 수 있는지 어떻게 확인하나요?

[CVM 인스턴스 구매 페이지](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.53600366.770173325.1571651505)에서 구매 가능한 인스턴스를 확인할 수 있습니다.

### 인스턴스를 구매할 때 리소스가 품절일 경우에는 어떻게 하나요?

인스턴스 생성 시 리소스 품절 문제가 발생한다면, 아래와 같이 해결하시기를 권장합니다.
- 리전 변경
- 가용존 변경
- 리소스 설정 변경

변경한 후에도 리소스가 없다면 잠시 기다린 후에 다시 구매하시기 바랍니다. 인스턴스 리소스가 동적이므로 Tencent Cloud에서 최대한 빠르게 부족한 리소스를 보충하고 있지만, 일정 시간이 소요될 수 있습니다.


### 나의 비즈니스에 적합한 CVM 인스턴스를 어떻게 선택하나요?

아래와 같은 부분을 통해 실제 비즈니스 수요를 확인하고, [인스턴스 사양](https://intl.cloud.tencent.com/document/product/213/11518)을 참조하여 적합한 CVM 인스턴스를 선택할 수 있습니다.
- 실제 비즈니스 수요에 따라.
- 웹 사이트 유형 확인.
- 웹 사이트의 일평균 PV 확인.
- 첫 페이지 사이즈 확인.
- 데이터 용량 확인.

### CVM 인스턴스를 구매할 때 결제는 어떻게 하나요?

- [온라인 결제](https://intl.cloud.tencent.com/document/product/555/7425)에서 신용카드를 통해 결제할 수 있습니다.

### CVM 하나를 활성화하는 데 얼마의 시간이 소요되나요?

인스턴스 생성까지 일반적으로 1~2분의 시간이 소요되며, 인스턴스 생성을 완료한 후에는,
- Linux 인스턴스의 경우, 인스턴스에 연결할 수 있습니다. 자세한 내용은 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참조 바랍니다.
- Windows 인스턴스의 경우, 인스턴스에 연결할 수 있습니다. 자세한 내용은 [Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5435)을 참조 바랍니다.

> CVM을 생성하는 과정에서 오류가 발생한다면 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 통해 문의 바랍니다.
>

### 인스턴스 구매 및 결제를 완료했으나 인스턴스가 생성되지 않은 이유는 무엇인가요?

해당 가용존의 인스턴스 사양 재고량이 없는 이유일 수 있습니다. 이럴 경우 시스템에서 자동으로 결제 금액을 환급하며, 30분 이내에 환급금을 받지 못했다면 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 통해 문의 바랍니다.
[CVM 인스턴스 구매 페이지](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.53600366.770173325.1571651505)에서 구매 가능한 인스턴스를 확인할 수 있습니다.
