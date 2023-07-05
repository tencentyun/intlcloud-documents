## 작업 시나리오
본 문에서는 운영 체제가 CentOS 8.0인 Tencent Cloud CVM(Cloud Virtual Machine)을 예로 들어 오픈 소스 툴 [Extundelete](https://sourceforge.net/projects/extundelete/)을 사용하여 실수로 삭제된 데이터를 빠르게 복원하는 방법을 소개합니다.
Extundelete는 파일 시스템 유형이 ext3 및 ext4인 파일의 우발적 삭제 복구를 지원하지만 구체적인 복구 정도는 삭제 후 덮어쓰기 여부, 메타데이터 journal 보존 여부 등과 같은 요인과 관련이 있습니다. 복구할 데이터의 파일 시스템이 시스템 디스크에 있고 비즈니스 프로세스나 시스템 프로세스가 항상 파일에 쓰기 중인 경우 복구 가능성이 낮습니다.

<dx-alert infotype="explain" title="">
Tencent Cloud는 [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755), [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 및 [객체 스토리지](https://intl.cloud.tencent.com/document/product/436/6222) 등의 데이터 스토리지 방식을 제공하오니, 정기적으로 데이터를 백업하여 데이터 보안성을 개선하시길 권장합니다.
</dx-alert>




## 준비 작업
데이터 복구 관련 작업을 수행하기 전에 다음 준비 작업을 완료하십시오.
- [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755) 및 [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)을 참고하여 문제 발생 시 초기 상태로 복구할 수 있도록 데이터를 백업하시기 바랍니다.
- 관련 비즈니스 프로그램을 중지하고 파일 시스템에 데이터 쓰기를 계속합니다. 데이터 디스크를 복원해야 하는 경우 먼저 데이터 디스크에서 'umount' 작업을 수행할 수 있습니다.


## 작업 단계

1. 다음 두 가지 방법으로 Extundelete를 설치합니다.
<dx-tabs>
::: 컴파일된 이진법 프로그램 다운로드(권장)
1. 다음 명령을 실행하여 컴파일된 이진법 프로그램을 직접 다운로드합니다.
```
wget https://github.com/curu/extundelete/releases/download/v1.0/extundelete
```
2. 다음 명령어를 실행하여 파일 권한을 부여합니다.
```
chmod a+x extundelete
```
:::
::: 수동 컴파일 설치

<dx-alert infotype="explain" title="">
이 단계는 CentOS 7 운영 체제를 예로 들며 시스템 환경에 따라 단계가 다르므로 실제 참고 문서에 따라 작업하십시오.
</dx-alert>



1. 다음 명령어를 순서대로 실행하여 Extundelete에 필요한 종속 및 라이브러리를 설치합니다.
```shell
yum install libcom_err e2fsprogs-devel
```
```shell
yum install gcc gcc-c++ 
```
2. 다음 명령어를 실행하여 Extundelete 소스 코드를 다운로드합니다.
```
wget https://github.com/curu/extundelete/archive/refs/tags/v1.0.tar.gz
```
3. 다음 명령어를 실행하여 v1.0.tar.gz 파일을 압축 해제합니다.
```
tar  xf v1.0.tar.gz
```
4. 다음 명령어를 순서대로 실행하여 컴파일 및 설치합니다.
```
cd extundelete-1.0
```
```
./configure
```
```
make
```
5. 다음 명령어를 실행하여 src 디렉터리로 이동하여 컴파일된 Extundelete 파일을 조회합니다.
```
cd ./src
```
:::
</dx-tabs>
2. 다음 명령어를 실행하여 데이터 복원을 시도합니다.
```
./extundelete  --restore-all  /dev/해당 디스크
```
복구된 파일은 같은 레벨 디렉터리의 'RECOVERED_FILES' 폴더에 있으므로 필요한 파일이 있는지 확인하십시오.


