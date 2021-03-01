

## 기능 설명 

COSFS 툴은 COS 버킷을 로컬에 마운트하여 로컬 파일 시스템을 사용하듯이 직접 Tencent Cloud COS에 있는 객체를 조작할 수 있으며, 다음과 같은 기능을 제공합니다.
- 파일 읽기/쓰기, 디렉터리 작업, 링크 작업, 권한 관리, uid/gid 관리 등 POSIX 파일 시스템 대부분의 기능 지원
- 대용량 파일 멀티파트 전송 기능
- MD5 데이터 검증 기능
- 로컬 데이터를 COS로 업로드하는 경우 [COS Migration 툴](https://intl.cloud.tencent.com/document/product/436/15392) 또는 [COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976)을 사용하는 것을 권장합니다.

## 국한성
**COSFS는 S3FS 구조를 기반으로 쓰기 및 읽기 작업이 모두 디스크를 경유해 전송되어 마운트 후 파일에 대한 간단한 관리 작업에 적합합니다. 로컬 파일 시스템의 일부 기능적 사용법을 지원하지 않으며, 성능 또한 클라우드 디스크(CBS) 또는 파일 스토리지(CFS)를 대체할 수 없습니다.** 다음과 같이 적합하지 않은 시나리오에서 주의가 필요합니다.
- 랜덤 또는 파일 추가 기록 시 전체 파일이 다운로드 및 다시 업로드되므로, Bucket과 동일한 리전의 CVM 가속을 이용해 파일을 업로드 및 다운로드할 수 있습니다.
- 여러 클라이언트를 동일한 COS 버킷에 마운트하는 경우, 사용자에 종속되어 각 클라이언트의 행위(예: 여러 클라이언트가 동일한 파일을 동시에 쓰는 행위 등)에 자체적으로 협조합니다.
- 파일/폴더의 rename 작업이 원자(atomic)가 아닌 경우
- list directory와 같은 메타데이터 작업 성능이 비교적 떨어지고 원격 액세스 COS 서버가 필요한 경우
- hard link를 지원하지 않으며, 동시 접속 읽기/쓰기가 많은 시나리오에 적합하지 않습니다.
- 동일한 마운트 포인트에서 파일을 마운트하거나 언마운트할 수 없으며, 먼저 cd 명령어로 다른 디렉터리로 전환한 후 다시 마운트 포인트에서 마운트 및 언마운트 작업일 진행해야 합니다.

## 설치 및 사용 
### 적합한 운영 체제 버전 
주요 Ubuntu, CentOS, SUSE, macOS 시스템

### 설치 방법

#### 1. 종속 소프트웨어 설치 
COSFS의 컴파일 설치는 automake, git, libcurl-devel, libxml2-devel, fuse-devel, make, openssl-devel 등의 소프트웨어 패키지에 종속되며 Ubuntu, CentOS, SUSE, macOS의 종속 소프트웨어 설치 과정은 다음과 같습니다.

- Ubuntu 시스템에서 종속 소프트웨어 설치

```shell
sudo apt-get install automake autotools-dev g++ git libcurl4-gnutls-dev libfuse-dev libssl-dev libxml2-dev make pkg-config fuse
```

- CentOS 시스템에서 종속 소프트웨어 설치

```shell
sudo yum install automake gcc-c++ git libcurl-devel libxml2-devel fuse-devel make openssl-devel fuse
```

- SUSE 시스템에서 종속 소프트웨어 설치

```shell
sudo zypper install gcc-c++ automake make libcurl-devel libxml2-devel openssl-devel pkg-config
```

- macOS 시스템에서 종속 소프트웨어 설치

```shell
brew install automake git curl libxml2 make pkg-config openssl 
brew cask install osxfuse
```

#### 2. 소스 코드 획득 

GitHub에서 [COSFS 소스 코드](https://github.com/tencentyun/cosfs)를 지정 디렉터리에 다운로드합니다. 다음은 `/usr/cosfs` 디렉터리에 다운로드하는 예시입니다(실제 작업 시 구체적인 작업 환경에 따라 디렉터리 선택).
```shell
git clone https://github.com/tencentyun/cosfs /usr/cosfs
```


#### 3. COSFS 컴파일 및 설치 
설치 디렉터리에 들어가 아래 명령어를 실행해 컴파일 및 설치를 진행합니다.
```shell
cd /usr/cosfs
./autogen.sh
./configure
make
sudo make install
cosfs --version  #cosfs 버전 확인
```

운영 체제에 따라 configure 작업 시 서로 다른 안내가 표시되며, 주로 다음과 같이 나뉩니다.
- fuse 버전이 2.8.4 보다 낮은 운영 체제에서 configure 작업 시 다음과 같은 오류가 표시됩니다.
```shell
checking for common_lib_checking... configure: error: Package requirements (fuse >= 2.8.4 libcurl >= 7.0 libxml-2.0 >= 2.6) were not met:
  Requested 'fuse >= 2.8.4' but version of fuse is 2.8.3 
```
이 때에는 fuse 2.8.4 이상 버전을 직접 설치해야 하며, 설치 명령어는 다음과 같습니다.
```shell
yum -y remove fuse-devel
wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
./configure
make
make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   #fuse 커널 모듈 마운트
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   #동적 링크 라이브러리 업데이트
pkg-config --modversion fuse  #fuse 버전 확인. “2.9.4”인 경우 fuse 2.9.4 설치에 성공한 것을 의미 
```
SUSE 시스템에서 직접 fuse 2.8.4 이상 버전을 설치할 경우 설치 명령어는 다음과 같습니다.
>설치 시 `example/fusexmp.c` 파일의 222행 내용을 주석으로 처리해야 하며, 그렇지 않을 경우 make 오류가 발생합니다. `/*content*/`와 같은 방법으로 주석 처리합니다.

	```shell
	zypper remove fuse libfuse2
	wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
	tar -zxvf fuse-2.9.4.tar.gz
	cd fuse-2.9.4
	./configure
	make 
	make install
	export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
	modprobe fuse   #fuse 커널 모듈 마운트
	echo "/usr/local/lib" >> /etc/ld.so.conf
	ldconfig   #동적 링크 라이브러리 업데이트
	pkg-config --modversion fuse  #fuse 버전 확인. “2.9.4”인 경우 fuse2.9.4 설치에 성공한 것을 의미 
	```

- macOS에서 configure 작업 시 다음과 같은 오류가 표시될 수 있습니다.
```shell
configure: error: Package requirements (fuse >= 2.7.3 libcurl >= 7.0 libxml-2.0 >2.6 libcrypto >= 0.9) were not met
No package 'libcrypto' found
```
이 경우, PKG_CONFIG_PATH 변수를 설정하여 pkg-config 툴이 openssl을 찾을 수 있도록 설정해야 합니다. 명령어는 다음과 같습니다.
```shell
brew info openssl 
export PKG_CONFIG_PATH=/usr/local/opt/openssl/lib/pkgconfig #바로 위 명령어의 안내 정보에 따라 이 명령어를 수정해야 할 수 있습니다.
```

### COSFS 사용 방법

#### 1. 키 파일 설정
파일 `/etc/passwd-cosfs`에 버킷 이름(형식: &lt;BucketName-APPID&gt; 및 해당 버킷에 해당하는 &lt;SecretId&gt;와 &lt;SecretKey&gt; 입력하고, 세 항목 간에는 반각 세미 콜론을 사용해 분리합니다. 또한 키 노출을 방지하기 위해 COSFS는 키 파일 권한을 640으로 설정하도록 요구합니다. `/etc/passwd-cosfs` 키 파일을 설정하는 명령 형식은 다음과 같습니다.
```shell
sudo su  # root 자격으로 전환하여 /etc/passwd-cosfs 파일 수정, 이미 root 사용자인 경우 해당 행 명령어를 실행할 필요 없음
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>&lt;BucketName-APPID&gt;, &lt;SecretId&gt;, &lt;SecretKey&gt;를 사용자의 정보로 대체
>- Bucket 이름 생성 규범은 [버킷 이름 생성 규범](https://intl.cloud.tencent.com/document/product/436/13312)을 참조하십시오.
>- &lt;SecretId&gt;와 &lt;SecretKey&gt;는 액세스 관리 콘솔의 [Tencent Cloud API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 획득할 수 있습니다.
>이 외에도, 키를 $HOME/.passwd-cosfs에 넣거나 -opasswd_file=[path]를 통해 키 파일 경로를 지정하는 경우 키 파일 권한을 600으로 설정해야 합니다.

**예시:**

```shell
echo examplebucket-1250000000:AKIDHTVVaVR6e3:PdkhT9e2rZCfy6 > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

#### 2. 툴 실행
다음 명령 라인을 사용하여 키 파일에 정보를 설정한 버킷을 특정 디렉터리에 마운트할 수 이습니다.

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=<CosDomainName> -odbglevel=info -oallow_other
```
이 중에서,
- &lt;MountPoint&gt;는 로컬 마운트 디렉터리(예: `/mnt`)입니다.
- &lt;CosDomainName&gt;은 버킷의 해당 액세스 도메인으로, 형식은 `http://cos.<Region>.myqcloud.com`(XML API에 적용하며, 해당 매개변수에 버킷 이름을 삽입하면 안됨)입니다. 여기에서 &lt;Region&gt;는 리전 약자(예: ap-guangzhou, eu-frankfurt 등)로, 리전에 대한 자세한 정보는 [가용 리전](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오.
- -odbglevel은 로그 레벨을 지정합니다.
- -oallow_other는 마운트하지 않은 사용자가 마운트 폴더에 액세스하는 것을 허용함을 의미입니다.

**예시:**

```shell
mkdir -p /mnt/cosfs
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -onoxattr -oallow_other
```

>v1.0.5 이전 버전의 COSFS 마운트 명령어는 다음과 같습니다.
```shell
cosfs <APPID>:<BucketName> <MountPoint> -ourl=<CosDomainName> -oallow_other
```
v1.0.5 이전 버전 COSFS의 설정 파일 형식은 다음과 같습니다.
```shell
<BucketName>:<SecretId>:<SecretKey>
```

#### 3. 버킷 언마운트

버킷 언마운트 예시:

```shell
방법1: fusermount -u /mnt, fusermount 명령어는 FUSE 파일 시스템을 언마운트하는 데 사용합니다. 
방법2: umount -l /mnt는 프로그램 레퍼런스 파일 시스템에 파일이 있을 때 언마운트를 실행하면 오류가 발생하지 않으며, 프로그램 레퍼런스가 없을 때 언마운트를 완료합니다.
방법3: umount /mnt는 프로그램 레퍼런스 파일 시스템에 파일이 있을 때 언마운트를 실행하면 오류가 발생합니다.
```

## 자주 사용하는 마운트 옵션

#### -omultipart_size=[size]
멀티파트 업로드 시 단일 블록의 크기(단위: MB)를 지정하는 데 사용하며, 기본값은 10MB입니다. 멀티파트 업로드는 단일 파일에 대한 최대 블록 수 제한(10000개)이 있어 100GB(10MB \* 10000)를 초과하는 파일은 구체적인 상황에 따라 매개변수를 조정해야 합니다.

#### -oallow_other
다른 사용자가 마운트 폴더에 액세스하는 것을 허용할 경우 COSFS 실행 시 해당 매개변수를 지정하면 됩니다.

#### -odel_cache
기본적으로 COSFS는 성능을 최적화하기 위해 umount 후, 로컬의 캐시 데이터를 삭제하지 않습니다. COSFS 로그아웃 시 자동으로 캐시를 삭제하고 싶은 경우 마운트 시 해당 옵션을 추가하면 됩니다.

####  -onoxattr
getattr/setxattr 기능을 비활성화합니다. 1.0.9 이전 버전의 COSFS는 확장 속성 설정 및 획득을 제공하지 않으며, 마운트 시 use_xattr 옵션을 사용하였다면 mv 파일을 Bucket에 저장할 때 실패합니다.


#### -opasswd_file=[path]
해당 옵션으로 COSFS 키 파일이 존재하는 경로를 지정할 수 있으며, 해당 옵션에서 설정한 키 파일은 권한을 600으로 설정해야 합니다.

#### -odbglevel=[dbg|info|warn|err|crit]

COSFS 로그 기록 레벨을 설정하며 info, dbg, warn, err, crit 중 선택할 수 있습니다. 환경 생성 시 info로 설정하는 것을 권장하며, 디버깅 시 dbg로 설정하는 것을 권장합니다. 시스템 로그가 정기적으로 삭제를 진행하지 않고 대량의 액세스로 인해 많은 로그가 생성되는 경우 err 또는 crit로 설정할 수 있습니다.

#### -oumask=[perm]

해당 옵션으로 사용자 지정 유형 사용자의 마운트 디렉터리 내 파일에 대한 작업 권한을 삭제할 수 있습니다. 예를 들어, -oumask=755를 실행하는 경우 해당 마운트 디렉터리의 권한을 022로 변경합니다.

#### -ouid=[uid]
해당 옵션으로 사용자 id가 [uid]인 사용자에게 마운트 디렉터리의 파일 권한 제한을 받지 않고 모든 파일을 액세스할 수 있도록 허용할 수 있습니다.
사용자 uid를 획득하기 위해서는 id 명령어를 사용하며, 형식은 ` id -u username`과 같습니다. 예를 들어, `id -u user_00`을 실행하면 사용자 user_00의 uid를 획득할 수 있습니다.


## FAQ
COSFS 툴 사용 중 문의 사항이 있는 경우 [COSFS 툴 관련 FAQ](https://intl.cloud.tencent.com/document/product/436/30587)를 참조하십시오.
