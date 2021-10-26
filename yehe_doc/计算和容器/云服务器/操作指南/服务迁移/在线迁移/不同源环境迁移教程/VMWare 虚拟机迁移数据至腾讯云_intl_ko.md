## 1. 마이그레이션 툴 다운로드  
 - 마이그레이션 툴 압축 패키지 [클릭하여 가져오기](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)

## 2. 인터넷 환경에 따라 마이그레이션 시나리오 확정
소스 서버와 타깃 CVM의 네트워크 환경에 따라 적합한 이전 모델을 결정하십시오.
현재 마이그레이션 툴은 기본 모드와 내부 네트워크 마이그레이션 모드를 지원합니다. 내부 마이그레이션 모드는 3가지 시나리오로 나뉘며, 마이그레이션 모드/시나리오에 따라 소스 서버와 타깃 CMV에 대한 네트워크 요구 조건이 다릅니다. 소스 서버와 타깃 CVM이 모두 공용 네트워크로 액세스할 수 있는 경우 직접 기본 모드를 사용해 마이그레이션할 수 있으며, 소스 서버와 타깃 CVM 중 하나라도 공용 네트워크로 직접 액세스할 수 없는 경우 먼저 [VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/document/product/216) 등의 방법으로 연결 터널을 구축한 후 내부 네트워크 모드로 마이그레이션합니다.

## 3. 데이터 백업
- 소스 서버: 클론 또는 기타 방법으로 가상 머신 데이터를 백업할 수 있습니다.
- 타깃 CVM：[스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 데이터를 백업할 수 있습니다.

## 4. 마이그레이션 전 점검

마이그레이션 전, 소스 서버 및 타깃 CVM에 별도의 점검이 필요합니다. 소스 서버 및 타깃 CVM에 점검이 필요한 내용은 다음과 같습니다.
<table>
	<tr><th style="width: 15%;">타깃 CVM</th><td><ol  style="margin: 0;"><li>스토리지 용량: 소스 데이터를 불러오기에 충분한 타깃 CVM CBS(시스템 디스크, 데이터 디스크 포함) 스토리지 용량을 확보해야 합니다.</li><li>보안 그룹: 보안 그룹에 443 포트 및 80 포트는 제한할 수 없습니다.</li><li>대역폭 설정: 마이그레이션 속도 향상을 위해, 대역폭의 범위를 가능한 크게 조정하기를 권장합니다. 마이그레이션 과정에서 데이터 용량과 거의 동일한 트래픽이 소모되므로, 필요할 경우 네트워크 과금 방식을 먼저 변경해 주시기 바랍니다.</li><li>타깃 CVM 및 소스 서버의 운영 체제 유형 일치 여부: 운영 체제 불일치 시, 후속 제작 이미지의 정보가 실제 운영 체제와 부합하지 않게 되므로, 타깃 CVM과 소스 서버의 운영 체제 유형을 통일해 주시기 바랍니다. 예를 들어, CentOS 7 시스템의 소스 서버 마이그레이션 시 타깃 CVM도 CentOS 7 시스템이어야 합니다.</li></ol></td></tr>
	<tr><th>Linux 소스 서버</th><td><ol  style="margin: 0;"><li> Virtio 점검 및 설치. 자세한 작업 방식은 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 Virtio 드라이버 점검</a>을 참고하십시오.</li><li>rsync가 설치되어 있는지 확인합니다.</li><li>SELinux가 열려있는지 확인합니다. 만약 SELinux가 열려있다면, SELinux를 종료하시기 바랍니다.</li><li>Tencent Cloud API에 마이그레이션 요청을 보내면, 클라우드 API가 현재 UNIX 시간을 사용하여 생성된 Token을 점검합니다. 현재 시스템 시간이 정확한지 확인하시기 바랍니다.</li><li> 소스 서버에 DHCP 서비스가 활성화되어있는지 확인하시기 바랍니다. DHCP 서비스가 활성화 상태가 아니라면 DHCP 서비스를 활성화하십시오.</li></ol></td></tr>
</table>

>? 
> - 소스 서버는 `sudo ./go2tencentcloud_x64 --check`와 같은 툴 명령어를 사용하여 자동으로 점검할 수 있습니다.
> - go2tencentcloud 마이그레이션 툴은 실행 시작 시 자동 점검하도록 기본 설정되어 있습니다. 점검 과정을 건너뛰고 강제 마이그레이션 하려는 경우, client.json 파일의 `Client.Extra.IgnoreCheck` 필드를 `true`로 설정하시기 바랍니다.
> -  go2tencentcloud 마이그레이션 툴 세부 정보는 [마이그레이션 툴 설명](https://intl.cloud.tencent.com/document/product/213/35640)을 참고하십시오.


## 5. 마이그레이션 시작

1. 소스 서버와 타깃 CVM의 연결 터널을 구축합니다. (선택사항)  
 - 내부 네트워크 마이그레이션 모드를 선택하는 경우 [VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003) 또는 [Direct Connect](https://intl.cloud.tencent.com/document/product/216) 등의 방법으로 소스 서버와 타깃 CVM 간의 연결 터널을 구축해야 합니다.
 - 기본 모드를 선택하는 경우 이 단계를 건너뛰십시오.
2. user.json 파일을 설정합니다.
user.json은 소스 서버와 타깃 CVM을 설정하는 파일로, 설정 항목은 다음과 같습니다.
 - 계정 API 호출 키 SecretId와 SecretKey. 자세한 정보는 [액세스 키](https://intl.cloud.tencent.com/document/product/598/32675)를 참고하십시오.
 - 타깃 CVM 소재 리전. CVM 리전 관련 내용은 [리전 및 가용존](https://intl.cloud.tencent.com/document/product/213/6091)을 참고하십시오.
 - 타깃 CVM 인스턴스 ID. [인스턴스 리스트](https://console.cloud.tencent.com/cvm/instance/index?rid=1) 페이지에서 확인할 수 있습니다.
 - 소스 서버 데이터 디스크 설정(선택사항)  
3. client.json 파일을 설정합니다.
client.json은 마이그레이션 모드와 기타 마이그레이션 설정 항목을 설정하는 파일입니다. 어떤 마이그레이션 시나리오를 선택하든 client.json의 `Client.Net.Mode` 항목에 상응하는 매개변수 값을 설정해야 합니다.
4. 소스 서버에서 마이그레이션하지 않을 파일과 디렉터리를 제외합니다. (선택사항)  
 Linux 소스 서버에서 rsync\_excludes\_linux.txt 파일을 편집하여 마이그레이션하지 않을 파일과 디렉터리를 제외합니다.
5. 툴을 실행합니다.
예를 들어, 64비트 Linux 소스 서버에서는 root 권한으로 다음 명령어를 실행하여 툴을 실행합니다.
```
sudo ./go2tencentcloud_x64
```
툴을 실행한 후, 마이그레이션 과정이 완료될 때까지 기다려 주시기 바랍니다.
마이그레이션 성공 시 콘솔에 출력되는 내용은 다음과 같습니다.
 ![](https://main.qcloudimg.com/raw/146fb9e1bbccb594e128648c4a723a6c.png)
