## 개요 정보

Batch Compute는 Cloud-init 서비스에 의존하여 CVM을 초기화해야 합니다. Batch Compute를 사용할 때 입력한 이미지는 반드시 Cloud-init을 성공적으로 설치 및 구성해야 합니다. 그렇지 않으면 작업 실행 또는 컴퓨팅 환경 내의 CVM 생성이 ``실패``할 수 있습니다.

(Cloud-init은 CVM 최초 초기화 시 사용자 지정 구성에 대한 능력을 제공합니다)

Cloud-init에 대한 설치와 구성은 아래 가이드를 따르십시오.
* Linux ``생성``CVM/사용자 지정 이미지: 현재 Tencent Cloud CentOS, Ubuntu 모든 버전 공유 이미지는 기본적으로 Cloud-init을 지원합니다. 이러한 공유 이미지로 CVM과 사용자 지정 이미지를 생성할 때 Cloud-init을 수동으로 설치 및 구성할 필요가 없습니다.
* Linux ``저장``CVM/사용자 지정 이미지: 이전에 생성한 CVM 또는 사용자 지정 이미지의 경우 Cloud-init을 수동으로 설치해야 합니다. [Linux Cloud-init 수동 설치>>>](https://intl.cloud.tencent.com/document/product/213/12587)를 참조하십시오.

Cloud-init을 포함한 자주 사용되는 운영 체제 이미지 ID는 다음과 같습니다.
* img-31tjrtph(CentOS 7.2 64비트)
* img-pyqx34y1(Ubuntu Server 16.04.1 LTS 64비트)









