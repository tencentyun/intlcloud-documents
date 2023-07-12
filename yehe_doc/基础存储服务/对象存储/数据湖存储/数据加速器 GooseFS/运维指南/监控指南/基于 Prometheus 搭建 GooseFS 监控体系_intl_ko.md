Goosefs는 설정을 통해 지표 데이터를 Prometheus와 같은 다른 모니터링 시스템으로 출력할 수 있습니다. Prometheus는 오픈 소스 모니터링 프레임워크로 현재 Tencent Cloud 모니터링은 Prometheus를 통합하였습니다. 다음으로 Goosefs의 모니터링 지표와 자체구축한 Prometheus와 클라우드 Prometheus에 모니터링 지표를 보고하는 과정을 중점적으로 소개합니다.

## 준비 작업

Prometheus를 통해 모니터링 시스템을 구축하려면 다음 준비 작업이 선행되어야 합니다.

- GooseFS 클러스터 설정
- Prometheus 공식 홈페이지의 설치 패키지 또는 Tencent Cloud Prometheus 설치 패키지 다운로드
- [Grafana](https://grafana.com/docs/grafana/latest/installation/#install-grafana/) 다운로드 및 설정

## GooseFS 모니터링 지표 보고 설정 활성화

1. GooseFs를 편집하여 conf/goosefs-site.properties를 설정합니다. 다음과 같은 설정 항목을 추가하고 goosefs copyDir conf/를 모든 worker 노드로 복사하며 `./bin/goosefs-start.sh all` 클러스터를 재시작합니다.

```plaintext
goosefs.user.metrics.collection.enabled=true
goosefs.user.metrics.heartbeat.interval=10s
```

2. master와 worker의 Prometheus 모니터링 지표는 다음과 같은 명령어로 조회할 수 있습니다. 그중 master의 metrics 포트는 9201이며, worker의 metrics 포트는 9204입니다.

```plaintext
curl <LEADING_MASTER_HOSTNAME>:<MASTER_WEB_PORT>/metrics/prometheus/
# HELP Master_CreateFileOps Generated from Dropwizard metric import (metric=Master.CreateFileOps, type=com.codahale.metrics.Counter)
...

curl <WORKER_IP>:<WOKER_PORT>/metrics/prometheus/
# HELP pools_Code_Cache_max Generated from Dropwizard metric import (metric=pools.Code-Cache.max, type=com.codahale.metrics.jvm.MemoryUsageGaugeSet$$Lambda$51/137460818)
...
```

## 자체구축 Prometheus에 모니터링 지표 보고

1. Prometheus 설치 패키지를 다운로드 및 압축 해제하고, prometheus.yml을 수정합니다.
<pre class="rno-code-pre"><code class="language-plaintext">
# prometheus.yml
global:
	scrape_interval:     10s
	evaluation_interval: 10s
scrape_configs:
	- job_name: 'goosefs masters'
		metrics_path: /metrics/prometheus
		file_sd_configs:
		- refresh_interval: 1m
		files:
		- "targets/cluster/masters/*.yml"
	- job_name: 'goosefs workers'
		metrics_path: /metrics/prometheus
		file_sd_configs:
		- refresh_interval: 1m
		files:
		- "targets/cluster/workers/*.yml"
</code></pre>

2. targets/cluster/masters/masters.yml을 생성하여 master의 IP와 port를 추가합니다.

<pre class="rno-code-pre"><code class="language-plaintext">
 - targets:
	- "&lt;TARGERTS_MASTER_IP>:&lt;TARGERTS_MASTER_PORT>"
</code></pre>

3. targets/cluster/workers/workers.yml을 생성하여 worker의 IP와 port를 추가합니다.

<pre class="rno-code-pre"><code class="language-plaintext">
 - targets:
	- "&lt;TARGERTS_WORKER_IP>:&lt;TARGERTS_WORKER_PORT>"
</code></pre>

4. Prometheus를 실행하고, 그중 --web.listen-address는 Prometheus 수신 주소를 지정합니다. 기본 포트 번호: 9090

<pre class="rno-code-pre"><code class="language-plaintext">
nohup ./prometheus --config.file=prometheus.yml --web.listen-address="&lt;LISTEN_IP>:&lt;LISTEN_PORT>" > prometheus.log 2>&1 &
</code></pre>

5. 시각화 인터페이스를 조회합니다.

``` plaintext
http://<PROMETHEUS_BI_IP>:<PROMETHEUS_BI_PORT>
```

6. 기기 인스턴스를 조회합니다.
``` plaintext
http://<PROMETHEUS_BI_IP>:<PROMETHEUS_BI_PORT>/targets
```

## Tencent Cloud Prometheus에 모니터링 지표 보고

1. 설치 가이드의 가이드에 따라, master 기기에 Promethus agent를 설치합니다.

<pre class="rno-code-pre"><code class="language-plaintext">
wget https://rig-1258344699.cos.ap-guangzhou.myqcloud.com/prometheus-agent/agent_install && chmod +x agent_install && ./agent_install prom-12kqy0mw agent-grt164ii ap-guangzhou &lt;secret_id> &lt;secret_key>
</code></pre>
2. master와 worker의 캡처 작업을 설정합니다.

**방식1:**
<pre class="rno-code-pre"><code class="language-plaintext">
 job_name: goosefs-masters
 honor_timestamps: true
 metrics_path: /metrics/prometheus
 scheme: http
 file_sd_configs:
 - files:
	- /usr/local/services/prometheus/targets/cluster/masters/*.yml
	refresh_interval: 1m
job_name: goosefs-workers
honor_timestamps: true
metrics_path: /metrics/prometheus
scheme: http
file_sd_configs:
 - files:
	- /usr/local/services/prometheus/targets/cluster/workers/*.yml
	refresh_interval: 1m
</code></pre>

>! job_name에는 빈칸이 없지만, 오프라인 Prometheus의 job_name에는 빈칸이 포함될 수 있습니다.
>

**방식2:**

<pre class="rno-code-pre"><code class="language-plaintext">
job_name: goosefs masters
honor_timestamps: true
metrics_path: /metrics/prometheus
scheme: http
static_configs:
- targets:
 - "&lt;TARGERTS_MASTER_IP>:&lt;TARGERTS_MASTER_PORT>"
 refresh_interval: 1m
 
job_name: goosefs workers
honor_timestamps: true
metrics_path: /metrics/prometheus
scheme: http
static_configs:
- targets:
 - "&lt;TARGERTS_WORKER_IP>:&lt;TARGERTS_WORKER_PORT>"
 refresh_interval: 1m
</code></pre>

>! 캡처 작업은 두 번째 방법에 따라 구성되며 targets/cluster/masters/경로에 masters.yml 및 workers.yml 파일을 생성할 필요가 없습니다.
> 

## Grafana를 사용하여 모니터링 지표 조회

1. Grafana를 실행합니다.

```plaintext
nohup ./bin/grafana-server web > grafana.log 2>&1 &
```

2. 로그인 페이지 http://&lt;GRAFANA_IP&gt;:&lt;GRAFANA_PORT&gt;를 엽니다. Grafana 기본 포트: 3000，username과 password는 모두 admin이며，첫 로그인 후 비밀번호를 수정할 수 있습니다.
3. 페이지 이동 후 Prometheus의 Datasource를 추가합니다.

```plaintext
<PROMETHEUS_IP>:<PROMETHEUS_PORT>
```

4. Goosefs의 Grafana 템플릿을 가져오고, 가져올 json 및 위에서 생성한 Datasource를 선택합니다([json 다운로드](https://cos-data-lake-release-1253960454.file.myqcloud.com/goosefs/grafana/goosefs-grafana-dashboard.json)).
>! 클라우드 Prometheus 구매 시 비밀번호를 설정해야 합니다. 클라우드 Grafana의 시각화 모니터링 인터페이스 설정은 위와 유사하며, job_name은 일치하도록 설정해야 합니다.
>
5. DashBoard 수정 후 DashBoard 내보내기가 가능합니다.
