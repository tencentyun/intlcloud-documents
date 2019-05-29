## Overview

A Job controller creates 1 to N Pods that run according to the running rules until the end of run. Jobs can be used for scenarios such as batch computation and data analysis. The business needs can be satisfied by setting the number of repeated runs, parallelism, and restart policy.
After a Job is completed, no more Pods will be created, and existing Pods will not be deleted. You can view the logs of the completed Pods in "Logs". If you delete the Job, the Pods created by the Job will also be deleted, and the logs of the Pods created by the Job will disappear.

## Operation Guide for Jobs in the Console

### Creating a Job

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Job needs to be created to enter the cluster management page.
4. Select "Workload" > "Job" to go to the Job information page. See the figure below:
![Job](https://main.qcloudimg.com/raw/0fa661e68d83d9cbb1f3228ad4988061.png)
5. Click **Create** to go to the "Create a workload" page. See the figure below:
![Create a workload](https://main.qcloudimg.com/raw/d0d07a0fdbfae2a2510aaef44d6e2e1a.png)
6. Set the Job parameters based on actual needs. Key parameters are as follows:
 - Workload name: Custom.
 - Namespace: Select based on actual needs.
 - Type: Select "Job (single-run task)".
 - Job settings: Set one or more different containers for a Pod of the Job based on actual needs.
    - Repetitions: Set the number of times the Job-managed Pod needs to be repeated.
    - Parallelism: Set the number of Pods that the Job runs in parallel.
    - Restart policy: Set the restart policy after a container in the Pod exits exceptionally.
       - Never: Do not restart the container until all containers in the Pod exit.
       - OnFailure: The Pod continues to run and the container will be restarted.
 - In-Pod containers: Set one or more different containers for a Pod of the Job based on actual needs.
    - Name: Custom.
    - Image: Select based on actual needs.
    - Image tag: Enter based on actual needs.
    - CPU/memory limits: Set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - Advanced settings: Parameters such as "**working directory**", "**run commands**", "**run parameters**", "**container health check**", and "**privilege level**" can be set.
7. Click **Create a workload** to complete the creation.

### Viewing Job Status

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Job status needs to be checked to enter the cluster management page.
4. Select "Workload" > "Job" to go to the Job information page. See the figure below:
![Job](https://main.qcloudimg.com/raw/0fa661e68d83d9cbb1f3228ad4988061.png)
5. Click the name of the Job for which to view the status to view its details.

### Deleting a Job

After a Job is completed, no more Pods will be created, and existing Pods will not be deleted. You can view the logs of the completed Pods in "Logs". If you delete the Job, the Pods created by the Job will also be deleted, and the logs of the Pods created by the Job will disappear.

## Using kubectl to Manipulate Jobs

<span id="YAMLSample"></span>
### YAML Sample

```Yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  completions: 2
  parallelism: 2
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4
```
- kind: This identifies the Job resource type.
- metadata: Basic information such as Job name and Label.
- metadata.annotations: An additional description of the Job. You can set additional enhancements to TKE through this parameter.
- spec.completions: The number of times the Job-managed Pod needs to be repeated.
- spec.parallelism: The number of Pods that the Job runs in parallel.
- spec.template: Detailed template configuration of the Pod managed by the Job.

### Creating a Job

1. See the [YAML sample](#YAMLSample) to prepare the Job YAML file.
2. Install kubectl and connect to a cluster. For detailed operations, see [Connecting a Cluster via kubectl](https://cloud.tencent.com/document/product/457/8438).
3. Create the Job YAML file.
```
kubectl create -f Job YAML filename
```
For example, to create a Job YAML file named pi.yaml, run the following command:
```shell
kubectl create -f pi.yaml
```
4. Run the following command to verify whether the creation is successful.
```shell
kubectl get job
```
If a message similar to the one below is returned, the creation is successful.
```
NAME      DESIRED   SUCCESSFUL   AGE
job       1         0            1m
```

### Deleting a Job

Run the following command to delete a Job.
```
kubectl delete job [NAME]
```
