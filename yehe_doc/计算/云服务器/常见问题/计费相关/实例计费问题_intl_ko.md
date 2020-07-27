## 구매 관련

### CVM 생성에 실패하면 어떻게 해결해야 하나요?

서버 생성 과정이 오래 걸릴 경우 잠시 기다리며 성공 여부를 확인 바랍니다. 생성이 실패했을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 발생한 문제를 보고하면 엔지니어의 도움으로 문제를 해결할 수 있습니다.

### CVM 발주 실패 시 어떻게 폐기해야 하나요?

[티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 고객센터로 연락하여 기기 정보에 대한 전체 화면 캡처와 폐기할 수 없는 상황에 대한 화면 캡처를 제공해 주시고, **발주 실패**로 표기해 주시면 문제 처리에 도움이 됩니다.


## 연장 관련

### CVM이 만료된 후에는 어떻게 연장하나요?

[인스턴스 연장](https://intl.cloud.tencent.com/document/product/213/6143)을 참조 바랍니다.

### CVM 연장 갱신은 어떻게 설정하나요?

[연장 갱신 설정 관련 작업 순서](https://intl.cloud.tencent.com/document/product/213/6143#.E8.AE.BE.E7.BD.AE.E8.87.AA.E5.8A.A8.E7.BB.AD.E8.B4.B9.E7.9A.84.E6.93.8D.E4.BD.9C.E6.AD.A5.E9.AA.A4)를 참조 바랍니다.

### 종량제 인스턴스도 연장이 필요하나요?

종량제 인스턴스는 정각에 한 번씩 계좌에서 자동으로 요금을 차감하므로 연장의 개념이 없습니다.

## 기타

### CVM 인스턴스 자동 릴리스(폐기)을 설정할 수 있나요?

자동 릴리스 시간에 따라 종량제 인스턴스 자동 릴리스(폐기)을 설정할 수 있습니다. 자세한 작업 방식은 [인스턴스 폐기/반환](https://intl.cloud.tencent.com/document/product/213/4930)을 참조 바랍니다.
그래도 문제가 해결되지 않을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 해주시기 바랍니다.

### 이미 20GB 이상의 CBS를 구매한 Linux CVM을 Windows 시스템으로 재설치할 경우, 비용은 어떻게 과금되나요?

- Windows 재설치 성공 후 기존에 구매한 20GB를 초과한 부분의 시스템 디스크에 대해서는 과금이 중지됩니다. 즉, 시스템 디스크가 더 이상 과금되지 않습니다.

### 이미 CBS 유형을 구매한 Windows CVM을 Linux 시스템으로 재설치할 경우, 비용은 어떻게 과금되나요?

현재 시스템 디스크의 용량 축소를 지원하지 않기 때문에 CBS는 현재 용량에 따라 재설치해야 하며 비용이 추가되지 않습니다. Linux 시스템으로 재설치 시, 시스템 디스크 용량을 확장하려면 대응하는 시스템 디스크 용량 설정만큼 비용을 추가 지불해야 합니다. 자세한 내용은 [시스템 디스크 및 데이터 디스크](https://intl.cloud.tencent.com/document/product/213/17351)에서 시스템 디스크 확장 관련 소개를 참조 바랍니다.
CBS 가격에 대한 자세한 내용은 [CBS 가격 리스트](https://intl.cloud.tencent.com/document/product/362/2413)를 참조 바랍니다.

> 중국 외 리전의 CVM은 시스템 재설치 시, Linux와 Windows 시스템 간의 호환이 지원되지 않습니다.
>

### CVM 청구서에서 연산 모듈은 무엇을 의미하나요?

연산 모듈은 인스턴스 사양과 일일이 대응되는 S5.SMALL4 등을 의미하며, CPU, 메모리, NVMe 로컬 디스크 등의 컴퓨팅 모듈이 포함됩니다.




