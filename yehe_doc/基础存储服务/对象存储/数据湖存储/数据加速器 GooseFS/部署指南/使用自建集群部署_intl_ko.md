본문은 주로 스탠드 얼론, 클러스터 및 Tencent Cloud EMR 클러스터(현재 GooseFS의 버전을 통합 지원하지 않습니다)에 GooseFS를 표준화적으로 배포, 설정, 실행하는 방법에 대해 설명합니다. 

## 배포 환경 요건

### 하드웨어 환경

현재 GooseFS는 주요 x86/x64 아키텍처의 Linux/MacOS 실행 환경을 지원합니다. (**주의: MacOS M1 프로세서 지원은 검증되지 않았습니다**). 자세한 실행 노드 구성은 아래와 같습니다.

#### Master 노드

- **CPU**: 작업 클럭 속도는 1GHz 이상이어야 하며, Master 노드는 많은 양의 데이터를 처리해야 하므로 프로덕션 환경에서는 멀티 코어 프로세서를 사용하는 것이 좋습니다.
- **물리적 메모리**: 1GB 이상이어야 하며, 프로덕션 환경에서는 8GB 이상의 메모리를 사용하는 것이 좋습니다.
- **디스크**: 20GB 이상이어야 하며, 프로덕션 환경에는 고성능 NVME SSD 디스크를 메타데이터 캐시 디스크를 구비하는 것을 권장합니다(RocksDB 모드).

#### Worker 노드

- **CPU**: 작업 클럭 속도는 1GHz 이상이어야 하며, Worker 노드도 많은 동시 요청을 처리해야 하므로 프로덕션 환경에서는 멀티 코어 프로세서를 사용하는 것이 좋습니다.
- **물리적 메모리**: 2GB 이상이어야 하며, 성능 요구 사항에 따라 프로덕션 환경에 메모리를 할당할 수 있습니다. 예를 들어 Worker 노드 메모리에 많은 데이터 블록을 캐시해야 하거나 혼합 스토리지(MEM + SSD/HDD)를 사용해야 하는 경우 메모리에 캐시될 수 있는 데이터의 양에 따라 물리적 메모리를 할당할 수 있습니다. 사용하는 캐싱 모드에 관계없이 프로덕션 환경의 Worker에 대해 16GB의 물리적 메모리를 사용하는 것이 좋습니다.
- **디스크**: 20GB 이상의 SSD/HDD 디스크, 프로덕션 환경에 캐시해야 하는 데이터의 양을 추정하여 각 Worker 노드에 디스크 공간을 할당하는 것이 좋습니다. 또한 더 나은 성능을 위해 Worker 노드에 NVME SSD 디스크를 사용하는 것이 좋습니다.

### 소프트웨어 환경

- Red Hat Enterprise Linux 5.5+, Ubuntu Linux 12.04 LTS+(일괄 배포하지 않을 경우 지원 가능), CentOS 7.4+ 및 TLinux 2.x(Tencent Linux 2.x), Intel 아키텍처 기반의 MacOS 10.8.3 이상 버전. Tencent Cloud CVM 사용자는 CentOS 7.4, Tencent(TLinux 2.x) 혹은 TencentOS Server 2.4 버전의 운영 체제 사용을 권장합니다. 
- OpenJDK 1.8/Oracle JDK 1.8, 주의해야 할 점은 JDK 1.9 이상의 버전에 대한 지원은 인증되지 않았습니다. 
- SSH 툴 세트 (SSH와 SCP 툴 포함), Expect Shell (일괄 배포할 경우 필요), Yum 패키지 관리 툴을 지원합니다. 

### 클러스터 네트워크 환경

- Master/Worker 노드 간 외부 네트워크 혹은 내부 네트워크 통신이 가능합니다. 일괄 배포할 경우에는 Master가 정상적으로 외부 네트워크 소프트웨어 보관소에 액세스할 수 있거나, 패키지 관리 시스템의 내부 네트워크 소프트웨어 소스를 올바르게 구성할 수 있어야 합니다. 
- 클러스터는 외부 네트워크 혹은 내부 네트워크를 통해 COS 버킷이나 CHDFS 파일 시스템에 액세스 할 수 있습니다.  

### 보안 그룹과 사용자 권한 요구

일반적으로 GooseFS는 사용자가 전용 Linux 계정을 사용하여 GooseFS의 배포 실행을 권장합니다. 예를 들어 자체 구축 클러스터와 EMR 환경에서 hadoop 사용자를 통합하여 GooseFS를 배포 실행할 수 있습니다. 일괄 배포할 경우 이래와 같은 사용자의 기능과 권한이 추가적으로 필요합니다. 

- root로 전환하거나 sudo 권한을 사용할 수 있어야 합니다.
- 배포 실행 계정은 설치 디렉터리를 읽고 쓸 수 있는 권한이 있어야 합니다. 
- Master 노드에는 클러스터의 모든 Worker 노드에 로그인할 수 있는 SSH 권한이 있어야 합니다.
- 클러스터에서 해당하는 노드 역할은 대응 포트를 개방해야 합니다. Master (9200과 9201), Worker (9203과 9204), Job Master (9205, 9206, 9207), Job Worker (9208, 9209, 9210), Proxy (9211), LogServer (9212). 

## 스탠드 얼론 모드 배포 실행 (가상 분산형 아키텍처)

가상 분산형 아키텍처 배포는 주로 GooseFS의 체험과 디버깅에 적용되며 초급 사용자는 본인의 Linux 혹은 Mac 시스템 호스트에서 GooseFS를 빠르게 체험하고 디버깅할 수 있습니다. 

### 배포

1. 먼저 [GooseFS 바이너리 배포 패키지를 다운로드](https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-1.4.1-bin.tar.gz)합니다.
2. 배포 패키지 다운로드 후 압축 해제하여 GooseFS의 디렉터리로 이동하고 아래의 작업을 실행합니다. 
- conf/goosefs-site.properties.template 복사를 통해 conf/goosefs-site.properties 구성 파일을 생성합니다. 
```bash
 $ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```
- conf/goosefs-site.properties 구성 파일에서 `goosefs.master.hostname`를 `localhost`로 설정합니다. 
- conf/goosefs-site.properties 구성 파일에서 `goosefs.master.mount.table.root.ufs`를 로컬 파일 시스템의 디렉터리로 설정합니다. 예시: /tmp 혹은 /data/goosefs 등.

localhost의 SSH 비밀번호 없이 로그인으로 설정을 권장합니다. 그렇지 않을 경우 포맷과 실행 등 작업 시 localhost의 로그인 비밀번호를 입력해야 합니다. 

### 실행

아래 명령어를 실행하면 하나의 RamFS 파일 시스템 마운트를 완료할 수 있습니다. 

```bash
$ ./bin/goosefs-mount.sh SudoMount
```

다음과 같이 상기 명령을 실행하지 않고 GooseFS 클러스터를 시작할 때 직접 마운트할 수도 있습니다.

```bash
$ ./bin/goosefs-start.sh local SudoMount
```

실행 후 ‘jps’ 명령어를 통해 가상 분산형 모드에서의 모든 GooseFS의 프로세스를 확인할 수 있습니다. 

```bash
$ jps
35990 Jps
35832 GooseFSSecondaryMaster
35736 GooseFSMaster
35881 GooseFSWorker
35834 GooseFSJobMaster
35883 GooseFSJobWorker
35885 GooseFSProxy
```

그 후, ‘goosefs’ 명령 라인을 통해 namespace, fileSystem, job, talble의 각 작업을 실행할 수 있습니다. 예를 들어, 로컬 파일을 GooseFS에 업로드하고, 현재 GooseFS 루트 디렉터리의 파일과 디렉터리를 나열할 수 있습니다. 

```bash
$ goosefs fs copyFromLocal test.txt /
Copied file:///Users/goosefs/test.txt to /

$ goosefs fs ls /
-rw-r--r--  goosefs         staff                        0       PERSISTED 04-28-2021 04:00:35:156 100% /test.txt

```

GooseFS의 명령 라인은 사용자에게 GooseFS의 모든 명령 라인 인터페이스의 관리와 액세스를 제공하며, 네임스페이스(namespace), 테이블(table), 작업 (job), 자주 사용하는 파일 시스템(fs) 작업 등을 포함합니다. 자세한 정보는 공식 문서를 참고하거나 ‘goosefs -h’ 명령 라인 매개변수를 통하여 알 수 있습니다. 

## 클러스터 모드 배포 실행

클러스터 배포 실행은 주로 사용자 자체구축 IDC 클러스터의 프로덕션 환경 혹은 미통합 GooseFS의 Tencent Cloud EMR 프로덕션 환경에 대한 것이며, 구체적으로 Standalone 아키텍처 배포와 고가용성 (HA) 아키텍처 배포로 나뉩니다. 

GooseFS는 ‘scripts’ 디렉터리에서 SSH 비밀번호 없이 로그인 일괄 설정 및 GooseFS의 스크립트 툴 일괄 설치 배포를 제공하며, 사용자가 빠르고 간편하게 GooseFS 대규모 클러스터의 설치 배포를 할 수 있습니다. 사용자는 이전 챕터에서 배포 환경 요건의 일괄 배포 조건을 다시 확인할 수 있으며, 일괄 배포 실행 여부를 효율적으로 선택할 수 있습니다. 

### 일괄 배포 툴 소개

GooseFS는 ‘scripts’ 디렉터리에서 SSH 비밀번호 없이 로그인 일괄 설정 및 GooseFS의 스크립트 툴 일괄 배포 설치를 제공하며, 사용자가 실행 조건을 만족할 경우 아래 순서대로 일괄 배포 작업을 할 수 있습니다.  
- GooseFS 압축 해제 디렉터리 `cd ${GOOSEFS_HOME}`으로 이동합니다.
- `conf/masters` 및 `conf/workers`에서 호스트 이름 또는 IP 주소를 구성합니다.
- `scripts` 디렉터리로 이동하여 `commons.sh` 구성 파일의 `SCRIPT_EXEC_USER` 및 `SCRIPT_EXEC_PASSWORD`를 구성합니다. 그 다음 `root` 계정으로 전환하거나 `sudo`를 사용하여 `config_ssh.sh`를 실행하여 전체 클러스터에 대해 암호 없는 로그인을 구성할 수 있습니다.
- ‘비밀번호 없이 로그인’ 설정 완료 후 `validate_env.sh` 툴을 실행하여 전체 클러스터 설정 상태를 검증합니다. 
- 구성 파일 디렉터리 `ln -s conf ~/.goosefs`에 대한 소프트 링크를 생성합니다.
- 마지막으로 `goosefs copy .` 및 `goosefs copy ~/.goosefs`를 실행하여 goosefs 바이너리 패키지와 구성 파일을 모든 노드에 배포합니다.

모든 배포 프로세스 완료 후 `./bin/goosefs-start.sh all SudoMount` 실행을 통해 전체 클러스터를 실행할 수 있습니다. 모든 실행 로그는 `${GOOSEFS_HOME}/logs` 에 기록되도록 기본 설정되어 있습니다. 

### Standalone 아키텍처 배포

Standalone 아키텍처는 단일 Master 노드, 다중 Worker 노드의 클러스터 배포 아키텍처를 적용했습니다. 아래 순서를 참고하여 배포를 실행합니다. 

1. [GooseFS 바이너리 배포 패키지를 다운로드](https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-1.4.1-bin.tar.gz)합니다.
2. `tar zxvf goosefs-x.x.x-bin.tar.gz` 명령어를 통해 설치 경로 뒤에 압축 해제합니다. 일괄 배포 툴의 소개를 참고하여 클러스터의 일괄 배포를 설정 및 실행할 수 있으며, 아래 상세한 수동 배포 프로세스 문장을 참고할 수 있습니다. 

 (1) ‘conf’ 디렉터리에서 ‘template’ 파일을 복사하여 구성 파일을 생성합니다. 


```bash
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```

(2) `goosefs-site.properties` 구성 파일에서 아래와 같은 설정을 지정합니다.

```properties
goosefs.master.hostname=<MASTER_HOSTNAME>
goosefs.master.mount.table.root.ufs=<STORAGE_URI>
```




`goosefs.master.hostname` 을 단일 master 노드의 hostname 혹은 ip로 설정합니다. `goosefs.master.mount.table.root.ufs`는 지정 GooseFS 루트 디렉터리가 마운트한 유닉스 파일 시스템 (UFS) 경로 URI 입니다. 

>! 해당 URI는 반드시 Master와 Worker 노드 모두 액세스 할 수 있어야 하므로 로컬 디렉터리는 지원되지 않습니다.

예를 들어, GooseFS를 루트 경로로 한 COS 경로를 마운트 할 수 있습니다. goosefs.master.mount.table.root.ufs=cosn://bucket-1250000000/goosefs/.

‘masters’ 구성 파일에서 단일 Master 노드의 hostname 혹은 ip를 지정합니다. 예시:



```plaintext
# The multi-master Zookeeper HA mode requires that all the masters can access
# the same journal through a shared medium (e.g. HDFS or NFS).
# localhost
cvm1.compute-1.myqcloud.com
```

‘workers’ 구성 파일에서 모든 Worker 노드의 host 혹은 ip를 지정합니다. 예시: 

```plaintext
# An GooseFS Worker will be started on each of the machines listed below.
# localhost
cvm2.compute-2.myqcloud.com
cvm3.compute-3.myqcloud.com
```

모든 설정 완료 후  `./bin/goosefs copyDir conf/`을 실행하면 구성을 모든 노드에 동기화할 수 있습니다. 

마지막으로 `./bin/goosefs-start.sh all`을 실행하면 GooseFS 클러스터를 실행할 수 있습니다. 


### 고가용성 아키텍처 배포

단일 Master 노드의 Standalone 아키텍처는 단일 문제가 쉽게 발생됨으로 실제 프로덕션 환경은 다중 Master 노드를 배포하여 고가용성 시스템 아키텍처로 사용을 권장합니다. 다수의 Master 노드 중 한 노드만 프라이머리(leader) 노드로 외부 서비스를 제공하고, 그 외 노드는 세컨더리(Standby) 노드로 공유 로그 (Journal)를 동기화하며 프라이머리 노드와 동일한 파일 시스템 상태를 유지합니다. 프라이머리 노드가 장애로 다운 됐을 경우 세컨더리 노드 중의 하나를 자동으로 선택하여 프라이머리 노드 대신 외부 서비스를 제공합니다. 이로써 시스템의 단일 장애를 제거하여 고가용성 아키텍처를 사용할 수 있습니다. 

현재 GooseFS는 Raft 로그와 Zookeeper 기반의 2가지 방식으로 프라이머리/세컨더리 노드 상태의 강한 일치성을 지원합니다. 다음으로 이 2가지 배포 방식에 대하여 각각 소개하겠습니다. 

#### Raft 임베디드 로그 기반의 고가용성 배포 설정

설정 템플릿에 따라 구성 파일을 생성합니다.

```bash
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```

```properties
goosefs.master.mount.table.root.ufs=<STORAGE_URI>
goosefs.master.embedded.journal.addresses=<EMBBEDDED_JOURNAL_ADDRESS>
```

>? 위의 구성 항목의 설명은 다음과 같습니다. 
-  `goosefs.master.mount.table.root.ufs`는 GooseFS 루트 디렉터리의 기본 스토리지 URI 마운트로 설정을 합니다. 
-  `goosefs.master.embedded.journal.addresses`는 모든 세컨더리 노드의 `ip:embedded_journal_port` 혹은 `host:embedded_journal_port`를 설정합니다. embedded_journal_port는 9202로 기본 설정되어 있습니다. 예시: 192.168.1.1:9202, 192.168.1.2:9202, 192.168.1.3:9202.

Raft 임베디드 로그 기반의 배포 방식은 [copycat](https://github.com/atomix/copycat)의 Leader 선출 메커니즘에 종속됨으로 Raft의 HA 배포 아키텍처는 Zookeeper와 함께 사용할 수 없습니다. 

모든 설정 완료 후 아래 명령어를 통해 모든 설정을 동기화할 수 있습니다. 

```bash
$ ./bin/goosefs copyDir conf/
```

포맷 완료 후 바로 GooseFS 클러스터를 실행할 수 있습니다. 

```bash
$ ./bin/goosefs format
```

```bash
$ ./bin/goosefs-start.sh all
```
권한이 부족하다는 메시지가 표시되면 다음과 같이 재시작합니다.
```bash
$ ./bin/goosefs-stop.sh all
$ ./bin/goosefs-start.sh all SudoMount
```

아래 명령어를 통해 현재 프라이머리(Leader) 노드를 확인할 수 있습니다. 

```bash
$ ./bin/goosefs fs leader
```

아래 명령어를 통해 클러스터 상태를 확인할 수 있습니다. 

```bash
$ ./bin/goosefs fsadmin report
```

#### Zookeeper 기반의 공유 로그 배포 설정

Zookeeper 서비스 구축 GooseFS의 고가용성 아키텍처 설정은 아래 조건을 만족해야 합니다. 
 - Zookeeper 클러스터, GooseFS Master는 Zookeeper를 통해 Leader를 선택하고, GooseFS의 클라이언트와 Worker 노드는 Zookeeper를 통해 프라이머리 Master 노드를 확인합니다. 
 - 모든 GooseFS의 Master 노드가 모두 액세스할 수 있는 고가용성, 고일치성 공유 스토리지 시스템. 프라이머리 Master 노드가 로그를 해당 스토리지 시스템에 쓰고 세컨더리 (Standby) 노드는 지속적으로 공유 스토리지 시스템에서 로그를 읽으며 프라이머리 로그의 상태와 일치하도록 유지합니다. 일반적으로 해당 공유 스토리지 시스템을 HDFS 혹은 COS로 설정을 권장합니다. 예시: `hdfs://10.0.0.1:9000/goosefs/journal` 혹은 `cosn://bucket-1250000000/journal`.

설정은 아래와 같습니다. 

```properties
goosefs.zookeeper.enabled=true
goosefs.zookeeper.address=<ZOOKEEPER_ADDRESSS>
goosefs.master.journal.type=UFS
goosefs.master.journal.folder=<JOURNAL_URI>
```

ZK 모드의 'JOURNAL_URI'는 공유 스토리지 시스템의 URI여야 합니다. 그 다음 `./bin/goosefs copyDir conf/`를 사용하여 클러스터의 모든 노드와 설정을 동기화 하고 클러스터`./bin/goosefs-start.sh all`을 실행합니다. 


## GooseFS의 프로세스 리스트

`goosefs-start.sh all` 스크립트를 실행하고 GooseFS를 실행하면 클러스터에 아래와 같은 프로세스가 포함됩니다. 

| 프로세스             | 설명                                |
| ---------------- | ----------------------------------- |
|GooseFSMaster    | 기본 RPC 포트: 9200, Web 포트: 9201 |
|  GooseFSWorker    | 기본 RPC 포트: 9203, Web 포트: 9204 |
|  GooseFSJobMaster | 기본 RPC 포트: 9205, Web 포트: 9206 |
|  GooseFSProxy     | 기본 Web 포트: 9211                 |
| GooseFSJobWorker | 기본 RPC 포트: 9208, Web 포트: 9210 |

