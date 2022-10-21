본문은 CentOS에 Java Web 프로젝트를 배포하는 방법을 설명합니다. Tencent Cloud의 새로운 개별 사용자에게 적합합니다.
## 소프트웨어 버전
본문에 사용된 소프트웨어 도구의 버전은 다음과 같으며 실제 작업 시 사용자의 소프트웨어 버전과 다를 수 있습니다.
- 운영 체제: CentOS 7.5
- Tomcat: apache-tomcat-8.5.39
- JDK: JDK 1.8.0_201

## JDK 설치
CVM을 구입한 후 CVM 세부 정보 페이지에서 [로그인]을 클릭하여 CVM 인스턴스에 로그인하면 사용자 이름과 비밀번호를 입력하여 Java Web 환경을 설정할 수 있습니다. CVM 인스턴스를 생성하는 방법에 대한 자세한 내용은 [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오.

### JDK 다운로드
다음 명령을 입력합니다.
```
mkdir /usr/java  # java 폴더 생성
cd /usr/java     # java 폴더로 이동
```
<pre>
<code># JDK 설치 패키지 업로드(권장)
<a href="https://winscp.net/eng/docs/lang:chs" target="_blank">WinSCP</a>와 같은 툴을 사용하여 JDK 설치 패키지를 위의 java 폴더에 업로드한 후 압축을 푸는 것이 좋습니다.
 또는 
# 명령 사용(설치 패키지 업로드 권장): wget을 실행하여 패키지를 다운로드합니다. 다운로드한 패키지는 기본적으로 Oracle BSD 라이선스를 거부하기 때문에 압축을 풀 수 없습니다. https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html로 이동하여 라이센스 계약에 동의하고 cookie가 포함된 다운로드 링크를 가져오십시오.
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz</code>
</pre>
```
# 압축 해제
chmod +x jdk-8u201-linux-x64.tar.gz
tar -xzvf jdk-8u201-linux-x64.tar.gz
```

### 환경 변수 설정
1. `/etc/profile` 파일을 엽니다.
```
vi /etc/profile
```
2. i를 눌러 편집 모드로 이동하여 다음 정보를 파일에 추가합니다.
```
# set java environment
export JAVA_HOME=/usr/java/jdk1.8.0_201
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```
3. Esc 키를 눌러 편집 모드를 종료하고 `:wq`를 입력하여 파일을 저장하고 닫습니다.
4. 환경 변수를 로딩합니다.
```
source /etc/profile
```

### JDK 설치 결과 보기
`java -version` 명령을 실행합니다. JDK 버전 정보가 표시되면 JDK가 성공적으로 설치된 것입니다.
![](https://main.qcloudimg.com/raw/6d3531f4d466e5428885ec38a3542c2e.png)

## Tomcat 설치
### Tomcat 다운로드
다음 명령을 입력합니다.
```
# 미러 주소는 변경될 수 있으며 Tomcat 버전은 지속적으로 업그레이드될 수 있습니다. 다운로드 링크가 만료된 경우 [Tomcat 공식 웹사이트](https://tomcat.apache.org/download-80.cgi)로 이동하여 적절한 설치 패키지 주소를 선택하십시오.
wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.39/bin/apache-tomcat-8.5.39.tar.gz
tar -xzvf apache-tomcat-8.5.39.tar.gz
mv apache-tomcat-8.5.39 /usr/local/tomcat/
```
다음 파일은 `/usr/local/tomcat/` 디렉터리에 있습니다.
- bin: Tomcat 서비스를 시작 및 중지하기 위한 스크립트가 포함된 스크립트 파일입니다.
- conf: 전역 구성 파일, 가장 중요한 것은 server.xml 및 web.xml입니다.
- webapps: Web 애플리케이션 파일을 저장하기 위한 기본 디렉터리인 Tomcat의 기본 Web 릴리스 디렉터리입니다.
- logs: Tomcat 로그 파일입니다.

>!다운로드 링크가 만료된 경우 [Tomcat 공식 웹사이트](https://tomcat.apache.org/download-80.cgi )에서 최신 링크로 교체하십시오.

### 사용자 추가
```
# Tomcat을 실행하기 위해 일반 사용자 www 추가
useradd www
# 웹사이트 루트 디렉터리 생성
mkdir -p /data/wwwroot/default
# Java Web 프로젝트 파일(WAR 패키지)을 웹사이트 루트 디렉터리에 업로드하고 디렉터리 아래의 파일 권한을 www로 수정합니다. 이 예시에서는 웹 사이트 루트 디렉터리에 Tomcat 테스트 페이지 생성 방법을 보여줍니다.
echo Hello Tomcat! > /data/wwwroot/default/index.jsp
chown -R www.www /data/wwwroot
```

### JVM 메모리 매개변수 설정
1. `/usr/local/tomcat/bin/setenv.sh` 스크립트 파일을 생성합니다.
```
vi /usr/local/tomcat/bin/setenv.sh
```
2. i를 눌러 편집 모드로 이동하여 다음을 추가합니다.
```
JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
```
3. Esc 키를 눌러 편집 모드를 종료하고 `:wq`를 입력하여 저장하고 종료합니다.

### server.xml 구성
1. `/usr/local/tomcat/conf/` 디렉터리로 전환합니다.
```
cd /usr/local/tomcat/conf/
```
2. server.xml 파일을 백업합니다.
```
mv server.xml server_default.xml
```
3. 새 server.xml 파일을 작성합니다.
```
vi server.xml
```
4. i를 눌러 편집 모드로 이동하여 다음을 추가합니다.
```
<?xml version="1.0" encoding="UTF-8"?>
<Server port="8006" shutdown="SHUTDOWN">
<Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>
<Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener"/>
<Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/>
<Listener className="org.apache.catalina.core.AprLifecycleListener"/>
<GlobalNamingResources>
<Resource name="UserDatabase" auth="Container"
 type="org.apache.catalina.UserDatabase"
 description="User database that can be updated and saved"
 factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
 pathname="conf/tomcat-users.xml"/>
</GlobalNamingResources>
<Service name="Catalina">
<Connector port="8080"
 protocol="HTTP/1.1"
 connectionTimeout="20000"
 redirectPort="8443"
 maxThreads="1000"
 minSpareThreads="20"
 acceptCount="1000"
 maxHttpHeaderSize="65536"
 debug="0"
 disableUploadTimeout="true"
 useBodyEncodingForURI="true"
 enableLookups="false"
 URIEncoding="UTF-8"/>
<Engine name="Catalina" defaultHost="localhost">
<Realm className="org.apache.catalina.realm.LockOutRealm">
<Realm className="org.apache.catalina.realm.UserDatabaseRealm"
  resourceName="UserDatabase"/>
</Realm>
<Host name="localhost" appBase="/data/wwwroot/default" unpackWARs="true" autoDeploy="true">
<Context path="" docBase="/data/wwwroot/default" debug="0" reloadable="false" crossContext="true"/>
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
prefix="localhost_access_log." suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
</Host>
</Engine>
</Service>
</Server>
```
5. Esc 키를 눌러 편집 모드를 종료하고 `:wq`를 입력하여 저장하고 종료합니다.

## Tomcat 실행
### 방법1
Tomcat 서버의 bin 디렉터리로 이동하고 `./startup.sh` 명령을 실행하여 Tomcat 서버를 시작합니다.
```
cd /usr/local/tomcat/bin
./startup.sh
```
실행 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/c118899986968ecd5982eb8cdb2beff9.png)
### 방법2
1. 빠른 실행을 설정하여 service tomcat start를 통해 어디에서나 Tomcat 서버를 실행할 수 있도록 합니다.
```
wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init
mv Tomcat-init /etc/init.d/tomcat
chmod +x /etc/init.d/tomcat
```
2. 다음 명령을 실행하고 JAVA_HOME 실행 스크립트를 설정합니다.
```
sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_201@' /etc/init.d/tomcat
```
3. 자동 실행을 설정합니다.
```
chkconfig --add tomcat
chkconfig tomcat on
```
4. Tomcat을 시작합니다.
```
# Tomcat 실행
service tomcat start
# Tomcat 서버 상태 보기
service tomcat status
# Tomcat 중지
service tomcat stop
```
실행 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/78800e85c09820d98a0a15dc2792aaa8.png)
5. 시스템에 권한이 없다는 메시지가 표시되면 root 사용자로 전환하고 권한을 수정합니다.
```
cd /usr/local
chmod -R 777 tomcat
```
6. 브라우저의 주소 표시줄에 `http://공중망 IP:포트`(여기서 포트는 server.xml에 설정된 connector port)를 입력합니다. 다음 페이지가 나타나면 설치가 성공한 것입니다.
![](https://main.qcloudimg.com/raw/a8d7c77aafc94c9bba262c06125b6c18.png)

### 보안 그룹 구성
접속 실패 시 보안 그룹을 확인하십시오. 위의 예시와 같이 server.xml의 connector port는 8080이므로 해당 CVM 인스턴스에 바인딩된 보안 그룹에서 인터넷에 TCP:8080을 열어야 합니다.
![](https://main.qcloudimg.com/raw/6ffabfd2ef027e4fc69e4fc1a85dde9f.png)
