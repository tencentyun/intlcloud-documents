## 기능 문의

### 임시 키를 사용하여 버킷을 마운트하는 방법은 무엇입니까?

임시 키(STS)를 사용하여 버킷을 마운트하는 방법은 다음 두 단계를 진행해야 합니다.

1단계: 임시 키 설정파일을 생성합니다. 예를 들어 /tmp/passwd-sts에 COSFS에 사용하는 명령어 선택 항목 -opasswd-file=\[path\]로 키 구성 파일을 지정합니다. 임시 키 관련 개념은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오. 임시 키 구성 파일 예시는 다음과 같습니다.
```shell
COSAccessKeyId=AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX  #이하 임시 키 Id, Key, Token 문자열
COSSecretKey=GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY
COSAccessToken=109dbb14ca0c30ef4b7e2fc9612f26788cadbfac3
COSAccessTokenExpire=2017-08-29T20:30:00  #임시 token 기간 만료는 GMT 시간을 기준으로 하며, 포맷은 예시와 일치해야 합니다.
```
이 중, COSFS는 COSAccessTokenExpire에 설정된 시간에 따라 다시 키 파일에서 설정을 로딩해야 하는지 여부를 판단합니다.

>!COSFS에서는 키 유출 방지를 위해 키 파일 권한을 600으로 설정할 것을 요구합니다. 실행 명령어는 다음과 같습니다.
><pre><code class="language-shell">chmod 600 /tmp/passwd-sts</code></pre>
>
2단계: COSFS 명령어를 실행합니다. 명령어 선택 항목 -ocam_role=[role]을 사용해 sts 역할을 지정하고, -opasswd_file=[path]로 키 파일 경로를 지정합니다. 예시는 다음과 같습니다.
```shell
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oallow_other -ocam_role=sts -opasswd_file=/tmp/passwd-sts
```

### COSFS에서 제공하는 마운트 매개변수 선택 항목 및 버전은 어떻게 확인합니까?

`cosfs --help` 명령어를 사용하여 COSFS에서 제공하는 매개변수 선택 항목을 확인할 수 있으며, `cosfs --version` 명령어를 사용하여 COSFS 버전을 확인할 수 있습니다.

### COSFS에 생성되는 로그는 어떻게 확인합니까?

CentOS의 경우 COSFS에 생성되는 로그는 /var/log/messages에 저장되며, Ubuntu의 경우 /var/log/syslog에 저장됩니다. 사용 중 문제가 발생할 경우 해당 시간의 로그를 보내주시기 바랍니다.

### 버킷에 있는 디렉터리 1개를 어떻게 마운트합니까?

마운트 명령어 실행 시 버킷에 있는 디렉터리 1개를 지정하면 됩니다. 명령어는 다음과 같습니다.
```shell
cosfs examplebucket-1250000000:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```
>! my-dir는 반드시 `/`로 시작해야 합니다.
>
v1.0.5 이전 버전을 사용하는 경우 마운트 명령어는 다음과 같습니다.
```shell
cosfs 1250000000:examplebucket:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

### 루트 사용자가 아닌 경우 COSFS를 어떻게 마운트합니까?

루트 사용자가 아닌 경우 개인 Home 디렉터리에 .passwd-cosfs 파일을 생성하는 것을 권장하며, 권한을 600으로 설정하면 정상적인 명령어에 따라 마운트됩니다. 이외에도 -opasswd_file=path 선택 항목을 통해 키 파일의 경로를 지정하고 권한을 600으로 설정하는 방법이 있습니다.

### COSFS는 HTTPS에 마운트를 지원합니까?

COSFS는 HTTPS를 지원하며 HTTP와 HTTPS 사용 방법은 다음과 같이 나뉩니다.
```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
-ourl=https://cos.ap-guangzhou.myqcloud.com
```

libcurl에 종속되는 NSS 라이브러리는 3.12.3 이상 버전(`curl -V` 명령어를 사용해 NSS 버전 확인)으로, HTTPS 방식으로 버킷을 마운트하는 경우 다음 명령어를 실행해야 합니다.

```shell
echo "export NSS_STRICT_NOFORK=DISABLED" >> ~/.bashrc
source ~/.bashrc
```

### COSFS 시작 시 자동 마운트는 어떻게 설정합니까?

/etc/fstab 파일에 다음 내용을 추가합니다. 이 중, _netdev 선택 항목은 네트워크 준비가 완료된 후 현재 명령어를 다시 실행하게 합니다.

```shell
cosfs#examplebucket-1250000000 /mnt/cosfs fuse _netdev,allow_other,url=http://cos.ap-guangzhou.myqcloud.com,dbglevel=info
```

### 여러 버킷을 어떻게 마운트합니까?

여러 버킷을 동시에 마운트해야 하는 경우 /etc/passwd-cosfs 구성 파일에서 마운트할 버킷별로 라인을 입력합니다. 라인별 내용 형식은 단일 버킷을 마운트할 때 정보와 동일하며, 예시는 다음과 같습니다.

```shell
echo examplebucket-1250000000:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
echo log-1250000000:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
```

### 마운트 후 어떻게 기기 상의 다른 계정으로 이미 마운트한 디렉터리를 액세스할 수 있도록 합니까?

권한을 개방하고 싶은 경우 마운트 시 `-oallow_other`를 지정합니다.

### COSFS 마운트 디렉터리에 파일 생성 시 이름 제한이 있습니까?

COSFS 마운트 디렉터리에 `/` 문자가 포함되지 않는 이름의 파일을 생성 및 삭제할 수 있습니다. Unix 시스템 상에서 `/` 문자는 디렉터리 세퍼레이터이므로 COSFS 마운트 디렉터리에 `/` 문자가 포함된 파일을 생성할 수 없습니다. 이외에도 특수문자가 포함된 파일 생성 시 특수 문자가 shell에 사용되어 파일 생성에 실패하는 문제가 발생할 수 있으니 유의해야 합니다.

### COSFS에서 파일 존재 여부를 어떻게 판단하나요?

COSFS 내부 로직에서 Head 요청으로 상위 디렉터리 및 파일의 존재 여부를 판단합니다.


### COSFS 스토리지 사용량을 확인하는 방법은 무엇입니까?
COSFS는 스토리지 사용량 직접 조회를 지원하지 않습니다. COS 버킷의 스토리지 용량을 계산하려면 데이터 볼륨이 비교적 작은 시나리오의 경우 COS 콘솔에 로그인하여 확인하시고, 데이터 볼륨이 큰 시나리오의 경우 [리스트](https://intl.cloud.tencent.com/document/product/436/30622) 기능을 사용하시기 바랍니다.



## 장애 진단

### COSFS 사용 중 갑자기 "unable to access MOUNTPOINT /path/to/mountpoint: Transport endpoint is not connected"가 표시되고 다시 액세스할 수 없습니다.

`ps ax|grep cosfs` 명령어를 사용하여 COSFS 프로세스가 존재하는지 확인할 수 있습니다. COSFS 프로세스가 오작동으로 종료된 경우 다음 명령어를 실행하여 다시 마운트할 수 있습니다.

```shell
umount -l /path/to/mnt_dir
cosfs examplebucket-1250000000:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

COSFS 프로세스가 오작동으로 종료된 게 아닌 경우 기기 상의 fuse 버전이 2.9.4 이하인지 확인합니다. libfuse가 2.9.4 버전 이하인 경우 COSFS 프로세스에 오류가 발생하여 종료될 수 있습니다. 이 경우 [COSFS 툴](https://intl.cloud.tencent.com/document/product/436/6883) 문서를 참고하여 fuse 버전을 업데이트하거나 COSFS 최신 버전 설치를 권장합니다.

### COSFS를 통해 업로드한 파일의 Content-Type이 "application/octet-stream"으로 변경되었습니다. 어떻게 해야 합니까?

COSFS는 /etc/mime.types에 따라 업로드 파일의 확장자명을 비교하여 COSFS에 업로드하는 파일의 Content-Type을 자동으로 설정합니다. Content-Type 문제가 발생하는 경우 시스템 상에 해당 구성 파일이 존재하는지 확인하시기 바랍니다. Ubuntu인 경우 sudo apt-get install mime-support를 통해 추가할 수 있으며, CentOS인 경우에는 sudo yum install mailcap를 통해 추가할 수 있습니다. 또한 수동으로 해당 파일을 생성할 수 있으며 모든 파일 포맷에 대해 다음과 같이 라인을 추가합니다.

```shell
image/jpeg                                      jpg jpeg
image/jpm                                       jpm jpgm
image/jpx                                       jpx jpf
```

### 마운트 시 Bucket not exist가 표시됩니다.

매개변수 -ourl을 확인하여 URL에 버킷 부분이 포함되어 있지 않은지 확인합니다. 정확한 형식은 다음과 같습니다.

```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
```

### 이전에는 쓰기가 가능했던 파일이 갑자기 쓰기가 허용되지 않습니다.

COS 제품 인증 정책이 변경되어 V1.0.0 이전 버전의 COSFS 툴을 사용하는 경우 정책 인증에 실패하게 됩니다. 최신 COSFS 툴을 설치하여 다시 마운트하시기 바랍니다.

### COSFS 툴 사용 중 Input/Output ERROR 등의 오류가 발생합니다. 어떻게 디버깅해야 합니까?

먼저 다음 순서에 따라 점검하여 문제를 확인하십시오.

1. 기기가 정상적으로 COS 도메인에 액세스되는지 확인합니다.
2. 계정이 정확하게 설정되어 있는지 확인합니다. 
3. cp 명령어를 사용해 복사하고 -p 또는 -a 매개변수가 있는 경우, 해당 매개변수를 제거한 후 해당 명령어를 실행합니다.

위의 설정이 올바른지 확인한 후 기기에서 `/var/log/messages` 로그 파일을 열어 s3fs 관련 로그를 확인합니다. 로그는 문제의 원인을 파악하는데 도움이 됩니다. 문제를 해결할 수 없는 경우 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하십시오.

### /etc/fstab을 사용하여 COSFS 시작 시 자동 마운트를 설정하였는 데 mount -a 실행 시 "wrong fs type, bad option，bad superblock on cosfs" 오류가 발생합니다.
해당 오류는 일반적으로 사용자 기기에 fuse 라이브러리가 존재하지 않아 발생합니다. 다음 명령어를 실행하여 fuse 라이브러리를 설치하십시오.
- CentOS
```shell
sudo yum install fuse
```
- Ubuntu
```shell
sudo apt-get install fuse
```

### 시스템 로그 /var/log/messages에서 대량의 404 에러 코드를 발견했습니다. 정상입니까?
COSFS 내부 로직 중 Head 요청으로 상위 디렉터리 및 파일이 존재하는지 여부를 판단하며, 해당 404 오류는 프로그램 실행 오류를 의미하지 않습니다.

### COS에서 파일 크기가 0으로 보이는 이유는 무엇입니까?
일반적으로 COSFS로 데이터를 쓸 때 먼저 COS에 크기가 0인 파일을 생성하고 데이터를 로컬 캐시 파일에 입력합니다.
쓰기 과정에서 해당 마운트 포인트 Is 명령어의 결과로 파일 크기가 변경되며, 파일을 닫을 때 COSFS가 로컬 캐시 파일 상에 입력한 데이터를 COS에 업로드합니다. 업로드 실패한 경우에만 크기가 0인 파일을 볼 수 있으며, 이 경우 실패한 파일을 다시 복사해 보시기 바랍니다.

### COSFS 캐시 디렉터리 파일과 COS 상의 파일이 일치하지 않습니다. 직접 사용할 수 있습니까?
직접 사용할 수 없습니다. 캐시 디렉터리 상의 파일은 COSFS 내부 가속 읽기/쓰기에 사용하는 파일로 COS 상에 있는 파일의 일부만 존재할 수 있습니다.

### rsync 명령어를 사용하여 파일을 COSFS에 복사하고 진행 상황이 이미 100%로 표시되는데 서버에 임시 파일만 보입니다. 어떻게 된 겁니까?
rsync 명령어가 마운트 디렉터리에 있어 임시 파일을 생성하게 되며, 진행 상황이 100%로 표시되는 것은 임시 파일이 로컬에 입력을 100% 완료했다는 의미입니다. 임시 파일 쓰기 완료 후에 COS에 업로드되며 다른 이름으로 변경하여 복사됩니다.
일반적으로 COSFS 마운트 디렉터리에 데이터를 복사하는 경우 rsync 명령어를 사용하여 cp 명령어에 비해 더 많은 시간이 소요될 수 있습니다.

### COSFS의 디스크 공간이 거의 꽉 찼습니다. 어떻게 처리해야 합니까? 
COSFS의 업로드/다운로드는 모두 디스크 파일 캐시를 사용하여 업로드/다운로드 시 -oensure_diskfree=[size] 매개변수를 지정하지 않은 경우 캐시 파일이 존재하는 디스크가 꽉 찰 수 있습니다. 캐시 파일이 존재하는 디스크의 남은 용량이 [size] MB 이하인 경우 COSFS가 최대한 디스크 사용 용량(단위: MB)을 줄일 수 있도록 -oensure_diskfree를 통해 매개변수를 지정하십시오. -ouse_cache=[path] 매개변수를 지정한 경우 캐시 파일은 path 디렉터리 안에 있으며, 지정하지 않은 경우 /tmp 디렉터리 안에 있습니다.

예시: 남은 디스크 용량이 10GB 이하인 경우 COSFS가 디스크 용량 사용을 줄이게 하는 명령어는 다음과 같습니다.
```shell
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oensure_diskfree=10240
```

### docker를 사용하여 COSFS 마운트 시 fuse: failed to open /dev/fuse: Operation not permitted 오류가 발생합니다. 어떻게 처리해야 합니까?
docker 미러링 실행 시 매개변수 --privileged를 추가해야 합니다.

### 특정 디렉터리를 멀티 마운트 포인트의 공용 캐시 디렉터리로 사용할 수 있습니까?
멀티 마운트 포인트의 공용 캐시 디렉터리 사용은 권장하지 않습니다. 캐시 디렉터리에는 COSFS를 사용하는 메타 정보가 포함되어 있어 공용으로 사용하는 경우 COSFS에서 사용하는 메타 정보에 혼란이 발생할 수 있습니다.

### COSFS 마운트 사용 시 /bin/mount:unrecognized option --no-canonicalize 오류가 발생합니다. 어떻게 처리해야 합니까?

비교적 낮은 버전의 mount는 `--no-canonicalize` 선택 항목을 지원하지 않습니다. mount 툴을 업데이트(v2.17 버전 권장, [다운로드]((https://cdn.kernel.org/pub//linux/utils/util-linux/v2.17/))한 후 다시 마운트하십시오. 설치 명령어는 다음과 같습니다.

```shell
tar -jxvf util-linux-ng-2.17.tar.bz2
cd util-linux-ng-2.17
./configure --prefix=/usr/local/util-linux-ng
make && make install
mv /bin/mount{,.off}
ln -s /usr/local/util-linux-ng/bin/mount /bin
```

### 마운트에 실패하면 어떻게 해야 합니까?

1단계: 로그 파일 및 안내 정보에 따라 마운트 명령어, 키 구성 파일 내용이 정확한지, 네트워크가 COS 서비스에 액세스할 수 있는지 확인합니다.

2단계: date 명령어를 사용하여 기기 시간이 정확한지 확인하고, 정확하지 않은 경우 date 명령어를 사용하여 시간을 수정한 후 다시 마운트 합니다. 예시: `date -s '2014-12-25 12:34:56'`

### `ls -l --time-style=long-iso` 명령어를 사용했는데 마운트 디렉터리 시간이 1970-01-01 08:00로 변경됐습니다. 정상입니까?

마운트 디렉터리 시간이 1970-01-01 08:00로 변경된 것은 정상적인 현상입니다. 마운트 포인트를 삭제하면 마운트 디렉터리 시간이 마운트 전 시간으로 복구됩니다.

 ### 마운트 디렉터리가Mount 비어 있지 않아도 됩니까?

`-ononempty` 매개변수를 사용하여 비어 있지 않은 디렉터리로 마운트할 수 있습니다. 그러나 비어 있지 않은 디렉터리에 마운트하는 것은 권장하지 않으며, 마운트 포인트와 원본 디렉터리에 동일한 경로의 파일이 존재하는 경우 문제가 발생할 수 있습니다.

### COSFS 디렉터리에서 Is 명령어를 실행하면 명령어 리턴 시간이 오래 걸리는 이유는 무엇입니까?
마운트 디렉터리에 파일이 많은 상황에서 Is 명령어를 실행하면 디렉터리 상의 모든 파일에 대해 HEAD 작업을 진행하게 됩니다. 따라서 비교적 많은 시간을 소모하여 디렉터리 시스템의 호출을 읽은 후 리턴하게 됩니다.
>!불필요한 재시작이 발생할 수 있어 IO hung 활성화는 권장하지 않습니다.
>


### info 레벨의 로그를 사용하여 생성되는 시스템 로그 파일이 스토리지 용량을 너무 많이 차지합니다. 어떻게 처리해야 합니까?
정기적으로 생성되는 시스템 로그 파일을 삭제하거나 `-odbglevel=crit`를 사용하여 마운트하는 등 로그 레벨을 높게 조정할 수 있습니다.


### COSFS는 어떤 시나리오에 적용할 수 있습니까? 읽기 및 쓰기 성능은 어떻습니까?
COSFS의 읽기 및 쓰기는 모두 디스크를 경유하여 전송되며, 공유 데이터 세트의 머신러닝 알고리즘에서 공유 데이터 읽고 간단하게 로그를 백업하는 등의 POSIX semantics를 요구하여 COS에 액세스하는 시나리오에 적용할 수 있습니다. COSFS는 멀티 스레드를 사용하여 동시 업로드 및 다운로드 시 가속을 진행하며 리전 내에서 내부 네트워크로 순차적으로 6GB의 파일 읽기에 소모되는 시간은 약 80s입니다. 순차적으로 6GB의 파일 쓰기에 소모되는 시간은 약 160s이며, 일반적으로 SDK와 멀티 스레드 등의 기술을 통해 더 높은 성능을 실현할 수 있습니다.

>! 파일 읽기/쓰기 시 발생하는 대량의 시스템 호출은 대량의 로그가 수반되어 COSFS 읽기/쓰기 성능에 영향을 미칩니다. 비교적 높은 성능이 필요한 경우 -odbglevel=warn 또는 더 높은 로그 레벨을 지정할 수 있습니다.
>

### COSFS RPM 패킷 설치 후 COSFS를 찾을 수 없다는 알림이 표시됩니다. 어떻게 해야 하나요?

cosfs 설치 경로는 /usr/local/bin입니다. cosfs를 찾을 수 없다는 알림이 표시되는 경우, 해당 경로가 PATH 환경 변수에 없기 때문일 수 있으므로 먼저 `~/.bashrc`에 행 설정을 추가해야 합니다.
```shell
export PATH=/usr/local/bin:$PATH
```
명령어 재실행:
```shell
source ~/.bashrc
```

### COSFS RPM 패킷 설치 후, conflicts with file from package fuse-libs-\*가 표시됩니다. 어떻게 해야 하나요?

 COSFS RPM 패킷 설치 치 옵션 `--force`를 추가합니다.
```shell
rpm -ivh cosfs-1.0.19-centos7.0.x86_64.rpm --force
```

### COFS에서 특정 디렉터리에 읽기 전용 권한을 부여했는데 단독 마운트에 해당하는 디렉터리에 권한이 없다고 표시됩니다.

COSFS에 루트 디렉터리의 GetBucket 권한이 필요하므로, 루트 디렉터리의 GetBucket 권한 및 해당 디렉터리의 읽기 권한을 추가해야 합니다. 이 경우 기타 디렉터리를 나열할 수 있으나 작업 권한은 없습니다.


### df를 실행하면 COSFS의 Size와 Available이 256T로 표시되는 이유는 무엇입니까?
COS 버킷의 공간은 무한합니다. Available 이 256T인 것은, df 결과를 보여주기 위한 것입니다. 실제로 COS 버킷이 저장할 수 있는 데이터 용량은 256T보다 훨씬 많습니다.

### df 실행 시 COSFS의 Used가 0으로 표시되는 이유는 무엇입니까?
COSFS는 로컬 저장 공간을 차지하지 않으며, df 등의 툴과 호환되기 위해 COSFS에서 표시되는 Size Used Available은 실제 값이 아닙니다.

### df -i 실행 시 Inode/IUsed/IFree가 모두 0로 표시되는 이유는 무엇입니까?
COSFS는 하드 디스크 기반 파일 시스템이 아니므로 inode가 없습니다.



