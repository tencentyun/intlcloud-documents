본 문서에서는 다양한 운영 체제에서 Python 개발 환경을 설치하는 방법을 간략하게 소개합니다.

## 설치 패키지를 통해 설치

### 1. 다운로드
[Python 공식 웹사이트](https://www.python.org/downloads/)로 이동하여 사용 중인 운영 체제에 따라 적절한 설치 패키지를 다운로드합니다.

>! Python은 2020년 1월 1일부터 공식적으로 Python2의 유지보수를 중단하였습니다. Python3 설치 및 사용을 권장합니다.

### 2. 설치
설치 패키지를 다운로드한 후 설치 패키지의 지시에 따라 Python 개발 환경의 설치를 완료합니다.

>? Windows 시스템 사용자는 설치할 때 "Add Python to environment variables" 옵션을 선택해야 합니다.
> ![](https://main.qcloudimg.com/raw/bd52e448e3ba0e8171b5a37b31caadb8.png)

### 3. 검증
단말에서 다음 명령을 실행하여 Python 버전을 확인합니다.
```shell
python -V
```
단말에서 Python 버전 번호가 출력되면 설치가 완료된 것입니다.

>? Windows 시스템 사용자는 설치가 완료된 후 컴퓨터를 다시 시작해야 할 수 있습니다.

### 4. 환경변수 설정
Windows 시스템에서 상기 명령어를 실행할 때 단말에서 "내부 또는 외부 명령어가 아닙니다"라는 메시지가 표시되면 [컴퓨터]> [속성]> [고급 시스템 설정]> [환경 변수]> [시스템 변수(S)] 에서 아래 그림과 같이 "Path"를 편집하고 Python의 설치 경로를 추가합니다.

## 패키지 관리자를 통해 설치

### Mac OS
Mac OS 사용자는 먼저 [HomeBrew](https://brew.sh/index_zh-cn)를 설치한 다음 HomeBrew를 통해 Python을 설치할 수 있습니다.
```shell
brew install python
```

### Ubuntu
Ubuntu 사용자는 Ubuntu의 apt(Advanced Packaging Tool) 패키지 관리자를 사용하여 Python을 설치할 수 있습니다.
```shell
sudo apt-get install python
```

### CentOS
CentOS 사용자는 CentOS의 yum(Yellow dog Updater, Modified) 패키지 관리자를 사용하여 Python을 설치할 수 있습니다.
```shell
sudo yum install -y python
```
