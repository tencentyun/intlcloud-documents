Ubuntu에서 Ubuntu 10.04 LTS의 점검을 종료하여, 더불어 Tencent Cloud에서도 Ubuntu 10.04버전의 공용 이미지 운영을 정지하였습니다.

최근 공식 리소스 웨어하우스에서 Ubuntu10.04 LTS 관련 디렉터리 트리가 삭제되었습니다. Tencent Cloud의 소프트웨어 웨어하우스는 공식 데이터와 일치하므로, 아울러 공식 소스 디렉터리 트리에서도 Ubuntu 10.04 LTS 에 대해 더는 지원하지 않으니 미러 이미지를 더 높은 버전으로 교체해 주시기 바랍니다.

인벤토리 사용자가 Ubuntu 10.04의 소프트웨어 소스를 계속 사용하려면 다음과 같은 2가지 방법이 있습니다.

## 방법1: 환경 설정 파일을 수동 업데이트
사용자의 사용 퀄리티를 높이기 위해 Tencent Cloud의 소프트웨어 웨어하우스에서는 Ubuntu 10.04 LTS의 공식 보관 소스 `http://old-releases.ubuntu.com/ubuntu/`를 불러와 사용자에게 제공하고 있으며, 사용자는 환경 설정 파일을 수동으로 수정하여 해당 웨어하우스를 정상적으로 사용할 수 있습니다.

apt원본 설정 파일 ‘vi /etc/apt/sources.list’ 를 열고 아래의 코드를 수정합니다.

```
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
```

## 방법2: 오토 스크립트 실행
Tencent Cloud에서 제공하는 스크립트 [old-archive.run](http://ubuntu10-10016717.cos.myqcloud.com/old-archive.run) 를 통해 설정하고 해당 파일을 Ubuntu 10.04 CVM 내부에 다운로드한 다음, 아래의 명령어를 실행합니다.

```
chmod +x old-archive.run
./old-archive.run
```
