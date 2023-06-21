JDK(Java Development Kit)는 Java용 SDK입니다. 본문은 JDK 1.8을 예로 들어 Windows 및 Linux에서 JDK를 설치하고 구성하는 방법을 설명합니다.

## Windows

#### 1. JDK 다운로드

[Oracle 공식 홈페이지](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 적합한 JDK 버전을 다운로드합니다.

#### 2. 설치

안내에 따라 순서대로 설치합니다. 설치 과정에서 설치 디렉터리(기본적으로 C 디스크에 설치)를 사용자 정의할 수 있습니다. 본 문서에서는 `D:\Program Files\Java\jdk1.8.0_31`과 `D:\Program Files\Java\jre1.8.0_31`에 설치합니다.


#### 3. 설정

마우스 오른쪽 버튼을 클릭한 후 **PC > 속성 > 고급 시스템 설정 > 환경 변수 > 시스템 변수 > 생성**을 선택하고 프로그램을 구성합니다.
변수 이름(N): **JAVA_HOME**   
변수값(V): `D:\Program Files\Java\jdk1.8.0_31`(실제 설치 경로에 따라 설정)

변수 이름(N): **CLASSPATH**   
변수값(V): `.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`(주의: 변수값 헤더에 `.` 존재)

변수 이름(N): **Path**
변수값(V): `%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`


#### 4. 테스트
구성 성공 여부 테스트: **시작(또는 단축키: Win+R)> 실행(cmd 입력)> 확인(또는 Enter 키 누르기)**을 클릭한 후, 명령어 javac를 입력하고 Enter 키를 눌러 테스트합니다. 다음과 같이 표시되면 환경 변수 구성이 완료된 것입니다.


## Linux
yum 또는 apt-get 명령어를 사용하여 openjdk를 설치하는 경우, 클래스 라이브러리가 불완전하여 설치 완료 후 관련 툴 실행 시 오류 문제가 발생할 수 있습니다. 따라서 수동 압축 해제 후 JDK를 설치하는 방식을 권장합니다. 작업 방법은 다음과 같습니다.

#### 1. JDK 다운로드
[Oracle 공식 홈페이지](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)에서 적합한 JDK 버전을 다운로드해 설치를 준비합니다.
>!다음은 jdk-8u151-linux-x64.tar.gz의 예시입니다. 다른 버전을 다운로드한 경우 파일 확장자명이 .tar.gz인 것만 확인하면 됩니다.

#### 2. 디렉터리 생성 

다음 명령어를 실행하여 /usr/ 디렉터리에 java 디렉터리를 생성합니다.
```shell
mkdir /usr/java
cd /usr/java 
```
다운로드한 파일 jdk-8u151-linux-x64.tar.gz를 /usr/java/ 디렉터리에 복사합니다. 

#### 3. JDK 압축 해제

다음 명령어를 실행하여 파일의 압축을 해제합니다.
```shell
tar -zxvf jdk-8u151-linux-x64.tar.gz 
```

#### 4. 환경 변수 설정

/etc/profile 파일을 편집합니다. profile 파일에 다음 내용을 추가하고 저장합니다.
```shell
# set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH 
```
>!여기서 JAVA_HOME, JRE_HOME은 실제 설치 경로 및 JDK 버전에 따라 설정하십시오.

변경 사항이 적용되면 다음을 실행합니다.
```shell
source /etc/profile 
```

#### 5. 테스트
다음 명령어를 실행하여 테스트합니다.
```sh
java -version
```

Java 버전 정보가 표시되면 JDK 설치가 완료되었다는 의미입니다.
```shell
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```

