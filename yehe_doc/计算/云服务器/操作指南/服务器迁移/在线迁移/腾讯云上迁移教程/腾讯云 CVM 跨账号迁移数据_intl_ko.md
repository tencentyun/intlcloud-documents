온라인 마이그레이션 툴은 Tencent Cloud CVM 계정 간 데이터 마이그레이션을 지원합니다. 계정 간 데이터 마이그레이션이란 서로 다른 계정의 CVM 간 데이터 마이그레이션을 의미합니다.

## 1. 마이그레이션 툴 다운로드  
 마이그레이션 툴 압축 패키지를 [다운로드](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip)합니다.

## 2. 네트워크 환경에 따라 마이그레이션 시나리오 확정
소스 CVM과 타깃 CVM의 네트워크 환경에 따라 적합한 마이그레이션 모드를 확정합니다.
현재 마이그레이션 툴은 기본 모드와 내부 네트워크 마이그레이션 모드를 지원합니다. 내부 마이그레이션 모드는 3가지 시나리오로 나뉘며, 마이그레이션 모드/시나리오에 따라 소스 CVM과 타깃 CMV의 요구가 달라집니다. 소스 CVM과 타깃 CVM이 모두 공용 네트워크로 액세스할 수 있는 경우 직접 기본 모드를 사용해 마이그레이션할 수 있으며, 소스 CVM과 타깃 CVM 중 하나라도 공용 네트워크로 직접 액세스할 수 없는 경우 먼저 [VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network(CCN)](https://intl.cloud.tencent.com/document/product/1003) 또는 [Direct Connect(DC)](https://intl.cloud.tencent.com/document/product/216) 등의 방법으로 터널을 연결한 후 내부 네트워크 모드로 마이그레이션합니다.

## 3. 데이터 백업
[스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 등의 방식을 선택해 데이터를 백업할 수 있습니다.

## 4. 마이그레이션 전 점검
마이그레이션을 하기 전에 소스 CVM 및 타깃 CVM에 별도의 점검이 필요합니다. 소스 CVM 및 타깃 CVM에 필요한 점검 내용은 다음과 같습니다.
<table>
	<tr><th style="width: 15%;">타깃 CVM</th><td><ol  style="margin: 0;"><li>스토리지 용량: 소스 데이터를 불러오기에 충분하도록 타깃 CVM의 CBS(시스템 디스크, 데이터 디스크 포함) 스토리지 용량을 확보해야 합니다.</li><li>보안 그룹: 보안 그룹에 443 포트 및 80 포트는 제한할 수 없습니다.</li><li>대역폭 설정: 마이그레이션 속도 향상을 위해, 대역폭의 범위를 가능한 크게 조정하기를 권장합니다. 마이그레이션 과정에서 데이터양과 거의 동일한 트래픽이 소모되므로, 필요할 경우 네트워크 과금 방식을 먼저 변경해 주시기 바랍니다.</li><li>타깃 CVM 및 소스 CVM의 운영 체제 유형 일치 여부: 운영 체제가 다를 경우, 이후에 생성한 이미지의 정보가 실제 운영 체제와 부합하지 않게 되므로, 타깃 CVM과 소스 CVM의 운영 체제 유형을 통일해 주시기 바랍니다. 예를 들어, CentOS 7 시스템의 소스 CVM 마이그레이션 시 타깃 CVM도 CentOS 7 시스템이어야 합니다.</li></ol></td></tr>
	<tr><th>Linux 소스 CVM</th><td><ol  style="margin: 0;"><li>Virtio를 점검 및 설치합니다. 자세한 작업 방식은 <a href="https://intl.cloud.tencent.com/document/product/213/9929">Linux 시스템 Virtio 드라이버 점검</a>을 참조하십시오.</li><li><code>which rsync</code> 명령어를 실행하여 rsync의 설치 여부를 확인합니다. </li><li>SELinux가 열려 있는지 확인합니다. 만약 SELinux가 열려 있다면, SELinux를 종료하시기 바랍니다.</li><li>Tencent Cloud API에 마이그레이션 요청을 보내면, 클라우드 API가 현재 UNIX 시간을 사용하여 생성된 Token을 점검하므로, 시스템 시간이 정확한지 확인하시기 바랍니다.</li></ol></td></tr>
</table>

>? 
> - 소스 CVM은 `sudo ./go2tencentcloud_x64 --check`와 같은 툴 명령어를 사용하여 자동으로 점검할 수 있습니다.
> - go2tencentcloud 마이그레이션 툴은 실행 시작 시 자동 점검하도록 기본 설정되어 있습니다. 점검 과정을 건너뛰고 강제 마이그레이션하려면 client.json 파일의 `Client.Extra.IgnoreCheck` 필드를 `true`로 설정하십시오.
> - go2tencentcloud 마이그레이션 툴에 대한 자세한 내용은 [마이그레이션 툴 설명](https://intl.cloud.tencent.com/document/product/213/35640)을 참조하십시오.

## 5. 마이그레이션 시작

1. 소스 CVM과 타깃 CVM의 연결 터널을 생성합니다. (선택사항) 
 - 내부 네트워크 마이그레이션 모드를 선택하는 경우 [VPC 피어링 연결](https://intl.cloud.tencent.com/document/product/553), [VPN 연결](https://intl.cloud.tencent.com/document/product/1037), [Cloud Connect Network(CCN)](https://intl.cloud.tencent.com/document/product/1003) 또는 [Direct Connect(DC)](https://intl.cloud.tencent.com/document/product/216) 등의 방법으로 소스 CVM과 타깃 CVM 간의 터널을 생성해야 합니다.
 - 기본 모드를 선택하는 경우 해당 절차는 생략합니다.
2. user.json 파일을 설정합니다.
user.json은 소스 CVM과 타깃 CVM의 설정 파일로, 설정 항목은 다음과 같습니다.
 - 계정 API 호출 키 SecretId와 SecretKey. 자세한 정보는 [호출 키](https://intl.cloud.tencent.com/document/product/598/32675)를 참조하십시오.
 - 타깃 CVM 소재 리전. CVM은 리전을 지원하며 자세한 내용은 [리전과 가용존](https://intl.cloud.tencent.com/document/product/213/6091)을 참조하십시오.
 - 타깃 CVM 인스턴스 ID. [인스턴스 리스트](https://console.cloud.tencent.com/cvm/instance/index?rid=1) 페이지에서 확인할 수 있습니다.
 - 소스 CVM의 데이터 디스크 설정(선택사항)  
3. client.json 파일을 설정합니다.
client.json은 마이그레이션 시나리오와 기타 마이그레이션 설정 항목을 설정하는 파일입니다. 어떤 마이그레이션 모드/시나리오를 선택하든 client.json의 `Client.Net.Mode` 항목에 상응하는 매개변수 값을 설정해야 합니다.
4. 소스 CVM에서 마이그레이션하지 않을 파일과 디렉터리를 제외합니다. (선택사항)  
 Linux 소스 CVM에서 rsync\_excludes\_linux.txt 파일을 편집하여 마이그레이션하지 않을 파일과 디렉터리를 제외합니다.
5. 툴을 실행합니다.
[내부 네트워크 마이그레이션 모드: 시나리오1](https://intl.cloud.tencent.com/document/product/213/35640#Scenario1)로 계정 간 마이그레이션하는 경우 예시:  
 1. 공용 네트워크에 액세스할 수 있는 CVM에서 다음 명령어로 툴을 실행하여, 1단계 마이그레이션을 진행합니다.
```
sudo ./go2tencentcloud_x64
```
`Stage 1 is finished and please run next stage at source machine.`이라는 문구가 출력되면, 1단계 마이그레이션이 완료되었다는 의미입니다. 
 ![](https://main.qcloudimg.com/raw/afeceabbdaad10f348cd0805b209e5cb.png)
 2. 위의 단계(1단계)가 완료되면, 1단계의 모든 툴 목록을 마이그레이션할 소스 CVM에 복사한 뒤, 다시 툴을 실행하여 2단계 마이그레이션을 진행합니다.
 예를 들어, 다음 명령어로 툴을 실행하여 2단계 마이그레이션을 진행합니다.
```
sudo ./go2tencentcloud_x64
```
`Stage 2 is finished and please run next stage at gateway machine.`이라는 문구가 출력되면, 2단계 마이그레이션이 완료되었다는 의미입니다.
 ![](https://main.qcloudimg.com/raw/be35753f3f8f3a30b8d6364a1052991f.png)
 3. 위의 단계(2단계)가 완료되면, 2단계의 모든 툴 목록을 1단계 소스 CVM에 복사한 뒤, 다시 툴을 실행하여 3단계 마이그레이션을 진행합니다.
 예를 들어, 다음 명령어로 툴을 실행하여 3단계 마이그레이션을 진행합니다.
```
sudo ./go2tencentcloud_x64
```
`Migrate successfully.`라는 문구가 출력되면, 모든 마이그레이션 작업이 완료되었다는 의미입니다.
 ![](https://main.qcloudimg.com/raw/1cf4ef72cebab8b42440608643cedade.png)

 
