

## 과금 항목
TKE의 서비스 요금은 클러스터 관리 요금과 Tencent Cloud 서비스 리소스 요금의 두 부분으로 구성됩니다.
#### 클러스터 관리 요금
>! Tencent Cloud는 2022년 3월 21일 10:00(베이징 시간)부터 관리형 클러스터에 대한 요금을 부과합니다. [Starting Charging for Managed Cluster](https://intl.cloud.tencent.com/document/product/457/45156)를 참고하십시오.
>
클러스터 관리 요금은 **관리형 클러스터에만 부과**됩니다. TKE 관리형 클러스터는 고가용성, 고성능, 스케일링이 가능하고 매우 안정적인 완전 관리형 컨트롤 플레인을 제공하여 클러스터 구축 및 확장 등을 단순화하여 클러스터 관리 및 점검에 대해 걱정하지 않고 컨테이너화된 애플리케이션 개발에 집중할 수 있습니다. 따라서 TKE는 사양이 다른 관리 클러스터에 해당하는 클러스터 관리 요금을 부과합니다. 자세한 과금 규정은 [클러스터 관리 요금](#cluster)를 참고하십시오.



#### Tencent Cloud 서비스 리소스 요금
TKE 사용 중에 생성된 기타 Tencent Cloud 서비스 리소스(CVM, CBS, CLB 등)는 각 리소스의 청구 모드에 따라 요금이 부과됩니다. 자세한 내용은 [Tencent Cloud 서비스 리소스 요금](#cloudproducts)을 참고하십시오.


## 클러스터 관리 요금[](id:cluster)

### 과금 방식
사용량 과금 모드는 일반적으로 TKE에 적용됩니다.

| 과금 항목    | 과금 방식 | 결제 방법                                                     | 과금 단위 |
| --------- | -------- | ------------------------------------------------------------ | -------- |
| 클러스터 수(개) | 사용량 과금 | 구매 시 [Freeze the fee](https://intl.cloud.tencent.com/document/product/555/12039)하고, 서비스는 시간 단위로 청구 | USD/시간  |

### 제품 가격
>? 
>- 노드는 CVM 노드, BM 노드, 외부 노드 및 가상 노드를 포함하는 Kubnernetss Node를 나타냅니다.
>- 유휴 상태인 클러스터에는 클러스터 관리 요금이 부과되지 않습니다.
>
| 최대 노드 수 | 가격(USD/시간) |
| ---------------- | -------------- |
| 5                | 0.02040816           |
| 20               | 0.06279435           |
| 50               | 0.11459969           |
| 100              | 0.19152276           |
| 200              | 0.40031397           |
| 500              | 0.8021978           |
| 1000             | 1.47252747           |
| 3000             | 2.44897959          |
| 5000             | 4.40188383          |


## Tencent Cloud 서비스 리소스 요금[](id:cloudproducts)
TKE 사용 중에 생성된 기타 Tencent Cloud 서비스 리소스(CVM, CBS CLB 등)는 각 과금 모드에 따라 청구됩니다. 자세한 내용은 각 리소스에 대한 과금 설명을 참고하십시오.

| Tencent 클라우드 서비스 | 과금 설명 문서 | 
|---------|---------|
| CVM | [CVM 과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)| 
| CBS | [CBS 가격 리스트](https://intl.cloud.tencent.com/document/product/213/2255)| 
| CLB | [CLB Billing Description](https://intl.cloud.tencent.com/document/product/214/36999)| 

>! TKE는 Kubernetes를 기반으로 하는 선언적 서비스입니다. TKE에서 생성한 CLB, CBS 또는 기타 IaaS 서비스 리소스가 필요하지 않은 경우 TKE 콘솔에서 삭제해야 합니다. 그렇지 않으면 TKE에서 다시 생성하고 계속 요금을 부과합니다. 예를 들어, TKE 콘솔 대신 CLB 콘솔에서 CLB 인스턴스를 삭제하면 TKE는 선언적 API를 기반으로 CLB 인스턴스를 다시 생성합니다.



