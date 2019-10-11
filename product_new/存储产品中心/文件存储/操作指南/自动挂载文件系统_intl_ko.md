
클라이언트 다시 시작 시에도 CFS 파일 시스템 자동 탑재를 실현하려면 파일 시스템을 탑재한 Linux 클라이언트 또는 Windows 클라이언트에서 구성할 수 있습니다.

## Linux에서 NFS 파일 시스템 자동 탑재
1. 우선 CVM 콘솔로 로그인 또는 원격 로그인을 통해 자동 탑재할 파일 시스템의 CVM 인스턴스에 연결합니다. "/etc/fstab" 파일을 엽니다. 로그인한 계정에 root 권한이 있는지 확인하십시오.
```
//아래 명령을 사용하여 fstab 파일 열기
vi /etc/fstab
```

2. "fstab" 파일을 연 뒤 "i"(insert)를 입력하고 /Etc/fstab에 다음 명령행을 추가합니다. 다음 몇 가지 탐재 방식이 있습니다.
```
NFS4.0을 통한 탑재
<탑재 지점 IP>:/ <탑재 예정 대상 디렉터리> nfs4 nfsvers=4,hard,timeo=600,retrans=2,_netdev 0 0
예:10.10.19.12:/ /local/test nfs4 nfsvers=4,hard,timeo=600,retrans=2,_netdev 0 0
```
```
NFS3.0을 통한 탑재
<탑재 지점 IP>:/<fsid> <탑재 예정 대상 디렉터리> nfs nfsvers=3,hard,timeo=600,retrans=2,_netdev 0 0
예:10.10.19.12:/djoajeo4 /local/test nfs nfsvers=3,hard,timeo=600,retrans=2,_netdev 0 0
```
3. 키보드의 "Esc"를 누르고 "：wq"를 입력해 위의 수정을 저장합니다. 클라이언트를 다시 시작하면 파일 시스템이 자동 탑재가 됩니다.

> **주의:**
> 자동 탑재 명령을 추가하였는데 공유 파일 시스템 상태가 이상하면 Linux 시스템을 정상 시작하지 못할 수 있습니다. Linux 시스템은 fstab의 자동 시작 명령을 성공적으로 실행해야 정상 시작할 수 있기 때문입니다. 이때 시스템 시작 시 ‘단일 사용자 모드’에 들어가 fstab의 자동 탑재 명령을 삭제한 후 CVM을 다시 시작하면 됩니다.


## Windows에서 파일 시스템 자동 탑재
탑재 시, 다음 그림과 같이 "로그인 시 다시 연결" 옵션을 선택합니다. 탑재 관련 더 많은 도움말은 [CFS 파일 시스템 사용(Windows)](https://cloud.tencent.com/document/product/582/11524)을 참조하십시오.
![](https://mc.qcloudimg.com/static/img/4bec827c8212a335b3173064184f7346/image.png)

