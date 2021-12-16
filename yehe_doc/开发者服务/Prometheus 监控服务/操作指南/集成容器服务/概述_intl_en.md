

Tencent Kubernetes Engine (TKE) provides container-centric solutions based on native Kubernetes to solve environmental problems in development, testing, and OPS processes and help you reduce costs and improve efficiency. Kubernetes is an open-source container orchestration tool developed by and used at Google for more than 15 years. As a de facto standard in the container field, it can greatly simplify application management and deployment. The integration of TMP with TKE makes it much easier for you to monitor the status of Kubernetes and services running on it through TMP.

## Key Points

- Prometheus' scrape configuration mechanism under Kubernetes.
- Monitoring of TKE cluster status.
- Monitoring of cluster infrastructure.
- Monitoring of resource usage by cluster application containers.
- Monitoring of user-deployed applications.

## Concepts

| Term | Description |
|--------|---------|
| Prometheus Operator | In order to simplify the operations of Kubernetes, CoreOS introduced the concept of Operator and launched Prometheus Operator for Prometheus, which provides Prometheus-related custom Kubernetes resources to facilitate Prometheus operations |
| ServiceMonitor | It declaratively manages the monitoring configurations related to Service |
| PodMonitor | It declaratively manages the monitoring configurations related to Pod |
| Scrape configuration | Prometheus provides scrape configurations for a variety of scrape tasks, such as file-based and Consul |

## Directions

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the TMP instance to be manipulated, click the **instance ID** or **Manage** on the right to enter the instance management page.
3. In the left menu on the management page, click **Integrate with TKE** to enter the TKE integration page. Currently, the following services are provided:
    - Install agent.
    - Integrate basic monitoring related to Kubernetes.
    - View scrape task status and agent status.
