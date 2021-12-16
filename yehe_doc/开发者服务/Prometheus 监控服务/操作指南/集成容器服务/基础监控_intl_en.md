

You can choose the basic monitoring components you need when installing the Prometheus agent, but in some cases, you may want to turn on or off some monitoring components later.

## Preparations

- The Prometheus agent has been installed in the TKE cluster. For more information, please see Agent Management.
- Click a **Cluster ID** in the TKE cluster list to enter the **Integrate with TKE** page.

## Monitoring Components 

| Component | Usage |
|---------|---------|
|core-dns| Collects DNS monitoring metric data |
|kube-apiserver| Collects APISever monitoring metric data |
|kube-etcd| Collects Etcd monitoring metric data |
|kube-controller-manager| Collects Controller Manager monitoring metric data |
|kube-scheduler| Collects Scheduler monitoring metric data |
|node-exporter| Collects node monitoring metric data |
|kube-state-metrics| Collects TKE cluster status monitoring metric data |
|kubelet| Collects Kubelet and container monitoring metric data |
|kube-proxy| Collects Kube Proxy monitoring metric data |

## Directions

1. In the basic monitoring component list, you can enable components in the **Disabled** status.
2. In the basic monitoring component list, you can disable components in the **Enabled** status.
![](https://qcloudimg.tencent-cloud.cn/raw/06017e503643d009f8ea24f9b5e94c23.png)
>?The corresponding operation is asynchronous and takes about 2–3 minutes.
