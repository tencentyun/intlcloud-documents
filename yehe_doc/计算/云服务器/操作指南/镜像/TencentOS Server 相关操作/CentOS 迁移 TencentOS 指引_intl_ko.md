## 작업 시나리오
CentOS는 공식적으로 CentOS Linux 프로젝트 유지 보수를 중단하고 2022년 01월 01일 CentOS 8 유지 보수 지원을 중단할 계획입니다. CentOS 7도 2024년 06월 30일에 유지 보수가 중단됩니다.

새로운 CVM 인스턴스를 구매해야 하는 경우 TencentOS Server 이미지 사용을 권장합니다. CentOS 인스턴스를 사용 중인 경우 본 문서를 참고하여 TencentOS Server로 교체할 수 있습니다.


## 버전 제안
- CentOS 7 시리즈는 TencentOS Server 2.4(TK4)로 마이그레이션하는 것이 좋습니다.
- CentOS 8 시리즈는 TencentOS Server 3.1(TK4)로 마이그레이션하는 것이 좋습니다.


## 주의 사항
- 다음과 같은 경우 마이그레이션 미지원:
 - 그래픽 인터페이스가 설치됨.
 - i686용 rpm 패키지가 설치됨.
- 다음과 같은 상황은 마이그레이션 후 비즈니스의 정상적인 실행에 영향을 미칠 수 있습니다.
 - 작업 프로그램을 설치했으며 타사 rpm 패키지에 종속된 경우
 - 작업 프로그램이 임의의 고정된 커널 버전에 종속되거나 커널 모듈을 자체적으로 컴파일한 경우
마이그레이션 후 타깃 버전은 5.4 커널 기반의 tkernel4입니다. 이 버전은 CentOS 7 및 CentOS 8 커널 버전보다 최신 버전이며 일부 이전 기능은 새 버전에서 변경될 수 있습니다.
 - 작업 프로그램은 고정된 gcc 버전에 종속됨
현재 TencentOS 2.4는 기본적으로 gcc 4.8.5를 설치하고 TencentOS 3.1은 기본적으로 gcc 8.5를 설치합니다.
- 마이그레이션 후 TencentOS 커널로 이동하려면 재시작해야 합니다.
- 마이그레이션은 데이터 디스크에 영향을 주지 않으며 OS 수준의 업그레이드일 뿐이며 데이터 디스크에 대한 작업은 수행하지 않습니다.

## 리소스 요구 사항
-  여유 메모리가 500MB 이상.
- 시스템 디스크 잔여 공간 10GB 이상.

## 작업 단계

### 데이터 백업
마이그레이션 작업은 되돌릴 수 없으며 작업 데이터의 보안을 위해 마이그레이션을 수행하기 전에 [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755)을 통해 시스템 디스크 데이터를 백업하는 것이 좋습니다.

### 마이그레이션 실행
<dx-tabs>
::: TencentOS 2.4(TK4)로 마이그레이션
1. 타깃 CVM에 로그인합니다. 자세한 내용은 [표준 로그인 방식으로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.
2. 다음 명령어를 실행하여 Python 3을 설치합니다.
```shell
yum install -y python3
```
3. 다음 명령을 실행하여 마이그레이션 툴을 가져옵니다.
```shell
wget http://mirrors.tencent.com/tencentos/2.4/tlinux/x86_64/RPMS/migrate2tencentos-1.0-3.tl2.noarch.rpm
```
4. 다음 명령을 실행하여 마이그레이션 툴을 설치합니다. 이 명령은 /usr/sbin 아래에 migrate2tencentos.py를 생성합니다.
```shell
rpm -ivh migrate2tencentos-1.0-3.tl2.noarch.rpm
```
5. 다음 명령을 실행하여 마이그레이션을 시작합니다.
```shell
/usr/sbin/migrate2tencentos.py -v 2.4
```
마이그레이션에는 다소 시간이 소요됩니다. 잠시만 기다려 주십시오. 스크립트 실행 완료 후, 다음과 같은 정보가 출력되면 마이그레이션이 완료되었음을 알 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a5d1a2cc65970b98b51071f6c90a40f5.png)
6. 인스턴스 재부팅의 자세한 내용은 [인스턴스 재기동](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.
7. 마이그레이션 결과를 확인합니다. 
   1. 다음 명령어를 실행하여 os-release를 확인합니다.
```shell
cat /etc/ os-releas
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/11ae97a1ed88d3a6e6ddfddc369b2574.png)
   2. 다음 명령어를 실행하여 커널을 확인합니다.
```shell
uname -r
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/cb34dbe478757069a4d3136a9384f711.png)
<dx-alert infotype="explain" title="">
커널은 최신 버전의 yum으로 기본 설정되어 있으므로 실제 반환 결과를 참고하십시오.
</dx-alert>
  3. 다음 명령어를 실행하여 yum을 확인합니다.
```shell
yum makecache
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/88b9468bed347c567223385b3df161b4.png)


:::
::: TencentOS 3.1(TK4)로 마이그레이션
1. 타깃 CVM에 로그인합니다. 자세한 내용은 [표준 로그인 방식으로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.
2. 다음 명령어를 실행하여 Python 3을 설치합니다.
```shell
yum install -y python3
```
3. 다음 명령을 실행하여 마이그레이션 툴을 가져옵니다.
```shell
wget http://mirrors.tencent.com/tlinux/3.1/Updates/x86_64/RPMS/migrate2tencentos-1.0-3.tl3.noarch.rpm
```
4. 다음 명령을 실행하여 마이그레이션 툴을 설치합니다. 이 명령은 /usr/sbin 아래에 migrate2tencentos.py를 생성합니다.
```shell
rpm -ivh migrate2tencentos-1.0-3.tl3.noarch.rpm
```
5. 다음 명령을 실행하여 마이그레이션을 시작합니다.
```shell
/usr/sbin/migrate2tencentos.py -v 3.1
```
마이그레이션에는 다소 시간이 소요됩니다. 잠시만 기다려 주십시오. 스크립트 실행 완료 후, 다음과 같은 정보가 출력되면 마이그레이션이 완료되었음을 알 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e272e5f6e5eba50a1e9bc74db536a592.png)
6. 인스턴스 재부팅의 자세한 내용은 [인스턴스 재기동](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.
7. 마이그레이션 결과를 확인합니다. 
   1. 다음 명령어를 실행하여 os-release를 확인합니다.
```shell
cat /etc/ os-releas
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/eb7333c8badf5d7a4852a66084fcc190.png)
   2. 다음 명령어를 실행하여 커널을 확인합니다.
```shell
uname -r
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/9bba4c6112c4bec1482d827ad02a39d6.png)
<dx-alert infotype="explain" title="">
커널은 최신 버전의 yum으로 기본 설정되어 있으므로 실제 반환 결과를 참고하십시오.
</dx-alert>
  3. 다음 명령어를 실행하여 yum을 확인합니다.
```shell
yum makecache
```
다음 이미지와 같은 정보 반환:
![](https://qcloudimg.tencent-cloud.cn/raw/83a6ec7fc69ab6bd26e9ff1cf0f443da.png)

:::
</dx-tabs>


