## 배경

Hadoop Ranger 권한 시스템은 빅 데이터 시나리오의 권한 솔루션입니다. 사용자는 스토리지 분리로 데이터를 COS에 호스팅합니다. COS는 Tencent Cloud CAM 권한 시스템을 사용하며 어떤 사용자 정보라도 권한 정책 등은 모두 로컬 Hadoop Ranger 시스템과 상이합니다. Tencent Cloud는 클라이언트의 원활한 사용을 위해 COS의 Ranger 액세스 솔루션을 제공합니다.


## 장점

- 세밀하게 분할된 권한 제어와 Hadoop 권한 로직 호환으로 사용자가 빅 데이터 모듈과 클라우드 호스팅 스토리지의 권한을 통합 관리합니다.
- 플러그 인에서 core-site 키를 설정할 필요가 없으며, 키는 COSRangerService에 통합 설치되어 있어 플레인 텍스트 키의 유출을 막을 수 있습니다.


## 솔루션 구성

![](https://main.qcloudimg.com/raw/47bcff91b29614141b9c88efd39e50c1.png)


Hadoop 권한 시스템에서의 인증은 Kerberos에서 제공하며 인증 권한은 Ranger에서 담당합니다. 다음과 같이 모듈을 제공하여 COS의 Ranger 권한 솔루션을 지원합니다.


1. cos-ranger-plugin: Ranger 서버의 서비스 정의 플러그 인을 제공합니다. 권한의 종류, 필요 매개변수 정의(COS의 bucket 매개변수와 region 매개변수)를 포함한 Ranger COS 서비스에 대한 설명을 제공합니다. 해당 플러그 인이 배포된 후 사용자는 Ranger의 제어 페이지에서 적절한 권한 정책을 작성할 수 있습니다.
2. COSRangerService: 이 서비스는 Ranger의 클라이언트를 통합하여 주기적으로 Ranger 서버와 권한 정책을 동기화하고 클라이언트의 인증 요청을 받은 후 로컬에서 권한 인증을 진행합니다. 또한 Hadoop에서 DelegationToken과 관련된 생성, 갱신 등의 인터페이스를 제공하며 모든 인터페이스는 Hadoop IPC를 통해 정의됩니다.
3. CosRangerClient: COSN 플러그 인을 동적으로 로딩하여 권한 인증 요청을 CosRangerService에 전달합니다.



## 배포 환경

- Hadoop 환경.
- ZooKeeper, Ranger, Kerberos 서비스(인증이 필요할 경우 설치).
>?위 서비스는 기술적으로 안정된 오픈 소스 모듈에 의한 것으로 클라이언트가 직접 설치할 수 있습니다.

## 배포 모듈


### COS-Ranger-Plugin 배포

COS-Ranger-Plugin이 Ranger Admin 콘솔 서비스 종류를 확장함에 따라 사용자가 Ranger 콘솔에서 COS와 관련된 작업 권한을 설정할 수 있습니다.

### 코드 주소

[Github](https://github.com/tencentyun/cos-ranger-service)의 ranger-plugin 디렉터리로 이동한 후 획득할 수 있습니다.

#### 버전

V1.0 이상 버전

#### 배포 순서
1. Ranger의 서비스 정의 디렉터리 하위에 새로운 COS 디렉터리를 생성합니다. 디렉터리 권한은 최소한 x와 r 권한이 필요합니다.
a. Tencent Cloud의 EMR 환경으로 경로는 ranger/ews/webapp/WEB-INF/classes/ranger-plugins입니다.
b. 자체구축된 hadoop 환경은 ranger 디렉터리에서 hdfs 등의 조회를 통해 이미 ranger 서비스의 모듈에 액세스하여 디렉터리 위치를 찾을 수 있습니다.
![](https://main.qcloudimg.com/raw/793f47a53343657a000b34b7ac66b074.png)
2. COS 디렉터리에 cos-chdfs-ranger-plugin-xxx.jar를 넣습니다. (jar 패키지는 최소한 r 권한이 있어야 합니다).
3. Ranger 서비스를 재시작합니다.
4. Ranger의 COS Service에 로그인하면 다음과 같은 명령어를 참고할 수 있습니다
```
## 서비스를 생성하려면 Ranger 관리자 계정 비밀번호 및 Ranger 서비스 주소를 입력해야 합니다.
## Tencent Cloud EMR 클러스터의 경우, 관리자 사용자는 root이고, 비밀번호는 emr 클러스터를 구축할 때 설정한 root 비밀번호이며, ranger 서비스의 IP는 EMR의 master 노드 IP로 바뀝니다.

adminUser=root
adminPasswd=xxxxxx
rangerServerAddr=10.0.0.1:6080

curl -v -u${adminUser}:${adminPasswd} -X POST -H "Accept:application/json" -H "Content-Type:application/json" -d @./cos-ranger.json http://${rangerServerAddr}/service/plugins/definitions

## 방금 정의된 서비스를 삭제하려면 서비스를 생성할 때 반환했던 서비스 ID를 입력합니다.
serviceId=102
curl -v -u${adminUser}:${adminPasswd} -X DELETE -H "Accept:application/json" -H "Content-Type:application/json" http://${rangerServerAddr}/service/plugins/definitions/${serviceId}
```
5. 서비스가 생성되면 Ranger 콘솔에서 COS 서비스를 다음과 같이 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/d1a6e2722d11f7177636a5e2c54226e3.png)
6. COS 서비스에서 [+]를 클릭하면 새로운 서비스 인스턴스가 정의되며 서비스 인스턴스 이름은 `cos.`서비스 설정과 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/2be86fb2b8232b16679b29e908f82d3a.png)
그중, policy.grantrevoke.auth.users는 후속 COSRangerService를 실행하는 사용자 이름(권한 정책 가져오기가 허용된 사용자)을 설정해야 합니다. 일반적으로 hadoop 설정을 권장하며 후속 COSRangerService는 이 사용자 이름을 사용하여 실행할 수 있습니다.
7. 새로 생성된 COS 서비스 인스턴스를 클릭하여 policy를 추가하면 다음과 같이 보여집니다.
![](https://main.qcloudimg.com/raw/58ded7125d5c5d161ca6e2f5a98d8e7b.png)
8. 리디렉션 인터페이스에서 다음과 같이 매개변수를 설정합니다.
 - **bucket**: 버킷 이름이며 examplebucket-1250000000이 예시입니다. [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에 로그인하여 조회할 수 있습니다.
 - **path**: COS객체 경로입니다. COS의 객체 경로가 /로 시작되지 않도록 주의하십시오.
    - include: 설정된 권한이 path 자체에 적용되었는지, 혹은 path 이외의 다른 경로에 적용되었는지 나타냅니다.
    - recursive: 권한이 path뿐만 아니라 path 경로의 서브 구성원(귀속되는 서브 구성원)에도 적용됨을 나타냅니다. 보통 path 설정을 디렉터리 시나리오로 사용합니다.
 - **user/group**: 사용자 이름과 사용자 그룹입니다. 둘 중 하나만 충족하면 되는 관계로, 사용자 이름 혹은 사용자 그룹 중 하나를 만족하면 상응하는 작업 권한을 보유할 수 있습니다.
 - **Permissions**:
    -  Read: 읽기 작업입니다. 객체 스토리지 안에 있는 GET, HEAD와 같은 작업에 대응하며, 객체 다운로드, 객체 메타데이터 조회 등을 포함합니다.
    - Write: 쓰기 작업입니다. COS 안에 있는 PUT과 같은 수정 작업으로 객체 업로드를 예로 들 수 있습니다.
    -  Delete: 삭제 작업입니다. 객체 스토리지 안에 있는 Object를 삭제합니다. Hadoop Rename 작업의 경우, 기존 경로에 대한 삭제 작업 권한과 신규 경로에 대한 입력 작업 권한이 필요합니다.
    - List: 순회 권한입니다. COS 안에 있는 List Object에 대응합니다.
![](https://main.qcloudimg.com/raw/00a619b4b963a9acf766411fad722fe4.png)

### COS-Ranger-Service 배포

COS-Ranger-Service는 전체 권한 시스템의 핵심으로, ranger 클라이언트를 통합하여 ranger client의 인증 요청, token 생성 및 갱신 요청, 임시 키 생성 요청을 담당합니다. 또한, 중요한 정보(Tencent Cloud 키 정보)가 있는 구역이기도 합니다. 보통 점프 서버에 배포되어 클러스터 관리자만 조회 및 설정 등의 작업을 할 수 있습니다. 

COS-Ranger-Service는 하나의 메인 서버와 다수의 데이터 노드로 구성된 HA를 배포하여 DelegationToken 상태가 HDFS까지 지속될 수 있도록 합니다. ZK 잠금 장치로 Leader 신분 정보를 결정합니다. Leader 신분을 획득한 서비스는 주소를 ZK로 입력하여 COS Ranger Client가 라우팅 어드레스 지정을 할 수 있도록 합니다.

### 코드 주소
[Github](https://github.com/tencentyun/cos-ranger-service)의 cos-ranger-server 디렉터리로 이동하여 얻을 수 있습니다.

#### 버전
V1.0 이상 버전

#### 배포 순서
1. COS Ranger Service 서비스 코드를 클러스터 기기 몇 대에 복사하고, 생성 환경은 최소 기기 두 대(메인 기기와 예비용 기기)를 권장합니다. 중요한 정보를 다루기 때문에 점프 서버 혹은 권한이 엄격히 통제되는 기기를 권장합니다.
2. cos-ranger.xml 파일의 관련 설정을 수정합니다. 이중 반드시 수정해야 하는 설정 항목은 다음과 같이 보여집니다. 설정 항목 설명은 파일의 주석 설명을 참조하십시오.
 - qcloud.object.storage.rpc.address
 - qcloud.object.storage.enable.cos.ranger
 - qcloud.object.storage.zk.address
 -  qcloud.object.storage.cos.secret.id
 -  qcloud.object.storage.cos.secret.key
3. ranger-cos-security.xml 파일의 관련 설정을 수정합니다. 이중 반드시 수정해야 하는 설정 항목은 다음과 같이 보여집니다. 설정 항목 설명은 파일의 주석 설명을 참조하십시오.
 -  ranger.plugin.cos.policy.cache.dir
 -  ranger.plugin.cos.policy.rest.url
4. start_rpc_server.sh에서 hadoop_conf_path, java.library.path의 설정을 수정합니다. 이 두 가지 설정은 각각 hadoop 구성 파일이 들어 있는 디렉터리(core-site.xml, hdfs-site.xml 등) 및 hadoop native lib 경로를 가리킵니다.

5. 다음 명령어를 실행하여 서비스를 시작합니다.
```
chmod +x start_rpc_server.sh
nohup ./start_rpc_server.sh &> nohup.txt &
```
6. 실행에 실패하면 log의 error 로그에 잘못된 정보가 있는지 조회합니다.

 

### COS-Ranger-Client 배포

COS-Ranger-Client는 hadoop cosn 플러그 인으로 동적 로딩을 하며 COS-Ranger-Service와 관련 있는 요청을 프록시 액세스합니다. 임시 키 획득, token 획득, 인증 작업 등이 포함됩니다.

### 코드 주소
[Github](https://github.com/tencentyun/cos-ranger-service)의 cos-ranger-client 디렉터리로 이동하여 얻을 수 있습니다.

#### 버전
V1.0 이상 버전

#### 배포 방식
1. cos-ranger-client jar 패키지를 COSN과 같은 디렉터리에 복사합니다(hadoop 자체 버전과 일치하는 jar 패키지 복사를 선택하십시오).
2. core-site.xml에서 다음과 같은 설정 항목을 추가하십시오.
```xml
<configuration>
           <!--*****필수 설정********-->
           <!-- zk의 주소, 클라이언트가 zk에서 조회하여 획득한 ranger-service의 서비스 주소 -->
           <property>
               <name>qcloud.object.storage.zk.address</name>
               <value>10.0.0.8:2121</value>
           </property>

           <!--***옵션 설정****-->           
           <!-- cos ranger service에서 사용하는 kerberos 근거를 설정하고, cos ranger service의 설정을 참조하여 반드시 일치하도록 합니다. 인증 요구가 없으면 설정하지 않아도 됩니다. -->
           <property>                
					 <name>qcloud.object.storage.kerberos.principal</name>
					 <value>hadoop/_HOST@EMR-XXXX</value>
           </property>

        <!--***옵션 설정****-->  
         <!-- zk에 기록된 ranger server의 ip 주소 경로로 기본값이 사용되었으며 설정은 반드시 cos-ranger-service의 설정과 일치해야 합니다. -->
          <property>              
					<name>qcloud.object.storage.zk.leader.ip.path</name> 
					<value>/ranger_qcloud_object_storage_leader_ip</value>
          </property>
</configuration>
```



### COSN 배포 

#### 버전

V5.9.0 이상 버전

#### 배포 방식
COSN 플러그 인 배포 방법은 [Hadoop 툴](https://intl.cloud.tencent.com/document/product/436/6884) 문서를 참조하시고 다음 몇 가지 사항을 주의하십시오.

1. ranger를 사용한 후, fs.cosn.userinfo.secretId와 fs.cosn.userinfo.secretKey 키 정보는 설정이 필요하지 않습니다. COSN 플러그 인은 향후 COSRangerService를 통해 임시 키를 획득합니다.
2. fs.cosn.credentials.provider는 org.apache.hadoop.fs.auth.RangerCredentialsProvider 설정이 되어야만 Ranger를 통해 다음과 같은 인증 진행이 가능합니다.
```
<property>
         <name>fs.cosn.credentials.provider</name>
         <value>org.apache.hadoop.fs.auth.RangerCredentialsProvider</value>
</property>
```

## 인증

1. hadoop cmd를 사용하여 COSN 액세스와 관련된 작업을 실행합니다. 예시는 다음과 같습니다.
```plaintext
#bucket, 경로 등을 자신의 실제 정보로 바꿉니다.
hadoop fs -lscosn://examplebucket-1250000000/doc
hadoop fs -put ./xxx.txt cosn://examplebucket-1250000000/doc/
hadoop fs -get cosn://examplebucket-1250000000/doc/exampleobject.txt
hadoop fs -rmcosn://examplebucket-1250000000/doc/exampleobject.txt
```
2. MR Job을 사용해 인증을 진행합니다. 인증 전 Yarn, Hive 등 관련 서비스를 재시작해야 합니다.


## FAQ

#### kerberos 설치가 꼭 필요한가요?
Kerberos는 인증 요구를 충족합니다. Kerberos가 있는 클러스터의 경우 사용자가 신뢰할 수 있습니다. 내부에서만 사용 가능한 클러스터가 그 예입니다. 권한이 없는 클라이언트의 오작동을 방지하기 위해 사용자가 인증 작업만 진행한다면 Kerberos를 설치하지 않고 ranger로만 인증 작업을 해도 됩니다. 또한, Kerberos는 일부 성능을 저하시킬 수도 있습니다. 클라이언트는 보안 및 성능에 관련된 니즈를 종합적으로 고려해야 합니다. 인증이 필요할 경우, Kerberos를 실행한 후 COS Ranger Service와 COS Ranger Client에 관련된 설정 항목을 세팅해야 합니다.

#### Ranger를 활성화했는데 어떠한 Policy도 설정되어 있지 않거나 다른 Policy와 매칭되지 않았을 경우 어떻게 작업하나요?
어떠한 Policy와 매칭되지 않은 경우 기본적으로 해당 작업이 거부됩니다.

#### COS Ranger Service의 키 설정은 서브 계정도 가능한가요?
서브 계정도 가능합니다. 그러나 bucket을 실행할 수 있는 권한이 있어야만, COSN 플러그 인에 들어가 관련 작업을 할 수 있는 임시 키 생성이 가능합니다. 일반적으로 여기서 설정하는 키는 해당 bucket의 모든 권한을 갖기를 권장합니다.

#### 임시 키는 어떻게 업데이트되나요? COS를 방문할 때마다 COS Ranger Service에서 임시 키를 획득해야 하나요?
임시 키는 COSN 플러그 인 cache에 있으며, 주기적으로 비동기화 업데이트됩니다.