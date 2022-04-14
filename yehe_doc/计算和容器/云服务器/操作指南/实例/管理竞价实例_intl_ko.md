## 작업 시나리오
본 문서는 스팟 인스턴스 관리와 구매에 대해 안내하며 현재 다음과 같은 세 가지 방식을 제공합니다.
- **CVM 콘솔**: CVM 구매 페이지는 스팟 인스턴스 모드를 지원하고 있습니다.
- **Batch Compute 콘솔**: Batch Compute은 작업 제출을 지원하고 컴퓨팅 환경 생성 시 스팟 인스턴스를 선택합니다.
- **클라우드 API**: [RunInstance 인터페이스](https://intl.cloud.tencent.com/zh/document/product/213/33237)에 스팟 인스턴스 관련 매개변수가 추가되었습니다.


## 작업 단계
<dx-tabs>
::: CVM 콘솔

1. [CVM 구매 페이지](https://buy.intl.cloud.tencent.com/cvm?regionId=1&projectId=-1)에 로그인합니다.
2. 모델 선택 시 과금 방식은 **스팟 인스턴스**를 선택합니다. 아래 이미지를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/1c6720cefc4f56bc05d7ba7fc7c31347.png)
3. 실제 필요와 페이지 안내에 따라 리전, 가용존, 네트워크, 인스턴스 등의 구성 정보를 설정하십시오.
4. 구매한 스팟 인스턴스 정보를 검토하여 각 구성의 과금 명세서를 파악합니다.
5. **활성화**를 클릭하여 결제를 완료합니다.
결제 완료 후 [CVM 콘솔](https://console.cloud.tencent.com/cvm)로 이동하여 스팟 인스턴스 가격을 조회할 수 있습니다.

:::
::: Batch Compute 콘솔
### Batch Compute 특징 설명
-  **비동기화 인터페이스**
작업 제출 및 컴퓨팅 환경 생성, 컴퓨팅 환경의 기대 수량을 수정할 경우 Batch Compute은 비동기화 형식으로 요청을 처리합니다. 재고 및 가격 원인으로 현재 요청을 충족하지 못할 경우 충족될 때까지 스팟 인스턴스 리소스를 신청합니다.
사용자가 인스턴스 릴리스가 필요할 경우 Batch Compute 콘솔에서 컴퓨팅 환경의 인스턴스 수량을 조정해야 합니다. CVM 콘솔에서 릴리스하면 Batch Compute은 기대 수량에 도달할 때까지 자동으로 생성합니다.
- **클러스터 모드**
Batch Compute의 컴퓨팅 환경은 클러스터 모드로 스팟 인스턴스를 유지 보수할 수 있도록 지원합니다. 필요한 수량, 구성 및 최고 입찰 가격만 제출하면 컴퓨팅 환경은 자동으로 기대 수량에 도달할 때까지 신청되며 중단된 후에도 자동으로 보충 수량을 다시 신청합니다.
- **고정 가격**
현재 단계에서 고정 할인 모드를 사용할 경우 사용자는 시장 가격보다 크거나 같은 매개변수를 설정해야 하며 시장 가격에 대한 자세한 내용은 [현재 스팟 인스턴스는 어떤 리전과 인스턴스 유형 및 사양을 지원합니까?](https://intl.cloud.tencent.com/document/product/213/17817)를 참고하십시오.

### 사용 방법
1. [Batch Compute 콘솔](https://console.cloud.tencent.com/batch/env)에 로그인합니다.
2. 컴퓨팅 환경 관리 페이지에서 임의로 리전(예를 들면 광저우 리전 선택)을 선택하고 **생성**을 클릭합니다.
컴퓨팅 환경 생성 페이지로 이동합니다.
3. 컴퓨팅 환경 생성 페이지에서 ‘과금 유형’을 **스팟 인스턴스**로 설정하고 실제 수요에 따라 모델, 이미지, 이름 및 기대 수량 등 정보를 선택합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/95437ac5e26f3270c758fcc282042972.png)
4. **확인**을 클릭하여 생성합니다.
생성 완료 후 [Batch Compute 콘솔](https://console.cloud.tencent.com/batch/env)에서 방금 생성한 컴퓨팅 환경을 조회할 수 있습니다. 컴퓨팅 환경 내의 CVM도 동기화되어 생성되므로 해당 컴퓨팅 환경의**이벤트 로그**와 **인스턴스 리스트**를 통해 생성 상황을 조회할 수 있습니다.
:::
::: 클라우드\sAPI
RunInstance 인터페이스 내 [InstanceMarketOptionsRequest](https://intl.cloud.tencent.com/zh/document/api/213/15753?from_cn_redirect=1) 매개변수는 스팟 인스턴스 모드와 구성 관련 정보를 지정하여 사용 가능합니다.
* **동기화 인터페이스**: 현재 RunInstance가 제공하는 일회용 동기화 요청 인터페이스로써 신청이 실패(재고 부족, 요청 가격이 시장 가격보다 낮은 경우)하면 즉시 실패를 반환하므로 더 이상 신청되지 않습니다.
* **고정 가격**: 현재 단계에서 고정 할인 모드를 사용할 경우 사용자는 시장 가격보다 크거나 같은 매개변수를 설정해야 하며 시장 가격에 대한 자세한 내용은 [현재 스팟 인스턴스가 지원하는 리전 및 인스턴스 유형 및 사양](https://intl.cloud.tencent.com/document/product/213/17817)를 참고하십시오.

### 예시 시나리오 설명
광저우3존의 인스턴스가 있으면 해당 인스턴스의 결제 모드는 시간 당 후불 입찰 모드입니다. 구체적인 입찰 모드의 구성 정보는 다음과 같습니다.
- 최고 입찰 가격: 0.0923달러/시간
- 입찰 요청 모드: 일회성 요청
- 이미지 ID：img-pmqg1cw7
- 모델 선택: 2C4G 2세대 표준형(S2.MEDIUM4)
- 구매 수량: 1대

### 요청 매개변수
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Placement.Zone=ap-guangzhou-3
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.0923
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&ImageId=img-pmqg1cw7
&InstanceType=S2.MEDIUM4
&InstanceCount=1
&<공통 요청 매개변수>
```

### 반환 매개변수
```
{
  "Response":{
    "InstanceIdSet": [
      "ins-1vogaxgk"
    ],
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```
:::
</dx-tabs>
