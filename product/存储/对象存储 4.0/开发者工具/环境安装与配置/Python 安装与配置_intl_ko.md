이 문서는 Python 2.7을 예제로 사용하여 Windows 및 Linux 시스템에서 Python을 설치하고 구성하는 방법을 설명합니다.

## Windows
### 1. 다운로드
[Python 공식 웹 사이트](https://www.python.org/downloads/)로 이동하여 적절한 버전을 다운로드하십시오. 이 예제에서는 [Python 2.7.13](https://www.python.org/ftp/python/2.7.13/python-2.7.13.amd64.msi)을 다운로드합니다.
### 2. 설치
Python 설치 프로그램 패키지를 두 번 클릭하고 지침에 따라 Python을 설치하십시오.
### 3. 환경 변수 구성
설치가 완료되면 [컴퓨터]를 마우스 오른쪽 단추로 클릭 한 다음 [속성] > [고급 시스템 설정] > [환경 변수] > [시스템 변수(S)]를 클릭하고 "Path"를 찾으십시오. Python 설치 경로`;C:\Python27`을 (변수로 바꾸고) "변수 값" 의 끝에 추가하고 [확인]을 클릭하여 저장하십시오.
![161709](//mc.qcloudimg.com/static/img/b5784ed03d0f2fd07195c9c3ae1e5075/image.png)
### 4 구성 테스트
[시작] (또는 Win+R) > [실행] (`cmd` 입력) > [확인] (또는 Enter 키를 누름)을 클릭하여 팝업 창에 Python 명령을 입력하고 Enter 키를 누르십시오. 다음 메시지가 나타나면 Python 2.7은 설치 및 구성이 성공합니다.
![152355](//mc.qcloudimg.com/static/img/026d7738b234171b285a98f0e751038a/image.png)
## Linux
### 1. Python 버전 확인
Linux의 yum에 빌드된 기본 Python 버전을 확인하십시오.
```
python -V
```
Python 2.7 이상이면 다음 단계를 무시하십시오. 그렇지 않으면 (Python 2.6.6의 경우) 다음 명령을 입력하십시오.
```
yum groupinstall "Development tools"
```
### 2. Python 컴파일에 사용할 구성 요소 설치
```
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel
```
### 3. Python 2.7 다운로드 및 압축 해제
```
wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tar.xz
tar xf Python-2.7.12.tar.xz
```
### 4. Python 컴파일 및 설치
```
cd Python-2.7.12 //디렉토리 입력
./configure -prefix=/usr/local
make && make install //설치
make clean
make distclean
```
### 5. 시스템 Python 명령을 Python 2.7로 보내
```
mv /usr/bin/python /usr/bin/python2.6.6
ln -s /usr/local/bin/python2.7 /usr/bin/python
```
### 6. 구성 테스트
```
python
```
다음 메시지가 나타나면 Python 2.7이 성공적으로 설치 및 구성되었음을 나타냅니다.
![112046](//mc.qcloudimg.com/static/img/0eb560566c1f67e302e75b1dcb515d98/image.png)

> <font color="#0000cc">**주의:** </font>
권한 관련 오류가 발생하면 명령 앞에 sudo를 추가하여 해결하는 것이 좋습니다.
