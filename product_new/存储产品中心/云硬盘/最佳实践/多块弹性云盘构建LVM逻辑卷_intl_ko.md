## LVM 소개
LVM(Logical Volume Manager)은 하드 디스크 및 파티션에 논리 레이어를 설정하여, 디스크 또는 파티션을 동일한 크기 PE(Physical Extents) 단위로 나눕니다. 다양한 디스크 및 파티션을 동일한 볼륨 그룹(VG, Volume Group)에 귀속시켜 VG에 LV(Logical Volume) 및 파일 시스템을 생성할 수 있습니다.
디스크 파티션을 직접 사용하는 방식에 비교하면 LVM은 탄력적으로 파일 시스템의 용량을 조정할 수 있는 장점이 있습니다.
- 파일 시스템은 물리적 디스크의 크기에 제한되지 않고 여러 디스크에 분포할 수 있습니다.
예를 들면, 3개의 4TB 엘라스틱 CBS를 구매하고 LVM을 사용하여 12TB의 초대형 파일 시스템을 생성할 수 있습니다.
- 논리 볼륨 크기를 동적으로 조정할 수 있어 디스크를 다시 파티션하지 않아도 됩니다.
LVM 볼륨 그룹의 용량이 수요를 충족하지 못할 경우, 엘라스틱 CBS를 별도로 구매하여 해당 CVM에 마운트한 후 LVM 볼륨 그룹에 추가하여 용량 확장할 수 있습니다.

## LVM 구축
>?본 문서는 LVM 작성을 통해 엘라스틱 CBS 3개를 사용하여 동적으로 파일 시스템의 크기를 조정할 수 있는 예시로 하였습니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/81086e80477ff7e374e7c3f0fe9d2788.png)

### 1단계 물리 볼륨 PV 생성
1. root 사용자로 [Linux CVM에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 진행하십시오
2. 다음 명령어를 실행하여 물리 볼륨(Physical Volume, PV)을 생성하십시오.
```
pvcreate <디스크 경로 1> ... <디스크 경로N>
```
본 문서는`/dev/vdc`,`/dev/vdd` 및`/dev/vde`를 예로 합니다. 다음을 참조하여 실행하십시오.
```
pvcreate /dev/vdc /dev/vdd /dev/vde
```
아래 이미지와 같이 성공적으로 생성됩니다.
![](https://main.qcloudimg.com/raw/5b92a6c7878e22906599af48bfa09d95.png)
3. 다음 명령어를 실행하여 현재 시스템의 물리 볼륨을 조회하십시오.
```
lvmdiskscan | grep LVM
```
![](https://main.qcloudimg.com/raw/1de75af4a49c2deea689a2576eb075d9.png)

### 2단계 볼륨 그룹 VG 생성
1. 다음 명령어를 실행하여 VG를 생성하십시오.
```
Vgcreate [-s <PE 크기 지정>] <볼륨 그룹 이름> <물리 볼륨 경로>
```
본 문서는 "lvm_demo0" 볼륨 그룹 생성을 예로 합니다. 다음을 참조하여 실행하십시오.
```
vgcreate lvm_demo0 /dev/vdc /dev/vdd
```
아래 이미지와 같이 성공적으로 생성됩니다.
![](https://main.qcloudimg.com/raw/3b8dba3329f62e85d2075fad10898632.png)
 "Volume group"<볼륨 그룹 이름> "successfully created"가 제시될 경우 볼륨 그룹이 성공적으로 생성되었음을 표시합니다.
 - 볼륨 그룹 생성한 후, 다음 명령어를 실행하여 볼륨 그룹에 새로운 물리 볼륨을 추가할 수 있습니다.
```
Vgextend 볼륨 그룹 이름, 새로운 물리 볼륨 경로
```
아래 이미지와 같이 성공적으로 추가됩니다.
![](https://main.qcloudimg.com/raw/105e5a77472f173ffd4a58624f20a863.png)
 - 볼륨 그룹이 생성되면 `vgs` 및`vgdisplay` 등 명령어를 실행하여 현재 시스템의 볼륨 그룹 정보를 조회할 수 있습니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/309c991d32cf4b801ddbe8d898f1bfbb.png)

### 3단계 논리 볼륨 LV 생성
1. 다음 명령어를 실행하여 LV를 생성하십시오.
```
lvcreate [-L <논리 볼륨 크기>][ -n <논리 볼륨 이름>] <VG이름>
```
본 문서는 8GB "lvm_demo0" 논리 볼륨 작성을 예로 합니다. 다음을 참조하여 실행하십시오.
```
lvcreate -L 8G -n lv_0 lvm_demo0
```
아래 이미지와 같이 성공적으로 생성됩니다.
![](https://main.qcloudimg.com/raw/ed6d2f827ae7c4a4630bf17e24d90df2.png)
>?`pvs` 명령어를 실행하면 `/dev/vdc` 가 8GB사용된 것을 확인할 수 있습니다. 아래 이미지를 참조합시오.
>![](https://main.qcloudimg.com/raw/2718d08f7c74b7b469a23473a1398dfe.png)

### 4단계 파일 시스템 생성 및 마운트
1. 다음 명령어를 실행하여 생성된 논리 볼륨에 파일 시스템을 생성하십시오.
```
mkfs.ext3 /dev/lvm_demo0/lv_0
```
2. 다음 명령어를 실행하여 파일 시스템을 마운트하십시오.
```
mount /dev/lvm_demo0/lv_0 vg0/
```
아래 이미지와 같이 성공적으로 마운트됩니다.
![](https://main.qcloudimg.com/raw/2a7701636c2604d67e0743de4f9a6af1.png)

### 5단계 논리 볼륨 및 파일 시스템 크기 동적 확장
>!VG 용량이 남은 경우에만 LV 용량을 동적으로 확장할 수 있습니다. LV 용량을 확장한 후 해당 LV에서 생성된 파일 시스템의 크기를 확장해야 합니다.

1. 다음 명령어를 실행하여 논리 볼륨 크기를 확장하십시오.
```
lvextend [-L +/- <용량 증가 및 감소>] <논리 볼륨 경로>
```
본 문서는 논리 볼륨 "lv_0"에 4GB 용량 확장을 예로 합니다. 다음을 참조하여 실행하십시오.
```
lvextend -L +4G /dev/lvm_demo0/lv_0
```
아래 이미지와 같이 성공적으로 확장됩니다.
![](https://main.qcloudimg.com/raw/eccd7d6aec587eb90ec655a384367595.png)
>?pvs` 명령어를 실행하여`/dev/vdc`가 완전히 사용되고`/dev/vdd`가 2GB를 사용하였는지 확인할 수 있습니다.아래 이미지를 참조하십시오.
>![](https://main.qcloudimg.com/raw/189155ca377ef9550c4587ca78ab5b27.png)
2. 다음 명령어를 실행하여 파일 시스템을 확장하십시오.
```
resize2fs /dev/lvm_demo0/lv_0
```
아래 이미지와 같이 성공적으로 확장됩니다.
![](https://main.qcloudimg.com/raw/2e37f35678014ab1ca398fe5470a754b.png)
확장 완료 후, 다음 명령어를 실행하여 논리 볼륨의 용량이 12GB로 변경되었는지 확인할 수 있습니다.
```
df -h
```
