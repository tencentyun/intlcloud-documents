## 작업 시나리오

Windows 파일 시스템은 일반적으로 NTFS 또는 FAT32 형식을 사용하고, Linux 파일 시스템은 일반적으로 EXT 시리즈의 형식을 사용합니다. CVM의 운영 체제를 Windows에서 Linux로 재설치 했을 경우, 운영 체제 유형은 바뀌었지만 CVM 내 데이터 디스크는 여전히 기존 시스템의 것을 사용하기 때문에, 시스템 재설치 후 CVM에서 데이터 디스크 파일 시스템에 액세스 할 수 없는 상황이 발생할 수 있습니다. 본 파일에서는 시스템 재설치 후 Linux CVM에서 기존 Windows 시스템의 데이터 디스크 데이터를 읽는 방법을 안내합니다.

## 작업 순서

### Linux 시스템 설정 NTFS 지원 

1. 시스템 재설치 후 Linux CVM에 로그인합니다.
2. 다음 명령어를 실행하여 ntfsprogs 소프트웨어를 설치하고, Linux CVM이 NTFS 파일 시스템에 액세스하도록 하세요.
>본 파일에서는 CentOS 시스템을 예로 들었습니다. 각 Linux 시스템 유형별로 설치 명령어가 다를 수 있으니 해당하는 설치 명령어를 사용하여 설치하시기 바랍니다.
>
```
yum install ntfsprogs
```


###  Windows CVM의 데이터 디스크를 Linux CVM로 마운트 합니다

> 귀하의 Windows CVM의 데이터 디스크가 이미 Linux CVM에 마운트 되어 있다면 이 조작은 스킵해도 됩니다.
>
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하십시오.
2. 왼쪽 사이드바에서 [[CBS](https://console.cloud.tencent.com/cvm/cbs)]를 클릭하여 CBS 관리 페이지에 진입합니다.
3. 마운트가 필요한 Windows 데이터 디스크를 선택하고 [더보기]>[마운트]를 클릭합니다.
4. "인스턴스로 마운트" 팝업창에서 마운트할 Linux CVM을 선택하고 [확인]을 클릭합니다.
5. 이미 Windows 데이터 디스크가 마운트되어 있는 Linux CVM에 로그인합니다.
6. 다음의 명령어를 실행하여 Windows CVM에서 마운트된 데이터 디스크를 조회합니다.
```
parted -l
```
다음과 비슷한 정보 리턴:
```
Model: Virtio Block Device (virtblk)
Disk /dev/vdb: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 
Number  Start   End     Size    File system  Name                          Flags
 1      17.4kB  134MB   134MB                Microsoft reserved partition  msftres
 2      135MB   53.7GB  53.6GB  ntfs         Basic data partition
```
7. 다음 명령어를 실행하여 데이터 디스크를 마운트합니다.
```
mount -t ntfs-3g 데이터 디스크 경로 마운트 포인트
```
예시, 경로가 ‘/dev/vdb1’인 데이터 디스크를  ‘/mnt’로 마운트하려면 다음 명령어를 실행합니다.
```
mount -t ntfs-3g /dev/vdb1 /mnt
```
이때 파일 시스템이 인식 가능하므로 마운트된 데이터 디스크를 Linux 시스템에서 바로 읽기 및 쓰기 할 수 있습니다.

