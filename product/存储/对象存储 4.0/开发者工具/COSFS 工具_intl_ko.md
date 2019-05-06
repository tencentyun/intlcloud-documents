## 기능 설명 
COSFS 도구는 COS 버킷을 로컬에 탑재하는 것을 지원하며 로컬 파일 시스템의 사용과 마찬가지로 Tencent Cloud COS의 객체를 직접 조작할 수 있습니다. COSFS에는 다음과 같은 주요 기능이 있습니다.
- POSIX 파일 시스템의 대부분 기능이 지원되며, 예를 들어 파일 읽기 및 쓰기, 디렉터리 조작, 링크 조작, 권한 관리, uid/gid 관리 등 기능이 있습니다.
- 큰 파일의 멀티파트 전송 기능.
- MD5 데이터 검증 기능.
- 로컬 데이터를 COS에 업로드할 경우 [COS 마이그레이션 도구](https://cloud.tencent.com/document/product/436/15392) 또는 [COSCMD 도구](https://cloud.tencent.com/document/product/436/10976)를 사용하십시오.

## 제한성
**COSFS는 탑재 후 파일을 간단히 관리하는 데만 적합합니다. 로컬 파일 시스템의 일부 기능을 지원하지 않으며 성능으로 CBS 또는 CFS를 대체할 수 없습니다.**다음과 같이 적용되지 않는 응용에 주의해야 합니다.

- 임의 또는 추가적인 파일 쓰기는 전체 파일의 재시작을 야기할 수 있습니다. 버킷과 같은 지역에 있는 CVM 가속 파일의 업로드 및 다운로드를 사용할 수 있습니다.
- 여러 개의 클라이언트가 동일한 COS 버킷을 탑재할 경우 사용자가 스스로 조율하는 각 클라이언트의 행동에 의존합니다. 예를 들어 여러 개의 클라이언트가 동일한 파일을 쓰는 것을 등 피합니다.
- 파일/폴더의 rename 조작은 원자성이 아닙니다.
- 메타데이터 조작, 예를 들어 list directory의 경우, 성능이 다소 떨어지는데 COS 서버를 원격으로 접근해야 하기 때문입니다.
- hard link는 지원되지 않습니다. 높은 동시 발생의 읽기/쓰기 응용에는 적합하지 않습니다.
- 하나의 탑재점에 동시의 탑재와 탑재 해제가 불가합니다. cd 명령을 사용하여 다른 디렉터리로 전환하여 탑재점에 대해 탑재와 탑재 해제의 조작을 할 수 있습니다.

## 설치 및 사용 
### 운영 체제 버전 
주류 Ubuntu, CentOS, macOS 시스템.

### 설치 절차

#### 1. 소스 코드 획득 
먼저 GitHub에서 [COSFS 소스 코드](https://github.com/tencentyun/cosfs)를 지정된 디렉터리에 다운로드해야 합니다. 아래 리스트 `/usr/cosfs`를 예로 들 수 있습니다.
```shell
git clone https://github.com/tencentyun/cosfs /usr/cosfs
```

#### 2. 의존 소프트웨어 설치 
COSFS의 컴파일 설치는 automake, git, libcurl-devel, libxml2-devel, fuse-devel, make, openssl-devel 등과 같은 소프트웨어 패키지에 의존합니다. Ubuntu, CentOS 및 macOS의 의존 소프트웨어 설치 프로세스는 다음과 같습니다.

- Ubuntu 시스템 하의 의존 소프트웨어 설치:

```shell
sudo apt-get install automake autotools-dev g++ git libcurl4-gnutls-dev libfuse-dev libssl-dev libxml2-dev make pkg-config fuse
```

- CentOS 시스템 하의 의존 소프트웨어 설치:

```shell
sudo yum install automake gcc-c++ git libcurl-devel libxml2-devel fuse-devel make openssl-devel fuse
```

- macOS 시스템 하의 의존 소프트웨어 설치:

```shell
brew install automake git curl libxml2 make pkg-config openssl 
brew cask install osxfuse
```
<a id="compile"> </a>
#### 3. 컴파일 및 설치 COSFS 
설치 디렉터리에 들어가서 다음과 같은 명령을 실행하여 컴파일 및 설치를 진행합니다.
```sh
cd /usr/cosfs
./autogen.sh
./configure
make
sudo make install
cosfs --version  # cosfs 버전 번호 확인
```

운영 체제에 따라 configure 조작 시 다른 프롬프트가 나타나며 주로 다음과 같은 측면으로 나눕니다.
- CentOS 6.5 및 더 낮은 버전의 운영 체제에서 configure 조작 시 낮은 fuse 버전으로 인해 다음과 같은 프롬프트가 나타날 수 있습니다.
```shell
checking for common_lib_checking... configure: error: Package requirements (fuse >= 2.8.4 libcurl >= 7.0 libxml-2.0 >= 2.6) were not met:
  Requested 'fuse >= 2.8.4' but version of fuse is 2.8.3 
```
이 경우, fuse 2.8.4 및 그 이상의 버전을 수동으로 설치해야 하며 설치 명령은 다음과 같습니다.
```sh
yum -y remove fuse-devel
wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
./configure
make
make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse # fuse 코어 모듈 탑재
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig #동적 링크 라이브러리 업데이트
pkg-config --modversion fuse #fuse 버전 번호를 확인하면 "2.9.4"가 보일 때 fuse2.9.4 설치가 성공적으로 완료되었음을 의미합니다. 
```

- macOS에서 configure 조작 시 다음과 같은 프롬프트가 나타날 수 있습니다.
```shell
configure: error: Package requirements (fuse >= 2.7.3 libcurl >= 7.0 libxml-2.0 >2.6 libcrypto >= 0.9) were not met
No package 'libcrypto' found
```
이때 pkg-config 도구가 openssl을 찾을 수 있도록 PKG_CONFIG_PATH 변수를 설정해야 하며 명령은 다음과 같습니다.
```shell
brew info openssl 
export PKG_CONFIG_PATH=/usr/local/opt/openssl/lib/pkgconfig #이전 명령의 프롬프트에 따라 이 명령을 수정해야 할 수도 있습니다.
```

### COSFS 사용 방법

#### 1. 키 파일 구성
파일 /etc/passwd-cosfs에 버킷 이름 &lt;Name&gt;-&lt;Appid&gt;, 이 버킷에 대응하는 &lt;SecretId&gt; 및 &lt;SecretKey&gt;를 적으며 세 항목 사이에 반각 사칭을 사용하여 나눕니다. 또한 키 유출을 방지하기 위하여 COSFS는 키 파일의 권한을 640으로 설정하여 /etc/passwd-cosfs 키 파일의 배치 명령 양식은 다음과 같습니다.
```shell
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```
>!&lt;Name&gt;, &lt;Appid&gt;, &lt;SecretId&gt; 및 &lt;SecretKey&gt;를 사용자 정보로 교체해야 합니다.
>버킷 명명 규범에 관련하여 [버킷 명명 규범](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83)을 참조하십시오. &lt;SecretId&gt; 및 &lt;SecretKey&gt;는 관리 콘솔 [클라우드 API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 획득할 수 있습니다. 이외에 키를 파일 $HOME/.passwd-cosfs에 넣을 수 있습니다. 또는 -opasswd_file=[path]를 통해 키 파일 경로를 지정할 경우 키 파일 권한을 600으로 설정해야 합니다.

**예시:**

```shell
echo examplebucket-1250000000:AKIDHTVVaVR6e3:PdkhT9e2rZCfy6 > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

#### 2. 도구 실행
이미 키 파일에 정보를 구성한 버킷을 지정된 디렉터리에 업로드하려면 다음과 같은 명령행을 사용할 수 있습니다.

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=<CosDomainName> -odbglevel=info
```
그 중:
- &lt;MountPoint&gt;는 로컬 탑재 디렉터리(예를 들어 /mnt)입니다.
- &lt;CosDomainName&gt;은 버킷에 대응하는 접근 도메인 이름이고 형식은 `http://cos.<Region>.myqcloud.com` (XML API에 적용되므로 이 매개 변수에서 버킷 이름을 가져오지 마십시오.)입니다. 그중에 &lt;Region&gt;은 ap-guangzhou , eu-frankfurt과 같은 지역 약칭입니다. 더 많은 지역 정보는 [가용 지역](https://cloud.tencent.com/document/product/436/6224)을 참조하십시오.
- -odbglevel 로그 클래스를 지정합니다.

**예시:**

```shell
mkdir -p /mnt/cosfs
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -onoxattr
```

>!v1.0.5 이전 버전의 COSFS에 대한 탑재 명령은 다음과 같습니다.
```shell
cosfs <APPID>:<BucketName> <MountPoint> -ourl=<CosDomainName>
```
v1.0.5 이전 버전의 COSFS에 대한 구성 파일 양식은 다음과 같습니다.
```shell
<BucketName>:<SecretId>:<SecretKey>
```

#### 3. 버킷 탑재 해제:

버킷 탑재 해제의 예시:

```shell
fusermount -u /mnt 또는 umount -l /mnt
```

## 상용 탑재 옵션

### -omultipart_size=[size]
멀티파트 업로드 시 단일 멀티파트의 크기(단위: MB)를 지정하고 기본적으로는 10MB입니다. 멀티파트 업로드는 단일 파일 멀티파트 수에 대해 최대 제한(10000파트)이 있으므로 100GB(10MB\*10000) 크기를 초과하는 파일에 대해서 상황에 따라 매개변수를 조정해야 합니다.

### -oallow_other
다른 사용자가 탑재 폴더를 접근하도록 허용하려면 COSFS를 실행할 때 이 매개변수를 지정할 수 있습니다.

### -odel_cache
기본적으로 COSFS는 최적의 성능을 위해 umount 뒤에는 로컬의 캐시 데이터가 제거되지 않습니다. COSFS 로그아웃 시 자동으로 캐시 제거가 필요할 경우, 탑재 시 이 옵션을 추가할 수 있습니다.

###  -onoxattr
getattr/setxattr 기능의 사용을 금지합니다. 1.0.9 이전 버전의 COSFS에서 확장 속성의 설정과 획득을 지원하지 않으며, 탑재할 때 use_xattr 옵션을 사용하면 mv 파일에서 버킷이 실패할 수 있습니다.
 
### -ouse_cache=[path]
캐시 디렉터리로 파일을 캐시 합니다. path는 로컬 디렉터리 경로이며, 이 옵션은 파일이 캐시 된 후 파일의 읽기 및 쓰기(처음 읽기 또는 쓰기가 아님)를 가속화할 수 있습니다. 로컬로 캐시 할 필요가 없거나 로컬 디스크 용량이 제한적이면 이 옵션을 지정하지 않아도 됩니다.

### -opasswd_file=[path]
이 옵션은 COSFS 키 파일이 위치한 경로를 지정할 수 있으며, 이 옵션이 설정한 키 파일에 대해 600으로 권한을 설정해야 합니다.

### -odbglevel=[info|dbg]

COSFS 로그 기록 클래스를 설정하려면 info, dbg를 선택할 수 있습니다. 생산 환경에서는 info로, 디버깅 시 dbg로 설정하는 것을 권장합니다.

### -oumask=[perm]

이 옵션은 지정 유형 사용자가 탑재 디렉터리 내 파일에 대한 조작 권한을 제거할 수 있습니다. 예를 들어 -oumask=007, 다른 사용자가 파일의 읽기 및 쓰기 실행 권한을 제거할 수 있습니다.

### -ouid=[uid]
이 옵션은 사용자 id가 [uid]인 사용자가 탑재 디렉터리 내의 파일 권한 비트에 제한을 받지 않고 탑재 디렉터리 내 모든 파일을 접근할 수 있습니다.
사용자 uid의 획득에는 id 명령을 사용할 수 있으며 형식은 `id -u username`입니다. 예를 들어 `id -u user_00`를 실행하면 사용자 user_00의 uid를 획득할 수 있습니다.

## FAQ
COSFS 도구 사용에 질문이 있다면 [COSFS 도구 FAQ](https://cloud.tencent.com/document/product/436/30743)를 참조하십시오.

