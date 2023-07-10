## 개요

Apache Ranger는 빅 데이터 생태 시스템에서 액세스 권한을 제어하는 ​​데 사용되는 표준 인증 모듈입니다. GooseFS는 빅 데이터 및 데이터 레이크 시나리오의 스토리지 가속화 시스템으로 Apache Ranger 통합 인증 플랫폼 액세스를 지원합니다. 본문은 Apache Ranger를 사용하여 GooseFS 리소스 액세스 권한을 제어하는 방법을 소개합니다.

## 강점

- GooseFS는 클라우드 네이티브 가속 스토리지 시스템으로서 Apache Ranger를 지원하여 HDFS와 거의 동일한 액세스 제어 수준에 도달했습니다. 따라서 원래 HDFS를 사용하던 빅 데이터 사용자는 매우 쉽게 GooseFS로 마이그레이션할 수 있으며 HDFS의 Ranger 권한 정책을 직접 재사용하여 일관된 사용자 경험을 얻을 수 있습니다.
- GooseFS with Ranger는 HDFS with Ranger의 인증 아키텍처와 비교하여 Ranger + 네이티브 ACL의 공동 인증 옵션도 제공합니다. Ranger 인증에 실패하면, 네이티브 ACL 인증을 사용하도록 선택할 수도 있어 일부 Ranger 인증 정책 설정의 미흡한 문제를 해결할 수 있습니다.

## GooseFS with Ranger의 인증 아키텍처

![](https://main.qcloudimg.com/raw/2f473b8cb8fc446c8b914101f548219a.png)

GooseFS를 Ranger 인증 플랫폼에 통합할 수 있도록 GooseFS Ranger Plugin을 개발하였으며, GooseFS Master 노드와 Ranger Admin측에 동시에 배포됩니다. 아래와 같은 작업을 책임지고 완성합니다.

- GooseFS Master 노드 측:
 - 'Authorizer' 인터페이스를 제공하여 GooseFS Master의 모든 메타데이터 요청에 대한 인증 결과를 제공합니다.
 - Ranger Admin에 접속하여 사용자가 설정한 인증 정책을 획득합니다.
- Ranger Admin 측: 
 - Ranger Admin에게 GooseFS의 리소스 조회(resource lookup) 기능을 제공합니다.
 - 구성 인증 기능을 제공합니다.

## 배포 시작

### 준비 과정

사용을 시작하기 전에 Ranger 관련 구성 요소(Ranger Admin 및 Ranger UserSync 포함)가 환경에 배포 및 구성되었는지, Ranger의 WebUI가 정상적으로 열리고 사용할 수 있는지 확인해야 합니다.

### 모듈 배포

#### Ranger Admin 측에 GooseFS Ranger Plugin을 배포하고 해당 서비스를 등록합니다.

>? 여기를 클릭하여 GooseFS Ranger Plugin을 다운로드하십시오.
>

배포 단계는 다음과 같습니다.

1. Ranger 서비스 정의 디렉터리 하위에 새로운 GooseFS의 디렉터리를 만듭니다(디렉터리 권한은 최소한 x와 r 권한을 보장합니다).
 1. 1. Tencent Cloud EMR 클러스터를 사용하는 경우 Ranger의 서비스 정의 디렉터리는 `/usr/local/service/ranger/ews/webapp/WEB-INF/classes/ranger-plugins`에 둡니다.
 2. 자체 구축 hadoop 클러스터의 경우 ranger 디렉터리에서 hdfs 등 이미 ranger 서비스에 액세스 된 모듈을 찾아 디렉터리 위치를 찾을 수 있습니다.
![ranger 서비스 정의 디렉터리](https://main.qcloudimg.com/raw/edb3882f1517f7231f2cc0a7f7a750f9.png)
2. GooseFS 디렉터리에 goosefs-ranger-plugin-${version}.jar 및 ranger-servicedef-goosefs.json을 넣고 읽기 권한을 가집니다.
3. Ranger 서비스를 재시작합니다.
4. Ranger에서 아래 명령어에 따라 GooseFS Service에 가입합니다.
```bash
# 서비스를 생성하려면 Ranger 관리자 계정 및 암호, Ranger 서비스 주소를 입력해야 합니다.
# Tencent Cloud EMR 클러스터의 경우, 관리자는 root이고, 암호는 EMR 클러스터를 구축할 때 설정한 root 암호이며, ranger 서비스의 IP는 EMR 서비스의 Master IP입니다.
adminUser=root
adminPasswd=xxxx

rangerServerAddr=10.0.0.1:6080

curl -v -u${adminUser}:${adminPasswd} -X POST -H "Accept:application/json" -H "Content-Type:application/json" -d @./ranger-servicedef-goosefs.json http://${rangerServerAddr}/service/plugins/definitions

# 서비스 가입이 완료되면 서비스 ID가 반환되므로 반드시 이 ID를 기록해 두시기 바랍니다.
# GooseFS 서비스를 삭제하려면, 방금 반환된 서비스 ID를 전달하고 다음 명령을 실행합니다.
serviceId=104
curl -v -u${adminUser}:${adminPasswd} -X DELETE -H "Accept:application/json" -H "Content-Type:application/json" http://${rangerServerAddr}/service/plugins/definitions/${serviceId}
```
5. 생성에 성공하면 Ranger의 Web 콘솔에서 GooseFS 관련 서비스를 볼 수 있습니다.
![ranger의 web 콘솔](https://main.qcloudimg.com/raw/3099cacd0fc907ea83ba418b5c873106.png)
6. GooseFS 서비스 측에서 [+]를 클릭하여 goosefs 서비스 인스턴스를 정의합니다.
![ranger의 web 콘솔에서 goosefs 서비스 인스턴스 정의](https://main.qcloudimg.com/raw/8142de87171eb21982c6bfda09e1c3d4.png)
7. 새로 생성된 goosefs 서비스 인스턴스를 클릭하여 인증 policy를 추가합니다.
![인증 추가 policy](https://main.qcloudimg.com/raw/b1ecd8453400c99318b1ee9bcfb608ff.png)

#### GooseFS Master측에 GooseFS Ranger 플러그인을 배포하고 Ranger 인증을 구성 및 활성화합니다.

1. goosefs-ranger-plugin-${version}.jar를 \${GOOSEFS_HOME}/lib 경로에 넣고 최소 읽기 권한을 가집니다.
2. ranger-goosefs-audit.xml, ranger-goosefs-security.xml 및 ranger-policymgr-ssl.xml 3개 파일을 `\${GOOSEFS_HOME}/conf` 경로에 넣고 필수 구성을 각각 입력합니다.
 - ranger-goosefs-security.xml：
    ```xml
    <configuration xmlns:xi="http://www.w3.org/2001/XInclude">
      <property>
        <name>ranger.plugin.goosefs.service.name</name>
        <value>goosefs</value>
      </property>
    
      <property>
        <name>ranger.plugin.goosefs.policy.source.impl</name>
        <value>org.apache.ranger.admin.client.RangerAdminRESTClient</value>
      </property>
    
      <property>
        <name>ranger.plugin.goosefs.policy.rest.url</name>
        <value>http://10.0.0.1:6080</value>
      </property>
    
      <property>
        <name>ranger.plugin.goosefs.policy.pollIntervalMs</name>
        <value>30000</value>
      </property>
    
      <property>
        <name>ranger.plugin.goosefs.policy.rest.client.connection.timeoutMs</name>
        <value>1200</value>
      </property>
    
      <property>
        <name>ranger.plugin.goosefs.policy.rest.client.read.timeoutMs</name>
        <value>30000</value>
      </property>
    </configuration>
    ```
 - ranger-goosefs-audit.xml(감사 미활성화, 설정하지 않아도 됨)
 - ranger-policymgr-ssl.xml
    ```xml
    <configuration>
      <property>
        <name>xasecure.policymgr.clientssl.keystore</name>
        <value>hadoopdev-clientcert.jks</value>
      </property>
    
      <property>
        <name>xasecure.policymgr.clientssl.truststore</name>
        <value>cacerts-xasecure.jks</value>
      </property>
    
      <property>
        <name>xasecure.policymgr.clientssl.keystore.credential.file</name>
        <value>jceks://file/tmp/keystore-hadoopdev-ssl.jceks</value>
      </property>
    
      <property>
        <name>xasecure.policymgr.clientssl.truststore.credential.file</name>
        <value>jceks://file/tmp/truststore-hadoopdev-ssl.jceks</value>
      </property>
    </configuration>
    ```
3. goosefs-site.xml 파일에 다음과 같은 구성을 추가합니다.
```properties
...
goosefs.security.authorization.permission.type=CUSTOM
goosefs.security.authorization.custom.provider.class=org.apache.ranger.authorization.goosefs.RangerGooseFSAuthorizer
...
```
4. \${GOOSEFS_HOME}/libexec/goosefs-config.sh에 goosefs-ranger-plugin-${version}.jar를 GooseFS 경로에 추가합니다.
```bash
...
GOOSEFS_RANGER_CLASSPATH="${GOOSEFS_HOME}/lib/ranger-goosefs-plugin-1.0.0-SNAPSHOT.jar"
GOOSEFS_SERVER_CLASSPATH=${GOOSEFS_SERVER_CLASSPATH}:${GOOSEFS_RANGER_CLASSPATH}
...
```

이렇게 모든 구성이 완료됩니다.

## 사용 인증

Hadoop 사용자에게 GooseFS의 루트 디렉터리에 대한 읽기 및 실행 권한은 있지만 쓰기는 허용하지 않는 정책을 추가하는 방법은 다음과 같습니다.

1. 다음과 같이 정책을 추가합니다.
![콘솔 정책 전달](https://main.qcloudimg.com/raw/7f0115000a0baef1089b281d415c095e.png)
2. 정책이 성공적으로 추가된 후, 정책을 인증하면 다음과 같이 정책이 적용된 것을 확인할 수 있습니다.
![사용 인증](https://main.qcloudimg.com/raw/a7c0a21220f8fcd3859e4fd98cc9a819.png)
