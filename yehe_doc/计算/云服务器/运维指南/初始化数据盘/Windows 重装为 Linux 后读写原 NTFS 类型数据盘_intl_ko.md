## 개요

Windows 파일 시스템은 일반적으로 NTFS 또는 FAT32 형식을 사용하는 반면 Linux 파일 시스템은 종종 EXT 시리즈 형식을 사용합니다. CVM의 운영 체제가 Windows에서 Linux로 재설치될 때 CVM의 데이터 디스크는 원래 운영 체제의 형식으로 유지됩니다. 결과적으로 시스템 재설치 후 CVM이 데이터 디스크 파일 시스템에 액세스하지 못할 수 있습니다. 본문은 운영 체제가 Windows에서 Linux로 재설치된 후 원래 Windows 시스템에서 데이터 디스크를 읽는 방법을 설명합니다.

## 작업 단계

### Linux CVM에 NTFS 소프트웨어 설치

1. 시스템 재설치 후 Linux CVM에 로그인합니다.
2. 다음 명령을 실행하여 Linux CVM이 NTFS 파일 시스템에 대한 액세스를 지원할 수 있도록 ntfsprogs 소프트웨어를 설치합니다.
<dx-alert infotype="explain" title="">
본문은 CentOS를 예로 들어 설명합니다. 다른 유형의 Linux 시스템에는 다른 설치 명령이 있습니다. 해당 설치 명령을 사용하십시오.
</dx-alert>
```shellsession
yum install  -y ntfsprogs
```


###  Windows CVM에서 Linux CVM으로 데이터 디스크 연결



>?
>- 귀하의 Windows CVM의 데이터 디스크가 이미 Linux CVM에 마운트 되어 있다면 이 작업은 건너뛰어도 됩니다.
>- 재설치한 Linux CVM에 새로운 데이터 디스크를 마운트하려면 [Initializing Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31597)해야 합니다.


1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 왼쪽 사이드바에서 **[CBS](https://console.cloud.tencent.com/cvm/cbs)** 를 클릭하여 CBS 관리 페이지로 이동합니다.
3. 마운트할 Windows 데이터 디스크를 선택하고 **더 보기** > **마운트**를 클릭합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6acf53df9c1df0518502402d8bcadb6b.png)
4. ‘인스턴스로 마운트’ 팝업 창에서 마운트할 Linux CVM을 선택하고 **확인**을 클릭합니다.
5. 이미 Windows 데이터 디스크가 마운트되어 있는 Linux CVM에 로그인합니다.
6. 다음의 명령을 실행하여 Windows CVM에서 마운트된 데이터 디스크를 쿼리합니다.
```shellsession
parted -l
```
다음과 유사한 정보가 반환됩니다.
```shellsession
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
```shellsession
mount -t ntfs-3g 데이터 디스크 경로 마운트 포인트
```
예시, 경로가 ‘/dev/vdb2’인 데이터 디스크를  ‘/mnt’로 마운트하려면 다음 명령어를 실행합니다.
```shellsession
mount -t ntfs-3g /dev/vdb2 /mnt
```
이때 파일 시스템이 인식 가능하므로 마운트된 데이터 디스크를 Linux 시스템에서 바로 읽기 및 쓰기 할 수 있습니다.




