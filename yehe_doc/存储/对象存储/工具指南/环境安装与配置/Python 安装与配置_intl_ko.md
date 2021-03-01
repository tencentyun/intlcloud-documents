본 문서에서는 Python 2.7.13 버전을 사용하여 Windows와 Linux 시스템에서의 Python 설치 및 환경 설정 방법을 자세하게 소개합니다.


## Windows 
#### 1. 다운로드
[Python 공식 홈페이지](https://www.python.org/downloads/)에 접속하여 적합한 버전을 선택해 다운로드합니다. 본 예시에서는 [Python 2.7.13](https://www.python.org/ftp/python/2.7.13/python-2.7.13.amd64.msi) 버전을 선택하여 다운로드합니다.

#### 2. 설치
Python 설치 패키지 다운로드 후, Python 설치 패키지를 더블 클릭하여 기본 안내에 따라 [다음 단계]를 클릭하여 설치를 진행합니다.

#### 3. 환경변수 설정
(1) 설치 완료 후 시스템 안내에 따라 재시작합니다.
(2) 재시작 완료 후, 마우스 오른쪽 버튼을 클릭하여 [내 컴퓨터]>[속성]>[시스템 고급 설정]>[환경변수]>[시스템 변수(S)]를 클릭하여 “Path”(해당 변수가 없는 경우 생성)를 찾습니다.
(3) [편집]>[텍스트 편집]을 클릭하고 "변수값" 끝에 Python 설치 경로인 `;C:\Python27`(실제 설치 경로 입력)을 추가합니다.
(4) 마지막으로 [확인]을 클릭하여 저장합니다.


#### 4. 설정 성공 여부 테스트
[시작](또는 단축키: Win+R)>[실행](`cmd` 입력)>[확인](또는 Enter 키 입력)을 클릭한 후, 팝업되는 창에 명령어 Python을 입력하고 Enter 키를 입력합니다. Python 버전 정보가 표시되면 Python 2.7 설치가 완료되었다는 의미입니다.

## Linux
#### 1. Python 버전 확인 
Linux의 yum에는 Python이 포함되어 있으며, 먼저 기본 Python 버전을 확인합니다.
```sh
python -V
```
이미 Python 2.7 이상의 버전이 설치되어 있는 경우 다음 절차는 생략합니다. 해당 버전 이하인 경우(본 예시에서는 현재 버전이 Python 2.6.6인 경우로 가정) 다음 명령어를 입력합니다.
```plaintext
yum groupinstall "Development tools"
```

#### 2. Python에 필요한 모듈 설치 및 컴파일
```sh
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel
```

#### 3. Python 2.7 다운로드 및 압축 해제 
```sh
wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tar.xz
tar xf Python-2.7.12.tar.xz
```

#### 4. Python 컴파일 및 설치
```plaintext
cd Python-2.7.12 //디렉터리로 이동
./configure -prefix=/usr/local
make && make install  //설치
make clean 
make distclean
```

#### 5. 시스템 Python 명령어를 Python 2.7로 지정
```shell
mv /usr/bin/python /usr/bin/python2.6.6
ln -s /usr/local/bin/python2.7 /usr/bin/python
```

#### 6. 설정 성공 여부 테스트
```sh
python
```
다음 이미지와 같이 정보가 표시되면 Python 2.7 설치가 완료되었다는 의미입니다.
![112046](//mc.qcloudimg.com/static/img/0eb560566c1f67e302e75b1dcb515d98/image.png)

>!권한 문제가 발생할 경우 명령어 입력 전 sudo를 추가하여 해결해 보시기 바랍니다.