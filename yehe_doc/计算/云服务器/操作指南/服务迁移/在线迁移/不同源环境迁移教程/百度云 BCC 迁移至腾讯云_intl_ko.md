## 1. 마이그레이션 툴 획득  
 마이그레이션 툴 압축 패키지는 [획득](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)할 수 있습니다.

## 2. 네트워크 환경에 따라 마이그레이션 방식 확인
사용자의 오리진 호스트와 타깃 CVM의 네트워크 환경에 맞는 마이그레이션 방식을 확인하세요.
현재 마이그레이션 툴은 기본 모드와 내부 네트워크 마이그레이션 모드를 지원하며, 그중 내부 네트워크 마이그레이션은 3가지 시나리오로 세분화됩니다. 각 마이그레이션 모드/시나리오가 요구하는 오리진 호스트와 타깃 CVM의 네트워크 수요가 다릅니다. 오리진 호스트와 타깃 CVM이 모두 공용 네트워크에 액세스할 수 있다면 직접 기본 모드로 마이그레이션 할 수 있습니다. 오리진 호스트와 타깃 CVM 중 하나가 공용 네트워크에 직접 액세스할 수 없으면, 우선 [VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/215/5000)， [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [CCN](https://intl.cloud.tencent.com/document/product/1003) 또는 [DC](https://intl.cloud.tencent.com/document/product/216) 등 방식을 통해 연결 터널을 구축한 후 내부 네트워크 모드로 마이그레이션 할 수 있습니다.

## 3. 데이터 백업
스냅샷 생성 등 방식을 선택해 데이터를 백업할 수 있습니다.

## 4. 마이그레이션 전 점검
마이그레이션 하기 전 오리진 호스트와 타깃 CVM을 각각 점검해야 합니다. 오리진 호스트와 타깃 CVM에서 점검해야 하는 내용은 아래와 같습니다.
<table>
	<tr><th style="width: 15%;">타깃 CVM</th><td><ol  style="margin: 0;"><li>스토리지 용량: 오리진 데이터 로딩을 위해 타깃 CVM의 CBS(시스템 디스크와 데이터 디스크 포함)에 반드시 충분한 스토리지 용량을 구비해야 합니다.</li><li>보안 그룹: 보안 그룹 중에 443 포트와 80 포트를 차단하면 안 됩니다.</li><li>대역폭 설정: 더 빠르게 마이그레이션 할 수 있도록 양쪽의 대역폭을 가능한 최대로 조정할 것을 권장합니다. 마이그레이션 과정에서 데이터양과 대략 같은 트래픽 소모가 발생하기 때문에 필요한 경우 미리 네트워크 과금 방식을 조정하시기 바랍니다.</li><li>타깃 CVM과 오리진 호스트의 운영 체제 유형의 일치 여부: 운영 체제가 다를 경우 후속 작업에서 미러 이미지의 정보가 실제 운영 체제와 다를 수 있기 때문에, 타깃 CVM의 운영 체제가 최대한 오리진 호스트의 운영 체제 유형과 일치할 것을 권장합니다. 예시, CentOS 7 시스템의 오리진 호스트 마이그레이션 시 CentOS 7 시스템의 CVM 1대를 마이그레이션 타깃으로 선택합니다.
	<tr><th>Linux 오리진 호스트</th><td><ol  style="margin: 0;"><li>Virtio를 점검 및 설치하며, 자세한 작업은 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 Virtio 드라이브 점검</a>을 참조할 수 있습니다.</li><li>rsync 와 grub2-install(또는 grub-install)의 설치 여부를 점검합니다.</li><li>SELinux의 활성화 여부를 점검합니다. SELinux가 활성화되어 있으면 SELinux를 비활성화하세요.</li><li>Tencent Cloud API에 마이그레이션 요청을 보낸 후, 클라우드 API가 현재 UNIX 시간을 사용해 생성된 Token을 점검하므로 현재 시스템 시간에 오류가 없도록 확인 바랍니다.</</li></ol></td></tr>
</table>

> 
> - 오리진 호스트 점검은 툴 명령어로 자동 점검 가능합니다. 예: `sudo ./go2tencentcloud_x64 --check`.
> - go2tencentcloud 마이그레이션 툴은 실행을 시작할 때 자동 점검을 기본으로 진행합니다. 점검을 생략하고 강제로 마이그레이션 해야 할 경우 client.json 파일에서 `Client.Extra.IgnoreCheck`필드를 `true`로 설정하세요.
> 

## 5. 마이그레이션 시작
 
1. 오리진 호스트와 타깃 CVM의 연결 터널을 구축합니다(선택).  
 - 내부 네트워크 마이그레이션 모드를 선택할 경우, [VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/215/5000), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [CCN](https://intl.cloud.tencent.com/document/product/1003) 또는 [DC](https://intl.cloud.tencent.com/document/product/216) 등의 방식을 통해 오리진 호스트와 타깃 CVM 간의 연결 터널을 구축해야 합니다.
 - 기본 방식을 선택할 경우, 이 단계를 건너뛰세요.
2. user.json 파일을 설정합니다.
user.json은 오리진 호스트와 타깃 CVM을 설정하는 파일입니다. 해당 파일의 설정 항목은 아래와 같습니다.
 - 사용자의 계정 API 액세스 키 SecretId와 SecretKey, 자세한 정보는 [액세스 키](https://intl.cloud.tencent.com/document/product/598/32675)를 참조 바랍니다.
 - 타깃 CVM이 위치한 리전.
 - 타깃 CVM의 인스턴스 ID.
 - 오리진 호스트의 데이터 디스크 설정(선택)  
3. client.json 파일을 설정합니다.
client.json은 마이그레이션 방식과 기타 마이그레이션 설정 항목을 설정하는 파일입니다. 어떤 마이그레이션 방식/시나리오를 선택하든 모두 client.json 안의 `Client.Net.Mode` 항목에서 상응하는 매개변수 값을 설정해야 합니다.
4. 오리진 호스트에서 마이그레이션이 필요하지 않은 파일과 디렉터리를 제거합니다(선택).  
 Linux 오리진 호스트에서 rsync\_excludes\_linux.txt 파일을 편집하여 마이그레이션이 필요하지 않은 파일과 디렉터리를 제거합니다.
5. 툴을 실행합니다.
예시, 64비트 Linux 오리진 호스트 아래에서 root 권한으로 아래 명령어를 사용해 툴을 실행합니다.
```
sudo ./go2tencentcloud_x64
```
툴을 실행한 후 마이그레이션 프로세스가 완료될 때까지 기다리세요.
일반적으로 마이그레이션에 성공한 콘솔의 출력은 다음과 같습니다.
 ![](https://main.qcloudimg.com/raw/0b53a6ecdfe9180a11d81bdb6ef6ca74.png)
