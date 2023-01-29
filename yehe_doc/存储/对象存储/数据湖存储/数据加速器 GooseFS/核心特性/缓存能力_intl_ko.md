## 캐시 능력 개요

GooseFS는 오픈 소스 Alluxio 아키텍처에 기반한 강력한 분산형 Cache 능력을 제공하여 사용자가 다양한 플랫폼의 사용자 데이터를 통합하는 동시에, 사용자의 전반적인 I/O 처리량을 향상할 수 있도록 돕습니다.

주로 아래 두 가지 방법을 사용합니다.

- GooseFS NameSpace 원격 스토리지: NS 스토리지 공간 기반은 외부 스토리지로, COSN 및 HDFS를 거쳐 하나 이상의 여러 NS를 동일한 인프라 스토리지에 연결하여, 대량의 데이터를 보존할 수 있습니다. COSN 스토리지 및 컴퓨팅 분리 솔루션을 사용하면, GooseFS NameSpace는 COSN을 통해 탄력적인 확장과 고가용성 기능을 갖춘 빅 데이터 스토리지를 제공할 수 있습니다.
- GooseFS 로컬 Cache 스토리지: GooseFS는 master와 worker가 제공하는 분산형 Cache 기능을 통해, 애플리케이션 레이어에서 생성된 데이터를 애플리케이션 노드의 로컬 메모리와 디스크에 보존하며, 주로 핫 데이터와 임시 데이터를 저장합니다. 각 로컬 스토리지 노드는 사용자가 구성할 수 있으며 NameSpace에 연결된 원격 영속 레이어도 동일한 client 서비스 사용자의 읽기/쓰기 작업을 경유하게 됩니다.

사용자는 Cache Policy 작업을 할 수 있습니다. 읽기/쓰기 모드에서 로컬 Cache 스토리지와 NameSpace 원격 스토리지 사용을 결정합니다.

![](https://main.qcloudimg.com/raw/c6ee0f55529fec5d60043577c3d1211d.png)

GooseFS는 동일한 로컬 Cache 및 원격 NameSpace 통합 기능을 제공하여 사용자가 스토리지 분리의 통합 방안을 완전히 구현하는 동시에 애플리케이션 노드에 대한 데이터 친연성를 설정할 수 있도록 지원합니다.

## GooseFS 캐시 설정

사용자는 goosefs-site.properties 파일에 들어가 GooseFS 캐시 설정 상황을 볼 수 있습니다. 현재 GooseFS의 캐시 설정은 캐시 레이어, 캐시 만료 정책 등 방면에서 이해할 수 있으며, 캐시 레이어 방면에는 주로 단일 레이어 스토리지와 멀티 레이어 스토리지 두 가지가 있습니다. 캐시 만료 정책은 주로 LRU와 LRFU의 두 가지 유형으로 나뉩니다. 자세한 소개는 아래와 같습니다.

### 1. 캐시 레이어

GooseFS는 단일 레이어 스토리지와 멀티 레이어 두 가지 캐시 레벨을 제공합니다. 단일 레이어 스토리지에는 하나의 스토리지만 사용하고, 멀티 레이어 스토리지에는 다양한 스토리지들이 사용되며, 업무 부하 상황에 따라 어떤 스토리지 미디어를 사용할지 결정하여 맞춤형 I/O 성능을 제공할 수 있습니다. GooseFS 기본 설정은 단일 스토리지로 되어 있습니다. 멀티 레이어 시나리오에서 캐시 만료는 많은 성능 비용을 가져오므로 **단일 레이어 스토리지**를 사용하는 것을 추천합니다. I/O 성능 수준에 따라 일반적으로 MEM, SSD, HDD를 스토리지 미디어로 선택할 수 있습니다.

goosefs-site.properties 설정 파일의 levels 매개변수를 수정하여 캐시 레벨을 수정할 수 있으며, 입력 매개변수가 1이면 단일 레이어 스토리지만 사용하고 입력 매개변수가 3이면 3개 레이어 스토리지를 사용합니다.

```plaintext
goosefs.worker.tieredstore.levels=1
```

goosefs-site.properties 구성 파일의 alias 매개변수를 수정하여 캐시 레이어에 해당하는 스토리지 미디어를 수정할 수 있습니다.

```plaintext
goosefs.worker.tieredstore.level{x}.alias=MEM
```

>!level{x}은 스토리지 레이어 레벨을 나타냅니다. 예를 들어 level 0은 단일 레이어 스토리지를 나타냅니다. 

**1.1 단일 레이어 스토리지**

단일 레이어 스토리지 모드에서 자주 사용하는 시스템 구성 항목은 다음과 같습니다:


```plaintext
goosefs.worker.tieredstore.levels=1
goosefs.worker.tieredstore.level0.alias=HDD
goosefs.worker.ramdisk.size=16GB
goosefs.worker.memory.size=100GB
goosefs.worker.tieredstore.level0.dirs.path=/data/GooseFSWorker,/data1/GooseFSWorker,/data2/GooseFSWorker,/data3/GooseFSWorker,/data4/GooseFSWorker
goosefs.worker.tieredstore.level0.dirs.mediumtype=MEM,MEM,MEM,SSD,SSD
goosefs.worker.tieredstore.level0.dirs.quota=16GB,16GB,16GB,100GB,100GB
```





다음은 각 구성 항목 내용에 대한 설명입니다.

- ramdisk.size: 이 구성 항목은 worker 노드가 차지하는 메모리 크기를 지정하는 데 사용되며 ramdisk의 용량은 memory보다 작아야 합니다. 설정 후 GooseFS는 각 worker 노드에 지정된 크기의 메모리 공간을 할당하고 시스템의 전체 메모리를 사용합니다.
-memory.size: 이 구성 항목은 GooseFS 시스템의 총 메모리를 지정하는 데 사용됩니다. 설정 후 GooseFS는 지정된 크기의 스토리지 미디어를 자동으로 점용합니다. 실제 물리적 스토리지 공간은 memory 값보다 커야 합니다.
-dirs.path: 이 구성 항목은 디렉터리를 지정하는 데 사용됩니다. GooseFS는 지정된 디렉터리에 대한 스토리지 미디어를 할당합니다. dirs.mediumtype과 함께 사용해야 합니다. 위의 예시와 같이 /data/GooseFSWorker를 MEM 스토리지 미디어에 마운트하고, /data4/GooseFSWorker를 SSD 스토리지 미디어에 마운트합니다. 각 디렉토리의 순서는 스토리지 미디어의 순서와 각각 일치해야 한다는 점에 유의해야 합니다.
-dirs.mediumtype: 이 구성 항목은 스토리지 미디어를 지정하는 데 사용됩니다. GooseFS는 지정된 디렉토리에 대해 스토리지 미디어를 할당합니다. dirs.path와 함께 사용해야 합니다. 사용 가능한 기본 스토리지 미디어는 MEM과 SSD가 있으며, HDD와 같은 다른 스토리지 미디어를 마운트한 경우 필요에 따라 구성을 수정할 수 있습니다.
-dirs.quota: 구성 항목을 변경하여 각 디렉터리의 사전 설정 공간을 지정합니다. 설정 후 GooseFS를 통해 지정 디렉터리에 대해 공간을 할당하고, 디렉터리 순서와 각각 대응되어야 합니다. 위의 예시는 /data/GooseFSWorker, /data1/GooseFSWorker, /data2/GooseFSWorker와 같은 디렉토리에 16GB MEM 공간을 할당하고 /data3/GooseFSWorker, /data4/GooseFSWorker 디렉터리에 100GB SSD 공간을 할당해야 함을 보여줍니다.

**1.2 티어링 스토리지**

티어링 스토리지 모드에서는 데이터 블록의 읽기 및 쓰기 모드와 단일 레이어 스토리지의 읽기 및 쓰기 모드 간에 차이가 있습니다. 단일 레이어 스토리지 모드에서 데이터는 스토리지 미디어에서 직접 읽고 쓰게 됩니다. 멀티 레이어 스토리지 모드에서 데이터는 기본적으로 최상위 스토리지 미디어에 먼저 기록됩니다. 읽을 때 데이터를 먼저 최상위 스토리지 미디어로 이동해야 합니다. 구체적인 내용은 다음과 같습니다.

- **데이터 쓰기**: 새 데이터 블록은 기본적으로 최상위 레이어 스토리지 미디어에 기록되며, 최상위 레이어 스토리지 미디어의 저장 공간이 가득 차면 GooseFS에서 다음 레이어 스토리지 미디어에 데이터를 순차적으로 저장합니다. 모든 스토리지 미디어에 데이터가 가득 차면 사용자가 지정한 캐시 만료 정책에 따라 GooseFS가 만료된 데이터를 제거합니다. 만료된 데이터를 제거할 수 없고 사용 가능한 저장 공간이 모두 차면 데이터를 쓸 수 없습니다.
- **데이터 읽기**: 멀티 레이어 스토리지 모드에서 콜드 데이터는 하위 수준 레이어 스토리지 미디어에 투명하게 덤프되고 데이터를 읽게되면 핫 데이터로 바뀌어 상위 수준 스토리지에 배치됩니다.


>!
>- 설정된 만료 정책에 의해, GooseFS는 지정된 릴리스 공간에 따라 일정량의 데이터를 제거합니다. 이 매개변수는 goosefs.worker.tieredstore.free.ahead.bytes로 지정할 수 있으며 기본값은 0입니다.
>- 티어링 스토리지 모드에서 데이터를 읽을 때 하위 레이어 스토리지 미디어에서 상위 레이어 스토리지 미디어로 데이터가 자주 덤프될 수 있으며, 이는 빈번한 캐시 제거 및 특정 성능 손실로 이어질 수 있습니다. 일반적으로 **단일 레이어 스토리지 사용을 권장합니다**.

티어링 스토리지 모드에서, 자주 사용하는 시스템 구성 항목은 다음과 같습니다.

```plaintext
goosefs.worker.tieredstore.levels
goosefs.worker.tieredstore.level{x}.alias
goosefs.worker.tieredstore.level{x}.dirs.path
goosefs.worker.tieredstore.level{x}.dirs.mediumtype
goosefs.worker.tieredstore.level{x}.dirs.quota
```

이 중 x는 캐시 레이어를 의미하며 일반적으로 MEM, SSD, HDD 등 스토리지 미디어에 상응하는 3개 레이어로 설정할 수 있습니다. 2개 레이어는 스토리지 레이어가 각각 MEM, SSD이며, 레이어당 100GB 스토리지를 할당하는 것을 예로 들면, 이에 대한 설정 정보는 다음과 같습니다.

```plaintext
goosefs.worker.tieredstore.levels=2
goosefs.worker.tieredstore.level0.alias=MEM
goosefs.worker.tieredstore.level0.dirs.path=/data/GooseFSWorker
goosefs.worker.tieredstore.level0.dirs.mediumtype=MEM
goosefs.worker.tieredstore.level0.dirs.quota=100GB
goosefs.worker.tieredstore.level1.alias=SSD
goosefs.worker.tieredstore.level1.dirs.path=/data1/GooseFSWorker
goosefs.worker.tieredstore.level1.dirs.mediumtype=SSD
goosefs.worker.tieredstore.level1.dirs.quota=100GB
```


GooseFS는 멀티 레이어 스토리지를 지원하며 레이어 수에 제한이 없습니다. 하지만 각 레이어의 이름(alias)의 유일성은 보장되어야 합니다. 일반적으로 3개 레이어 캐시를 제공하며 각 레이어가 각각 MEM, SSD, HDD에 대응되어 티어링 효과가 좋습니다.

### 2. 캐시 만료 정책

GooseFS는 두 가지 캐시 만료 정책을 제공합니다.

- LRUAnnotator：최근 사용 횟수가 가장 적은(least-recently-used) 순서대로 캐시를 제거합니다. 이는 GooseFS의 기본 설정 정책입니다.
- LRFUAnnotator：최근 사용 횟수가 가장 적은(least-recently-used) 순서 및 최근 사용 빈도가 가장 적은(least-frequently-used) 순서대로 캐시를 삭제합니다. 가중치 설정 goosefs.worker.block.annotator.lrfu.step.factor과 goosefs.worker.block.annotator.lrfu.attenuation.factor 를 통해 두 가지 정책의 삭제 과정 중의 작용을 조정합니다.
- 만약 least-recently-used 의 가중치를 최대로 조정하면, 해당 정책의 결과는  LRUAnnotator와 같게 됩니다.

goosefs.worker.block.annotator.class 설정 항목에서 캐시 만료 정책을 설정할 수 있습니다. 설정 시 정책 이름을 올바르게 설정해야 합니다.

```plaintext
goosefs.worker.block.annotator.LRUAnnotator
goosefs.worker.block.annotator.LRFUAnnotator
```



## 데이터 라이프사이클 관리

이 라이프사이클는 GooseFS 중의 데이터 라이프사이클을 지칭하며, 원격 스토리지 시스템 UFS가 아닙니다. 라이프사이클 관리는 주로 아래 4가지 작업이 있습니다.

- free: 이 작업은 GooseFS에서 해당 디렉터리나 파일의 데이터를 삭제합니다. (UFS 중의 상응 데이터는 삭제하지 않습니다). 이 작업은 주로 GooseFS의 캐시 공간을 릴리스하여 더 자주 사용되는 데이터를 사용할 수 있도록 합니다.
- load：이 작업은 UFS에 상응하는 디렉터리 또는 파일의 데이터를 GooseFS에 로딩하는데 사용되며, 이러한 작업은 콜드 데이터의 핫 데이터로의 전환 및  I/O 성능 향상에 사용됩니다.
- persist：이 작업은 GooseFS 내의 데이터를 UFS 스토리지에 쓰는 데에 사용됩니다. 이러한 작업은 데이터 영속화 및 데이터 손실 방지에 사용됩니다.
-TTL(Time to Live): TTL 속성은 주로 GooseFS에서의 디렉터리나 파일의 라이프사이클을 설정하는 데 사용되며, 수명 주기가 초과되면 GooseFS 및 UFS에서 삭제됩니다. 설정을 통해 GooseFs 데이터만 삭제하거나 디스크 공간만 릴리스할 수 있습니다.

### 1. GooseFS에서 데이터 릴리스

free 명령을 통해 GooseFS에서 데이터를 릴리스 합니다. 다음 예시는 데이터 릴리스 후, GooseFS의 데이터 상태가 0%로 바뀌는 것을 나타냅니다.

```plaintext
$ goosefs fs free /data/test.txt
/data/test.txt was successfully freed from GooseFS space.
$ goosefs fs ls /data/test.txt
-rw-rw-rw-  hadoop         hadoop                      14       PERSISTED 03-11-2021 11:46:15:000 0% /data/test.txt
```

예시 중의 /data/test.txt는 임의의 유효한 GooseFS파일 경로일 수 있습니다. 만약 데이터를 원격 스토리지 UFS에 저장할 경우, load 명령을 통해 재로딩할 수 있습니다.

>! 일반적으로, 캐시 정책 설정을 통해 GooseFS 중의 과거 데이터를 자동 제거할 것을 권장합니다. 

### 2. GooseFS로 데이터 로딩

load 명령을 통해 GooseFS에서 데이터를 로딩할 수 있습니다. 아래 예시는 데이터 릴리스 후, GooseFS 중의 데이터 상태가 100%로 바뀌는 것을 나타냅니다.

```plaintext
$ goosefs fs load /data/test.txt
/data/test.txt loaded
$ goosefs fs ls /data/test.txt
-rw-rw-rw-  hadoop         hadoop                      14       PERSISTED 03-11-2021 11:46:15:000 100% /data/test.txt
```


예제의 /data/test.txt는 모든 유효한 GooseFS 파일 경로일 수 있습니다. 로컬 파일 시스템에서 데이터를 로딩하는 경우 copyFromLocal 명령을 사용해야 합니다. 로컬 파일 시스템에서 데이터를 로드하는 작업은 데이터를 원격 스토리지 UFS에 보존하지 않습니다. 기본적으로 GooseFS는 파일에 처음 액세스할 때 데이터를 GooseFS에 자동으로 캐시에 로딩하므로 일반적으로 이 명령을 사용하여 데이터를 로딩할 필요는 없지만 비즈니스에서 미리 캐시에 데이터를 로딩해야 하는 경우 , 이 명령을 통해 로딩할 수 있습니다.

### 3. GooseFS에서의 데이터 영속화

persist 명령을 통해 데이터를 원격 스토리지 시스템 UFS에 영속화할 수 있습니다.

```plaintext
$ goosefs fs persist /data/test.txt
$ goosefs fs ls /data/test.txt
-rw-rw-rw-  hadoop         hadoop                      14       PERSISTED 03-11-2021 11:46:15:000 100% /data/test.txt
```


예시 중의 data/test.txt 는 임의의 유효한 GooseFS 파일 경로일 수 있습니다. 캐시 정책 설정을 통해 영속화 작업을 자동 실행할 것을 권장합니다.

### 4. 데이터 TTL 속성 설정

GooseFS는 네임스페이스의 모든 파일 또는 디렉터리에 대한 TTL 속성 설정을 지원합니다. 이 속성은 비즈니스 데이터가 지정된 기간에 따라 주기적으로 삭제되도록 하여 새 파일을 위한 공간을 확보하고 로컬 디스크 공간을 효과적으로 사용할 수 있도록 합니다. GooseFS 파일 및 디렉터리의 TTL 속성은 파일 메타데이터의 일부로서, 클러스터가 재시작된 후에도 TTL 속성이 여전히 유효함을 보장할 수 있으며, 백엔드 스레드의 정기 점검 프로그램은 이러한 TTL 속성을 확인하고 자동으로 만료된 파일을 삭제합니다.

정기 점검 프로그램의 점검 주기 및 점검 유형은 goosefs-site.preperties에서 설정할 수 있으며 다음 예시에서는 점검 주기를 10분으로, 점검 유형을 FREE로 설정합니다.

```plaintext
goosefs.master.ttl.checker.interval=10m
goosefs.user.file.create.ttl.action=FREE
```

설정이 완료되면 GooseFS 백그라운드 스레드가 10분마다 점검하고 현재 검사 주기에서 발견된 만료된 파일은 다음 검사 주기 후에 캐시 리소스를 릴리스합니다. 예를 들어 00:00:00에 첫 번째 점검 중에 만료된 파일 배치가 발견되면 이 파일 배치의 캐시는 00:10:00에 지워집니다.

>!기본적으로 입력 매개변수 단위는 밀리초(ms)이며, 매개변수를 입력할 때 감지 시간 주기의 단위를 초(s), 분(m), 시(h) 등과 같이 지정할 수 있습니다. 자세한 설명은 설정 설명서를 참고하십시오.

## 데이터 복사 관리

데이터 복사는 수동과 능동 두 가지 형식으로 나눠집니다.

### 1. 수동 레플리케이션

GooseFS의 각 파일에는 클러스터에 분산 저장된 하나 이상의 스토리지 블록이 포함되어 있으며 기본적으로 GooseFS는 부하 및 용량에 따라 데이터 블록의 복사 수준을 자동으로 조정할 수 있습니다. 수동 레플리케이션은 아래 시나리오에서 발생할 수 있습니다.

- 여러 클라이언트가 같은 블록을 동시에 읽게 되면 여러 block이 다른 worker에 동시에 존재하게 됩니다.
- ’로컬 읽기 우선’가 활성화 된 후, 데이터가 로컬에 없는 경우, remote read가 발송되고, 로컬 worker에 저장됩니다.
- 수동 레플리케이션으로 발생된 복제본의 수가 설정된 복제본 수보다 클 경우, 비동기적으로 초과된 복제본을 삭제합니다. 위의 과정은 사용자에게 투명하게 공개됩니다.

### 2. 능동 레플리케이션

능동 레플리케이션은 파일의 복제본 수 설정을 통해 구현되며, 설정한 복제본 수에 맞지 않는 block은 비동기적으로 보완하고, 설정한 복제본 수를 초과하는 block은 초과된 복제본을 삭제합니다. 아래 명령을 통해 능동 레플리케이션 레벨을 조정할 수 있습니다.

```plaintext
$ goosefs fs setReplication  [-R] [--max | --min ] <path>
```

매개변수 설정 설명

- max: 지정 파일의 최대 복제본 수로, 기본값은 -1입니다. 상한선을 설정하지 않습니다. 0으로 설정하면 지정 파일의 콜드 데이터를 GooseFS에 저장하지 않습니다. 일반적으로 자연수로 설정합니다. 설정 후 GooseFS는 파일의 복제본 수를 체크하고 잔여 복제본을 삭제합니다.
- min: 지정 파일의 최소 복제본 수로, 기본값은 0입니다. 이는 GooseFS가 데이터 콜드화 후 해당 데이터를 삭제하고 어떤 복제본도 남기지 않음을 나타냅니다. 일반적으로 자연수로 설정하며, **max값보다 작아야 합니다**. 설정 후 GooseFS는 파일 복제본 수를 검사하고 최소값보다 작으면 복제본 수를 자동으로 채웁니다.
- path: 지정된 파일 이름으로, 디렉토리 또는 특정 파일 경로가 될 수 있습니다.
- R: path의 입력 매개변수가 디렉터리인 경우 -R을 지정하면 지정된 최소 복제본 수와 최대 복제본 수에 따라 지정된 디렉터리의 모든 파일 및 하위 디렉터리를 중복 재귀 복제합니다.

지정된 파일의 복사 상태를 확인해야 하는 경우 stat 명령을 통해 볼 수 있습니다. 다음 예제는 /data/test.txt 파일의 최대 복제본 수가 -1임을 보여줍니다. 이는 해당 파일이 콜드 데이터로 변환된 후, 만료 및 삭제됨을 나타냅니다.

```plaintext
$ goosefs fs stat /data/test.txt
/data/test.txt is a file path.
FileInfo{fileId=50331647, fileIdentifier=null, name=test.txt, path=/data/test.txt, ufsPath=hdfs://172.16.16.16:4007/data/test.txt, length=0, blockSizeBytes=134217728, creationTimeMs=1618193473555, completed=true, folder=false, pinned=false, pinnedlocation=[], cacheable=true, persisted=true, blockIds=[], inMemoryPercentage=100, lastModificationTimesMs=1616763603692, ttl=-1, lastAccessTimesMs=1616763603692, ttlAction=DELETE, owner=hadoop, group=supergroup, mode=420, persistenceState=PERSISTED, mountPoint=false, replicationMax=-1, replicationMin=0, fileBlockInfos=[], mountId=1, inGooseFSPercentage=100, ufsFingerprint=TYPE|FILE UFS|hdfs OWNER|hadoop GROUP|supergroup MODE|420 CONTENT_HASH|(len:0,_modtime:1616763603692) , acl=user::rw-,group::r--,other::r--, defaultAcl=}
This file does not contain any blocks.
```


## 캐시 사용량 확인

GooseFS는 로컬 캐시 용량과 사용 상황을 기록하며, 다음 명령을 통해 GooseFS의 실행 상황을 확인하여 로컬 캐시에 대해 맞춤형 관리 및 점검을 진행할 수 있습니다

- GooseFS 사용 중 캐시 확인. 단위: 바이트.

```plaintext
$ goosefs fs getUsedBytes
Used Bytes: 0
```


- GooseFS 총 캐시 용량 확인. 단위: 바이트.

```plaintext
$ goosefs fs getCapacityBytes
Capacity Bytes: 1610612736000
```


- GooseFS의 캐시 사용 리포트 조회:

```plaintext
$ goosefs fsadmin report
GooseFS cluster summary: 
    Master Address: 172.16.16.16:19998
    Web Port: 19999
    Rpc Port: 19998
    Started: 04-12-2021 10:52:05:255
    Uptime: 0 day(s), 1 hour(s), 28 minute(s), and 57 second(s)
    Version: 2.5.0-SNAPSHOT
    Safe Mode: false
    Zookeeper Enabled: false
    Live Workers: 3
    Lost Workers: 0
    Total Capacity: 1500.00GB
        Tier: HDD  Size: 1500.00GB
    Used Capacity: 0B
        Tier: HDD  Size: 0B
    Free Capacity: 1500.00GB
```
