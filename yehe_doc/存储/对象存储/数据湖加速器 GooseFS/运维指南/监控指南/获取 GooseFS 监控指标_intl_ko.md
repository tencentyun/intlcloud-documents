Goosefs는 [Coda Hale Metrics Library](https://github.com/dropwizard/metrics)를 기반으로 모니터링 데이터를 기록하고 명령 라인, 콘솔, 파일 등 여러 경로를 통한 지표 획득을 지원합니다. 현재 지원되는 지표 획득 방법은 다음과 같습니다.
- MetricsServlet: Json 형식으로 사용자에게 모니터링 지표를 제공합니다.
- CsvSink: CSV 파일을 통해 모니터링 지표를 표시합니다. 설정 후 모니터링 지표를 기록하는 CSV 파일은 주기적으로 생성됩니다.
- PrometheusMetricsServlet: Prometheus에서 정의한 형식으로 사용자에게 모니터링 지표를 제공합니다.

상기 모니터링 지표의 설정은 구성 파일을 통해 지정할 수 있습니다. GooseFS 모니터링 지표 구성 파일의 기본 파일 경로는 `$ GooseFS_HOME/conf/metrics.properties`이며, goosefs.metrics.conf.file을 통한 사용자 정의 모니터링 구성 파일 지정을 지원합니다. GooseFS는 설정 가능한 모든 속성을 포함하는 기본 템플릿 metrics.properties.template을 사용자에게 제공합니다.

## 모니터링 지표 가져오기

다음은 모니터링 지표를 얻는 세 가지 기본 경로를 소개합니다.

### 1. JSON 형식으로 모니터링 지표 가져오기

GooseFS가 모니터링 지표를 얻는 기본 방법은 MetricsServlet 설정 항목에 해당하는 JSON 형식으로 풀링하는 것입니다. 명령 라인에서 GooseFS의 Leading Master 노드에 대한 HTTP 요청을 제안하여 필요한 모니터링 지표를 풀링합니다. 그 중 master의 metrics 포트는 9201이고 worker의 metrics 포트는 9204입니다. 요청 명령어 형식은 다음과 같습니다. 

```plaintext
$ curl <LEADING_MASTER_HOSTNAME>:<MASTER_WEB_PORT>/metrics/json
```

상기 예시에서 <LEADING_MASTER_HOSTNAME>은 올바른 MASTER 노드의 IP여야 하고 <MASTER_WEB_PORT>는 활성화된 포트여야 합니다.

WORKER 노드의 모니터링 지표를 가져와야 하는 경우 다음과 같은 방법으로 얻을 수 있습니다.

```plaintext
$ curl <WORKER_HOSTNAME>:<WORKER_WEB_PORT>/metrics/json
```

### 2. CSV 파일로 모니터링 지표 가져오기

GooseFS는 CSV 형식 파일로 데이터 내보내기를 지원합니다. 이 기능을 통해 모니터링 지표를 얻으려면 먼저 모니터링 지표를 저장할 디렉터리를 준비해야 합니다.

```plaintext
$ mkdir /tmp/goosefs-metrics
```

스토리지 경로를 준비한 후 구성 파일 conf/metrics.properties를 수정하여 CsvSink 능력을 활성화합니다.

```plaintext
sink.csv.class=goosefs.metrics.sink.CsvSink # CsvSink 기능 활성화

sink.csv.period=1 # 모니터링 지표 내보내기 주기 설정
sink.csv.unit=senconds # 모니터링 지표 내보내기 주기 단위 설정

sink.csv.directory=/tmp/goosefs-metrics # 모니터링 지표 내보내기 경로 설정
```


설정이 완료된 후 설정을 적용하려면 노드를 재시작해야 합니다. 설정이 적용된 후 모니터링 지표는 주기적으로 CSV 형식으로 내보내기되고 지정된 경로에 저장됩니다.

>!
- GooseFS는 모니터링 설정 템플릿을 준비했습니다. conf/metrics.properties.template 파일을 참고하십시오.
- GooseFS가 클러스터에 배포된 경우 지정된 지표 스토리지 경로를 모든 노드에서 읽을 수 있도록 보장되어야 합니다.

### 3. Prometheus 모니터링 지표 풀링
GooseFS master와 worker의 Prometheus 모니터링 지표는 다음과 같은 명령어로 조회할 수 있습니다. 그 중 master의 metrics 포트는 9201이며, worker의 metrics 포트는 9204입니다.
```plaintext
curl <LEADING_MASTER_HOSTNAME>:<MASTER_WEB_PORT>/metrics/prometheus/
# HELP Master_CreateFileOps Generated from Dropwizard metric import (metric=Master.CreateFileOps, type=com.codahale.metrics.Counter)
...

curl <WORKER_IP>:<WOKER_PORT>/metrics/prometheus/
# HELP pools_Code_Cache_max Generated from Dropwizard metric import (metric=pools.Code-Cache.max, type=com.codahale.metrics.jvm.MemoryUsageGaugeSet$$Lambda$51/137460818)
...
```
