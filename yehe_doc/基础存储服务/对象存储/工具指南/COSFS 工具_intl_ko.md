## 기능 설명 

COSFS 툴은 Cloud Object Storage(COS) 버킷을 로컬로 마운트하는 기능을 제공하여 로컬 파일 시스템을 사용하듯이 직접 Tencent Cloud COS에 있는 객체를 조작할 수 있습니다. COSFS는 다음과 같은 주요 기능을 제공합니다.
- POSIX 파일 시스템의 대부분 기능 지원. 예: 파일 읽기/쓰기, 디렉터리 작업, 링크 작업, 권한 관리, uid/gid 관리 등의 기능
- 대용량 파일 멀티파트 전송 기능
- MD5 데이터 검증 기능
- 로컬 기기의 데이터를 COS로 업로드하는 경우 [COS Migration 툴](https://intl.cloud.tencent.com/document/product/436/15392) 또는 [COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976) 사용을 권장합니다.

## 제한성
**COSFS는 S3FS를 기반으로 합니다. COSFS 읽기 및 쓰기 작업에는 디스크가 필요하므로 COSFS는 마운트된 파일의 간단한 관리에만 적합하지만 로컬 파일 시스템의 모든 기능을 지원하지는 않습니다. CSG(Tencent Cloud Storage Gateway)를 사용하여 COS에 액세스하는 것이 좋습니다. CSG는 네트워크 파일 시스템을 사용하여 여러 서버에 COS 버킷을 마운트할 수 있습니다. 사용자는 POSIX 파일 프로토콜을 사용하여 마운트 포인트를 통해 COS에서 객체를 읽고 쓸 수 있습니다.** COSFS를 사용하려면 다음 사항에 유의하십시오.

- 랜덤 또는 추가 파일 작성 시 전체 파일을 다운로드하고 재업로드합니다. Bucket과 동일한 리전의 CVM을 사용해 파일의 업로드 및 다운로드 속도를 높일 수 있습니다.
- 여러 클라이언트에 동일한 COS 버킷을 마운트하는 경우 사용자가 자체적으로 각 클라이언트를 조정하는 행위에 종속됩니다. 예: 여러 클라이언트에서 동일한 파일 쓰기 방지 등
- 파일/폴더의 rename 작업에는 원자성(Atomicity)이 없습니다.
- list directory와 같은 메타데이터 작업은 원격으로 COS 서버에 액세스해야 하므로 성능이 비교적 떨어집니다.
- hard link를 지원하지 않아 동시 읽기/쓰기량이 많은 시나리오에 적합하지 않습니다.
- 한 개의 마운트 포인트에 파일을 동시에 마운트 및 언마운트할 수 없습니다. 먼저 cd 명령어를 사용하여 다른 디렉터리로 전환한 후, 다시 마운트 포인트에 마운트와 언마운트 작업을 진행할 수 있습니다.

## 사용 환경
Ubuntu, CentOS, SUSE, macOS 주요 시스템을 지원합니다.


## 설치 방법
COSFS는 패키지 방식과 컴파일 소스 코드 방식의 두 가지 설치 방법을 제공합니다.


### 방법1: 패키지로 설치하기
>? 해당 방법은 Ubuntu, CentOS 주요 시스템을 지원합니다.
>

#### Ubuntu 시스템

1. 시스템 버전에 따라 해당하는 설치 패키지를 선택합니다. 현재 지원하는 Ubuntu 릴리스 버전은 Ubuntu14.04, Ubuntu16.04, Ubuntu18.04, Ubuntu20.04를 포함합니다.
Github 다운로드 링크:
```plaintext
#Ubuntu14.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu14.04_amd64.deb
#Ubuntu16.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu16.04_amd64.deb
#Ubuntu18.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu18.04_amd64.deb
#Ubuntu20.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu20.04_amd64.deb
```
CDN 다운로드 링크:
[cosfs_1.0.20-ubuntu14.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu14.04_amd64.deb)
[cosfs_1.0.20-ubuntu16.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu16.04_amd64.deb)
[cosfs_1.0.20-ubuntu18.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu18.04_amd64.deb)
[cosfs_1.0.20-ubuntu20.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu20.04_amd64.deb)

2. 설치. (예시: Ubuntu16.04).
```shell
sudo dpkg -i cosfs_1.0.20-ubuntu16.04_amd64.deb
```

#### CentOS 시스템

1. 종속 설치
```plaintext
sudo yum install  libxml2-devel libcurl-devel -y
```
2. 시스템 버전에 따라 해당하는 설치 패키지를 선택합니다. 현재 지원하는 CentOS 릴리스 버전은 CentOS6.5, CentOS7.0을 포함합니다.
Github 다운로드 링크:
```plaintext
#CentOS6.5
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs-1.0.20-centos6.5.x86_64.rpm
#CentOS7.0
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs-1.0.20-centos7.0.x86_64.rpm
```
CDN 다운로드 링크:
[cosfs-1.0.20-centos6.5.x86_64.rpm](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs-1.0.20-centos6.5.x86_64.rpm)
[cosfs-1.0.20-centos7.0.x86_64.rpm](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs-1.0.20-centos7.0.x86_64.rpm)
3. 설치. (예시: CentOS7.0)
```shell
sudo rpm -ivh cosfs-1.0.20-centos7.0.x86_64.rpm
```
>? 설치 시 오류가 보고되고 `conflicts with file from package fuse-libs-*`가 표시되는 경우, `--force` 매개변수를 추가한 후 다시 설치합니다.
>

### 방법2: 컴파일 소스 코드로 설치하기

>? 해당 방법은 Ubuntu, CentOS, SUSE, macOS 주요 시스템을 지원합니다.
>


#### 1. 종속 소프트웨어 설치 
COSFS의 컴파일 설치는 automake, git, libcurl-devel, libxml2-devel, fuse-devel, make, openssl-devel 등의 소프트웨어 패키지에 종속됩니다. Ubuntu, CentOS, SUSE, macOS의 종속 소프트웨어 설치 과정은 다음과 같습니다.

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
brew install cask osxfuse
```

#### 2. 소스 코드 획득 

GitHub에서 [COSFS 소스 코드](https://github.com/tencentyun/cosfs)를 지정 디렉터리로 다운로드합니다. 다음은 디렉터리를 `/usr/cosfs`로 지정한 예시이며, 실제 작업 시 구체적인 작업 환경에 따라 디렉터리를 선택하시기 바랍니다.
```shell
sudo git clone https://github.com/tencentyun/cosfs /usr/cosfs
```


#### 3. COSFS 컴파일 및 설치 
설치 디렉터리로 이동하여 다음 명령어를 실행해 컴파일 및 설치를 진행합니다.
```shell
cd /usr/cosfs
sudo ./autogen.sh
sudo ./configure
sudo make
sudo make install
cosfs --version  #cosfs 버전 넘버 조회
```

#### 4. Configure 작업 문제 처리

운영 체제에 따라 configure 작업 시 서로 다른 안내가 표시됩니다. fuse 버전이 2.8.4 보다 낮은 운영 체제에서는 configure 작업 시 다음과 같은 오류가 보고됩니다.
```shell
checking for common_lib_checking... configure: error: Package requirements (fuse >= 2.8.4 libcurl >= 7.0 libxml-2.0 >= 2.6) were not met:
  Requested 'fuse >= 2.8.4' but version of fuse is 2.8.3 
```
이 경우, fuse 2.8.4 이상 버전을 직접 설치해야 하며 설치 명령어 예시는 다음과 같습니다.
```shell
sudo yum -y remove fuse-devel
sudo wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
sudo ./configure
sudo make
sudo make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   #fuse 커널 모듈 마운트
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   #동적 링크 라이브러리 업데이트
pkg-config --modversion fuse  #fuse 버전 넘버 조회, “2.9.4”가 표시되는 경우 fuse 2.9.4 설치가 완료되었다는 의미입니다. 
```
- SUSE 시스템에서는 fuse 2.8.4 이상 버전을 직접 설치해야 하며 설치 명령어 예시는 다음과 같습니다.
>! 설치 시 `example/fusexmp.c` 파일의 제 222행 내용을 주석 처리해야 합니다. 주석 처리하지 않을 경우 make에 오류가 발생합니다. 주석 방법: `/*content*/` .
>
```shell
zypper remove fuse libfuse2
sudo wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
sudo ./configure
sudo make 
sudo make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   #fuse 커널 모듈 마운트
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   #동적 링크 라이브러리 업데이트
pkg-config --modversion fuse   #fuse 버전 넘버 조회. “2.9.4”가 표시되는 경우 fuse2.9.4 설치가 완료되었다는 의미입니다. 
```
- macOS에서 configure 작업 시 다음과 같은 안내가 표시될 수 있습니다.
```shell
configure: error: Package requirements (fuse >= 2.7.3 libcurl >= 7.0 libxml-2.0 >2.6 libcrypto >= 0.9) were not met
No package 'libcrypto' found
```
 이 때, PKG_CONFIG_PATH 변수를 설정하여 pkg-config 툴에서 openssl을 찾을 수 있도록 해야 합니다. 명령어는 다음과 같습니다.
```shell
brew info openssl 
export PKG_CONFIG_PATH=/usr/local/opt/openssl/lib/pkgconfig #윗줄 명령어 안내 정보에 따라 해당 명령어를 수정해야 할 수 있습니다.
```


## 사용 방법

### 1. 키 파일 설정
`/etc/passwd-cosfs` 파일에 버킷 이름(BucketName-APPID 형식), &lt;SecretId&gt; 및 &lt;SecretKey&gt;를 포함한 버킷 정보를 작성하고 콜론(:)으로 구분합니다. 키 손상을 방지하려면 COSFS 키 파일에 대한 권한을 640으로 설정합니다. 다음 명령을 실행하여 `/etc/passwd-cosfs` 키 파일을 구성합니다.
```shell
sudo su  #/etc/passwd-cosfs 파일 수정을 위해 root로 전환. root 사용자인 경우 해당 명령어는 생략합니다.
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>? &lt;&gt;의 매개변수를 사용자 정보로 변경해야 합니다.
> - &lt;BucketName-APPID&gt;는 버킷 이름 포맷입니다. 버킷 이름 생성 규칙에 대한 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오.
> - &lt;SecretId&gt; 및 &lt;SecretKey&gt;는 키 정보입니다. 위험을 줄이기 위해 서브 계정 키를 사용하고 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)에 따라 서브 계정을 승인하는 것이 좋습니다. 서브 계정 키를 얻는 방법에 대한 자세한 내용은 [Access Key](https://intl.cloud.tencent.com/document/product/598/32675)를 참고하십시오.
> - 키는 $HOME/.passwd-cosfs 파일에서 설정하거나 -opasswd_file=[path]로 키 파일 경로를 지정할 수 있으며, 키 파일의 권한 값은 600으로 설정해야 합니다.
> 

**예시:**

```shell
echo examplebucket-1250000000:AKIDHTVVaVR6e3****:PdkhT9e2rZCfy6**** > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>! V1.0.5 이하 버전 COSFS의 구성 파일 포맷은 &lt;BucketName>:&lt;SecretId>:&lt;SecretKey>입니다.
>


### 2. 툴 실행
키 파일에 설정한 버킷을 지정 디렉터리에 마운트하는 명령 라인은 다음과 같습니다.

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=http://cos.<Region>.myqcloud.com -odbglevel=info -oallow_other
```
이 중,
- &lt;MountPoint&gt;:는 로컬 마운트 디렉터리(예: `/mnt`)입니다.
- &lt;Region&gt;는 리전 약칭입니다(예시: ap-guangzhou, eu-frankfurt 등). 리전 약칭에 대한 자세한 정보는 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.
- -odbglevel은 로그 레벨을 지정합니다. 기본 값은 crit이며, 옵션값은 crit, error, warn, info, debug입니다.
- -oallow_other: 마운트되지 않은 사용자의 마운트 폴더 액세스를 허용합니다.

**예시:**

```shell
mkdir -p /mnt/cosfs
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -onoxattr -oallow_other
```

>!
>- COSFS 툴은 성능 향상을 위해 기본적으로 업로드 및 다운로드의 임시 캐시를 시스템 디스크에 저장하고 파일을 닫은 후 공간을 릴리스합니다. 동시에 열려 있는 파일의 수가 많거나 대용량 파일을 읽고 쓸 때 COSFS 툴은 성능 향상을 위해 가능한 한 많은 디스크를 사용합니다. 기본적으로 다른 프로그램에서 사용할 수 있도록 100MB의 여유 디스크 공간만 보관되어 있습니다. oensure_diskfree=[size] 옵션을 사용하여 COSFS 툴이 보관한 사용 가능한 하드 디스크 공간의 크기를 MB 단위로 설정할 수 있습니다. 예를 들어 `-oensure_diskfree=1024`인 경우 COSFS 툴은 1024MB의 여유 공간을 보관합니다.
>- V1.0.5 이하 버전 COSFS의 마운트 명령어는 cosfs &lt;APPID>:&lt;BucketName> &lt;MountPoint> -ourl=&lt;CosDomainName> -oallow_other입니다.
>


### 3. 버킷 언마운트

버킷 언마운트 예시는 다음과 같습니다.

```shell
방법1: fusermount -u /mnt, fusermount는 FUSE 파일 시스템 언마운트 전용 명령어입니다. 
방법2: umount -l /mnt, 프로그램 참고 파일 시스템에 파일이 있는 경우 언마운트 시 오류가 발생하지 않으며 프로그램 참고가 없을 때 언마운트가 완료됩니다.
방법3: umount /mnt, 프로그램 참고 파일 시스템에 파일이 있는 경우 언마운트 시 오류가 발생합니다.
```

## 주요 마운트 옵션

#### -omultipart_size=[size]
멀티파트 업로드 시 단일 파트의 크기(단위: MB)를 지정하며, 기본값은 10MB입니다. 멀티파트 업로드는 단일 파일 파트의 수량에 제한이 있어(최대 10000개) 100GB(10MB \* 10000) 이상의 파일인 경우 구체적인 상황에 따라 해당 매개변수를 조정해야 합니다.

#### -oallow_other
다른 사용자에게 마운트 폴더 액세스를 허용할 경우 COSFS 실행 시 해당 매개변수를 지정합니다.

#### -odel_cache
기본적으로 COSFS 툴은 성능 최적화를 위해 umount 후 로컬의 캐시 데이터를 삭제하지 않습니다. COSFS 로그아웃 시 캐시를 자동 삭제하려는 경우 마운트할 때 이 옵션을 추가합니다.

####  -onoxattr
getattr/setxattr 기능을 비활성화합니다. COSFS 1.0.9 이전 버전은 확장 속성을 설정하거나 획득할 수 없습니다. 마운트 시 use_xattr 옵션을 사용한 경우 mv 파일을 Bucket에 업로드 시 실패가 발생할 수 있습니다.

#### -opasswd_file=[path]
이 옵션으로 COSFS 키 파일의 소재 경로를 지정할 수 있습니다. 이 옵션 설정의 키 파일은 권한을 600으로 설정해야 합니다.

#### -odbglevel=[dbg|info|warn|err|crit]

COSFS 로그 기록 레벨을 설정합니다. info, dbg, warn, err, crit 중에서 선택할 수 있으며, 생성 환경은 info로 설정하고 디버깅 시에는 dbg로 설정하는 것을 권장합니다. 시스템 로그를 정기적으로 정리하지 않고 액세스량이 매우 많아 대량의 로그가 생성되는 경우 err 또는 crit로 설정할 수 있습니다.

#### -oumask=[perm]

이 옵션으로 특정 유형 사용자의 마운트 디렉터리 내 파일 작업 권한을 삭제할 수 있습니다. 예를 들어, -oumask=755로 설정하는 경우 해당 마운트 디렉터리의 권한이 022로 변경됩니다.

#### -ouid=[uid]
이 옵션으로 사용자 ID가 [uid]인 사용자가 마운트 디렉터리 내 파일 권한 제한에 영향을 받지 않고 마운트 디렉터리의 모든 파일에 액세스할 수 있도록 허용할 수 있습니다.
사용자의 uid는 ID 명령어를 사용하여 획득할 수 있으며, 포맷은 ` id -u username`입니다. 예를 들어, `id -u user_00`을 실행하는 경우 사용자 user_00의 uid를 획득할 수 있습니다.

#### -oensure_diskfree=[size]

COSFS 툴은 성능 향상을 위해 기본적으로 업로드 및 다운로드의 임시 캐시를 시스템 디스크에 저장하고 파일을 닫은 후 공간을 릴리스합니다. 동시에 열려 있는 파일의 수가 많거나 대용량 파일을 읽고 쓸 때 COSFS 툴은 성능 향상을 위해 가능한 한 많은 디스크를 사용합니다. 기본적으로 다른 프로그램에서 사용할 수 있도록 100MB의 여유 디스크 공간만 보관되어 있습니다. oensure_diskfree=[size] 옵션을 사용하여 COSFS 툴이 예약한 사용 가능한 하드 디스크 공간의 크기를 MB 단위로 설정할 수 있습니다. 예를 들어 `-oensure_diskfree=1024`인 경우 COSFS 도구는 1024MB의 여유 공간을 보관합니다.


## FAQ
COSFS 툴 사용 중 문의 사항이 있는 경우 [COSFS 툴 FAQ](https://intl.cloud.tencent.com/document/product/436/30587)를 참고하십시오.
