## 작업 시나리오
본 문서는 스팟 인스턴스 관리와 구매에 대해 안내하며 현재 다음과 같은 세 가지 방식을 제공합니다.
- **CVM 콘솔**: CVM 구매 페이지는 스팟 인스턴스 모드를 지원하고 있습니다.
- **배치 컴퓨팅 콘솔**: 배치 컴퓨팅은 작업 제출을 지원하고 컴퓨팅 환경 생성 시 스팟 인스턴스를 선택합니다.
- **클라우드 API**: [RunInstance 인터페이스](https://cloud.tencent.com/document/api/213/15730)에 스팟 인스턴스 관련 파라미터를 추가하였습니다.


## 작업 순서
### CVM 콘솔

1. [CVM 구매 페이지](https://buy.cloud.tencent.com/cvm)에 로그인합니다.
2. 모델 선택 시 과금 방식은 [스팟 인스턴스]를 선택합니다. 아래 이미지를 참조하십시오.
> 스팟 인스턴스는 현재 베타 테스트 단계이며 베타 테스트되지 않은 사용자는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 사전 이용을 신청할 수 있습니다.
>
3. 인스턴스 실제 요구 사항과 페이지 알림에 따라 리전, 가용존, 네트워크 및 인스턴스 등 구성 정보를 설정합니다.
4. 구매한 스팟 인스턴스 정보를 검토하여 각 구성의 과금 명세서를 파악합니다.
5. [활성화]를 클릭하고 결제를 완료합니다.
결제 완료 후 [CVM 콘솔](https://console.cloud.tencent.com/cvm)에 진입해서 스팟 인스턴스 가격을 조회할 수 있습니다.

### Batch Compute 콘솔
- **비동기 인터페이스**: 작업 제출 및 컴퓨팅 환경 생성, 컴퓨팅 환경의 기대 수량을 수정할 경우 배치 컴퓨팅은 비동기 형식으로 요청을 처리합니다. 재고 및 가격 원인으로 현재 요청을 충족하지 못할 경우 충족될 때까지 스팟 인스턴스 리소스를 신청합니다.
사용자가 인스턴스 릴리스가 필요할 경우 배치 컴퓨팅 콘솔에서 컴퓨팅 환경의 인스턴스 수량을 조정해야 합니다. CVM 콘솔에서 릴리스하면 배치 컴퓨팅은 기대 수량에 도달할 때까지 자동으로 생성합니다.
- **클러스터 모드**: 배치 컴퓨팅의 컴퓨팅 환경은 클러스터 모드로 스팟 인스턴스를 유지 보수할 수 있도록 지원합니다. 필요한 수량, 구성 및 최고 입찰 가격만 제출하면 컴퓨팅 환경은 자동으로 기대 수량에 도달할 때까지 신청되며 중단된 후에도 자동으로 보충 수량을 다시 신청합니다.
- **고정 가격**: 현재 단계에서 고정 할인 모드를 사용할 경우 사용자는 시장 가격보다 크거나 같은 파라미터를 설정해야 하며 파라미터에 대한 자세한 내용은 [현재 스팟 인스턴스는 어떤 리전과 인스턴스 유형 및 사양을 지원합니까?](https://intl.cloud.tencent.com/document/product/213/17817)를 참조하십시오.

#### 이용 순서

1. [배치 컴퓨팅 콘솔](https://console.cloud.tencent.com/batch/env)에 로그인합니다.
2. 컴퓨팅 환경 관리 페이지에서 임의로 리전(예를 들면 광저우 리전 선택)을 선택하고[생성]을 클릭합니다.
컴퓨팅 환경 생성 페이지에 진입합니다.
3. 컴퓨팅 환경 생성 페이지에서 [과금 유형]을 [스팟 인스턴스]로 설정하고 실제 수요에 따라 모델, 미러 이미지, 이름 및 기대 수량 등 정보를 선택합니다. 아래 이미지를 참조하십시오.
4. [확인]을 클릭하고 생성을 완료합니다.
생성 완료 후 [배치 컴퓨팅 콘솔](https://console.cloud.tencent.com/batch/env)에서 방금 생성한 컴퓨팅 환경을 조회할 수 있습니다. 컴퓨팅 환경 내의 CVM도 동기화되어 생성되므로 해당 컴퓨팅 환경의[활동 로그]와 [인스턴스 리스트]를 통해 생성 상황을 조회할 수 있습니다.


### 클라우드 API
RunInstance 인터페이스 내 [InstanceMarketOptionsRequest](https://cloud.tencent.com/document/api/213/15753#InstanceMarketOptionsRequest) 파라미터는 스팟 인스턴스 모드와 구성 관련 정보를 지정하여 사용 가능합니다.
* **동기화 인터페이스**: 현재 RunInstance가 제공하는 일회용 동기화 요청 인터페이스로써 신청이 실패(재고 부족, 요청 가격이 시장 가격보다 낮은 경우)하면 즉시 실패를 반환하므로 더 이상 신청되지 않습니다.
- **고정 가격**: 현재 단계에서 고정 할인 모드를 사용할 경우 사용자는 시장 가격보다 크거나 같은 파라미터를 설정해야 하며 시장 가격에 대한 자세한 내용은 [현재 스팟 인스턴스는 어떤 리전과 인스턴스 유형 및 사양을 지원합니까?](https://intl.cloud.tencent.com/document/product/213/17817)를 참조하십시오.

#### 예시 시나리오 설명
광저우3존의 인스턴스가 있으면 해당 인스턴스의 결제 모드는 시간 당 후불 입찰 모드입니다. 구체적인 입찰 모드의 구성 정보는 다음과 같습니다.
- 최고 입찰 가격: 0.6원/시간
- 입찰 요청 모드: 일회성 요청
- 미러 이미지 ID：img-pmqg1cw7
- 모델 선택: 2C4G 2세대 표준형(S2.MEDIUM4)
- 구매 수량: 1대

#### 파라미터 요청
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Placement.Zone=ap-guangzhou-3
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.60
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&ImageId=img-pmqg1cw7
&InstanceType=S2.MEDIUM4
&InstanceCount=1
&<파라미터 공개 요청>
```

#### 파라미터 리턴
```
{
  "Response": {
    "InstanceIdSet": [
      "ins-1vogaxgk"
    ],
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```

