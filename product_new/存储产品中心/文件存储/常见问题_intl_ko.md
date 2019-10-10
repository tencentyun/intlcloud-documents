### CFS는 어떤 플랫폼을 지원하나요?
Linux, Unix, Windows 등 클라이언트를 지원합니다.

### CFS는 어떻게 비용을 받나요?
저장 비용만 받습니다. 실제 저장량에 따라 요금이 계산되며 시간별 저장량 키크값에 따라 비용을 받습니다.

### CFS는 어떤 접근 프로토콜을 지원하나요?
NFS v3.0/v4.0 및 CIFS/SMB 프로토콜을 지원하며 그 중 CIFS/SMB 프로토콜은 공개 테스트 중이며 신청을 제출하여 체험할 수 있습니다.

그 중 Windows 및 Linux 3.10(예 CentOS 6.\* ) 초기 버전 커널의 운영체제 클라이언트는 NFS 4.0 프로토콜을 호환하지 않아 탑재 후에는 정상적으로 사용할 수 없습니다. 이런 유형의 클라이언트는 NFS 3.0을 사용하여 탑재하십시오.

프로토콜 호환 문제로 인해 Docker 또는 Kubernetes 등 클라이언트를 사용하여 CFS를 탑재할 경우 NFS v3 프로토콜 사용을 권장합니다. NFS v4 프로토콜을 사용하면 일부 클라이언트를 정상 탑재할 수 없는 문제가 발생할 수 있기 때문입니다. 

### CFS 관련 용어 정의는 무엇인가요?
파일 시스템: 파일 시스템은 CFS 인스턴스입니다. 파일 시스템을 CVM에 탑재하면 로컬 파일 시스템처럼 CFS를 사용할 수 있습니다. 디렉터리로 탑재를 지원합니다.

탑재 지점: 탑재 지점은 컴퓨팅 노드가 CFS에 접근하는 입구로 네트워크 컴퓨팅 노드의 유형 및 CFS에 접근 권한을 정의합니다.

### 사용자는 몇 개의 파일 시스템을 생성할 수 있나요?
단일 사용자의 지역별 한도는 10개이며 특별한 상황에서 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 용량 확장을 신청할 수 있습니다.

### 탑재 지점은 탑재할 수 없으면 어떻게 처리해야 하나요?
아래 방법으로 검사하십시오.
- 오류 정보를 확인합니다.
- nfs-utils, nfs-common, cifs-utils 등 설치되었는지를 검사합니다.
- 로컬 탑재 디렉터리가 존재하는지 확인합니다
- 탑재 지점 소재 VPC 네트워크가 클라이언트 CVM 소재 VPC 네트워크와 일치한지 여부, 지역이 동일한지 여부를 확인합니다.
- CFS 클라이언트 소재의 VM 호스트에 외부 포트에 대한 접근을 금지하는 보안 그룹 전략이 설정되었는지 확인합니다. 구체적인 포트는 [파일 시스템 포트 문제](https://cloud.tencent.com/document/product/582/9551#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E7.AB.AF.E5.8F.A3.E9.97.AE.E9.A2.98)를 참조하십시오.

### CFS는 기록할 수 없습니다. 어떻게 처리하나요?
아래 방법으로 검사하십시오.
- 오류 정보를 확인합니다.
- 클라이언트 소재의 VM 호스트 네트워크 정상 여부, telnet 탑재 지점 포트 연결 여부를 확인합니다. 구체적인 포트는 [파일 시스템 포트 문제](https://cloud.tencent.com/document/product/582/9551#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E7.AB.AF.E5.8F.A3.E9.97.AE.E9.A2.98)를 참조하십시오. 
- 탑재한 것이 탑재 지점의 루트 디렉터리가 아닌 경우, 해당 탑재 지점 루트 디렉터리 존재 여부를 확인하십시오. 여기에서 오류 정보 "Stale file handle"이 자주 표시되며 이미 루트 디렉터리로 탑재한 설비를 통해 해당 서브 디렉터리 존재 여부를 확인할 수 있습니다.

### 파일 시스템 포트 문제

파일 시스템 프로토콜 | 개방 포트 | 네트워크 연결성 확인
------- | ------- | ---------
NFS 3.0 | 111, 892, 2049 |  telnet 파일 시스템 IP 2049
NFS 4.0 | 2049 |  telnet 파일 시스템 IP 2049
CIFS/SMB | 445 |  telnet 파일 시스템 IP 445 

> **주의:**
> CFS는 ping을 지원하지 않습니다.

### 권한 적용 문제
NFS 프로토콜의 파일 시스템은 여러 규칙 구성을 지원하며 우선 순위에 따라 적용됩니다.
- 동일 권한 그룹 내 단일 IP가 IP 주소 범위에 포함된 IP의 권한과 충돌할 경우, 우선 순위가 높은 규칙을 적용합니다. 우선 순위가 같을 경우 우선 단일 IP 권한을 적용합니다.

- 겹친 부분이 있는 두개의 IP 주소 범위는 다른 권한을 가지지만 우선 순위는 같을 경우, 겹친 주소 범위의 권한은 랜덤으로 적용되므로 겹친 IP 주소 범위 구성을 최대한 피하십시오. 

> **주의:**
CIFS/SMB 파일 시스템은 우선 순위 구성을 지원하지 않으며 구성 후에도 적용되지 않습니다.

### CFS에 로컬 파일 복사 속도를 어떻게 높이나요?
Linux는 다음 shell 스크립트를 사용하여 로컬 파일을 CFS에 빠르게 복사할 수 잇습니다. 다음 코드 중 '스레드 수량'은 필요에 따라 조정할 수 있습니다.
```
threads=<스레드 수량>; src=<오리진 경로/>; dest=<대상 경로/>; rsync -av -f"+ */" -f"- *" $src $dest && (cd $src && find . -type f | xargs -n1 -P$threads -I% rsync -av % $dest/% )

<!--예, threads=24; src=/root/github/swift/; dest=/nfs/; rsync -av -f"+ */" -f"- *" $src $dest && (cd $src && find . -type f | xargs -n1 -P$threads -I% rsync -av % $dest/% )-->
```

### Windows에서 파일 이름/디렉터리 이름 오류를 어떻게 수정하나요?
프로토콜에 대한 클라이언트의 지원으로 인해 Windows 클라이언트는 NFS 프로토콜을 사용하여 파일 시스템을 탑재하면 파일 또는 디렉터리 이름을 바꿀 수 없는 상황이 발생할 수 있습니다. 이런 상황에서 Windows 사용자는 CIFS/SMB 프로토콜을 사용하여 CFS 파일 시스템을 탑재하길 권장합니다.


### nfs를 사용하여 탑재하면 Windows에 쓰기 권한이 없는데 어떻게 처리해야 하나요?
작업 가이드를 엄격히 준수하여 레지스트리에 AnonymousUid와 AnonymousGid를 추가하고 시스템을 다시 시작한 뒤 다시 시도하십시오.
문서: [파일 시스템 탑재-Windows에서 파일 시스템 사용](https://cloud.tencent.com/document/product/582/9133#.E5.9C.A8-windows-.E4.B8.8A.E4.BD.BF.E7.94.A8.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)

### Windows IIS는 mapped driver를 사용할 수 없는데 어떻게 해야 하나요?
[파일 시스템 탑재-Windows에서 파일 시스템 사용](https://cloud.tencent.com/document/product/582/9133#.E5.9C.A8-windows-.E4.B8.8A.E4.BD.BF.E7.94.A8.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)의 절차에 따라 정확한 NFS 클라이언트 프로그램을 구성하고 레지스트리(접근 사용자 추가)를 수정합니다.
클라이언트를 다시 시작하고 IIS 구성 페이지를 열어 사이트를 추가하고 [고급 설정]을 클릭합니다.
![](https://mc.qcloudimg.com/static/img/bdd15aa1ca694653b5595442cbc38737/IIS.png)
고급 설정에서 '물리 경로'를 CFS 탑재 지점으로 설정합니다.
![](https://main.qcloudimg.com/raw/54375f5bab346a95785bd26575a86fea.png)

### Docker 또는 Kubernetes 탑재 부분 성공, 부분 실패 문제

프로토콜 호환 문제로 인해 Docker 또는 Kubernetes 등 클라이언트를 사용하여 CFS를 탑재할 경우 NFS v3 프로토콜 사용을 권장합니다. NFS v4 프로토콜을 사용하면 일부 클라이언트를 정상 탑재할 수 없는 문제가 발생할 수 있기 때문입니다.


### 어느 가용 영역에서 CFS 리소스가 이미 매진되었으면 어떻게 계속 사용하나요?
광저우를 예로 들면, 광저우 1지역의 CVM이 있는데 이때 CFS를 사용해야 하지만 광저우 1지역은 리소스가 매진되어 파일 시스템을 바로 생성할 수 없습니다.
**VPC 네트워크에서**
CVM이 VPC의 '광저우 1지역 서브넷'에 있으면 [VPC 콘솔](https://console.cloud.tencent.com/vpc)에 로그인하여 해당 VPC를 위해 가용 영역이 '광저우 2지역'인 서브넷을 생성합니다.
![](https://main.qcloudimg.com/raw/d25fc9283b76f114a772bebb1b703548.png)
![](https://main.qcloudimg.com/raw/5c0bb3dc41a7759bacf0c096dee4b413.png)

서브넷 생성 완료 후 CFS 콘솔로 돌아와 광저우 2지역의 리소스를 생성할 때 해당 VPC 및 방금 생성한 서브넷을 선택합니다. 이때 기존에 해당 VPC 광저우 1지역 서브넷의 CVM은 CFS 파일 시스템에 바로 탑재됩니다.
파일 시스템 사용 가이드:
- [Linux](https://cloud.tencent.com/document/product/582/11523)
- [Windows](https://cloud.tencent.com/document/product/582/11524)

**기본 네트워크에서** 
CVM이 기본 네트워크에 있는 경우, VPC 및 광저우 2지역 서브넷을 생성하고 해당 네트워크에서 파일 시스템을 생성합니다. '기본 네트워크 상호 연결' 방법을 통해 CVM 소재의 기본 네트워크 및 해당 VPC를 연결시키면 접근을 실현시킬 수 있습니다. [기본 네트워크 상호 연결 도움말>>](https://cloud.tencent.com/document/product/215/5002)

### 파일 내용 업데이트 비동기화는 어떻게 해결하나요?
#### 문제 설명
두 대의 Linux CVM에 동일한 NFS 파일 시스템을 탑재하고 CVM A에서 append 방식을 사용하여 파일을 기록하고 CVM B에서 `tail -f`를 사용하여 파일 내용 변화를 관찰합니다. CVM A에 기록을 완료하면 10 ~ 30초 대기 시간이 지나야 CVM B에서 업데이트 후 내용을 볼 수 있습니다. 단, 동일한 상황에서 CVM B에서 바로 파일(예: vi 명령 사용)을 열면 업데이트 내용을 바로 볼 수 있습니다.

#### 문제 발생 원인
NFS 프로토콜 mount 명령의 옵션 및 `tail -f` 실현과 관련이 있습니다. 탐재 명령:   
```
sudo mount -t nfs -o vers=4 <탑재 지점 IP>:/ <탑재 예정 대상 디렉터리>
```
 
CVM B가 NFS mount 명령으로 파일 시스템을 탑재하면 기본적으로 kernel이 파일과 디렉터리 속성의 metadata 캐시를 유지합니다. 파일과 디렉터리 속성은 허가권, 크기와 타임스탬프 등을 포함하며 캐시는 NFSPROC_GETATTR 원격 절차 호출(RPC) 횟수를 줄이는 데 목적이 있습니다.

`tail -f`는 sleep+fstat를 통해 파일 속성(주로 파일 크기) 변화를 관찰한 뒤 파일에 기록하여 출력해 실현합니다. 그렇기 때문에 fstat 결과는 `tail -f`가 실시간으로 파일 내용을 출력할 수 있는지 여부를 결정합니다. 하지만 파일 및 디렉터리의 metadata 캐시 존재 때문에 fstat이 폴링한 것은 실시간 파일 속성이 아닙니다. 그러므로 NFS 서버 파일은 업데이트되었어도 `tail -f`는 파일에 어떤 변화가 일어났는지 알지 못해 출력 지연이 발생하는 것입니다.

#### 해결 방법
mount 명령을 사용하여 파일 시스템을 탑재할 때 noac 옵션을 추가하면 파일과 디렉터리 속성의 캐시를 사용금지할 수 있습니다. 탑재 명령은 다음과 같습니다.
```
sudo mount -t nfs -o vers=4 noac <탑재 지점 IP>:/ <탑재 예정 대상 디렉터리>
sudo mount -t nfs -o vers=3 noac,nolock,proto=tcp <탑재점 IP>:/<FSID 또는 서브 디렉터리> <탑재 예정 대상 디렉터리>
```

### Windows 7-based 또는 Windows Server 2008 R2-based 운영체제는 NFS 프로토콜을 사용하여 탑재했을 때 오류 보고(0x800704C9)

#### 문제의 원인
이 버전의 장치는 NFS 초기 포트 주소를 캐시하여 이전 주소를 통해 nlockmgr과 통신하였기 때문입니다. 상세한 원인은 [Microsoft 도움말](https://support.microsoft.com/en-us/help/2761774/0x800704c9-error-when-you-copy-files-to-an-nfs-server-from-a-windows-7)을 참조하십시오.

#### 해결 방법
Windows의 자동 업데이트 기능을 활성화하여 시스템을 공식 최신 버전으로 업그레이드하면 해당 문제를 해결할 수 있습니다.

