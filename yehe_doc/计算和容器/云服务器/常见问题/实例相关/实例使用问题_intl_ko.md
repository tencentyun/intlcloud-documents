### 현재 사용 중인 CVM은 어떻게 조회합니까?

[CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 뒤, CVM 페이지에서 사용 중인 CVM을 조회할 수 있습니다.

### CVM이 버츄얼 머신의 설치를 지원합니까?

CVM은 버츄얼 머신 설치를 지원하지 않습니다.

### 인스턴스는 어떻게 종료합니까?

자세한 작업 방식은 [인스턴스 종료](https://intl.cloud.tencent.com/document/product/213/4929)를 참고하십시오.

### 인스턴스는 어떻게 재시작합니까?

자세한 작업 방식은 [인스턴스 재시작](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.

### 인스턴스는 어떻게 폐기합니까?

자세한 작업 방식은 [인스턴스 폐기](https://intl.cloud.tencent.com/zh/document/product/213/4930)를 참고하십시오.

### Linux 인스턴스의 계정과 비밀번호를 어떻게 조회하나요?
CVM 인스턴스의 계정과 비밀번호는 생성 성공 후 Tencent Cloud 계정의 [내부 메시지](https://console.cloud.tencent.com/message)로 발송해드립니다. Linux 시스템의 기본 관리자 계정은 root입니다.

### Linux 인스턴스 디스크 확인 및 파티션 포맷은 어떻게 하나요?

`df –h` 명령어를 사용하여 디스크 공간 및 사용량을 조회할 수 있으며, `fdisk -l' 명령어를 사용하여 디스크 정보를 조회할 수 있습니다. Linux 인스턴스 디스크 파티션 및 포맷 작업은 [CBS 초기화(2TB 미만)](https://intl.cloud.tencent.com/document/product/362/31597) 및 [CBS 초기화(2TB 이상)](https://intl.cloud.tencent.com/document/product/362/31598)를 참고하십시오.

### Linux 인스턴스에 파일을 업로드하는 방법은 무엇인가요?
- [SCP 방식으로 파일을 Linux 인스턴스에 업로드](https://intl.cloud.tencent.com/document/product/213/2133)할 수 있습니다.
- [FTP 방식으로 파일을 Linux 인스턴스에 업로드](https://intl.cloud.tencent.com/document/product/213/35307)할 수 있습니다.

### Linux 인스턴스 디렉터리 파일의 소유자와 소유 그룹을 변경하려면 어떻게 해야 하나요?
웹서비스에서 파일 혹은 디렉터리의 권한이 정확하지 않으면 웹 사이트 액세스 시 403 오류가 발생할 수 있습니다. 따라서, 파일 및 디렉터리를 변경하기 전에 위치한 프로세스의 실행 자격 증명을 확인해야 합니다.
- `ps` 및 `grep` 명령어를 통해 파일 및 디렉터리가 위치한 프로세스의 실행 자격 증명을 조회할 수 있습니다.
- `ls –l` 명령어를 통해 파일 및 디렉터리의 소유자 및 소유 그룹을 조회할 수 있습니다.
- `chown` 명령어를 통해 권한을 수정할 수 있습니다. 예시, `chown -R www.www /tencentcloud/www/user/` `/tencentcloud/www/user` 디렉터리의 모든 파일 및 디렉터리의 소유자와 소유 그룹을 www 계정으로 변경할 수 있습니다.

### Linux 인스턴스가 시각화 인터페이스를 지원하나요?
지원합니다. Linux 인스턴스에 시각화 인터페이스를 구축하려는 경우, 자세한 내용은 [Ubuntu 시각화 인터페이스 구축](https://intl.cloud.tencent.com/document/product/213/37500)을 참고하십시오.

### CVM 인스턴스 구매 후 사운드 카드와 그래픽 카드를 추가할 수 없는 이유는 무엇인가요?
Tencent Cloud CVM에서는 일반 서버를 제공하며, 멀티미디어 서버는 제공하지 않기 때문에 사운드 카드 및 그래픽 카드 컴포넌트를 기본적으로 제공하지 않습니다. 따라서, 시스템에서 사운드 카드와 그래픽 카드를 추가할 수 없습니다.

### 클라우드 서비스 인스턴스를 구매할 때 MAC 주소를 지정할 수 있습니까?
지정할 수 없습니다. MAC 주소는 CVM 인스턴스가 생성될 때 임의로 할당되며 지정할 수 없습니다.

### 한 CVM에 남은 시간을 다른 CVM으로 이전할 수 있나요?
이전할 수 없습니다. 효율성과 비율을 고려하신다면 인스턴스 구매 시 종량제 인스턴스를 선택하시기 바랍니다.

### CVM 인스턴스에서 CVM IP 주소의 귀속 리전을 조회하려면 어떻게 해야 하나요?
구매하신 CVM 인스턴스가 위치한 리전이 곧 IP 주소의 귀속 리전입니다.

### CVM은 기본으로 데이터베이스를 제공하나요?
CVM은 기본으로 데이터베이스를 제공하지 않습니다. 다음과 같이 작업하실 수 있습니다.
- 데이터베이스를 자체 배포합니다. 예: [MySQL 데이터베이스 설치](https://intl.cloud.tencent.com/document/product/213/10190).
- [TencentDB MySQL](https://intl.cloud.tencent.com/zh/products/cdb) 서비스를 개별 구입합니다.
- 이미지 마켓을 이용하여 환경 데이터베이스를 설정합니다.

### CVM에 데이터베이스를 구축할 수 있나요?
구축할 수 있습니다. 필요에 따라 CVM의 제한을 받지 않고, 데이터베이스 소프트웨어 설치 및 환경 설정을 하실 수 있습니다. 한편, [Tencent CDB MySQL](https://intl.cloud.tencent.com/zh/products/cdb) 서비스를 개별 구매하실 수도 있습니다.

### CVM에서 Oracle 데이터베이스를 지원하나요?
지원합니다. Oracle 데이터베이스를 설치하기 전에 CVM 성능에 대해 스트레스 테스트를 진행하여 CVM 인스턴스가 귀하의 데이터베이스 읽기 및 쓰기 수요를 만족시킬 수 있는지 확인할 것을 권장합니다.

### 어떤 경우에 인스턴스를 강제 중지하나요? 중지 후에는 어떻게 되나요?
정상적인 종료 프로세스로 인스턴스를 중지하지 못할 경우에 강제 중지할 수 있습니다. 인스턴스 강제 중지는 정전 시의 처리와 같으므로, 인스턴스 운영 체제에서 디스크에 입력하지 못한 데이터를 손실할 수도 있습니다.
