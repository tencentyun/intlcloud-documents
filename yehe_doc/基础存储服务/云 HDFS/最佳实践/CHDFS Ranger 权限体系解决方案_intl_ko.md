## 배경

빅 데이터 사용자는 스토리지-컴퓨팅 분리를 통해 데이터를 클라우드 HDFS(Cloud HDFS，CHDFS)에 호스팅합니다. CHDFS의 권한 시스템 관리 기능은 HDFS와 유사합니다. Hadoop Ranger는 HDFS 권한을 기본으로 하여 사용자 그룹 권한 설정, 특정 접두사에 대한 권한 설정 같은 더욱 정교한 권한 관리 기능을 제공하며 Hadoop Ranger은 스토리지 권한 관리뿐 만 아니라 YARN，Hive 등 모듈 권한 관리 기능도 지원하는 원스톱 솔루션입니다. 고객의 기존 사용 습관을 고려하고 보다 편리하게 사용할 수 있도록 CHDFS의 Ranger 연결 솔루션을 제공하여 Ranger로 CHDFS 권한을 관리할 수 있게 하였습니다.


## 강점

- 세밀한 권한 관리, Hadoop 권한 사용법과 호환
- 빅 데이터 모듈과 클라우드 호스팅 스토리지 권한 통합 관리

## 솔루션 아키텍처

![](https://main.qcloudimg.com/raw/ccbe75fb92788fce02b02cf0ce63de1c.png)

Hadoop 권한 시스템에서 인증은 Kerberos에서, 권한 인증은 Ranger에서 담당합니다. 여기에 다음과 같은 모듈을 제공하여 CHDFS의 Ranger 권한 솔루션을 지원합니다.

- CHDFS-Ranger-Plugin: Ranger 서버의 서비스 정의 플러그 인을 제공합니다. Ranger CHDFS 서비스 설명을 제공하여 해당 플러그인 설치 후, 바로 Ranger 제어 페이지에서 해당 권한 정책을 작성할 수 있습니다. 
- COSRangerService: 이 서비스는 Ranger의 클라이언트를 통합하여 주기적으로 Ranger 서버와 권한 정책을 동기화하고, 클라이언트의 인증 요청을 받은 후 로컬에서 권한 인증을 진행합니다. 또한, Hadoop에서 DelegationToken과 관련된 생성, 지속 대여 등의 인터페이스를 제공하며, 모든 인터페이스는 Hadoop IPC를 통해 정의됩니다.
- CosRangerClient: COSN 플러그 인을 동적으로 로딩하여 권한 인증 요청을 CosRangerService에 전달합니다.

## 설치 환경

- Hadoop 환경
- ZooKeeper, Ranger, Kerberos 서비스(인증이 필요할 경우 설치).

>?위 서비스는 기술적으로 안정된 오픈 소스 모듈에 의한 것으로 클라이언트가 직접 설치할 수 있습니다.
>

## 설치 모듈

<dx-tabs>
::: CHDFS-Ranger-Plugin\s배포
CHDFS-Ranger-Plugin이 Ranger Admin 콘솔의 서비스 종류를 확장함에 따라, 사용자는 Ranger 콘솔에서 CHDFS와 관련된 작업 권한을 설정할 수 있습니다.

#### 코드 주소

[Github](https://github.com/tencentyun/cos-ranger-service)의 ranger-plugin 목록으로 이동 후 획득할 수 있습니다.

#### 버전

V1.2 이상 버전

#### 설치 절차

1. Ranger의 서비스 정의 디렉터리 하위에 새로운 COS 디렉터리를 만듭니다. (주의: 디렉터리 권한은 최소한 x와 r 권한이 필요합니다).
 1. Tencent Cloud의 EMR 환경으로, 경로는 ranger/ews/webapp/WEB-INF/classes/ranger-plugins입니다.
 2. 자체구축한 hadoop 환경에서는 ranger 디렉터리의 find hdfs 등 방식을 통해 ranger 서비스에 액세스한 모듈 및 ranger-plugins 디렉터리 위치를 찾을 수 있습니다. 
![](https://main.qcloudimg.com/raw/679f61339b8c3864a84b3b757dd84815.png)
2. CHDFS 디렉터리에 cos-chdfs-ranger-plugin-xxx.jar를 넣습니다. jar 패키지는 최소한 r 권한이 필요합니다. 
3. Ranger 서비스를 재시작합니다.
4. Ranger에 CHDFS Service를 등록합니다. 다음과 같은 명령어를 참고할 수 있습니다
<dx-codeblock>
::: plaintext
## 서비스를 생성하려면 Ranger 관리자 계정 암호 및 Ranger 서비스 주소를 입력해야 합니다.
## Tencent Cloud EMR 클러스터의 경우, 관리자는 root이고, 암호는 emr 클러스터를 구축할 때 설정한 root 암호이며, ranger 서비스의 IP는 EMR의 master 노드 IP로 바뀝니다.
adminUser=root
adminPasswd=xxxxxx
rangerServerAddr=10.0.0.1:6080
curl -v -u${adminUser}:${adminPasswd} -X POST -H "Accept:application/json" -H "Content-Type:application/json" -d @./chdfs-ranger.json http://${rangerServerAddr}/service/plugins/definitions
## 방금 정의된 서비스를 삭제하려면 관련 서비스를 생성할 때 반환했던 서비스 ID를 입력합니다.
serviceId=102
curl -v -u${adminUser}:${adminPasswd} -X DELETE -H "Accept:application/json" -H "Content-Type:application/json" http://${rangerServerAddr}/service/plugins/definitions/${serviceId}
:::
</dx-codeblock>
5. 서비스가 생성되면 Ranger 콘솔에서 CHDFS 서비스를 다음과 같이 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/163aac38c68931f51ab34c221ea3cef1.png)
6. CHDFS 서비스에서 [+]를 클릭해 새로운 서비스의 인스턴스를 정의합니다. 인스턴스 이름은 chdfs 또는 chdfs_test 처럼 사용자 정의가 가능합니다. 서비스 설정은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/255869b8c485a93427585d21476ec001.png)
policy.grantrevoke.auth.users는 COSRangerService 서비스를 실행할 수 있는 사용자 이름을 설정해야 합니다. 일반적으로 hadoop 설정이 권장되며, 후속 COSRangerService는 이 사용자 이름으로 실행할 수 있습니다.
7. 새로 생성된 CHDFS 서비스 인스턴스를 클릭하고 다음과 같이 policy를 추가합니다.
![](https://main.qcloudimg.com/raw/f0d76ecf787eec3340f7d923e65b9b48.png)
8. 리디렉션 인터페이스에서 다음과 같이 매개변수를 설정합니다. 자세한 설명은 다음과 같습니다. 
![](https://main.qcloudimg.com/raw/317e1b5cb39abae6904552cb1ebade58.png)
 - **MountPoint**:  마운트 포인트 이름으로, 형식은 f4mxxxxxx-yyyy 등 입니다. [CHDFS 콘솔](https://console.cloud.tencent.com/chdfs/filesystem)에 로그인하여 조회할 수 있습니다. 
 - **path**: CHDFS 경로입니다. 주의사항: CHDFS 경로는 반드시 `/`로 시작해야 합니다. 
    - include: 설정된 권한이 path 자체에 적용되었는지, 혹은 path 이외의 다른 경로에 적용되었는지 나타냅니다.
    - recursive: 권한이 path 외에 path 경로의 하위 구성원(귀속되는 구성원)에도 적용된다는 것을 나타냅니다. 보통 path 설정을 디렉터리로 사용하는 경우입니다.
 - **user/group**: 사용자 이름과 사용자 그룹입니다. 둘 중 하나만 충족하면 되는 관계로, 사용자 이름 혹은 사용자 그룹 중 하나를 만족하면 상응하는 작업 권한을 보유할 수 있습니다.
 - **Permissions**:
    - Read: 읽기 작업입니다. 객체 다운로드, 객체 메타데이터 조회 등 COS의 GET, HEAD와 같은 작업에 대응됩니다 
    - Write: 쓰기 작업입니다.  객체 업로드 같이 COS의 PUT과 같은 수정 작업에 대응됩니다.
    -  Delete: 삭제 작업입니다. COS의 Object 삭제와 대응됩니다. Hadoop의 Rename 작업의 경우, 기존 경로에 대한 삭제 작업과 신규 경로에 대한 입력 작업 권한이 필요합니다.
    - List: 탐색 권한입니다. COS의 List Object에 대응됩니다.

:::
::: COS-Ranger-Service\s배포
COS-Ranger-Service는 전체 권한 시스템의 핵심으로, ranger 클라이언트를 통합하여 ranger client의 인증 요청, token 생성 및 지속 대여 요청, 임시 키 생성 요청을 접수합니다. 또한, 중요한 정보(Tencent Cloud 키 정보)가 있는 구역이기도 합니다. 보통 점프 서버에 설치되어 클러스터 관리자만 조회 및 설정 등의 작업을 할 수 있습니다.

COS-Ranger-Service는 하나의 메인 서버와 다수의 데이터 노드로 구성된 HA를 지원하여 HDFS에서 DelegationToken Status가 지속될 수 있도록 합니다. ZK 잠금 장치로 Leader의 신분을 결정합니다. Leader의 신분을 획득한 서비스는 주소를 ZK에 입력하여 COS Ranger Client가 라우팅 어드레스 지정을 할 수 있도록 합니다.

#### 코드 주소

[Github](https://github.com/tencentyun/cos-ranger-service)의 cos-ranger-server 디렉터리로 이동하여 얻을 수 있습니다.

#### 버전

V1.2 이상 버전

#### 설치 절차

1. COS Ranger Service 서비스 코드를 클러스터의 기기 몇 대에 복사하고, 생성 환경은 최소 기기 두 대(메인 기기와 예비용 기기)를 권장합니다. 중요한 정보를 다루기 때문에 점프 서버 혹은 권한이 엄격히 통제되는 기기를 권장합니다.
2. cos-ranger.xml 파일의 관련 설정을 수정합니다. 이중 수정해야 하는 설정 항목은 다음과 같습니다. 설정 항목 설명은 파일의 주석 설명을 참조하십시오.
 -  qcloud.object.storage.rpc.address
 -  qcloud.object.storage.status.port
 -  qcloud.object.storage.enable.chdfs.ranger
 -  qcloud.object.storage.zk.address
3. ranger-chdfs-security.xml 파일의 관련 설정을 수정합니다. 이중 수정해야 하는 설정 항목은 다음과 같습니다. 설정 항목 설명은 파일의 주석 설명을 참고하십시오.
 -  ranger.plugin.chdfs.policy.cache.dir
 -  ranger.plugin.chdfs.policy.rest.url
 -  ranger.plugin.chdfs.service.name
4. start_rpc_server.sh에서 hadoop_conf_path, java.library.path의 설정을 수정합니다. 이 두 가지 설정은 각각 hadoop 설정 파일이 들어 있는 디렉터리(core-site.xml, hdfs-site.xml 등) 및 hadoop native lib 경로를 가리킵니다.
5. 다음 명령어를 실행하여 서비스를 시작합니다.
```
chmod +x start_rpc_server.sh
nohup ./start_rpc_server.sh &> nohup.txt &
```
6. 실행에 실패하면 log의 error 로그에 잘못된 정보가 있는지 조회합니다.
7. cos-ranger-service는 HTTP 포트 상태(포트 이름은 qcloud.object.storage.status.port, 기본값은 9998)표시를 지원합니다. 사용자는 다음의 명령어를 사용하여 상태 정보(leader 포함 여부, 인증 권한 통계 등)를 알 수 있습니다.
```
# 아래의 10.xx.xx.xxx를 ranger service를 설치할 기기 IP로 대체하십시오.
# port 9998을 qcloud.object.storage.status.port의 설정값으로 세팅하십시오.
curl -v http://10.xx.xx.xxx:9998/status
```

:::
::: COS-Ranger-Client\s설치
COS-Ranger-Client는 hadoop chdfs 플러그 인의 동적 로딩으로 token 획득, 인증 작업 등 COS-Ranger-Service 관련 요청을 대신 액세스해 줍니다.

#### 코드 주소

[Github](https://github.com/tencentyun/cos-ranger-service)의 cos-ranger-client 디렉터리로 이동하여 얻을 수 있습니다.

#### 버전

V1.0 이상 버전

#### 배포 방식
1. cos-ranger-client jar 패키지를 CHDFS 플러그 인과 같은 디렉터리에 복사합니다(본인의 hadoop 자체 버전과 일치하는 jar 패키지 선택).
2. core-site.xml에 다음과 같은 설정 항목을 추가하십시오.
<dx-codeblock>
::: xml
```
<configuration>
           <!--*****필수 설정********-->
           <!-- zk의 주소, 클라이언트가 zk에서 조회하여 획득한 ranger-service의 서비스 주소 -->
           <property>
               <name>qcloud.object.storage.zk.address</name>
               <value>10.0.0.8:2121</value>
           </property>

           <!--***선택 가능한 설정****-->           
           <!-- cos ranger service에서 사용하는 kerberos 근거를 설정하고, cos ranger service의 설정을 참고하여 반드시 일치하도록 합니다. 인증 요구가 없으면 설정하지 않아도 됩니다. -->
           <property>                
					 <name>qcloud.object.storage.kerberos.principal</name>
					 <value>hadoop/_HOST@EMR-XXXX</value>
           </property>

         <!--***선택 가능한 설정****-->  
         <!-- zk에 기록된 ranger server의 ip 주소 경로, 여기에 사용된 기본값과 설정은 반드시 cos-ranger-service의 설정과 일치해야 합니다. -->
          <property>              
					<name>qcloud.object.storage.zk.leader.ip.path</name> 
					<value>/ranger_qcloud_object_storage_leader_ip</value>
          </property>
</configuration>
```
:::
</dx-codeblock>
:::
::: CHDFS\s설치

#### 버전

V2.1 이상 버전

#### 설치 방식

CHDFS 플러그인의 설치 방법은 [CHDFS 마운트](https://intl.cloud.tencent.com/document/product/1106/41965) 문서를 참고하십시오. 다음 방법을 추가하면 ranger를 활성화할 수 있습니다. 


<dx-codeblock>
::: plaintext 
```
    <property>
        <name>fs.ofs.ranger.enable.flag</name> 
        <value>true</value>
    </property>
```
:::
</dx-codeblock>
:::
</dx-tabs>


## 인증

1. 다음과 같이 hadoop cmd로 chdfs 액세스 관련 작업을 실행합니다.
```plaintext
# 마운트 포인트, 경로 등을 본인의 실제 정보로 변경합니다. 
hadoop fs -ls ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/doc
hadoop fs -put ./xxx.txt ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/doc/
hadoop fs -get ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/exampleobject.txt
hadoop fs -rm ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/exampleobject.txt
```
2. MR Job을 사용하여 인증합니다. 인증 전 Yarn, Hive 등 관련 서비스를 재시작해야 합니다.


## FAQ

#### kerberos 설치가 꼭 필요한가요?

내부 사용 클러스터처럼 클러스터 내의 사용자를 모두 신뢰할 수 있다면 Kerberos를 설치하여 인증할 수 있습니다. 권한이 없는 사람의 작업 오류를 막기 위해 단순히 인증 작업만 하는 경우 Kerberos 설치 없이 ranger만으로도 인증이 가능합니다. 
Kerberos를 설치하면 성능 저하가 발생할 수 있으니 본인의 보안 및 성능 관련 사항에 맞춰 신중히 선택하십시오. 인증이 필요한 경우, Kerberos 실행한 후 COS Ranger Service 및 COS Ranger Client 관련 설정 항목을 설정해야 합니다. 

#### Ranger를 실행했는데 Policy가 설정되어 있지 않거나 Policy가 매칭되지 않았을 경우, 어떻게 작업하나요?

Policy가 매칭되지 않았을 경우 기본적으로 해당 작업이 거부됩니다.

#### ranger를 실행한 후, CHDFS에서 POSIX 인증을 진행하나요?

Ranger 인증은 클라이언트 환경에서 진행되는 것으로 ranger 인증을 거친 요청은 CHDFS 서버로 전달되어 POSIX 인증을 받습니다. 그렇기 때문에 Ranger에서 모든 권한을 제어하는 경우에는 CHDFS 콘솔에서 POSIX 권한을 비활성화하십시오. 
