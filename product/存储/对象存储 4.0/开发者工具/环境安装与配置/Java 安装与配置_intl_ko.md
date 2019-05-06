JDK는 Java 용 SDK입니다. 이 문서는 JDK 1.7 및 1.8을 예제로 Windows 및 Linux 시스템에서 JDK를 설치하고 구성하는 방법을 설명합니다.

## Windows
### 1. JDK 다운로드
[Oracle 공식 웹사이트](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)로 이동하여 JDK 버전을 다운로드합니다.
### 2. 설치
지시대로 JDK를 설치하십시오. 설치 과정 중에 디렉토리(기본값은 C 드라이브)를 지정할 수 있습니다. 이 예에서는 다음 디렉토리를 사용합니다.
`D:\Program Files\Java\jdk1.8.0_31`
`D:\Program Files\Java\jre1.8.0_31`
![로컬 동기화 도구1](//mc.qcloudimg.com/static/img/0652f9759c4f7fa7e61aa406ca1ad822/image.png)
### 3. 구성
설치가 완료되면 [컴퓨터]를 마우스 오른쪽 단추로 클릭 한 다음 [속성] > [고급 시스템 설정] > [환경 변수] > [시스템 변수] > [생성]를 클릭하고 소프트웨어를 각각 구성하십시오.
변수 이름(N):**JAVA_HOME**   
변수 값(V):`D:\Program Files\Java\jdk1.8.0_31`(실제 설치 경로에 따라 설정).
![로컬 동기화 도구2](//mc.qcloudimg.com/static/img/f02f0ec6b87576f32fbade9cd8d55c1e/image.png)
변수 이름(N):**CLASSPATH**   
변수 값(V):`.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`(변수 시작에 `.`가 있음).
![로컬 동기화 도구3](//mc.qcloudimg.com/static/img/d2c87f5ce4c2927f5e9ca9d20e4478d6/image.png)
변수 이름(N):**경로**
변수 값(V):`%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`
![로컬 동기화 도구4](//mc.qcloudimg.com/static/img/5ee8cc105d52f9052cc49251ce88ed9a/image.png)
### 4. 테스트
구성을 테스트하려면 [시작] (또는 Win + R) > [실행] (`cmd`를 입력) > [확인] (또는 Enter 키)을 클릭하여 명령`javac`를 입력하고 Enter를 누르십시오. 아래에 표시된 메시지가 나타나면 환경 변수 구성이 성공합니다.
![로컬 동기화 도구5](//mc.qcloudimg.com/static/img/83f8417d6f540c20182267acba29f2ad/image.png)

## Linux
yum 또는 apt-get 명령을 사용하여 openjdk를 설치하면 클래스 라이브러리가 불완전한 상황이 있습니다. 설치 후 관련 도구를 실행할 때 오류가 발생할 수 있습니다. 따라서 수동 압축 풀기 및 설치를 통해 JDK를 설치하는 것이 좋습니다. 구체적인 내용은 다음과 같습니다.

### 1. JDK 다운로드
[Oracle 공식 웹사이트](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)로 이동하여 JDK 버전을 다운로드합니다.
>!Linux 용 버전을 다운로드 해야 합니다. jdk-8u151-linux-x64.tar.gz를 예로 들어 보겠습니다. 다운로드 한 파일은 다른 버전 일 수 있지만 파일의 접미사는 .tar.gz 여야 합니다.

### 2. 디렉터리 만들기
`/usr/` 디렉터리에 `java` 디렉터리를 만듭니다.
```shell
mkdir /usr/java
cd /usr/java
```
다운로드 한 jdk-8u151-linux-x64.tar.gz 파일을 /usr/java/ 디렉토리에 복사하십시오.

### 3. JDK 압축 해제
```shell
tar -zxvf jdk-8u151-linux-x64.tar.gz
```

### 4. 환경 변수 설정
/etc/profile 파일을 편집하십시오. 프로필 파일에 다음 내용을 추가하고 저장하십시오.
```shell
set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH
```
>!JAVA_HOME 및 JRE_HOME은 실제 설치 경로 및 JDK 버전에 따라 구성해야 합니다.

변경 사항을 적용합니다.
```shell
source /etc/profile
```

### 5. 테스트
```sh
java -version
```
Java 버전 정보가 나타나면 JDK가 성공적으로 설치되었습니다.
```shell
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```
