Tencent Cloud의 네트워크 환경은 [VPC](https://cloud.tencent.com/product/vpc?idx=2)(Virtual Private Cloud)와 기본 네트워크 두 가지로 나뉩니다.
2017년 6월 13일 이후에 새로 등록한 계정은 기본 네트워크를 지원하지 않고 있으며, VPC 사용을 권장합니다. 이유는 다음과 같습니다.
- 완전한 기능: 기본 네트워크 기능은 모두 VPC를 통해 충족될 수 있으며, VPC는 보다 유연한 네트워크 서비스를 제공합니다. 예를 들어, 사용자 정의 IP 대역, 라우팅, DC 지원, VPN, NAT 등이 있습니다.
- 유연한 마이그레이션: 업계에는 유연한 마이그레이션에 대한 방안이 없습니다(종료, 개인 IP 변경 등이 필요합니다). 이후, 사용자는 서비스 증가로 인해 VPC를 사용해야 할 경우 마이그레이션 절차가 사용자의 업무에 영향을 미칠 수 있습니다.

## VPC와 기본 네트워크

### VPC

Tencent Cloud [VPC](https://cloud.tencent.com/document/product/215)는 사용자가 Tencent Cloud에서 정의한 논리적 격리 네트워크 공간입니다. 동일한 리전 내에서 다른 VPC는 기본적으로 서로 통신할 수 없습니다. 데이터센터에서 운영하는 일반적인 네트워크와 마찬가지로, Tencent Cloud VPC 내에 호스팅하는 것은 사용자의 Tencent Cloud 서비스 리소스입니다. 여기에 [CVM](https://intl.cloud.tencent.com/document/product/213/495), [CLB](https://intl.cloud.tencent.com/document/product/214/524), [CDB](https://cloud.tencent.com/document/product/236) 등 클라우드 서비스 리소스가 포함됩니다. 사용자는 VPC 환경을 완전히 파악할 수 있으며, 자세한 내용은 [VPC 제품 설명](https://intl.cloud.tencent.com/document/product/215/535)을 참조하십시오. VPC는 비교적 복잡한 네트워크 아키텍처를 구축할 수 있어 네트워크 관리에 익숙한 사용자에게 적합합니다.

![](https://mc.qcloudimg.com/static/img/33f800da64d2b7c0e6c2f23f102e059a/image.png)

### 기본 네트워크

기본 네트워크는 Tencent Cloud에 있는 모든 사용자의 공용 네트워크 리소스풀입니다. 사용자의 클라우드에 있는 모든 리소스는 Tencent Cloud에서 쉽고 빠르게 통합 관리됩니다.

### 기능 차이

| **기능**| **기본 네트워크**| **VPC** |
|---------|---------|---------|
| 테넌트 연결 | 테넌트 연결| GRE 캡슐을 기반으로한 논리적 격리 네트워크 |
| 네트워크 사용자 정의 | 미지원| 지원|
| 라우팅 사용자 정의 | 미지원| 지원|
| 사용자 정의 IP| 미지원| 지원|
| 통신 규칙 |동일 테넌트의 리전 내 통신| 리전 간 계정 간 통신 지원 |
| 보안 컨트롤 | [보안 그룹](https://intl.intl.intl.cloud.tencent.com/document/product/213/12452)| [보안 그룹](https://intl.intl.intl.cloud.tencent.com/document/product/213/12452)과 [ACL 네트워크](https://intl.cloud.tencent.com/document/product/215/5132) |

## VPC와 기본 네트워크 간 리소스 공유 및 액세스

Tencent Cloud에서 일부 클라우드 리소스와 기능은 동시에 두가지 네트워크 환경을 지원하여 다른 네트워크 간 공유 및 액세스할 수 있습니다.

|**리소스**|**설명**|
|--|--|
|[미러 이미지](https://intl.cloud.tencent.com/document/product/213/4940)|미러 이미지를 사용해 어떠한 환경에서도 CVM 인스턴스를 작동할 수 있습니다.|
|[EIP](https://intl.cloud.tencent.com/document/product/213/5733)|EIP는 어떠한 네트워크 환경의 CVM 인스턴스도 바인딩할 수 있습니다.|
|인스턴스|기본 네트워크의 인스턴스와 VPC 내의 인스턴스는 [공인 IP](https://intl.cloud.tencent.com/document/product/213/5224) 또는 [클래식링크](https://cloud.tencent.com/document/product/215/20083) 기능을 통하여 상호 통신할 수 있습니다.|
|[SSH 키](https://intl.cloud.tencent.com/document/product/213/6092)|SSH 키는 어떠한 네트워크 환경에서도 CVM 인스턴스 로딩을 지원합니다.|
|[보안 그룹](https://intl.intl.intl.cloud.tencent.com/document/product/213/12452)|보안 그룹은 어떠한 네트워크 환경에서도 CVM의 인스턴스를 바인딩할 수 있도록 지원합니다.|

> [CLB](https://cloud.tencent.com/document/product/214) 기본 네트워크와 VPC 간에 공유할 수 없습니다. 네트워크 통신 연결이 이미 구축되어 있더라도 CLB가 VPC 내의 인스턴스와 기본 네트워크 인스턴스를 동시에 바인딩하는 것을 지원하지 않습니다.

## 기본 네트워크 내의 인스턴스를 VPC로 마이그레이션

[VPC 서비스 전환](https://cloud.tencent.com/document/product/213/20278)을 참조하여, 기본 네트워크 내의 인스턴스를 VPC로 마이그레이션하십시오.
