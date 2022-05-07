## 작업 시나리오
CVM 운영 체제 프로세스 중 기기 grub 부팅 파일 유실, 시스템 키 파일 누락, lib 동적 라이브러리 파일 손상/누락 등의 경우 운영 체제가 단일 사용자 모드로 복구를 완료하지 못할 수 있습니다. 이 경우 CVM 복구 모드를 사용하여 시스템을 복구해야 합니다. 본 문서는 CVM 콘솔을 통해 복구 모드를 사용하는 방법에 대해 소개합니다.


## 작업 순서

### 복구 모드 시작

<dx-alert infotype="notice" title="">
복구 모드 시작 전, 오작동 등으로 인한 영향을 방지하기 위해 인스턴스 백업을 적극 권장합니다. CBS는 [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755)으로 백업할 수 있고 로컬 시스템 디스크는 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)으로 백업할 수 있습니다.
</dx-alert>

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/instance/index?rid=1)에 로그인합니다.
2. 인스턴스 관리 페이지에서 실제 뷰 모드에 따라 작업합니다.
<dx-tabs>
::: 리스트 모드
인스턴스가 위치한 행의 오른쪽에서 **더 보기** > **유지보수 및 점검** > **복구 모드 시작**을 선택합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1c550dfc43f5b136401f877a1621a84e.png)
:::
::: 탭 모드
인스턴스가 위치한 탭을 선택하고 오른쪽 상단에서 **더 많은 작업** > **유지보수 및 점검** > **복구 모드 시작**을 선택합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/633e92a792afa8d19e735db38c7e5598.png)
:::
</dx-tabs>
3. [](id:step3) ‘복구 모드 시작’ 팝업 창에서 복구 모드에서 인스턴스에 로그인하기 위한 비밀번호를 설정합니다. 아래 이미지와 같습니다.
<dx-alert infotype="notice" title="">
- 현재 복구 모드는 Linux 인스턴스만 지원되며, Windows 인스턴스는 지원되지 않습니다. Windows 인스턴스로 복구 모드를 시작하면 기본적으로 Linux 복구 모드(CentOS 7.5 64비트)로 시작됩니다.
- 복구 모드의 인스턴스 사용자 이름은 기본적으로 'root'로 설정됩니다.
- 인스턴스가 종료된 상태에만 복구 모드를 시작할 수 있으며 강제 종료 시 데이터 유실 또는 파일 시스템 손상이 발생할 수 있으므로 작업을 진행하기 전 인스턴스를 종료하는 것이 좋습니다. 인스턴스 종료 작업은 [인스턴스 종료](https://intl.cloud.tencent.com/document/product/213/4929)를 참고하십시오.
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/0c4462f0c86de84a23cac475e0541c84.png"/>
4. **복구 모드 시작**을 클릭합니다.
이 때 인스턴스가 복구 모드를 시작하는 것을 확인할 수 있으며, 아래 이미지와 같이 인스턴스 상태가 확인되면 성공적으로 복구 모드를 시작한 것이므로 가능한 한 빨리 인스턴스를 수정하려면 다음 단계를 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/46661eec9cabb65ab9ba358015373492.png)



### 복구 모드를 사용한 시스템 복구
1. [3단계](#step3)에서 설정한 'root' 계정과 비밀번호로 다음과 같이 인스턴스에 로그인합니다.
 - 인스턴스에 공용 IP가 있는 경우 [SSH를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)을 참고하십시오.
 - 인스턴스에 공용 IP가 없는 경우 [VNC를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)을 참고하십시오.
2. 로그인 성공 후 다음 명령어를 순서대로 실행하여 시스템 디스크의 루트 파티션을 마운트합니다.
복구 모드에서 인스턴스 시스템 디스크의 장치 이름은 'vda'이고 루트 파티션은 'vda1'이며 기본적으로 마운트되지 않습니다.
```
mkdir -p /mnt/vm1
```
```
mount /dev/vda1 /mnt/vm1
```
마운트가 성공하면 루트 파티션의 데이터 작업을 할 수 있습니다. 또한 `mount -o bind` 명령어를 사용하여 원본 파일 시스템의 일부 서브 디렉터리를 마운트하고 `chroot` 명령어를 사용하여 지정된 루트 디렉터리에서 명령을 실행할 수 있습니다. 구체적인 작업 명령어는 다음과 같습니다.
```
mount -o bind /dev /mnt/vm1/dev
mount -o bind /dev/pts /mnt/vm1/dev/pts
mount -o bind /proc /mnt/vm1/proc
mount -o bind /run /mnt/vm1/run
mount -o bind /sys /mnt/vm1/sys
chroot /mnt/vm1 /bin/bash
```


### 복구 모드 종료
1. 인스턴스가 복구된 후 실제 사용된 뷰 모드에 따라 다음 단계를 통해 복구 모드를 종료합니다.
<dx-tabs>
::: 리스트 모드
인스턴스가 위치한 행의 오른쪽에서 **더 보기** > **유지보수 및 점검** > **복구 모드 종료**를 선택합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/42b6657af00132b39a4b3242748a449c.png)
:::
::: 탭 모드
인스턴스가 위치한 탭을 선택하고 오른쪽 상단에서 **더 많은 작업** > **유지보수 및 점검** > **복구 모드 종료**를 선택합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/24df2366e42e1bdc22c171d871073c68.png)
:::
</dx-tabs>
2. 인스턴스 복구 모드 종료 후, 종료 상태가 되며, [인스턴스 시작]을 참고하여 인스턴스를 시작하면 다시 사용할 수 있습니다.

