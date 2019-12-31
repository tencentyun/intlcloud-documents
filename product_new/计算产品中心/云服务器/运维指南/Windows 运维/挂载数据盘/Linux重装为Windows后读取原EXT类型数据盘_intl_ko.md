
## 작업 시나리오
본 문서는 Linux [재설치 시스템](https://intl.cloud.tencent.com/document/product/213/4933)을 Windows에 로딩한 후 클라우드 서버에서 원래 Linux 시스템 하의 데이터 디스크의 데이터를 읽는 작업 방법에 대해 설명합니다.
Windows 파일 시스템 형식은 일반적으로 NTFS 또는 FAT32이고 Linux 파일 시스템 형식은 일반적으로 EXT 시리즈입니다. 운영 체제가 Linux에서 Windows로 재설치된 후 운영 체제 유형은 변경되지만 데이터 디스크는 여전히 원래 포맷입니다. 재설치된 시스템은 데이터 디스크 파일 시스템에 액세스하지 못할 수 있습니다. 원본 데이터를 읽으려면 포맷 변환 소프트웨어가 필요합니다.

## 전제 조건
- 이미 Windows 로 재설치된 클라우드 서버에 DiskInternals Linux Reader 소프트웨어를 설치합니다.
DiskInternals Linux Reader 소프트웨어 획득 방법: `http://www.diskinternals.com/download/Linux_Reader.exe `
- 재설치하기 전에 Linux 클라우드 서버 데이터 디스크에 마운트하는 파티션은 vdb1 및 vdb2 두가지 입니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/ef515a31c27e5ea96993af60dfc9ab55.png)

## 작업 순서
### 데이터 디스크 마운트

> 데이터 디스크가 마운트 된 경우, 이 단계를 건너 뛰십시오.
>
1. [클라우드 서버 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
2. 왼쪽 사이드바에서 [CBS]를 선택하여 CBS 관리 페이지로 진입합니다.
3. 재설치된 시스템의 인스턴스 라인을 선택하고 오른쪽의 [더 알아보기]> [마운트]를 클릭하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/810d9328e0b8d91ed5912b4f7183edd4.png)
4. 팝업 창에서 재설치한 Windows 클라우드 서버를 선택하고 [확인]을 클릭하십시오.

### 데이터 디스크 정보 조회 
1. DiskInternals Linux Reader 소프트웨어를 실행하여 방금 마운트된 데이터 디스크 정보를 조회하십시오. `/root/mnt` 및 `/root/mnt1`은 각각 재설치 전 Linux 클라우드 서버 데이터 디스크의 vdb1과 vdb2 두 개의 파티션입니다. 아래 이미지를 참조하십시오.
> 이제 Linux 데이터 디스크는 읽기 전용입니다. 이 데이터 디스크를 Windows 데이터 디스크로 읽고 쓰려면 먼저 필요한 파일을 백업하고 Windows 운영 체제에서 지원하는 표준 유형으로 다시 포맷하십시오. 자세한 내용은 [Windows 인스턴스: 데이터 디스크 초기화](https://intl.cloud.tencent.com/document/product/213/2158)를 참조하십시오.
>
![](https://main.qcloudimg.com/raw/490428b0668dcd61c4c60bcb75121462.png)
2. `/root/mnt` 디렉터리를 더블 클릭하고 복사할 파일을 마우스 우클릭으로 클릭한 후 [저장]을 선택하여 파일을 저장하십시오. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/2d2f39e89014f72aaef1bfc3d1d101f3.png)




