## 작업 시나리오
본 문서는 CentOS 7.7 운영 체제의 Tencent Cloud CVM을 예로, 오픈 소스 툴 Extundelete를 사용하여 잘못 삭제한 데이터를 빠르게 복구하는 방법에 관해 소개합니다. Extundelete는 ext3 및 ext4 두 가지 형식의 파티션 복구를 지원하며 기능 면에서 뛰어납니다. 본 문서는 데이터 디스크 파일을 실수로 잘못 삭제한 후에 디스크에 쓰기 등 작업을 하지 않은 경우에 해당합니다.
Tencent Cloud는 [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755), [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942) 및 [객체 스토리지](https://intl.cloud.tencent.com/document/product/436/6222) 등의 데이터 저장 방식도 제공하고 있으니, 정기적으로 데이터를 백업하여 데이터 보안성을 향상하시길 권장합니다.

## 예시 소프트웨어 버전
- Linux: Linux 운영 체제의 경우, 본 문서는 CentOS 7.7을 예로 듭니다.
- Extundelete: 오픈 소스 데이터 복구 툴로, 본 문서는 Extundelete 0.2.4를 예로 듭니다.


## 작업 순서
>!작업을 시작하기 전에, [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755), [사용자 정의 이미지 생성](https://intl.cloud.tencent.com/document/product/213/4942)을 참조하여 문제 발생 시 초기 상태로 복구할 수 있도록 데이터를 백업하시기 바랍니다.
>

### Extundelete 설치
1. 다음 명령어를 실행하여 Extundelete에 필요한 종속 및 라이브러리를 설치합니다.
>!
>- Extundelete는 libext2fs 1.39 이상의 버전이 필요합니다.
>- ext4 형식 지원이 필요하다면, e1fsprogs 1.41 이상 버전이 설치되어야 합니다. `dumpe2fs` 명령어를 실행하여 버전을 조회할 수 있습니다. 
>
```
yum -y install  bzip2  e2fsprogs-devel  e2fsprogs  gcc-c++  make
```
2. [Extundelete](https://sourceforge.net/projects/extundelete/) 설치 패키지를 다운로드합니다.
3. 다음 명령어를 순서대로 실행하여 Extundelete 설치 패키지를 압축 해제하고 프로그램 디렉터리로 이동합니다.
```
tar -xvjf extundelete-0.2.4.tar.bz2
```
```
cd extundelete-0.2.4 
```
4. 다음 명령어를 순서대로 실행하여 Extundelete를 컴파일 및 설치합니다.
```
./configure   
```
```
make && make install
```
설치가 완료되면 `usr/local/bin` 디렉터리에서 extundelete 실행 파일을 확인할 수 있습니다.

### 데이터 복구 테스트
아래의 절차를 참고하여 데이터 복구 과정을 이해하고 실제 상황에 맞게 작업할 수 있습니다.
1. [파티션에 파일 시스템 구축](https://intl.cloud.tencent.com/document/product/362/31597)을 참조하여 데이터 디스크를 초기화 및 분할하고, 다음 명령어를 실행하여 기존 디스크 및 가용 파티션을 확인합니다.
```
fdisk -l
```
출력 결과는 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/34abb1b0c7a1f6fb4ff233a42a781123.png)
2. 다음 명령어를 순서대로 실행하여 마운트 포인트와 마운트 파티션을 생성합니다. 본 문서는 파티션 `/dev/vdb1`을 `/test`에 마운트하였습니다.
```
mkdir /test
```
```
mount /dev/vdb1 /test
```
3. 다음 명령어를 순서대로 실행하여 마운트 포인트에 테스트 파일 hello를 생성합니다.
```
cd /test
```
```
echo test > hello
```
4. <span id="Step4"></span>다음 명령어를 실행하여 hello 파일의 md5 값을 기록합니다. md5 값은 삭제 전과 복구 후의 두 파일을 인증할 때 사용합니다.
```
md5sum hello
```
출력 결과는 아래와 같습니다.
![](https://main.qcloudimg.com/raw/230d4c9a4456df8b3623c0bd401d878a.png)
5. 다음 명령어를 순서대로 실행하여 hello 파일을 삭제합니다.
```
rm -rf hello
```
```
cd ~
```
```
fuser -k /test
```
6. 다음 명령어를 실행하여 마운트한 파티션을 언마운트합니다.
```
umount /dev/vdb1
```
7. 다음 명령어를 실행하여 파티션에서 잘못 삭제한 파일을 검색합니다.
```
extundelete --inode 2 /dev/vdb1
```
출력 결과는 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/97a64a2e0de658f4ed55500f162b1eb7.png)
8. 다음 명령어를 실행하여 Extundelete로 파일을 복구합니다.
```
/usr/local/bin/extundelete  --restore-inode 12  /dev/vdb1
```
복구가 완료되면 동일 레벨의 디렉터리에 `RECOVERED_FILES` 폴더가 나타납니다.
9. `RECOVERED_FILES` 폴더로 이동해 복구된 파일을 확인하고 다음 명령어를 실행합니다.
```
md5sum 파일 복구됨
```
획득한 md5 값이 [4단계](#Step4)에서 알게 된 hello 파일의 md5 값과 같다면 데이터 복구에 성공했음을 의미합니다.
