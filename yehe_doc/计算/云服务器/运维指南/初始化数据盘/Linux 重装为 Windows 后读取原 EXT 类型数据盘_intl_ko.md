
## 작업 시나리오
본 문서는 Linux를 Windows로 [시스템 재설치](https://cloud.tencent.com/document/product/213/4933) 후 Cloud Virtual Machine(CVM)에서 기존 Linux 시스템의 데이터 디스크 데이터를 읽는 작업 방법에 관해 설명합니다.
Windows 파일 시스템 형식은 일반적으로 NTFS 또는 FAT32이지만, Linux 파일 시스템 형식은 일반적으로 EXT 시리즈입니다. 운영 체제가 Linux에서 Windows로 재설치된 후 운영 체제 유형은 변경되지만, 데이터 디스크는 아직 기존 형식이므로 재설치된 시스템이 데이터 디스크 파일 시스템에 액세스하지 못할 수 있습니다. 원본 데이터를 읽으려면 형식 변환 소프트웨어가 필요합니다.

## 전제 조건
- 이미 Windows 로 재설치된 CVM에 DiskInternals Linux Reader 소프트웨어를 설치합니다.
DiskInternals Linux Reader 소프트웨어 획득 방법: `http://www.diskinternals.com/download/Linux_Reader.exe `
- 재설치하기 전에 Linux CVM 데이터 디스크에 마운트할 파티션은 vdb1과 vdb2 두 가지입니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/ef515a31c27e5ea96993af60dfc9ab55.png)

## 작업 순서
### 데이터 디스크 마운트

>! 데이터 디스크가 마운트 된 경우, 이 단계를 건너뛰세요.
>
1. [Tencent Cloud CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 왼쪽 메뉴에서 [Cloud Block Storage]를 선택하여 CBS 관리 페이지에 접속합니다.
3. 재설치된 시스템의 인스턴스 라인을 선택하고 오른쪽의 [More]>[Mount]를 클릭합니다.
4. 팝업 창에서 재설치한 Windows CVM를 선택하고 [OK]를 클릭합니다.

### 데이터 디스크 정보 조회 
1. DiskInternals Linux Reader 소프트웨어를 실행하여 방금 마운트된 데이터 디스크 정보를 조회할 수 있습니다. `/root/mnt` 및 `/root/mnt1`은 각각 재설치 전의 Linux CVM 데이터 디스크인 vdb1과 vdb2 두 파티션입니다. 아래 이미지 참조
>! 이때의 Linux 데이터 디스크는 읽기 전용입니다. 이 데이터 디스크를 Windows 데이터 디스크로서 읽고 쓰려면 먼저 필요한 파일을 백업하고 Windows 운영 체제에서 지원하는 표준 유형으로 다시 포맷하세요. 자세한 내용은 [Windows 인스턴스: 데이터 디스크 초기화](https://cloud.tencent.com/document/product/213/2158)를 참조 바랍니다.
>
![](https://main.qcloudimg.com/raw/490428b0668dcd61c4c60bcb75121462.png)
2. `/root/mnt` 디렉터리를 더블 클릭하고 복사할 파일을 마우스 우클릭한 후 [Save]를 선택하여 파일을 저장합니다.
![](https://main.qcloudimg.com/raw/f36cbf32a7b423b8800e1fda6ba1c038.png)




