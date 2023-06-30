## Tencent Cloud CVM이란?

Tencent Cloud CVM은 Tencent Cloud가 제공하는 확장 가능한 컴퓨팅 서비스입니다. CVM을 사용하면 기존 서버를 사용할 때와 달리 리소스 용량 및 초기 투자를 예측할 필요가 없으며, 단기간에 여러 CVM을 빠르게 실행함과 동시에 응용 프로그램을 즉시 배포할 수 있습니다.
CVM은 CPU, 메모리, 디스크, 네트워크, 보안 등 모든 리소스의 사용자 정의를 지원하며, 변경이 필요한 경우 쉽게 조정할 수 있습니다.

## CVM은 어떻게 사용하나요?

Tencent Cloud에서는 CVM의 설정과 관리를 위해 다음과 같은 방식을 제공합니다.
- **콘솔**: Tencent Cloud에서 제공하는 웹서비스 인터페이스로 CVM을 설정하고 관리하는 데 사용됩니다.
- **API**: Tencent Cloud는 간편한 CVM 관리를 위해 API 인터페이스를 제공합니다. API에 대한 설명은 [API 개요](https://intl.cloud.tencent.com/document/api/213/15689)를 참조하십시오.
- **SDK**: [SDK 프로그래밍](https://intl.cloud.tencent.com/document/product/494)이나 Tencent Cloud [TCCLI](https://intl.cloud.tencent.com/document/product/1013)를 사용해 CVM API를 호출할 수 있습니다.

## 관련 개념

CVM 사용 전 다음 개념을 이해해야 합니다.
<table>
<tr>
<th width="12%">개념 </th><th>설명</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4939">인스턴스</a></td>
<td>클라우드의 가상 컴퓨팅 리소스는 CPU, 메모리, 운영 체제, 네트워크, 디스크 등 가장 기본적인 컴퓨팅 모듈을 포함하고 있습니다. Tencent Cloud는 CVM을 위해 다양한 CPU, 메모리, 스토리지, 네트워크 구성을 제공합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/213/11518">인스턴스 사양</a>을 참조하십시오.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">이미지</a></td>
<td>CVM이 실행하는 사전 제작 템플릿으로 사전 설정한 운영 체제 및 사전 설치한 소프트웨어 등을 포함합니다. CVM은 Windows, Linux 등 다양한 사전 제작 이미지를 제공합니다.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4953">CBS</a></td>
<td>제공되는 분산형 영구 블록 스토리지 디바이스는 인스턴스의 시스템 디스크나 확장 가능한 데이터 디스크로 사용 가능합니다.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a></td>
<td>Tencent Cloud가 제공하는 격리된 가상 네트워크로, 다른 리소스 로직과 격리되어 있습니다.</td>
</tr>
<tr>
<td>IP 주소</td>
<td>Tencent Cloud에서는 <a href="https://intl.cloud.tencent.com/doc/product/213/5225">내부 IP</a>와 <a href="https://intl.cloud.tencent.com/document/product/213/5224">공용 IP</a>를 제공합니다. 내부 IP는 LAN 서비스와 CVM 간의 상호 액세스를 지원하며, 공용 IP는 CVM 인스턴스에서 인터넷 액세스가 필요할 때 사용합니다.</td>
</tr>
<tr>
<td>EIP</td>
<td>동적 네트워크만을 위해 설계된 정적 공용 IP로, 오류를 빠르게 해결합니다.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/12452">보안 그룹</a></td>
<td>보안 그룹은 일종의 가상 방화벽으로, 상태 검증과 데이터 패킷 필터 기능을 갖추고 있습니다. 단일 또는 다중 CVM의 네트워크 액세스 제어에 사용되는 중요한 네트워크 보안 격리 방법입니다.</td>
</tr>
</table>

## 빠른 구매 및 CVM 사용자 정의 설정

CVM의 고급 설정(예: 스토리지 미디어, 용량, 네트워크 대역폭, 보안 그룹 사용자 정의 설정)에 대해서는 다음을 참조하십시오.
- [Windows CVM 사용자 정의 설정](https://intl.cloud.tencent.com/document/product/213/10516)
- [Linux CVM 사용자 정의 설정](https://intl.cloud.tencent.com/document/product/213/10517)

## CVM 가격

CVM은 종량제 과금을 지원합니다. 자세한 내용은 [가격 리스트](https://intl.cloud.tencent.com/document/product/213/2176)를 참조하십시오.
CVM 및 관련 리소스 가격 정보는 [제품 가격](https://buy.cloud.tencent.com/price/cvm/overview)을 참조하십시오.

## 기타 관련 제품

- Auto Scaling을 사용하면 정해진 시간이나 조건에 맞춰 서버 클러스터 수량을 자동으로 늘리거나 줄일 수 있습니다. 자세한 내용은 [Auto Scaling 제품 문서](https://intl.cloud.tencent.com/document/product/377)를 참조하십시오.
- CLB를 사용하면 클라이언트의 요청 트래픽을 자동으로 여러 CVM의 인스턴스에 할당할 수 있습니다. 자세한 내용은 [CLB 제품 문서](https://intl.cloud.tencent.com/document/product/214)를 참조하십시오.
- TKE를 사용하면 CVM의 애플리케이션 라이프사이클을 관리할 수 있습니다. 자세한 내용은 [TKE 제품 문서](https://intl.cloud.tencent.com/document/product/457)를 참조하십시오.
- 클라우드 모니터링 서비스를 사용하면 CVM 인스턴스 및 시스템 디스크를 모니터링할 수 있습니다. 자세한 내용은 [클라우드 모니터링 제품 문서](https://intl.cloud.tencent.com/document/product/248)를 참조하십시오.
- 클라우드에 관계형 데이터베이스를 배포하면 Tencent Cloud CDB도 사용할 수 있습니다. 자세한 내용은 [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236)을 참조하십시오.


