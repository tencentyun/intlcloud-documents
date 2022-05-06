TencentOS Server(Tlinux, 줄여서 TS라고도 함)는 클라우드 시나리오용으로 Tencent Cloud에서 개발한 Linux 운영 체제로, CVM(Cloud Virtual Machine) 인스턴스의 애플리케이션에 더 높은 성능과 높은 보안성과 안정적인 실행 환경을 제공하기 위해 특정 기능과 성능 최적화를 제공합니다. TencentOS Server는 Linux 커널을 기반으로 자체 개발 및 설계되었으며 10년 이상 운영 체제 분야에서 Tencent의 기술을 축적했으며, 수년간 Tencent 내부 대규모 비즈니스에 의해 검증 및 최적화 되었습니다. Tencent 내부 운영 체제의 99% 이상을 차지하며, Tencent의 모든 비즈니스를 포괄합니다. 동시에 Tencent는 소셜 네트워킹, 게임, 금융 결제, AI, 보안 등 중국 내에서 가장 다양한 비즈니스 생태계를 보유하고 있으며, 안정성, 보안성, 호환성 및 성능 등 핵심 능력이 충분히 검증되었습니다. 커뮤니티 OS 버전 대비, TencentOS Server는 안정성, 성능, 컨테이너 인프라 등 기타 핵심 능력 측면에서 포괄적으로 향상되고 최적화되어, 기업에 안정적이고 가용성이 높은 서비스를 제공합니다. 최고의 클라우드 운영 체제를 목표로 노력하고 있으며, CentOS보다 더 나은 엔터프라이즈급 운영 체제 솔루션입니다.

현재 TencentOS Server는 오픈되어 있으며, 사용자 모드 환경은 CentOS와 호환되고 CentOS에서 개발된 애플리케이션은 TencentOS Server에서 직접 실행할 수 있습니다.


## 사용 설명
TencentOS Server는 표준형, 컴퓨팅형, 메모리성 및 높은 IO형 등을 포함한 대부분의 표준 모델에 적합합니다. 또한 CPM(Cloud Physical Machine)2.0 및 고성능 컴퓨팅 클러스터를 지원합니다.

<dx-alert infotype="notice" title="">
GPU 인스턴스를 실행하기 위해 TencentOS Server를 사용해야 하는 경우 해당 GPU 드라이버를 설치하십시오.
</dx-alert>


## TencentOS Server 장점
- **천만 규모의 노드에서 검증된 고도의 안정성**
TencentOS Server는 총 수천만 개의 배포 규모와 99.999%의 전체 가용성으로 대규모 비즈니스에 대한 장기간의 실질적인 검증을 거쳤습니다.
- **완전히 최적화된 더 높은 성능**
고도로 최적화된 고성능 OS는 시스템의 다양한 소프트웨어에 최적화되어 있으며, 일반적인 비즈니스 성능은 50% 이상 향상되었습니다. Tencent Cloud를 통해 TencentOS Server를 사용하면 더 높은 성능을 얻을 수 있습니다.
- **오픈 소스 호환, 클라우드에서 더 나은 OS**
100% 오픈 소스 Linux 릴리스 버전인 사용자 모드는 CentOS와 계속 호환되며 안정성과 성능 면에서 더 많은 장점이 있으며 클라우드에서 CentOS보다 더 나은 대안입니다.
- **클라우드를 위해 탄생, 고도화된 커스터마이징**
최신 개방 표준 기반 버츄얼화 및 클라우드 네이티브 툴 포함하고, 다양한 워크로드에 적합하며, 클라우드 전용으로 개발되었습니다.
- **보안 및 컴플라이언스, 무중단 복구**
Security Lab은 시스템 보안을 유지하고, 시스템 수준의 보안을 강화하며, 다양한 취약점을 적시에 수정하고, 핫 패치 복구를 지원하여 불필요한 중단 시간을 방지합니다.



## TencentOS Server 이미지 버전
현재 Tencent Cloud에는 사용자가 선택할 수 있는 3개의 TencentOS Server 이미지가 있습니다.

<table>
<tr>
<th width="35%">이미지 버전</th>
<th>설명</th>
</tr>
<tr>
<td>TencentOS Server 3.1</td>
<td>CentOS 8 사용자 모드와 호환되며 커뮤니티 5.4 LTS 커널을 기반으로 심층 최적화된 tkernel4 버전을 지원합니다.</td>
</tr>
<tr>
<td>TencentOS Server 2.4</td>
<td>CentOS 7 사용자 모드와 호환되며 커뮤니티 4.14 LTS 커널을 기반으로 심층 최적화된 tkernel3 버전을 지원합니다.</td>
</tr>
<tr>
<td>TencentOS Server 2.4(TK4)</td>
<td>CentOS 7 사용자 모드와 호환되며 커뮤니티 5.4 LTS 커널을 기반으로 심층 최적화된 tkernel3 버전을 지원합니다.</td>
</tr>
</table>



## TencentOS Server 커널
TencentOS Server 커널(tkernel이라고 함)은 릴리스 버전에서 분리되어 있으며 현재 기본 커널은 두 가지 버전으로 나뉩니다.
- 커뮤니티 5.4 LTS에 기반하여 심층 최적화된 tkernel4(tk4라고 함).
- 커뮤니티 4.14 LTS에 기반하여 심층 최적화된 tkernel3(tk3이라고 함)
자세한 내용은 [TencentOS kernel github 라이브러리](https://github.com/Tencent/TencentOS-kernel)를 참고하십시오.

## TencentOS Server 사용 

### 클라우드에서 사용
인스턴스를 생성하거나 기존 인스턴스의 운영 체제를 재설치할 때 공용 이미지를 선택하고 해당 버전의 OpenCloudOS를 사용하도록 선택할 수 있습니다. 자세한 작업은 [인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855) 및 [시스템 재설치](https://intl.cloud.tencent.com/document/product/213/4933)를 참고하십시오.

### 로컬 경험
다음의 방법을 통해 로컬에서 TencentOS Server를 경험할 수 있습니다.
- TencentOS Server 2.4 : [iso](http://mirrors.tencent.com/tlinux/2.4/iso/) 및 [qcow](http://mirrors.tencent.com/tlinux/2.4/images/). 
- TencentOS Server 3.1  : [iso](http://mirrors.tencent.com/tlinux/3.1/iso/) 및 [qcow](http://mirrors.tencent.com/tlinux/3.1/images/). 



## 서비스 및 업데이트
Tencent Cloud는 정기적인 이미지 업데이트, 새로운 기능 및 최적화 도입, 신속한 보안 취약점 수정, Bug 수정 등을 포함하여 TencentOS Server의 각 주요 버전에 대해 5년 이상의 점검 및 업데이트를 제공합니다. yum을 통해 기존 저장 콘텐츠 서버를 업그레이드하여 신속하게 취약점 수정을 완료할 수 있습니다.
TencentOS Server에 대한 자세한 정보가 필요한 경우 미니프로그램을 통해 Tencent Cloud Assistant에 문의할 수 있습니다.

