## 작업 시나리오

본 문서는 Linux 이미지의 생성 과정을 안내합니다.

## 작업 순서

### 준비 과정

생성한 시스템 디스크의 이미지를 내보낼 때 아래의 검사를 진행해야 합니다.
>? 데이터 디스크를 통해 이미지를 내보내는 경우에는 이 작업을 건너뛸 수 있습니다.
>

#### OS 파티션 및 실행 모드 검사
1. 다음 명령어를 실행하여 OS 파티션이 GPT 파티션인지 확인합니다.
```
sudo parted -l /dev/sda | grep 'Partition Table'
```
 - 출력 결과가 msdos인 경우, MBR 파티션임을 의미하므로 다음 단계로 이동합니다.
 - 출력 결과가 gpt인 경우, GPT 파티션임을 의미합니다. 현재는 서비스 마이그레이션에서 GPT 파티션을 지원하지 않으므로 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 피드백 바랍니다.
2. 다음 명령어를 실행하여 운영 체제가 EFI 모드로 실행되는지 확인합니다.
```
sudo ls /sys/firmware/efi
```
 - 파일이 포함되어 있다면, 현재 운영 체제가 EFI 모드에서 실행된 것이므로 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 피드백 바랍니다.
 - 파일이 존재하지 않으면 다음 단계로 이동합니다.

#### 시스템 키 파일 검사
검사할 시스템 키 파일에는 다음과 같은 파일이 포함됩니다.
>? 정상적인 읽기 및 쓰기를 위해 시스템 키 파일의 위치 및 권한이 올바르도록, 해당하는 릴리스 버전의 표준을 따르십시오.
>
 - /etc/grub2.cfg: kernel 매개변수에서는 uuid로 root를 마운트하시길 권장하며, 다른 방식(예: root=/dev/sda)을 사용할 경우 시스템이 실행되지 않을 수 있습니다.
 - /etc/fstab: 다른 하드 디스크를 마운트하지 마십시오. 마이그레이션 후 디스크 결함으로 인해 시스템이 실행되지 않을 수 있습니다.
 - /etc/shadow: 정상적인 권한으로 읽기 및 쓰기가 가능합니다.

#### 소프트웨어 언마운트
충돌이 발생하는 드라이버와 소프트웨어(VMware tools, Xen tools, Virtualbox GuestAdditions 및 일부 하위 드라이버 자체 소프트웨어 포함)를 언마운트 합니다.

#### virtio 드라이버 검사
작업에 대한 자세한 내용은 [Linux 시스템 Virtio 드라이버 검사](https://intl.cloud.tencent.com/document/product/213/9929)를 참조 바랍니다.

#### cloud-init 설치
설치에 대한 자세한 내용은 [Linux 시스템에서 Cloud-init 설치](https://intl.cloud.tencent.com/document/product/213/12587)를 참조 바랍니다.

#### 기타 하드웨어 관련 설정 검사
클라우드로 업로드한 후, 하드웨어에 나타나는 변경 사항은 다음과 같습니다.
 - 그래픽 카드가 Cirrus VGA로 교체됩니다.
 - 하드 디스크가 Virtio Disk로 교체되고 장치 이름은 vda 및 vdb입니다.
 - ENI가 Virtio Nic으로 교체되고 기본으로 eth0만 제공됩니다.

### 파티션 및 크기 조회
다음 명령어를 실행하여 현재 운영 체제의 파티션 형식을 조회하고 복사할 파티션 및 크기를 결정합니다.
```
mount
```
아래의 출력 결과를 예로 듭니다.
```
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sys on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
dev on /dev type devtmpfs (rw,nosuid,relatime,size=4080220k,nr_inodes=1020055,mode=755)
run on /run type tmpfs (rw,nosuid,nodev,relatime,mode=755)
/dev/sda1 on / type ext4 (rw,relatime,data=ordered)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/unified type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,rdma)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
systemd-1 on /home/libin/work_doc type autofs (rw,relatime,fd=33,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12692)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=39,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=12709)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,pagesize=2M)
tmpfs on /tmp type tmpfs (rw,nosuid,nodev)
configfs on /sys/kernel/config type configfs (rw,relatime)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,size=817176k,mode=700,uid=1000,gid=100)
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=100)
```
루트 파티션이 `/dev/sda1` 안에 있고, `/boot` 및 `/home`이 독립적인 파티션이 아닌 것과 더불어, sda1에 boot 파티션이 포함되어 있으나 mbr은 누락되어 있음을 알 수 있습니다. 따라서 sda 전체를 복사하면 됩니다.
>! 내보낸 이미지에는 최소한 루트 파티션과 mbr이 포함되어 있어야 합니다. 내보낸 이미지에 mbr이 없다면 실행할 수 없게 됩니다.
> 현재 운영 체제에서 `/boot` 및` /home`이 독립적인 파티션인 경우 내보낸 이미지에도 두 개의 독립적인 파티션이 포함되어 있어야 합니다.
> 

### 이미지 내보내기
실제 수요에 따라 이미지 내보내기 방식을 선택합니다.


<dx-tabs>
<span id="Useplatform"></span>
:::플랫폼\s툴을\s사용해\s이미지\s내보내기
VMWare vCenter Convert 혹은 Citrix XenConvert 등과 같은 가상 플랫폼의 이미지 내보내기 툴을 사용합니다. 자세한 내용은 각 플랫폼의 내보내기 툴 문서를 참조 바랍니다.
<dx-alert infotype="explain">
현재 Tencent Cloud의 서비스 마이그레이션에서 지원하는 이미지 형식은 qcow2, vhd, raw, vmdk입니다.
</dx-alert> 
:::
<span id="ExportImageForUsingCommand"></span>
:::명령어를\s사용해\s이미지\s내보내기
<dx-alert infotype="notice">
명령어를 사용한 수동 이미지 내보내기 방식은 상대적으로 리스크가 높습니다(IO가 혼잡할 때 파일 시스템의 metadata 오류를 야기하는 등). 이미지를 내보낸 후 [이미지 검사](# CheckMirror)를 실행하여 오류를 확인하시길 권장합니다.
</dx-alert> 

[qemu-img 명령어 사용](#qemuimg)이나 [dd 명령어 사용](#dd) 중에서 하나를 선택하여 이미지를 내보낼 수 있습니다.
- **`qemu-img` 명령어 사용**<span id="qemuimg"></span>
 1. 다음 명령어를 실행하여 필요한 패키지를 설치합니다. 본 문서는 Debian을 예로 들며 릴리스 버전에 따라 패키지가 다를 수 있으므로 실제 상황에 맞게 변경하시기 바랍니다. 예: CentOS의 패키지 이름은 `qemu-img`입니다.
```
apt-get install qemu-utils
```
 2. 다음 명령어를 실행하여 `/dev/sda`를 `/mnt/sdb/test.qcow2`로 내보냅니다.
```
sudo qemu-img convert -f raw -O qcow2 /dev/sda /mnt/sdb/test.qcow2
```
그중에서 `/mnt/sdb`는 마운트한 새 디스크이거나 다른 네트워크 스토리지입니다.
다른 형식으로 전환해야 할 경우 `-O`의 매개변수 값을 수정하시기 바랍니다. 수정 가능한 매개변수는 다음과 같습니다.
<span id="-OParameterValue"></span>
<table>
	<tr><th>매개변수 값</th><th>설명</th></tr>
	<tr><td>qcow2</td><td>qcow2 형식</td></tr>
	<tr><td>vpc</td><td>vhd 형식</td></tr>
	<tr><td>vmdk</td><td>vmdk 형식</td></tr>
	<tr><td>raw</td><td>형식 없음</td></tr>
</table>
- **`dd` 명령어 사용**<span id="dd"></span>
예를 들면, 다음 명령어를 실행하여 raw 형식의 이미지를 내보냅니다.
```
sudo dd if=/dev/sda of=/mnt/sdb/test.imag bs=1K count=$count
```
그중에서 `count` 매개변수가 복사해야 할 파티션의 수량이며, `fdisk` 명령어로 해당 수량 값을 조회할 수 있습니다. 전체 디스크를 복사해야 하는 경우 `count` 매개변수를 무시해도 됩니다.
예를 들면, 다음 명령어를 실행하여 `/dev/sda`의 파티션 수량을 조회합니다.
```
fdisk -lu /dev/sda
```
다음과 같은 결과를 출력합니다.
```
Disk /dev/sda: 1495.0 GB, 1494996746240 bytes
255 heads, 63 sectors/track, 181756 cylinders, total 2919915520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disk identifier: 0x0008f290

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048    41945087    20971520   83  Linux
/dev/sda2        41945088    46123007     2088960   82  Linux swap / Solaris
/dev/sda3        46123008    88066047    20971520   83  Linux
/dev/sda4        88066048  2919910139  1415922046   8e  Linux LVM
```
`fdisk` 명령어의 출력 결과에 따르면, sda1의 종료 위치는 41945087 \* 512 바이트이고 `count`는 20481M으로 설정됩니다.
<dx-alert infotype="explain">
 `dd` 명령어를 통해 내보낸 이미지는 raw 형식이므로 [qcow2, vhd 혹은 기타 이미지 형식으로 전환](# ImageFormatConversion)하시길 권장합니다.
</dx-alert>
:::
</dx-tabs>

<span id="ImageFormatConversion"></span>
### 이미지 형식 전환
>? 현재 Tencent Cloud의 서비스 마이그레이션은 qcow2, vhd, vmdk, raw 형식의 이미지를 지원합니다. 압축한 이미지 형식을 사용하여 전송 및 마이그레이션 시간을 단축하시길 권장합니다.
> 
`qemu-img` 명령어를 사용해 이미지 형식을 전환합니다.
예를 들면, 다음 명령어를 실행하여 raw 형식의 이미지를 qcow2 형식으로 전환합니다.
```
sudo qemu-img convert -f raw -O qcow2 test.img test.qcow2
```
- `-f`는 소스 이미지 파일 형식입니다.
- `-O` 는 타깃 이미지 파일 형식입니다. 지원되는 형식은 [`-O` 매개변수 값](#-OParameterValue)를 참조 바랍니다.

<span id="CheckMirror"></span>
### 이미지 검사
>? 서비스를 중지하지 않고 바로 이미지를 생성했거나 다른 원인으로 인해 생성한 이미지 파일 시스템에 오류가 있을 수 있으므로 이미지를 생성한 후에 오류가 없는지 확인하시기 바랍니다.
>
이미지 형식이 현재 플랫폼에서 지원하는 형식과 일치할 경우 이미지를 열어 파일 시스템을 바로 확인할 수 있습니다. 예시, Windows 플랫폼은 vhd 형식의 이미지를 바로 첨부할 수 있고, Linux 플랫폼은 qemu-nbd를 사용해 qcow2 형식의 이미지를 열 수 있으며, Xen 플랫폼은 vhd 파일을 바로 사용할 수 있습니다. 본 문서는 Linux 플랫폼을 예로 들었으며 검사 순서는 아래와 같습니다.
1. 다음 명령어를 순서대로 실행하여 nbd 모듈이 있는지 확인합니다.
```
modprobe nbd
```
```
lsmod | grep nbd
```
출력 결과가 아래와 같다면 nbd 모듈이 있음을 의미합니다. 출력 결과가 공백이라면 커널 컴파일 옵션 `CONFIG_BLK_DEV_NBD`가 열려있는지 확인하고, 실행할 수 없다면 시스템을 교체하거나 `CONFIG_BLK_DEV_NBD` 컴파일 옵션을 연 다음 커널을 다시 컴파일해야 합니다.
![](https://main.qcloudimg.com/raw/190bd78d60c7340fb95210f60e126105.png)
2. 다음 명령어를 순서대로 실행하여 이미지를 검사합니다.
```
qemu-nbd -c /dev/nbd0 xxxx.qcow2
```
```
mount /dev/nbd0p1 /mnt
```
`qemu-nbd` 명령어를 실행한 후에는 `/dev/nbd0`가 `xxx.qcow2`에 있는 콘텐츠에 매핑됩니다. `/dev/nbd0p1`이 해당 가상 디스크의 첫 번째 파티션임을 의미하므로, nbd0p1이 존재하지 않거나 마운트에 실패할 경우 이미지 오류일 가능성이 있습니다.
또한, 이미지를 업로드하기 전에 먼저 CVM을 실행하여 이미지 파일의 사용 가능 여부를 테스트할 수 있습니다.


