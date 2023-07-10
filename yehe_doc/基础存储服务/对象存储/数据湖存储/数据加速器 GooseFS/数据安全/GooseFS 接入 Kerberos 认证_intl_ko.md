## 개요

Kerberos는 빅 데이터 에코시스템에서 널리 사용되는 통합 인증 서비스입니다. 빅 데이터 및 데이터 레이크 시나리오를 위한 스토리지 가속 서비스인 GooseFS를 사용하면 클러스터 노드와 사용자 액세스 요청을 Kerberos에 연결할 수 있습니다. 이 문서에서는 Kerberos에 대한 GooseFS 연결을 구성하는 방법과 Hadoop Delegation Token을 사용하여 인증하는 방법을 설명합니다.

## Kerberos 인증 아키텍처에 GooseFS 연결

![](https://qcloudimg.tencent-cloud.cn/raw/f3fa3d97e385d113faf053cb989edef7.png)

## GooseFS용 Kerberos 인증의 강점

- 인증 아키텍처 및 프로세스는 기본적으로 Kerberos에 대한 HDFS 연결과 동일합니다. HDFS에서 Kerberos 인증 프로세스가 활성화된 애플리케이션은 GooseFS로 쉽게 마이그레이션할 수 있습니다.
- Hadoop Delegation Token 인증 메커니즘이 지원되므로 GooseFS는 Hadoop 기반 애플리케이션 작업과 잘 호환됩니다.

## Kerberos에 대한 GooseFS 연결 구성

### 전제 조건

-GooseFS 1.3.0 이상.
- Kerberos KDC 서비스가 귀하의 환경에 존재하며, GooseFS 및 애플리케이션 클라이언트가 포트에 정상적으로 액세스 할 수 있는지 확인합니다.

### Kerberos KDC에서 GooseFS ID 정보 생성

먼저 연결을 구성하기 전에 Kerberos KDC의 GooseFS 클러스터 Server 및 Client에 대한 Kerberos ID를 생성하십시오. 여기에서 `kadmin.local`은 **Kerberos KDC 서버**에서 생성에 사용됩니다.
>! root/sudo 권한으로`kadmin.local` 툴을 실행해야합니다.
>

```shell
$ sudo kadmin.local
```

명령이 성공적으로 실행되면 kadmin의 인터랙티브 shell 환경에 들어갑니다.

```shell
Authenticating as principal root/admin@GOOSEFS.COM with password.
kadmin.local:  
```

여기서`kadmin.local`은 인터랙티브 실행 환경의 명령 프롬프트를 나타냅니다.

#### GooseFS Server / Client ID 생성

다음은 Kerberos 구성 방법 설명을 위한 간단한 테스트 클러스터와 사용 사례 예시입니다.
1. 클러스터 환경 설명
하나의 Master 듀얼 Worker의 Standalone 아키텍처가 사용됩니다.
 - Master(JobMaster): 172.16.0.1
 - Worker1(JobWorker1): 172.16.0.2
 - Worker2(JobWorker2): 172.16.0.3
 - Client: 172.16.0.4
2.`kadmin.local`에서 Server 및 Client ID를 생성합니다.
```shell
kadmin.local: addprinc -randkey goosefs/172.16.0.1@GOOSEFS.COM
kadmin.local: addprinc -randkey client/172.16.0.4@GOOSEFS.COM
```
>! 여기서`-randkey`를 사용하는 이유는, Server 또는 Client GooseFS 로그인 시 일반 텍스트 암호 대신 `keytab` 파일 인증을 사용합니다. password로 로그인 시 ID 정보를 사용하려면 이 필드를 제거 할 수 있습니다.
>
3. 각 ID에 대해 `keytab` 파일을 생성하고 내보내기합니다.
```shell
kadmin.local: xst -k goosefs_172_16_0_1.keytab goosefs/172.16.0.1@GOOSEFS.COM
kadmin.local: xst -k client_172_16_0_4.keytab client/172.16.0.4@GOOSEFS.COM
```

### GooseFS Server/Client 액세스용 Kerberos 인증 구성

1. 위에서 내보내기한 `keytab` 파일을 해당 서버로 배포합니다. 여기서는 `${GOOSEFS_HOME}/conf/` 경로를 사용하는 것이 좋습니다.
```shell
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.1:${GOOSEFS_HOME}/conf/
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.2:${GOOSEFS_HOME}/conf/
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.3:${GOOSEFS_HOME}/conf/
$ scp client_172_16_0_4.keytab <username>@172.16.0.4:${HOME}/.goosefs/
```
2. 해당 서버에서 Server Principal KeyTab 파일이 GooseFS Server 실행 시 사용되는 사용자/사용자 그룹에 속하는 사용자/사용자 그룹을 변경하여 GooseFS에 실행 시 필요한 읽기 권한을 부여합니다.
```shell
$ chown <GooseFS_USER>:<GOOSEFS_USERGROUP> goosefs_172_16_0_1.keytab
$ # Unix 액세스 권한 비트를 수정합니다
$ chmod 0440 goosefs_172_16_0_1.keytab
```
3. Client 파일 읽기 권한을 보장하기 위해 Client KeyTab 파일이 GooseFS 요청을 시작하는 클라이언트 계정에 속하는 사용자/사용자 그룹을 변경하십시오.
```shell
$ chown <client_user>:<client_usergroup> client_172_16_0_4.keytab
$ # Unix 액세스 권한 비트를 수정합니다
$ chmod 0440 client_172_16_0_4.keytab
```

#### Server 및 Client의 GooseFS 구성

1. Master/Worker Server의 goosefs-site.properties
```properties

# Security properties
# Kerberos properties
goosefs.security.authorization.permission.enabled=true
goosefs.security.authentication.type=KERBEROS
goosefs.security.kerberos.unified.instance.name=172.16.0.1
goosefs.security.kerberos.server.principal=goosefs/172.16.0.1@GOOSEFS.COM
goosefs.security.kerberos.server.keytab.file=${GOOSEFS_HOME}/conf/goosefs_172_16_0_1.keytab

```
GooseFS Server에서 인증을 구성한 후 구성이 적용되도록 전체 클러스터를 다시 시작합니다.
2. Client의 goosefs-site.properties
```properties
# Security properties
# Kerberos properties
goosefs.security.authorization.permission.enabled=true
goosefs.security.authentication.type=KERBEROS
goosefs.security.kerberos.unified.instance.name=172.16.0.1
goosefs.security.kerberos.server.principal=goosefs/172.16.0.1@GOOSEFS.COM
goosefs.security.kerberos.client.principal=client/172.16.0.4@GOOSEFS.COM
goosefs.security.kerberos.client.keytab.file=${GOOSEFS_HOME}/conf/client_172_16_0_4.keytab

```
>! Kerberos 인증 시스템에서와 같이 KDC는 현재 Client가 액세스 한 Service를 알아야 하며, GoosFS는 Server principal을 사용하여 현재 Client가 요청한 Service를 식별해야 합니다.
>

이 시점에서 GooseFS는 Kerberos의 기본 인증 서비스에 연결되었으며 클라이언트가 시작한 모든 요청은 이후 Kerberos가 인증합니다.

