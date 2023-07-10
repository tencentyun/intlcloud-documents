GooseFS의 Master와 Worker 노드 및 Spark 등 컴퓨팅 프레임워크가 GooseFS Client를 통해 GooseFs에게 요청을 진행할 경우, 요청 로그에 모두 기록됩니다. 사용자는 해당 출력 로그를 분석하여 문제를 진단할 수 있습니다. GooseFS 로그 출력은 [log4j](https://logging.apache.org/log4j/2.x/)에 기반하여 구현되며, log4j.properties 설정 파일을 변경하여 로그 저장 경로, 로그 레벨, RPC 호출 상황 기록 여부 등의 GooseFS 로그 출력을 설정할 수 있습니다. 사용자는 GooseFS의 설정 파일 디렉터리의 log4j.properties 파일을 수정할 수 있습니다.

```plaintext
$ cd /usr/local/service/goosefs/conf
$ cat log4j.properties

# May get overridden by System Property

log4j.rootLogger=INFO, ${goosefs.logger.type}, ${goosefs.remote.logger.type}

log4j.category.goosefs.logserver=INFO, ${goosefs.logserver.logger.type}
log4j.additivity.goosefs.logserver=false

log4j.logger.AUDIT_LOG=INFO, ${goosefs.master.audit.logger.type}
log4j.additivity.AUDIT_LOG=false

...
```

GooseFS의 로그 설정 상세 설명은 아래와 같습니다.

## 로그 저장 위치

GooseFS가 수집한 로그는 기본적으로 ${GOOSEFS_HOME}/logs 디렉터리에 저장됩니다. 그중, Master가 수집한 로그는 logs/master.log에 저장되고, Worker가 수집한 로그는 logs/worker.log에 저장됩니다. 주의할 것은, 노드 프로세스에서 발생된 오류에 대한 로그는 master.out 또는 worker.out에 저장되고, 일반적인 상황에서 이 두 종류의 파일은 빈 파일입니다. 시스템에서 오류가 발생되었을 시, 문제 추적을 위해 오류를 기록합니다.

Master 노드의 로그 기록 설정을 예로 든다면, 자주 사용하는 설정들은 아래와 같습니다.
```plaintext
# Appender for Master
log4j.appender.MASTER_LOGGER=org.apache.log4j.RollingFileAppender
log4j.appender.MASTER_LOGGER.File=${goosefs.logs.dir}/master.log
log4j.appender.MASTER_LOGGER.MaxFileSize=10MB
log4j.appender.MASTER_LOGGER.MaxBackupIndex=100
log4j.appender.MASTER_LOGGER.layout=org.apache.log4j.PatternLayout
log4j.appender.MASTER_LOGGER.layout.ConversionPattern=%d{ISO8601} %-5p %c{1} - %m%n
```

매개변수 설정 설명은 다음과 같습니다.
- MASTER_LOGGER: MASTER의 로그 출력 설정
- MASTER_LOGGER.File: 로그의 저장 경로 지정. 경로 수정을 통해 로그 저장 위치를 사용자 정의할 수 있습니다.
- MASTER_LOGGER.MaxFileSize: 단일 로그 파일에 대한 크기 제한 설정
- MASTER_LOGGER.MaxBackupIndex: 로그 파일 수량 제한 설정
- MASTER_LOGGER.layout: 로그 출력 형식 템플릿 지정
- MASTER_LOGGER.layout.ConversionPattern: 로그 출력의 상세 형식 지정

>!
>-.log 파일은 롤링 방식으로 저장되며 UFS에 백업할 수 있습니다. .out 파일 같은 경우, 롤링 방식으로 저장되지 않기 때문에 .out 파일을 제거해야 하는 경우 수동으로 삭제 작업을 진행해야 합니다.
> - log4j의 자세한 매개변수 설정은 [log4j configuration 문서](https://logging.apache.org/log4j/2.x/manual/configuration.html)를 참고하십시오.
> - GooseFS는 자체 생성된 로그만을 저장합니다. 상위 레이어의 컴퓨팅 애플리케이션에서 생성된 로그는 컴퓨팅 애플리케이션의 로그 설정에 따라 로그 저장 위치를 확인할 수 있습니다. 자주 사용되는 컴퓨팅 애플리케이션 로그 설정 정보는 다음과 같습니다. [Apache Hadoop](https://docs.alluxio.io/os/user/stable/en/compute/Hadoop-MapReduce.html#logging-configuration), [Apache HBase](https://docs.alluxio.io/os/user/stable/en/compute/HBase.html#logging-configuration), [Apache Hive](https://docs.alluxio.io/os/user/stable/en/compute/Hive.html#logging-configuration), [Apache Spark](https://docs.alluxio.io/os/user/stable/en/compute/Spark.html#logging-configuration)。
> 

## 로그 레벨

GooseFS는 아래와 같은 5개 레벨의 로그를 제공합니다.
- TRACE: 상세 호출 로그. 메소드와 클래스 호출의 디버깅에 사용됩니다.
- DEBUG: 비교적 상세한 호출 로그. DEBUG 과정 중의 문제를 진단할 수 있습니다. 
- INFO: 요청 처리 과정 중의 주요 정보.
- WARN: 알람류 정보. 작업은 계속 실행될 수 있지만 발생 가능한 문제에 주의해야 합니다.
- ERROR: 시스템 오류 보고 정보. 작업 진행에 영향을 미칩니다.

위의 5개 레벨의 로그에 대한 상세 수준은 높음에서 낮음 순이며, 높은 레벨의 로그는 낮은 레벨의 로그 정보도 기록합니다. 기본적으로 GooseFS는 INFO 레벨의 로그를 구성하고 INFO, WARN, ERROR 3가지 레벨의 로그를 기록합니다.

GooseFS의 설정 파일 디렉터리로 이동하여 log4j.properties 파일을 열고 수정할 수 있습니다. 아래의 예시는 모든 GooseFS의 로그 레벨을 DEBUG 레벨로 수정하는 방법을 보여줍니다.

```plaintext
log4j.rootLogger=DEBUG, ${goosefs.logger.type}, ${goosefs.remote.logger.type}
```

지정된 유형의 로그 레벨을 수정해야 하는 경우 설정 파일에 선언문을 추가할 수 있습니다. 아래의 예시는 GooseFSFileInStream 클래스의 로그 레벨이 DEBUG임을 보여줍니다.

```plaintext
log4j.logger.com.qcloud.cos.goosefs.client.file.GooseFSFileInStream=DEBUG
```

일반적으로 로그 설정 파일에서 로그 레벨을 수정하는 것이 좋습니다. 그러나 일부 특정 시나리오에서는 사용자가 클러스터 작업 중 로그 매개변수를 수정해야 할 수 있으며 이때 명령 라인에 goosefs logLevel 명령을 입력하여 수정할 수 있습니다. 다음은 logLevel에서 지원하는 설정 옵션입니다.

```plaintext
usage: logLevel [--level <arg>] --logName <arg> [--target <arg>]
    --level <arg>     The log level to be set.
    --logName <arg>   The logger's name(e.g. com.qcloud.cos.goosefs.master.file.DefaultFileSystemMaster) you want to get or set level.
    --target <arg>    <master|workers|host:webPort>. A list of targets separated by, can be specified. host:webPort pair must be one of workers. Default target is master and all workers
```


각 설정 항목의 상세 설명은 다음과 같습니다.

- level：로그 레벨. TRACE, DEBUG, INFO, WARN, ERROR 다섯 가지의 레벨.
- logName：로그 출력 logger. 예: com.qcloud.cos.goosefs.underfs.hdfs.HdfsUnderFileSystem 등.
- target: 수정 범위. Master 또는 Worker 노드(IP: PORT 방식으로 지정)를 지정하여 설정할 수 있으며 기본 값은 Master 및 모든 Worker 노드입니다.

사용자는 시스템 작동 중 문제를 해결하기 위해 필요에 따라 로그 레벨을 조정할 수 있습니다. 예를 들어 다음 예는 모든 Worker 노드의 com.qcloud.cos.goosefs.underfs.hdfs.HdfsUnderFileSystem 클래스의 로그 레벨을 DEBUG 레벨로 변경하고 디버깅이 완료된 후 다시 INFO 레벨로 수정하는 것을 보여줍니다.

```plaintext
$  goosefs logLevel --logName=com.qcloud.cos.goosefs.underfs.hdfs.HdfsUnderFileSystem --target=workers --level=DEBUG # DEBUG 모드로 변경

$  goosefs logLevel --logName=com.qcloud.cos.goosefs.underfs.hdfs.HdfsUnderFileSystem --target=workers --level=INFO # NFO 모드로 변경
```

## 고급 설정

GooseFS는 GC 이벤트 로그, FUSE 인터페이스 로그, RPC 호출 로그, UFS 작업 로그, 로그 분할 및 로그 필터링과 같은 작업의 설정을 지원합니다. 다음은 몇 가지 일반적인 고급 설정을 사용하는 방법을 설명합니다.

- **GC 이벤트 로그**
GooseFS는 .out 파일에 GC 이벤트 로그를 기록합니다. conf/goosefs-env.sh에서 다음과 같은 설정을 추가할 수 있습니다.
```plaintext
GOOSEFS_JAVA_OPTS+=" -XX:+PrintGCDetails -XX:+PrintTenuringDistribution -XX:+PrintGCTimeStamps"
```
 GOOSEFS_JAVA_OPTS는 모든 유형의 GooseFS 노드에 대한 Java 가상 머신 매개변수입니다. GOOSEFS_MASTER_JAVA_OPTS 및 GOOSEFS_WORKER_JAVA_OPTS를 지정하여 Master 및 Worker에 대한 가상 머신 매개변수를 각각 지정할 수도 있습니다.
- **FUSE 인터페이스 로그**
FUSE 로그 레벨의 기록은 conf/log4j.properties 파일에서 설정할 수 있습니다.
```plaintext
goosefs.logger.com.qcloud.cos.goosefs.fuse.GoosefsFuseFileSystem=DEBUG
```
 활성화한 후 FUSE 인터페이스 로그는 logs/fuse.log에서 볼 수 있습니다. 
- **RPC 호출 로그 활성화**
GooseFS는 conf/log4j.properties 구성 파일에서 Client 또는 Master의 RPC 호출 로그 설정을 지원합니다.
log4j.properties 파일을 통해 클라이언트가 RPC 요청 로그를 출력하도록 설정할 수 있습니다.
```plaintext
log4j.logger.com.qcloud.cos.goosefs.client.file.FileSystemMasterClient=DEBUG # Client와 FileSystemMaster 간의 RPC 요청 로그
log34j.logger.com.qcloud.cos.goosefs.client.block.BlockSystemMasterClient=DEBUG # Client와 BlockMaster 간의 RPC 요청 로그
```
 logLevel 명령을 통해 Master가 RPC 요청 로그를 출력하도록 설정할 수 있습니다.
```plaintext
$ goosefs logLevel \--logName=com.qcloud.cos.goosefs.master.file.FileSystemMasterClientServiceHandler \--target master --level=DEBUG # 파일 관련 RPC 요청 로그
$ goosefs logLevel \--logName=com.qcloud.cos.goosefs.master.block.BlockSystemMasterClientServiceHandler \--target master --level=DEBUG # 블록 관련 RPC 요청 로그
```
- **UFS 작업 로그**
UFS 작업 로그 출력 설정은 log4j.properties 파일에 설정 항목을 추가하거나 logLevel 명령을 사용하여 설정할 수 있습니다. 다음은 logLevel 명령의 예시입니다.
```plaintext
$ goosefs logLevel \--logName=com.qcloud.cos.goosefs.underfs.UnderFileSystemWithLogging \--target master --level=DEBUG # Master 노드의 UFS에 대한 작업 로그 기록
$ goosefs logLevel \--logName=com.qcloud.cos.goosefs.underfs.UnderFileSystemWithLogging \--target workers --level=DEBUG # Worker 노드의 UFS에 대한 작업 로그 기록
```
- **로그 분할**
GooseFS는 지정된 유형의 로그를 지정된 저장 경로에 저장할 수 있도록 지원하며, 만약 모든 로그가 .log 파일에 기록되면 다음과 같은 문제가 발생할 수 있습니다.
 - 클러스터 크기가 크고 처리량이 클 경우 master.log 또는 worker.log 파일이 비정상적으로 커지거나 롤링에 의해 많은 수의 로그 파일이 생성될 수 있습니다.
 - 로그 정보가 많아 대상 분석을 위한 타깃성 로그 분석에 적합하지 않습니다.
 - 많은 양의 로그가 로컬 노드에 저장되어 공간을 차지합니다.

 따라서 서비스의 필요에 따라 log4j.properties 파일에 설정 항목을 추가하여 지정된 클래스에 의해 생성된 로그를 지정된 파일 경로에 저장합니다. 다음 예시는 Statelock.log에 StateLockManager 클래스 로그를 저장하는 방법을 보여줍니다.
```plaintext
log4j.category.com.qcloud.cos.goosefs.master.StateLockManager=DEBUG, State_LOCK_LOGGER
log4j.additivity.com.qcloud.cos.goosefs.master.StateLockManager=false
log4j.appender.State_LOCK_LOGGER=org.apache.log4j.RollingFileAppender
log4j.appender.State_LOCK_LOGGER.File=<GOOSEFS_HOME>/logs/statelock.log
log4j.appender.State_LOCK_LOGGER.MaxFileSize=10MB
log4j.appender.State_LOCK_LOGGER.MaxBackupIndex=100
log4j.appender.State_LOCK_LOGGER.layout=org.apache.log4j.PatternLayout
log4j.appender.State_LOCK_LOGGER.layout.ConversionPattern=%d{ISO8601} %-5p %c{1} - %m%
```
- **로그 필터링**
GooseFS는 전체 로그를 기록하는 대신 특정 조건에 따라 필터링 및 기록을 지원합니다. 예를 들어 성능 테스트 시 RPC 호출 로그를 기록해야 하지만, 서비스에서는 모든 RPC 호출 로그를 기록할 필요는 없고 대기 시간이 긴 일부 로그만 기록하면 됩니다. 이때 설정 항목을 추가할 수 있습니다. log4j.properties 파일에서 로그 필터링 조건 설정을 추가하기만 하면 필터링이 가능합니다. 다음은 RPC 호출 딜레이가 200ms를 초과하고 FUSE 호출이 1초를 초과하는 요청의 필터링을 보여줍니다.
```plaintext
goosefs.user.logging.threshold=200ms
goosefs.fuse.logging.threshold=1s
```
