## Overview

Based on [Custom Metrics API](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/instrumentation/custom-metrics-api.md), TKE supports many metrics for auto scaling, including CPU, memory, disk, network and GPU related metrics, which can cover most HPA scenarios. For detailed metrics, see [HPA Metrics](https://intl.cloud.tencent.com/document/product/457/34025).
For complex scenarios such as auto scaling based on the number of the service single-replica QPS, you can install [prometheus-adapter](https://github.com/DirectXMan12/k8s-prometheus-adapter) to implement auto scaling. Kubernetes provides [Custom Metrics API](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/instrumentation/custom-metrics-api.md) and <a href="https://github.com/kubernetes/community/blob/master/contributors/design-proposals/instrumentation/external-metrics-api.md">External Metrics API</a> for HPA to perform auto scaling based on metrics, allowing users to customize auto scaling as needed.
Prometheus-adapter supports the above two APIs. In the actual environment, the Custom Metrics API can meet most scenarios. This document describes how to use custom metrics for auto scaling through the Custom Metrics API.




## Prerequisites

- You have created a TKE cluster of v1.12 or later version. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- You have deployed the PROM instance and collected the corresponding custom metrics.
- You have installed [Helm](https://helm.sh/docs/intro/install/).

## Directions

<span id="example"></span>

### Opening the monitoring metric

This document takes the Golang service application as an example, which opens the `httpserver_requests_total` metric and records HTTP requests. This metric can be used to calculate the QPS value of the service application, as shown below:
```go
package main

import (
		"github.com/prometheus/client_golang/prometheus"
		"github.com/prometheus/client_golang/prometheus/promhttp"
		"net/http"
		"strconv"
)

var (
HTTPRequests = prometheus.NewCounterVec(
		prometheus.CounterOpts{
			Name: "httpserver_requests_total",
			Help: "Number of the http requests received since the server started",
		},
		[]string{"status"},
	)
)

func init() {
	prometheus.MustRegister(HTTPRequests)
}

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		path := r.URL.Path
		code := 200
		switch path {
		case "/test":
			w.WriteHeader(200)
			w.Write([]byte("OK"))
		case "/metrics":
			promhttp.Handler().ServeHTTP(w, r)
		default:
			w.WriteHeader(404)
			w.Write([]byte("Not Found"))
		}
		HTTPRequests.WithLabelValues(strconv.Itoa(code)).Inc()
	})
	http.ListenAndServe(":80", nil)
}
```



### Deploying the service application

By using Deployment, you can containerize and deploy the service application to the TKE cluster, as shown below:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpserver
  namespace: httpserver
spec:
  replicas: 1
  selector:
    matchLabels:
      app: httpserver
  template:
    metadata:
      labels:
        app: httpserver
    spec:
      containers:
      - name: httpserver
        image: imroc.tencentcloudcr.com/test/httpserver:v1
        imagePullPolicy: Always

---

apiVersion: v1
kind: Service
metadata:
  name: httpserver
  namespace: httpserver
  labels:
    app: httpserver
  annotations:
    prometheus.io/scrape: "true"
    prometheus.io/path: "/metrics"
    prometheus.io/port: "http"
spec:
  type: ClusterIP
  ports:
  - port: 80
    protocol: TCP
    name: http
  selector:
    app: httpserver
```


### Collecting service monitoring metrics through PROM instance

You can configure PROM instance to collect the monitoring metrics opened by service through [PROM Instance Collection Rules](#way1) or [ServiceMonitor](#way2).

<span id="way1"></span>

#### Method 1: Configuring PROM instance collection rules

Add the following collection rules to the configuration file of PROM instance collection rule, as shown below:
```yaml
	- job_name: httpserver
		scrape_interval: 5s
		kubernetes_sd_configs:
		- role: endpoints
			namespaces:
				names:
				- httpserver
		relabel_configs:
		- action: keep
			source_labels:
			- __meta_kubernetes_service_label_app
			regex: httpserver
		- action: keep
			source_labels:
			- __meta_kubernetes_endpoint_port_name
			regex: http
```

[](id:way2)

#### Method 2: Configuring ServiceMonitor

If prometheus-operator has been installed, you can create a CRD object of the ServiceMonitor to configure PROM instance, as shown below:
```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: httpserver
spec:
  endpoints:
  - port: http
    interval: 5s
  namespaceSelector:
    matchNames:
    - httpserver
  selector:
    matchLabels:
      app: httpserver
```

### Installing prometheus-adapter

1. Use Helm to install [prometheus-adapter](https://artifacthub.io/packages/helm/prometheus-community/prometheus-adapter). Please confirm and configure custom metrics before installation. According to the example in [Opening the monitoring metric](#example) above, the `httpserver_requests_total` metric is used in the service to record HTTP requests, so you can calculate the QPS of each service Pod through the following PromQL, as shown below:
```
sum(rate(http_requests_total[2m])) by (pod)
```
2. Convert it to the configuration of prometheus-adapter. Create `values.yaml` with the following content:
```yaml
rules:
      default: false
      custom:
      - seriesQuery: 'httpserver_requests_total'
        resources:
          template: <<.Resource>>
        name:
          matches: "httpserver_requests_total"
          as: "httpserver_requests_qps" # QPS metric calculated by PromQL
        metricsQuery: sum(rate(<<.Series>>{<<.LabelMatchers>>}[1m])) by (<<.GroupBy>>)
prometheus:
      url: http://prometheus.monitoring.svc.cluster.local # Replace PROM instance API address (Do not need a port)
      port: 9090
```
3. Run the following Helm command to install prometheus-adapter, as shown below:
>! Before installation, you need to delete the TKE's registered Custom Metrics API using the following command:
> `kubectl delete apiservice v1beta1.custom.metrics.k8s.io`
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
# Helm 3
helm install prometheus-adapter prometheus-community/prometheus-adapter -f values.yaml
# Helm 2
# helm install --name prometheus-adapter prometheus-community/prometheus-adapter -f values.yaml
```

### Verifying installation result

If the installation is correct, you can run the following command to view the configured QPS related metrics returned by the Custom Metrics API, as shown below:
```bash
$ kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1
{
  "kind": "APIResourceList",
  "apiVersion": "v1",
  "groupVersion": "custom.metrics.k8s.io/v1beta1",
  "resources": [
    {
      "name": "jobs.batch/httpserver_requests_qps",
      "singularName": "",
      "namespaced": true,
      "kind": "MetricValueList",
      "verbs": [
        "get"
      ]
    },
    {
      "name": "pods/httpserver_requests_qps",
      "singularName": "",
      "namespaced": true,
      "kind": "MetricValueList",
      "verbs": [
        "get"
      ]
    },
    {
      "name": "namespaces/httpserver_requests_qps",
      "singularName": "",
      "namespaced": false,
      "kind": "MetricValueList",
      "verbs": [
        "get"
      ]
    }
  ]
}
```

Run the following command to view the QPS value of the Pod, as shown below:
>?In the following example, the value is 500m, which means the value of QPS is 0.5 request/second.
``` bash
$ kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1/namespaces/httpserver/pods/*/httpserver_requests_qps
{
  "kind": "MetricValueList",
  "apiVersion": "custom.metrics.k8s.io/v1beta1",
  "metadata": {
    "selfLink": "/apis/custom.metrics.k8s.io/v1beta1/namespaces/httpserver/pods/%2A/httpserver_requests_qps"
  },
  "items": [
    {
      "describedObject": {
        "kind": "Pod",
        "namespace": "httpserver",
        "name": "httpserver-6f94475d45-7rln9",
        "apiVersion": "/v1"
      },
      "metricName": "httpserver_requests_qps",
      "timestamp": "2020-11-17T09:14:36Z",
      "value": "500m",
      "selector": null
    }
  ]
}
```



### Testing HPA

If the scaling out is triggered when the average QPS of each service Pod reaches 50 requests/second, and the minimum and maximum number of replicas are 1 and 1000 respectively, the configuration example will be as follows:
``` yaml
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: httpserver
  namespace: httpserver
spec:
  minReplicas: 1
  maxReplicas: 1000
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: httpserver
  metrics:
  - type: Pods
    pods:
      metric:
        name: httpserver_requests_qps
      target:
        averageValue: 50
        type: AverageValue
```

Run the following command to test the service and observe whether the scaling out is triggered, as shown below:
``` bash
$ kubectl get hpa
NAME         REFERENCE               TARGETS     MINPODS   MAXPODS   REPLICAS   AGE
httpserver   Deployment/httpserver   83933m/50   1         1000      2          18h
$ kubectl get pods
NAME                          READY   STATUS              RESTARTS   AGE
httpserver-6f94475d45-47d5w   1/1     Running             0          3m41s
httpserver-6f94475d45-7rln9   1/1     Running             0          37h
httpserver-6f94475d45-6c5xm   0/1     ContainerCreating   0          1s
httpserver-6f94475d45-wl78d   0/1     ContainerCreating   0          1s
```

If the scaling out is triggered normally, it means that HPA has implemented auto scaling based on service custom metrics.
