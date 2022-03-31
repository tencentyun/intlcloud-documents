
## TKE 과금 설명
TKE 서비스 자체는 현재 무료이지만 관련 Tencent Cloud 제품 사용은 요금이 발생됩니다. TKE를 사용하려면 다음 제품을 사용해야 합니다. 자세한 내용은 해당 제품의 과금 문서를 참고하십시오.

- [CVM 과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)
- [CBS 가격 리스트](https://intl.cloud.tencent.com/document/product/213/2255)
- [CLB 과금 안내](https://intl.cloud.tencent.com/document/product/214/8848)

>! TKE는 Kubernetes 기반 선언적 서비스입니다. TKE에서 CLB 및 CBS와 같은 IaaS 리소스를 생성한 후 더 이상 사용할 필요가 없으면 TKE 콘솔에서 해당 서비스 리소스를 삭제하십시오. 특정 서비스 콘솔에서 서비스 리소스만 삭제하면 TKE가 이를 다시 생성하고 요금이 계속 발생합니다. 예를 들어, TKE에서 CLB 리소스를 생성하고 CLB 콘솔에서 CLB 인스턴스를 삭제한 경우 TKE는 선언적 API를 기반으로 CLB 인스턴스를 다시 생성합니다.

## EKS 과금 안내
EKS는 사용한 만큼만 과금되며 설정된 리소스 및 사용 기간을 기준으로 청구됩니다. 자세한 내용은 [EKS 과금 개요](https://intl.cloud.tencent.com/document/product/457/34054)를 참고하십시오.

