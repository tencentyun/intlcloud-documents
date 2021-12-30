## Overview
CLS supports log collection for self-built Kubernetes clusters. Before performing log collection on a self-built Kubernetes cluster, you need to use a custom resource definition (CRD) to define log collection configuration (LogConfig), and deploy Log-Provisioner, Log-Agent, and LogListener on the cluster. If you are a Tencent Kubernetes Engine (TKE) user, you can quickly access and use the CLS service by referring to [Enabling log collection](https://intl.cloud.tencent.com/document/product/457/32419).


## Prerequisites

- You have created a cluster of Kubernetes 1.10 or above.
- You have enabled CLS, created a logset and a log topic, and obtained the log topic ID (`topicId`).
For configuration details, please see [Creating a log topic](https://intl.cloud.tencent.com/document/product/614/34239).
- You have obtained the domain name (`CLS_HOST`) of the region of your log topic.
For details of the CLS domain name list, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
- You have obtained the API key ID (`TmpSecretId`) and API key (`TmpSecretKey`) required for CLS authentication.
To obtain the API key and API key ID, go to [Manage API Key](https://console.cloud.tencent.com/cam/capi).

## Kubernetes Log Collection Principles
Log collection on a Kubernetes cluster requires the following:
- LogConfig: CRD of log collection configuration, which defines where logs are collected, how they are parsed, and to which CLS log topic they are shipped after being parsed.
- Log-Provisioner: component used to synchronize the log collection configuration defined in LogConfig to CLS.
- Log-Agent: component used to listen for changes in LogConfig and containers on nodes and dynamically calculate the actual positions of log files in containers on node hosts.
- LogListener: component used to collect log file content from node hosts, parses it, and uploads it to CLS.


## Directions
<dx-steps>
- <a href="#crd">Define the LogConfig resource type</a>
- <a href="#logconfig_def">Define the LogConfig object</a>
- <a href="#logconfig_create">Create a LogConfig object</a>
- <a href="#configmap">Configure CLS authentication ConfigMap</a>
- <a href="#log-provisioner">Deploy Log-Provisioner</a>
- <a href="#log-agent">Deploy Log-Agent and LogListener</a>
</dx-steps>

## Directions

### Step 1. Define the LogConfig resource type[](id:crd)

Define the LogConfig resource type using a Kubernetes CRD. 
Run the wget command to download the `CRD.yaml` declaration file and run the kubectl command to define the LogConfig resource type, using the master node path `/usr/local/` as an example.
```shell
wget https://mirrors.tencent.com/install/cls/k8s/CRD.yaml
kubectl create -f /usr/local/CRD.yaml
```

### Step 2. Define the LogConfig object[](id:logconfig_def)

Create a LogConfig object to define log collection configuration. Run the wget command to download the `LogConfig.yaml` declaration file, using the master node path `/usr/local/` as an example.
```shell
wget https://mirrors.tencent.com/install/cls/k8s/LogConfig.yaml
```
The `LogConfig.yaml` declaration file consists of the following two parts:
- clsDetail: defines the log parsing format and the target log topic ID (`topicId`).
- inputDetail: defines the log source from which logs are collected.

>! During configuration, change the `topicId` item in `clsDetail` to the ID of the log topic that you created.


#### Log parsing format

<dx-tabs>
::: Full text in a single line [](id:single_line)
In "full text in a single line" mode, a line is a full log. When CLS collects logs, it uses the line break `\n` to mark the end of a log. For easier structural management, a default key value `\_\_CONTENT\_\_` is given to each log, but the log data itself will no longer be structured, nor will the log field be extracted. The time attribute of a log is determined by the collection time.

Assume that the raw data of a log is as follows:
```
Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```

A sample of LogConfig configuration is as follows:
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # Single-line log
    logType: minimalist_log
```

The data collected to CLS is as follows:
```
__CONTENT__:Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```
:::
::: Full text in multi lines [](id:multi_line)
In "full text in multi lines" mode, a log may span multiple lines (such as Java stacktrace), and the line break `\n` cannot be used to mark the end of a log. To help CLS distinguish between logs, a first-line regular expression is used for matching. When a line of a log matches the preset regular expression, it is considered as the beginning of the log, and the log ends before the next matching line.

In the "full text in multi lines" mode, a default key `\_\_CONTENT\_\_` is also set, but the log data itself is not structured, and no log fields are extracted. The time attribute of a log is determined by the collection time.

Assume that the raw data of a multi-line log is:
```
2019-12-15 17:13:06,043 [main] ERROR com.test.logging.FooFactory:
java.lang.NullPointerException
    at com.test.logging.FooFactory.createFoo(FooFactory.java:15)
    at com.test.logging.FooFactoryTest.test(FooFactoryTest.java:11)
```

A sample of LogConfig is as follows:
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # Multi-line log
    logType: multiline_log
    extractRule:
      # Only a line that starts with a date time is considered the beginning of a new log. Otherwise, add the line break `\n` to the end of the current log.
      beginningRegex: \d{4}-\d{2}-\d{2}\s\d{2}:\d{2}:\d{2},\d{3}\s.+
```

The data collected to CLS is as follows:
```
__CONTENT__:2019-12-15 17:13:06,043 [main] ERROR com.test.logging.FooFactory:\njava.lang.NullPointerException\n    at com.test.logging.FooFactory.createFoo(FooFactory.java:15)\n    at com.test.logging.FooFactoryTest.test(FooFactoryTest.java:11)
```
:::
::: Single line - full regex [](id:single_full_regex)
The "single line - full regex" mode is often used to process structured logs. It parses a full log by extracting multiple key-value pairs based on a regex. 

Assume that the raw data of a log is as follows:
```
10.135.46.111 - - [22/Jan/2019:19:19:30 +0800] "GET /my/course/1 HTTP/1.1" 127.0.0.1 200 782 9703 "http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum" "Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0"  0.354 0.354
```

A sample of LogConfig is as follows:
```
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # Full Regex
    logType: fullregex_log
    extractRule:
      # Regular expression, in which the corresponding values will be extracted based on the `()` capture groups
      logRegex: (\S+)[^\[]+(\[[^:]+:\d+:\d+:\d+\s\S+)\s"(\w+)\s(\S+)\s([^"]+)"\s(\S+)\s(\d+)\s(\d+)\s(\d+)\s"([^"]+)"\s"([^"]+)"\s+(\S+)\s(\S+).*
      beginningRegex: (\S+)[^\[]+(\[[^:]+:\d+:\d+:\d+\s\S+)\s"(\w+)\s(\S+)\s([^"]+)"\s(\S+)\s(\d+)\s(\d+)\s(\d+)\s"([^"]+)"\s"([^"]+)"\s+(\S+)\s(\S+).*
      # List of extracted keys, which are in one-to-one correspondence with the extracted values
      keys:  ['remote_addr','time_local','request_method','request_url','http_protocol','http_host','status','request_length','body_bytes_sent','http_referer','http_user_agent','request_time','upstream_response_time']
```

The data collected to CLS is as follows:
```
body_bytes_sent: 9703
http_host: 127.0.0.1
http_protocol: HTTP/1.1
http_referer: http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum
http_user_agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0
remote_addr: 10.135.46.111
request_length: 782
request_method: GET
request_time: 0.354
request_url: /my/course/1
status: 200
time_local: [22/Jan/2019:19:19:30 +0800]
upstream_response_time: 0.354
```
:::
::: Multiple lines - full regex [](id:multi_full_regex)
In "multiple lines - full regex" mode, multiple key-value pairs can be extracted from a complete piece of log data that spans multiple lines in a log text file (such as Java program logs) based on a regular expression. If you don't need to extract key-value pairs, please configure it by referring to the "full text in multi lines" mode.

Assume that the raw data of a log is as follows:
```
[2018-10-01T10:30:01,000] [INFO] java.lang.Exception: exception happened
   at TestPrintStackTrace.f(TestPrintStackTrace.java:3)
   at TestPrintStackTrace.g(TestPrintStackTrace.java:7)
   at TestPrintStackTrace.main(TestPrintStackTrace.java:16)
```

A sample of LogConfig is as follows:
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec: 
  clsDetail: 
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
        # Multiple lines - full regex
        logType: multiline_fullregex_log
        extractRule: 
          # The first-line full regular expression: only a line that starts with a date time is considered the beginning of a new log. Otherwise, add the line break `\n` to the end of the current log.
          beginningRegex: \[\d+-\d+-\w+:\d+:\d+,\d+\]\s\[\w+\]\s.*
          # Regular expression, in which the corresponding values will be extracted based on the `()` capture groups
          logRegex: \[(\d+-\d+-\w+:\d+:\d+,\d+)\]\s\[(\w+)\]\s(.*)
          # List of extracted keys, which are in one-to-one correspondence with the extracted values
          keys: ['time','level','msg']
```

Based on the extracted key, the data collected to CLS is as follows:
```
time: 2018-10-01T10:30:01,000`
level: INFO`
msg: java.lang.Exception: exception happened
   at TestPrintStackTrace.f(TestPrintStackTrace.java:3)
   at TestPrintStackTrace.g(TestPrintStackTrace.java:7)
   at TestPrintStackTrace.main(TestPrintStackTrace.java:16)
```
:::
::: JSON format [](id:json)
A JSON log automatically extracts the key at the first layer as the field name and the value at the first layer as the field value to implement structured processing of the entire log. Each complete log ends with a line break `\n`.

Assume the raw data of a JSON log is as follows:
```
{"remote_ip":"10.135.46.111","time_local":"22/Jan/2019:19:19:34 +0800","body_sent":23,"responsetime":0.232,"upstreamtime":"0.232","upstreamhost":"unix:/tmp/php-cgi.sock","http_host":"127.0.0.1","method":"POST","url":"/event/dispatch","request":"POST /event/dispatch HTTP/1.1","xff":"-","referer":"http://127.0.0.1/my/course/4","agent":"Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0","response_code":"200"}
```

A sample of LogConfig is as follows:
```
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # JSON log
    logType: json_log
```

The data collected to CLS is as follows:
```
agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0
body_sent: 23
http_host: 127.0.0.1
method: POST
referer: http://127.0.0.1/my/course/4
remote_ip: 10.135.46.111
request: POST /event/dispatch HTTP/1.1
response_code: 200
responsetime: 0.232
time_local: 22/Jan/2019:19:19:34 +0800
upstreamhost: unix:/tmp/php-cgi.sock
upstreamtime: 0.232
url: /event/dispatch
xff: -
```
:::
::: Separator format [](id:delimiter)
For a log in separator format (separator log), the entire log data can be structured according to the specified separator, and each complete log ends with a line break `\n`. When CLS processes separator logs, you need to define a unique key for each separate field.

Assume the raw data of a log is as follows:
```
10.20.20.10 ::: [Tue Jan 22 14:49:45 CST 2019 +0800] ::: GET /online/sample HTTP/1.1 ::: 127.0.0.1 ::: 200 ::: 647 ::: 35 ::: http://127.0.0.1/
```

A sample of LogConfig is as follows:
```
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # Separator log
    logType: delimiter_log
    extractRule:
      # Separator
      delimiter: ':::'
      # List of extracted keys, which are in one-to-one correspondence to the separated fields
      keys: ['IP','time','request','host','status','length','bytes','referer']
```

The data collected to CLS is as follows:
```
IP: 10.20.20.10
bytes: 35
host: 127.0.0.1
length: 647
referer: http://127.0.0.1/
request: GET /online/sample HTTP/1.1
status: 200
time: [Tue Jan 22 14:49:45 CST 2019 +0800]
```
:::
</dx-tabs>


#### Log source

CLS supports the following cluster log sources:

<dx-tabs>
::: Standard container output [](id:pod_stdout)
Sample 1: collecting the standard output of all containers in the default namespace
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_stdout
    containerStdout:
      namespace: default
      allContainers: true
 ...
```

Sample 2: collecting the container standard output in the Pod that belongs to ingress-gateway deployment in the production namespace
```
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_stdout
    containerStdout:
      allContainers: false
      workloads:
      - namespace: production
        name: ingress-gateway
        kind: deployment
  ...
```

Sample 3: collecting the container standard output in the Pod whose Pod labels contain "k8s-app=nginx" in the production namespace
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_stdout
    containerStdout:
      namespace: production
      allContainers: false
      includeLabels:
        k8s-app: nginx
  ...
```
:::
::: Container file [](id:pod_file)
Sample 1: collecting the `access.log` file in the `/data/nginx/log/` path in the NGINX container in the Pod that belongs to ingress-gateway deployment in the production namespace
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_file
    containerFile:
      namespace: production
      workload:
        name: ingress-gateway
        type: deployment
      container: nginx
      logPath: /data/nginx/log
      filePattern: access.log
  ...
```

Sample 2: collecting the `access.log` file in the `/data/nginx/log/` path in the NGINX container in the Pod whose pod labels contain "k8s-app=ingress-gateway" in the production namespace
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_file
    containerFile:
      namespace: production
      includeLabels:
        k8s-app: ingress-gateway
      container: nginx
      logPath: /data/nginx/log
      filePattern: access.log
  ...
```
:::
::: Host file [](id:node_file)
Sample: collecting all `.log` files in the host path `/data/`
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: host_file
    hostFile:
      logPath: /data
      filePattern: *.log
  ...
```
:::
:::
</dx-tabs>

### Step 3. Create a LogConfig object [](id:logconfig_create)

Since the `LogConfig.yaml` declaration file is defined in [Step 2. Define the LogConfig object](#logconfig_def), you can run the kubectl command to create a LogConfig object.
```shell
kubectl create -f /usr/local/LogConfig.yaml
```

### Step 4. Configure CLS authentication ConfigMap [](id:configmap)

To upload logs from a self-built Kubernetes cluster to CLS, you need to create a ConfigMap for storing the **API key ID** and **API key**.

1. Run the wget command to download the `ConfigMap.yaml` declaration file, using the master node path `/usr/local/` as an example.
```shell
wget https://mirrors.tencent.com/install/cls/k8s/ConfigMap.yaml
```
>! During configuration, set **TmpSecretId** and **TmpSecretKey** in `ConfigMap.yaml` to your **API key ID** and **API key** respectively.
2. Run the kubectl command to create a ConfigMap object.
```shell
kubectl create -f /usr/local/ConfigMap.yaml
```


### Step 5. Deploy Log-Provisioner [](id:log-provisioner)

Log-Provisioner discovers and listens for CLS consumer information, log collection rules, and log file paths from LogConfig resources and synchronizes them to CLS. 

1. Run the wget command to download the `Log-Provisioner.yaml` declaration file, using the master node path `/usr/local/` as an example.
```shell
wget https://mirrors.tencent.com/install/cls/k8s/Log-Provisioner.yaml
```
>! During configuration, set the `env` environment variable field **CLS_HOST** in `Log-Provisioner.yaml` to the domain name of the region where the target log topic belongs. For the domain names of different regions, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). In addition, the `env` environment variable field **CLUSTER_ID** must be set to any name that is different from the names of all machine groups under your account. You can view all machine groups under your account on the machine group management page in the CLS console.
>
2. Use kubectl to deploy Log-Provisioner in Deployment mode.
```shell
kubectl create -f /usr/local/Log-Provisioner.yaml
```


### Step 6. Deploy Log-Agent and LogListener [](id:log-agent)

Cluster log collection requires two components:
- Log-Agent: pulls the information of log sources specified in the cluster LogConfig and calculates the absolute paths of the container logs mapped on hosts.
- LogListener: collects and parses log files in host log file paths and uploads them to CLS.


1. Run the wget command to download the declaration files of Log-Agent and LogListener, using the master node path `/usr/local/` as an example.
```shell
wget https://mirrors.tencent.com/install/cls/k8s/Log-Agent.yaml
```
>! 
> - During configuration, set the `env` environment variable field **CLS_HOST** in `Log-Agent.yaml` to the domain name of the region where the target log topic belongs. For the domain names of different regions, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). In addition, the `env` environment variable field **CLUSTER_ID** must be set to any name that is different from the names of all machine groups under your account. You can view all machine groups under your account on the machine group management page in the CLS console.
> - If the docker root directory of the host is not under `/var/lib/docker` (root directory of the host), you need to map the docker root directory to the container in the `Log-Agent.yaml` declaration file. As shown in the following figure, mount `/data/docker` to the container.
> ![](https://qcloudimg.tencent-cloud.cn/raw/8899c793eba711d3aa0f6a164b747019.jpg)
2. Run the kubectl command to deploy Log-Agent and LogListener in DaemonSet mode.
```shell
kubectl create -f /usr/local/Log—Agent.yaml
```

## Subsequent Operations

After the deployment for cluster log collection is completed, you can go to [CLS console > Search and Analysis](https://console.cloud.tencent.com/cls/search) to view collected logs.
