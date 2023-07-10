## 기능 문의

### 임시 키를 사용하여 버킷을 마운트하는 방법은 무엇입니까?

임시 키(STS)를 사용하여 버킷을 마운트하는 방법은 다음 두 단계를 진행해야 합니다.

1단계: 임시 키 구성 파일을 생성합니다. 예를 들어 /tmp/passwd-sts에 COSFS에 사용하는 명령어 선택 항목 -opasswd-file=\[path\]로 키 구성 파일을 지정합니다. 임시 키 관련 개념은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오. 임시 키 구성 파일 예시는 다음과 같습니다.
```shell
COSAccessKeyId=AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX  #임시 키의 Id, Key, Token 필드는 아래와 같음
COSSecretKey=GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY
COSAccessToken=109dbb14ca0c30ef4b7e2fc9612f26788cadbfac3
COSAccessTokenExpire=2017-08-29T20:30:00  #GMT 시간의 임시 token 만료 시간, 여기에 표시된 것과 동일한 형식이어야 함
```
COSFS는 COSAccessTokenExpire에 구성된 시간을 기반으로 키 파일에서 구성을 다시 로딩해야 하는지 여부를 결정합니다.

>!키 유출을 방지하려면 다음 명령을 실행하여 COSFS에서 키 파일의 권한을 600으로 설정해야 합니다.
><pre><code class="language-shell">chmod 600 /tmp/passwd-sts</code></pre>
>
2단계: COSFS 명령을 실행하십시오. 명령 옵션 -ocam_role=[role]을 사용하여 역할을 sts로 지정하고 아래와 같이 -opasswd_file=[path]를 사용하여 키 파일의 경로를 지정합니다.
```shell
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oallow_other -ocam_role=sts -opasswd_file=/tmp/passwd-sts
```

### COSFS에서 제공하는 마운트 매개변수 옵션과 버전 번호는 어떻게 확인하나요?

`cosfs --help` 명령을 사용하여 COSFS에서 제공하는 매개변수 옵션을 확인하고 `cosfs --version`을 사용하여 COSFS 버전 번호를 확인할 수 있습니다.

### COSFS에 생성되는 로그는 어떻게 보나요?

CentOS에서 COSFS 생성 로그는 /var/log/messages에 저장됩니다. Ubuntu에서 이러한 로그는 /var/log/syslog에 저장됩니다. 작업 중 문제가 발생하면 해당 기간의 로그를 보내주십시오.

### Bucket에 디렉터리를 마운트하려면 어떻게 해야 합니까?

마운트 명령을 실행할 때 아래와 같이 Bucket에 디렉터리를 지정할 수 있습니다.
```shell
cosfs examplebucket-1250000000:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```
>! my-dir는 반드시 `/`로 시작해야 합니다.
>
v1.0.5 이전 버전에서 마운트 명령은 다음과 같습니다.
```shell
cosfs 1250000000:examplebucket:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

### root 사용자가 아닌 사용자가 COSFS를 어떻게 마운트합니까?

root 사용자가 아닌 경우 개인 Home 디렉터리에 .passwd-cosfs 파일을 생성하고 권한을 600으로 설정한 후 마운트 명령을 사용하여 COSFS를 마운트하는 것이 좋습니다. 또한 -opasswd_file=path 옵션을 사용하여 키 파일 경로를 지정하고 권한을 600으로 설정할 수도 있습니다.

### COSFS는 HTTPS를 통한 마운트를 지원합니까?

예, 지원합니다. HTTP 및 HTTPS를 통한 마운트 방법은 다음과 같습니다.
```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
-ourl=https://cos.ap-guangzhou.myqcloud.com
```

libcurl이 의존하는 NSS 라이브러리의 버전이 v3.12.3 이상인 경우(`curl -V`를 사용하여 NSS 버전 확인) 다음 명령을 실행하여 HTTPS를 통해 Bucket을 마운트할 수 있습니다.

```shell
echo "export NSS_STRICT_NOFORK=DISABLED" >> ~/.bashrc
source ~/.bashrc
```

### COSFS 시작 시 자동 마운트는 어떻게 설정합니까?

먼저 fuse 패키지를 설치해야 합니다.
```shell
#CentOS 시스템
#sudo yum install -y fuse

#Ubuntu시스템
#sudo apt-get install fuse
```

/etc/fstab 파일에 다음을 추가합니다. _netdev 선택 항목은 네트워크가 준비된 후에만 명령을 실행할 수 있도록 지정합니다.

```shell
cosfs#examplebucket-1250000000 /mnt/cosfs fuse _netdev,allow_other,url=http://cos.ap-guangzhou.myqcloud.com,dbglevel=info
```

### 마운트 타깃에서 파일 또는 디렉터리의 사용자 및 사용자 그룹을 어떻게 설정합니까?

특정 시나리오(예: nginx 서버)에서는 www 사용자(uid=1002, gid=1002)와 같은 마운트 타깃 아래에 파일 또는 디렉터리의 사용자 및 사용자 그룹을 설정해야 합니다. 이 경우 다음 마운트 매개변수를 추가해야 합니다.

```shell
-ouid=1002 -ogid=1002
```

### 여러 버킷을 어떻게 마운트합니까?

여러 Bucket을 동시에 마운트해야 하는 경우 /etc/passwd-cosfs 구성 파일에 마운트할 각 Bucket에 대한 행을 작성하십시오. 각 행의 내용은 다음과 같이 단일 Bucket의 내용과 동일한 형식이어야 합니다.

```shell
echo examplebucket-1250000000:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
echo log-1250000000:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
```

### 마운트된 디렉터리를 서버의 다른 계정에서 액세스할 수 있도록 하려면 어떻게 해야 합니까?

마운트된 디렉터리를 다른 계정에서 액세스할 수 있도록 하려면 마운트하는 동안 `-oallow_other`를 지정하십시오.

### COSFS 마운트 디렉터리의 파일 이름에 제한이 있습니까?

COSFS 마운트 디렉터리에서 `/` 문자가 포함되지 않는 이름의 파일을 생성할 수 있습니다. Unix 계열 시스템에서 `/` 문자는 디렉터리 구분 기호이므로 `/` 문자는 COSFS 마운트 디렉터리의 파일 이름에 허용되지 않습니다. 또한 이름에 특수 문자가 포함된 파일을 만들 때 이러한 문자가 shell에서 사용되지 않는지 확인하십시오. 그렇지 않으면 파일 생성이 실패할 수 있습니다.

### COSFS는 파일 존재 여부를 어떻게 판단합니까?

COSFS 내부 로직에서 Head 요청을 사용하여 상위 디렉터리와 파일이 존재하는지 판단합니다.


### COSFS로 스토리지 사용량을 보려면 어떻게 해야 합니까?
COSFS는 스토리지 사용량 직접 조회를 지원하지 않습니다. COS 버킷의 스토리지 용량을 계산하려면 데이터 볼륨이 비교적 작은 시나리오의 경우 COS 콘솔에 로그인하여 확인하시고, 데이터 볼륨이 큰 시나리오의 경우 [인벤토리](https://intl.cloud.tencent.com/document/product/436/30622) 기능을 사용하시기 바랍니다.

### 마운트된 디렉터리에 액세스한 프로세스를 어떻게 확인합니까?
다음 명령을 실행하여 /mnt/cosfs와 같은 마운트된 디렉터리에 액세스한 프로세스를 확인하십시오.
```
lsof /mnt/cosfs 
```


## 문제 해결에 대한 FAQ

### "unable to access MOUNTPOINT /path/to/mountpoint: Transport endpoint is not connected" 오류 메시지가 표시되고 COSFS에 액세스할 수 없게 되면 어떻게 해야 합니까?

`ps ax|grep cosfs` 명령을 사용하여 COSFS 프로세스가 존재하는지 확인할 수 있습니다. COSFS 프로세스가 잘못된 작업으로 인해 다운된 경우 다음 명령을 실행하여 다시 마운트합니다.

```shell
umount -l /path/to/mnt_dir
cosfs examplebucket-1250000000:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

COSFS 프로세스가 오작동으로 종료된 게 아닌 경우 기기 상의 fuse 버전이 2.9.4 이하인지 확인합니다. libfuse가 2.9.4 버전 이하인 경우 COSFS 프로세스에 오류가 발생하여 종료될 수 있습니다. 이 경우 [COSFS 툴](https://intl.cloud.tencent.com/document/product/436/6883) 문서를 참고하여 fuse 버전을 업데이트하거나 COSFS 최신 버전 설치를 권장합니다.

### COSFS를 통해 업로드된 파일의 Content-Type이 "application/octet-stream"으로 변경된 경우 어떻게 해야 하나요?

COSFS는 파일의 접미사를 /etc/mime.types와 비교하여 COS에 업로드된 파일의 Content-Type을 자동으로 설정합니다. Content-Type 문제가 발생하면 시스템에 설정 파일이 존재하는지 확인하십시오. Ubuntu의 경우 sudo apt-get install mime-support를 사용하여 추가할 수 있습니다. CentOS의 경우 sudo yum install mailcap을 사용하여 추가할 수 있습니다. 이 파일을 수동으로 생성할 수도 있습니다. 여기서 아래와 같이 각 파일 형식에 대해 한 줄이 추가됩니다.

```shell
image/jpeg                                      jpg jpeg
image/jpm                                       jpm jpgm
image/jpx                                       jpx jpf
```

### 마운트 중에 Bucket not exist가 표시되면 어떻게 해야 합니까?

-ourl 매개변수를 확인하여 Bucket 부분이 URL에 포함되지 않았는지 확인하십시오. 올바른 형식은 다음과 같습니다.

```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
```

### 이전에 쓸 수 있었던 파일에 쓸 수 없는 이유는 무엇입니까?

COS 인증 정책에 대한 조정으로 인해 v1.0.0 이전 버전의 COSFS 도구를 사용하면 정책 확인이 실패하게 됩니다. 최신 COSFS 도구를 설치하고 다시 마운트할 수 있습니다.

### COSFS 도구를 사용할 때 Input/Output ERROR 등과 같은 오류가 발생하면 어떻게 해야 합니까?

오류의 원인을 확인하려면 아래 단계를 따르십시오.

1. 서버가 COS 도메인 이름에 정상적으로 액세스할 수 있는지 확인합니다.
2. 계정이 정확하게 설정되어 있는지 확인합니다. 
3. 복사를 위해 -p 또는 -a 매개변수가 포함된 cp 명령을 사용한 경우 매개변수를 제거하고 명령을 다시 실행하는 것이 좋습니다.

위의 설정이 올바른지 확인한 후 서버에서 `/var/log/messages` 로그 파일을 열고 s3fs에 대한 로그 항목을 찾으면 오류 원인을 식별하는 데 도움이 됩니다. 오류가 지속되면 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하십시오.

### /etc/fstab을 사용하여 COSFS 시작 시 자동 마운트를 설정했지만 mount -a를 실행할 때 "wrong fs type, bad option，bad superblock on cosfs" 오류가 발생합니다. 왜 그렇습니까?
해당 오류는 일반적으로 서버에 fuse 라이브러리가 없기 때문에 발생합니다. 다음 명령을 실행하여 fuse 라이브러리를 설치하는 것이 좋습니다.
- CentOS
```shell
sudo yum install fuse
```
- Ubuntu
```shell
sudo apt-get install fuse
```

### 시스템 로그 /var/log/messages에 대량의 404 오류 코드가 나타나는 것이 정상입니까?
COSFS 내부 로직에서는 Head 요청을 사용하여 상위 디렉터리와 파일이 존재하는지 여부를 확인하며 404 오류가 반드시 프로그램이 잘못 실행되고 있음을 의미하지는 않습니다.

### COS에서 보는 파일의 크기가 0인 이유는 무엇입니까?
일반적으로 COSFS에 데이터를 쓸 때 COS에서는 먼저 크기가 0인 파일을 생성하고 로컬 캐시 파일에 데이터를 씁니다.
쓰기 프로세스 중 마운트 타깃 ls 명령의 결과는 파일 크기의 변화를 보여줍니다. 파일이 닫히면 COSFS는 로컬 캐시 파일에 기록된 데이터를 COS에 업로드하고, 업로드에 실패하면 크기가 0인 파일만 볼 수 있으며, 이 경우 실패한 파일을 다시 복사할 수 있습니다.

### COSFS 캐시 디렉터리에 있는 파일이 COS에 있는 파일과 동일한가요? 직접 사용할 수 있습니까?
직접 사용할 수 없습니다. 캐시 디렉터리의 파일은 COSFS에서 읽기 및 쓰기를 가속화하는 데 사용되며 COS에서 파일의 일부만 포함할 수 있습니다.

### rsync 명령을 사용하여 파일을 COSFS에 복사했는데 진행률이 100%에 도달했지만 서버에 임시 파일만 표시됩니다. 왜 그렇습니까?
rsync 명령은 마운트된 디렉터리에 임시 파일을 생성합니다. 100% 진행률은 임시 파일이 로컬에서 100% 기록되었음을 의미합니다. 그 후 COS에 업로드한 다음 이름을 변경하고 복사합니다.
일반적으로 cp 명령을 사용하는 것보다 rsync 명령을 사용하여 COSFS 마운트 디렉터리에 데이터를 복사하는 데 더 많은 시간이 걸립니다.

### COSFS가 디스크 용량을 다 사용하면 어떻게 해야 하나요?
COSFS를 사용한 업로드 및 다운로드에는 디스크 파일 캐시가 포함됩니다. 대용량 파일을 업로드하거나 다운로드할 때 -oensure_diskfree=[size] 매개변수를 지정하지 않으면 파일이 캐시된 디스크가 모두 사용됩니다. -oensure_diskfree 매개변수를 사용하여 디스크의 남은 용량이 [size] MB 미만인 경우 COSFS가 디스크 용량 사용량(MB)을 최소화하도록 지정할 수 있습니다. -ouse_cache=[path] 매개변수를 지정하면 캐시 파일은 path 디렉터리에 위치합니다. 그렇지 않으면 /tmp 디렉터리에 있습니다.

예를 들어 다음 명령을 실행하여 남은 용량이 10GB 미만일 때 디스크 용량 사용량을 줄이도록 COSFS를 구성할 수 있습니다.
```shell
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oensure_diskfree=10240
```

### docker를 사용하여 COSFS를 마운트할 때 fuse: failed to open /dev/fuse: Operation not permitted 오류 메시지가 표시되면 어떻게 해야 합니까?
docker 이미지를 시작하려면 --privileged 매개변수를 추가해야 합니다.

### 디렉터리를 여러 마운트 타깃에 대한 공유 캐시 디렉터리로 사용할 수 있습니까?
멀티 마운트 타깃이 캐시 디렉터리를 공유하지 않도록 하는 것이 좋습니다. 캐시 디렉터리에는 COSFS에서 사용하는 메타데이터가 포함되어 있으며 이를 공유하면 메타데이터가 엉망이 될 수 있습니다.

### 마운트에 COSFS를 사용할 때 /bin/mount:unrecognized option --no-canonicalize 오류 메시지가 표시되면 어떻게 해야 합니까?

mount 도구의 이전 버전은 `--no-canonicalize` 옵션을 지원하지 않습니다. mount 도구를 업데이트합니다. [v2.17 다운로드](https://cdn.kernel.org/pub//linux/utils/util-linux/v2.17/) 후 다시 마운트하는 것이 좋습니다. 설치 명령은 다음과 같습니다.

```shell
tar -jxvf util-linux-ng-2.17.tar.bz2
cd util-linux-ng-2.17
./configure --prefix=/usr/local/util-linux-ng
make && make install
mv /bin/mount{,.off}
ln -s /usr/local/util-linux-ng/bin/mount /bin
```

### 마운트에 실패하면 어떻게 해야 합니까?

1단계: 마운트 명령어와 키 설정 파일이 맞는지, 로그 파일과 에러 메시지를 기반으로 COS 서비스 액세스가 가능한지 확인합니다.

2단계: date 명령을 실행하여 서버 시간이 올바른지 확인합니다. 정확하지 않은 경우 date 명령어를 사용하여 수정한 후 `date -s '2014-12-25 12:34:56'`과 같이 다시 마운트합니다.

### `ls -l --time-style=long-iso` 명령을 사용할 때 마운트된 디렉터리의 시간이 1970-01-01 08:00으로 변경되는 것이 정상입니까?

예. 마운트 타깃을 마운트 해제하면 마운트된 디렉터리의 시간이 마운트하기 전의 시간으로 돌아갑니다.

 ### 마운트된 디렉터리가 비어 있지 않을 수 있습니까?

`-ononempty` 매개변수를 사용하여 비어 있지 않은 디렉터리로 마운트할 수 있지만 마운트 타깃과 원본 디렉터리에 동일한 경로의 파일이 있는 경우 문제가 발생할 수 있으므로 그렇게 하지 않는 것이 좋습니다.

### COSFS 디렉터리에서 실행할 때 ls 명령을 반환하는 데 왜 그렇게 오래 걸리나요?
마운트된 디렉터리에 많은 파일이 있는 경우 ls 명령을 실행하려면 디렉터리의 각 파일에 대해 HEAD 작업이 필요하므로 명령이 반환되기 전에 디렉터리 시스템을 읽는 데 많은 시간이 걸립니다.
>! 불필요한 재시작을 초래할 수 있는 IO hung을 활성화하지 않는 것이 좋습니다.
>


### 로그 레벨을 info로 설정할 때 생성된 시스템 로그 파일이 저장 공간을 많이 차지하면 어떻게 해야 합니까?
정기적으로 생성되는 시스템 로그 파일을 삭제하거나 `-odbglevel=crit`를 사용하여 마운트하는 등 로그 레벨을 높게 조정할 수 있습니다.


### COSFS는 어떤 시나리오에 적용되며 읽기 및 쓰기 성능은 어떻습니까?
COSFS의 읽기 및 쓰기 작업에는 디스크가 필요하므로 COSFS는 공유 데이터를 읽는 공유 데이터 세트의 머신러닝 알고리즘 및 단순 로그 백업과 같이 COS 액세스에 POSIX 액세스 구문이 필요한 시나리오에만 적합합니다. COSFS는 가속을 위해 멀티 스레드 업로드 및 다운로드를 채택합니다. 같은 리전의 사설망을 통해 COSFS는 6GB 파일을 순차적으로 읽는 데 약 80초, 6GB 파일을 순차적으로 쓰는 데 약 160초가 걸립니다. 일반적으로 SDK와 멀티 스레드를 사용하여 더 나은 성능을 얻을 수 있습니다.

>! 파일 읽기 및 쓰기로 인한 많은 시스템 호출과 많은 로그는 COSFS 읽기 및 쓰기 성능에 어느 정도 영향을 미칠 수 있습니다. 고성능 요구 사항이 있는 경우 -odbglevel=warn 또는 더 높은 로그 레벨을 지정할 수 있습니다.
>

### COSFS RPM 패키지를 설치한 후 COSFS를 찾을 수 없다는 메시지가 표시되면 어떻게 해야 합니까?

cosfs 설치 경로는 /usr/local/bin입니다. 시스템이 cosfs를 찾을 수 없다는 메시지를 표시하는 경우 가능한 원인은 경로가 PATH 환경 변수에 지정되지 않았으며 `~/.bashrc`에 구성 행을 추가해야 합니다.
```shell
export PATH=/usr/local/bin:$PATH
```
그런 다음 다음 명령을 실행해야 합니다.
```shell
source ~/.bashrc
```

### COSFS RPM 패키지를 설치할 때 시스템이 conflicts with file from package fuse-libs-\*를 보고하면 어떻게 해야 합니까?

COSFS RPM 패키지를 설치할 때 `--force` 옵션을 추가하십시오.
```shell
rpm -ivh cosfs-1.0.19-centos7.0.x86_64.rpm --force
```

###  COSFS에서 읽기 전용 권한이 부여된 디렉터리를 별도로 마운트할 때 시스템에 권한 없음이 표시되는 이유는 무엇입니까?

COSFS는 루트 디렉터리에 대한 GetBucket 권한이 필요합니다. 따라서 루트 디렉터리에 대한 GetBucket 권한과 해당 디렉터리에 대한 읽기 권한을 추가해야 합니다. 그런 식으로 다른 디렉터리를 나열할 수 있지만 작업 권한은 없습니다.

### COSFS는 매일 일정 시간대에 CPU 사용률이 높고, COS에 대량의 Head, List 요청을 전송하여 요청 횟수 요금이 많이 발생합니다. 어떻게 처리해야 하나요?

이는 일반적으로 시스템에 예약된 디스크 스캔 작업이 있기 때문입니다. Linux 시스템의 일반적인 디스크 스캔 프로그램은 updatedb입니다. COSFS 마운트 포인트 디렉터리를 updatedb의 구성 파일의 /etc/updatedb.conf 파일에 있는 PRUNEPATHS 구성 항목에 추가하여 프로그램의 디스크 스캔 동작을 방지할 수 있습니다. 또한 Linux 툴 auditd를 사용하여 COSFS 마운트 포인트에 액세스하는 프로그램을 찾을 수 있습니다.

작업 순서는 다음과 같습니다.

1단계: auditd 설치

Ubuntu:

```
ap-get install auditd -y
```

CentOS：

```
 yum install audit audit-libs
```

2단계: auditd 서비스 실행

```
systemctl start auditd
systemctl enable auditd
```

3단계: 마운트 디렉터리 모니터링

>?`-w`는 COSFS 마운트 디렉터리를 지정하며, `-k`는 audit 로그의 key 출력입니다.

```
auditctl -w /usr/local/service/mnt/ -k cosfs_mnt
```

4단계: 로그에 따라 액세스 프로그램 결정

audit 로그 디렉터리: /var/log/audit, 쿼리 명령은 다음과 같습니다.

```
ausearch -i|grep 'cosfs_mnt'
```

5단계: auditd 서비스 중지
auditd 서비스를 중지해야 하는 경우 다음 명령을 사용할 수 있습니다.

```
/sbin/service auditd stop
```

>!마운트 포인트에 액세스하는 프로그램이 실행 중이면 새로 시작된 auditd는 프로그램의 액세스 동작을 모니터링하지 않으며 프로그램의 마운트 디렉터리에 대한 다중 호출은 처음에만 기록됩니다.

### df를 실행한 후 Size 및 Available 값이 256T인 이유는 무엇입니까?
COS 버킷은 무제한 저장 용량을 제공합니다. 표시된 256T는 df의 출력으로만 사용됩니다.

### df를 실행한 후 Used 값이 0인 이유는 무엇입니까?
COSFS는 로컬 저장소를 차지하지 않습니다. df와 같은 툴과의 호환성을 위해 COSFS에 표시되는 Size Used Available 값은 실제 값이 아닙니다.

### df -i를 실행한 후 Inode/IUsed/IFree의 값이 0인 이유는 무엇입니까?
COSFS는 디스크 기반 파일 시스템이 아니므로 inode가 없습니다.

