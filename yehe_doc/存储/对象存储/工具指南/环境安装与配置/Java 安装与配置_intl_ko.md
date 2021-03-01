JDK는 Java 소프트웨어 개발 툴 패키지입니다. 본 문서에서는 JDK 1.7 및 1.8 버전을 사용하여 Windows와 Linux 시스템에서의 JDK 설치 및 환경 설정 방법을 소개합니다.

## Windows
### 1. JDK 다운로드
[Oracle 공식 홈페이지](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에 접속하여 적합한 JDK 버전을 다운로드하여 설치를 준비합니다.
### 2. 설치
안내에 따라 모두 설치하고, 설치 중 설치 디렉터리(기본적으로 C 드라이브에 설치)를 사용자 정의 선택할 수 있습니다. 예를 들어 본 문서에서는 설치 디렉터리를 다음과 같이 선택합니다.
`D:\Program Files\Java\jdk1.8.0_31`
`D:\Program Files\Java\jre1.8.0_31`

### 3. 설정
설치 완료 후, 마우스 오른쪽 버튼을 클릭하여 [내 컴퓨터]> [속성]>[시스템 고급 설정]>[환경변수]>[시스템 변수]>[생성]을 클릭해 각 소프트웨어를 설정합니다.
변수 이름(N): **JAVA_HOME**   
변수값(V): `D:\Program Files\Java\jdk1.8.0_31`(실제 설치 경로에 따라 설정)
변수 이름(N): **CLASSPATH**   
변수값(V): `.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`(주의: 변수값 헤더에 `.` 존재)
변수 이름(N): **Path**
변수값(V): `%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`

### 4. 테스트
설정 성공 여부 테스트: [시작](또는 단축키: Win+R)>[실행](`cmd` 입력)>[확인](또는 Enter 키 입력)을 클릭한 후, 명령어 `javac`를 입력하고 Enter 키를 입력합니다. 다음과 같은 이미지 정보가 표시되면 환경변수 설정이 완료되었다는 의미입니다.

## Linux
yum 또는 apt-get 명령어를 사용해 openjdk를 설치하는 경우 클래스 라이브러리가 완전하지 못할 수 있으며, 이로 인해 사용자가 설치 후 관련 툴 실행 시 오류가 나타날 수 있습니다. 따라서 수동으로 압축 해제해 설치하는 방식으로 JDK를 설치하는 것을 권장합니다. 자세한 작업 방법은 다음과 같습니다.

### 1. JDK 다운로드
[Oracle 공식 홈페이지](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에 접속하여 적합한 JDK 버전을 다운로드하여 설치를 준비합니다.
>!Linux 버전을 다운로드해야 합니다. 본 문서에서는 jdk-8u151-linux-x64.tar.gz를 예시로 하며, 실제 다운로드하는 파일은 해당 버전이 아닐 수 있으나 이는 상관 없으며 확장명(.tar.gz)이 동일하면 됩니다.

### 2. 디렉터리 생성 
`/usr/` 디렉터리에 `java` 디렉터리를 생성합니다.
```shell
mkdir /usr/java
cd /usr/java 
```
다운로드한 파일 jdk-8u151-linux-x64.tar.gz를 /usr/java/ 디렉터리로 복사합니다. 

### 3. JDK 압축 해제
```shell
tar -zxvf jdk-8u151-linux-x64.tar.gz 
```

### 4. 환경변수 설정
/etc/profile 파일을 편집합니다. profile 파일에 다음 내용을 추가하고 저장합니다.
```shell
set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH 
```
>!여기에서 JAVA_HOME, JRE_HOME은 실제 설치 경로 및 JDK 버전에 따라 설정

수정 적용:
```shell
source /etc/profile 
```

### 5. 테스트
```sh
java -version
```
java 버전 정보가 표시되면 JDK 설치가 완료되었다는 의미입니다.
```shell
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```
