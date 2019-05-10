## 기능에 대한 FAQ
### 어떻게 임시 키로 버킷을 탑재합니까?

임시 키(STS)를 사용하여 버킷을 탑재하려면 다음 두 단계를 수행해야 합니다.

1단계: 임시 키 구성 파일을 생성합니다. 예를 들어 /tmp/passwd-sts에 대해 COSFS 명령 옵션 -opasswd-file=\[path\]을 사용하여 임시 키 구성 파일 지정하십시오. 임시 키에 대한 자세한 내용은 [임시 키 생성 및 사용 설명서](https://cloud.tencent.com/document/product/436/14048) 문서를 참조하십시오. 다음은 임시 키 구성 파일의 예시입니다.

```shell
COSAccessKeyId=AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX  # 다음은 임시 키의 Id, Key 및 Token 필드입니다.
COSSecretKey=GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY
COSAccessToken=109dbb14ca0c30ef4b7e2fc9612f26788cadbfac3
COSAccessTokenExpire=2017-08-29T20:30:00  # 임시 token의 만료 시간은 GMT 시간이며 형식이 예시와 일치해야 합니다.
```
그중 COSFS는 COSAccessTokenExpire에 구성된 시간에 따라 키 파일에서 구성을 리로드 해야 하는지를 판단합니다.

>!키 누출을 방지하기 위해 COSFS에서 다음 명령을 실행하여 키 파일의 권한을 600으로 설정해야 합니다.
>```shell
>chmod 600 /tmp/passwd-sts
>```

2단계: COSFS 명령을 실행하십시오. 명령 옵션-ocam_role=[role]을 사용하여 역할을 sts로 지정하고, -opasswd_file =[path]를 사용하여 키 파일의 경로를 지정하십시오. 예시는 다음과 같습니다.

```shell
cosfs example-1253972369 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oallow_other -ocam_role=sts -opasswd_file=/tmp/passwd-sts
```

### COSFS에서 제공하는 탑재 매개변수 옵션과 버전 번호를 어떻게 확인합니까?

`cosfs --help` 명령을 사용하여 COSFS가 제공하는 매개변수 옵션을 확인할 수 있고 `cosfs --version` 명령을 사용하여 COSFS 버전 번호를 확인할 수 있습니다.

### COSFS에서 생성된 로그는 어떻게 확인할 수 있습니까?

CentOS에서 COSFS가 생성된 로그는 /var/log/messages에 저장됩니다. Ubuntu에서는 COSFS 로그가 /var/log/syslog에 저장됩니다. 사용 중에 문제가 발생하면 해당 기간 동안의 로그를 보내주십시오.

### 버킷 아래의 디렉터리를 탑재하려면 어떻게 해야 합니까?

탑재 명령을 실행할 때 버킷 아래의 디렉터리를 지정할 수 있습니다. 명령은 다음과 같습니다.

```shell
cosfs example-1253972369:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

>!my-dir은 반드시 `/`로 시작해야 합니다.

v1.0.5 이전 버전을 사용할 경우 탑재 명령은 다음과 같습니다.

```shell
cosfs 1253972369:example:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

### root가 아닌 사용자는 어떻게 COSFS를 탑재합니까?

root가 아닌 사용자인 경우 개인 Home 디렉터리에 passwd-cosfs 파일을 작성하고 권한을 600으로 설정한 다음 정상적으로 명령을 사용하여 탑재하면 됩니다. 또한 -opasswd_file=path 옵션을 사용하여 키 파일의 경로를 지정하고 권한을 600으로 설정할 수 있습니다.

### COSFS는 탑재를 위해 HTTPS를 지원합니까?

예. COSFS는 HTTPS를 지원합니다. HTTP와 HTTPS의 사용 형식은 다음과 같습니다.

```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
-ourl=https://cos.ap-guangzhou.myqcloud.com
```

libcurl이 의존하는 NSS 라이브러리가 3.12.3 이상 버전(`curl -V '명령으로 NSS 버전 확인)인 경우 HTTPS 방식으로 버킷을 탑재하기 전에 다음 명령을 실행해야 합니다.

```shell
echo "export NSS_STRICT_NOFORK=DISABLED" >> ~/.bashrc
source ~/.bashrc
```

### COSFS에 대해 시작 시 자동 탑재를 어떻게 설정합니까?

/etc/fstab 파일에 다음 내용을 추가하십시오. 그중, _netdev 옵션은 네트워크가 준비된 후에 현재 명령을 실행할 수 있음을 지정합니다.

```shell
cosfs#example-1253972369 /mnt/cosfs fuse _netdev,allow_other,url=http://cos.ap-guangzhou.myqcloud.com,dbglevel=info
```

### 여러 버킷을 탑재하려면 어떻게 해야 합니까?

여러 Bucket을 동시에 탑재할 경우 /etc/passwd-cosfs 구성 파일에 탑재할 Bucket마다 한 줄씩 작성할 수 있습니다. 각 행의 내용 형식은 단일 Bucket의 탑재 정보와 동일합니다. 예를 들면:

```shell
echo example-123456789:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
echo log-123456789:AKIDXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:GYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY >> /etc/passwd-cosfs
```

### 탑재 후 어떻게 서버의 다른 계정이 이미 탑재된 디렉터리를 접근할 수 있게 합니까?

권한을 개방하려면 탑재를 할 때 `-oallow_other`를 지정해야 합니다.

### COSFS 탑재 디렉터리에 생성된 파일의 이름에는 제한이 있습니까?

COSFS 탑재 디렉터리에서 `/` 문자 이외의 이름으로 파일을 생성할 수 있습니다. 유사 Unix 시스템에서 `/` 문자는 디렉터리 구분 기호이므로 COSFS 탑재 디렉터리에서 `/` 문자를 포함하는 이름으로 파일을 생성할 수 없습니다. 또한 특수 문자가 포함된 이름으로 파일을 생성할 때 특수 문자가 shell에서 사용되어 파일 생성이 실패하는 것을 방지해야 합니다.


## 고장 검사 처리

### COSFS를 사용하는 동안 갑자기 "unable to access MOUNTPOINT /path/to/mountpoint: Transport endpoint is not connected"라는 메시지가 나타나고 접근이 불가능하다면 어떻게 해야 합니까?

`ps ax|grep cosfs` 명령을 사용하여 COSFS 프로세스가 존재하는지 확인할 수 있습니다. 오작동으로 인해 COSFS 프로세스가 중단된 경우 다음 명령을 실행하여 다시 탑재하십시오.

```shell
umount -l /path/to/mnt_dir
cosfs example-1253972369:/my-dir /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info
```

COSFS 프로세스가 오작동으로 인해 중단된 것이 아닌 경우 서버의 fuse 버전이 2.9.4보다 낮은지 확인하십시오. 2.9.4 이전 버전의 libfuse에서 COSFS 프로세스가 이상적으로 종료될 수 있습니다. 이 경우, [COSFS 컴파일 및 설치](https://cloud.tencent.com/document/product/436/6883#compile)에 설명된 대로 fuse 버전을 업데이트하거나 최신 버전의 COSFS를 설치하는 것을 권장합니다.

### COSFS를 통해 업로드된 파일 Content-Type이 "application/octet-stream"으로 변경되면 어떻게 해야 합니까?

COSFS는 /etc/mime.types와 업로드된 파일의 접미사에 대해 비교하여 COS에 업로드할 파일의 Content-Type을 자동으로 설정합니다. Content-Type 문제가 발생하면 이 구성 파일이 시스템에 존재하는지 확인하십시오. Ubuntu의 경우 sudo apt-get install mime-support를 사용하여 추가할 수 있습니다. CentOS의 경우 sudo yum install mailcap을 사용하여 추가할 수 있습니다. 또한 이 파일을 수동으로 생성할 수도 있습니다. 각 파일 형식에 한 줄씩 추가됩니다. 예를 들면:

```shell
image/jpeg                                      jpg jpeg
image/jpm                                       jpm jpgm
image/jpx                                       jpx jpf
```

### 탑재 시 "Bucket not exist"가 표시되면 어떻게 해야 합니까?

버킷 부분이 URL에 포함되지 않도록 -ourl 매개변수를 확인하십시오. 정확한 형식은 다음과 같습니다.

```shell
-ourl=http://cos.ap-guangzhou.myqcloud.com
```

### 이전에 파일에 대한 쓰기가 가능하는데 지금은 불가능한 원인은 무엇입니까?

COS 인증 제품의 정책 조정으로 인해 V1.0.0 이전 버전의 COSFS 도구를 사용하면 정책 확인에 실패됩니다. 최신 COSFS 도구를 설치하고 다시 탑재할 수 있습니다.

### COSFS 도구를 사용하는 동안 Input/Output ERROR와 같은 오류를 어떻게 처리합니까?

아래 단계에 따라 점검하여 문제의 원인을 확인하십시오.

1. 서버가 COS의 도메인 이름에 정상적으로 접근할 수 있는지 확인하십시오.
2. 계정이 정확하게 구성되었는지 확인하십시오.

위의 구성이 정확한지 확인한 후, 서버의 `/var/log/messages` 로그 파일을 열고 s3fs 관련 로그를 찾으십시오. 이 로그는 문제의 원인을 식별하는 데 도움이 될 수 있습니다. 문제가 지속되면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)로 Tencent Cloud 기술 지원부에 문의해서 문제 해결하도록 협조를 청원하십시오.

### /etc/fstab을 사용하여 COSFS의 시작 시 자동 탑재를 설정했지만 mount -a를 실행할 때 "wrong fs type, bad option, bad superblock on cosfs"가 나타나 오류가 보고하면 어떻게 해야 합니까?
일반적으로 이 오류는 서버에 fuse 라이브러리가 부족함으로 인해 발생합니다. 다음 명령을 실행하여 fuse 라이브러리를 설치하는 것을 권장합니다.
- CentOS
```shell
sudo yum install fuse
```
- Ubuntu
```shell
sudo apt-get install fuse
```
