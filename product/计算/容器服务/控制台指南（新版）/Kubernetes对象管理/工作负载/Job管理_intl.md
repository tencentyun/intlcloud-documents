## Overview

A Job creates one or more Pods and ensures that a specified number of them successfully terminate.  Jobs work in many application scenarios, such as batch computation and data analysis. You can specify the number of repeated runs, the level of parallelism and the restart policy as needed. A Job will keep existing Pods and not create new Pods after it is complete. You can view the logs of the completed Pods in *Logs*. Deleting a Job will clean up the Pods it created as well as the logs of those Pods.
 
## Operation Guide for Jobs in the Console

### Creating a Job

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster in which the Job is created to enter the cluster management page of that Job.
4. Select "Workload" > "Job" to go to the Job information page. See the figure below:
![Job](https://main.qcloudimg.com/raw/0fa661e68d83d9cbb1f3228ad4988061.png)
5. Click **Create** to go to the "Create a workload" page. See the figure below:
![Create a workload](https://main.qcloudimg.com/raw/d0d07a0fdbfae2a2510aaef44d6e2e1a.png)
6. Specify the Job's parameters based on your needs. Key parameters are as follows:
 - Workload name: Custom.
 - Namespace: Select based on your actual needs.
 - Type: Select "Job (single-run task)".
 - Job settings: Set one or more containers for a Pod of the Job as needed.
    - Repetitions: Specify how many times the Pod the Job creates to repeat.
    - Parallelism: Specify the number of Pods the Job runs in parallel.
    - Restart policy: declare the restart policy which activates when the container of the Pod exits exceptionally.
       - Never: Do not restart the container until all containers in the Pod exit.
       - OnFailure: The Pod continues running while the containers will be restarted.
 - In-Pod containers: Set one or more different containers for a Pod of the Job based on actual needs.
    - Name: Customize the name of the in-Pod container.
    - Image: Select a value based on your actual needs.
    - Image tag: Enter a value based on your actual needs.
    - CPU/memory limits: Set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - Advanced settings: Parameters such as "**working directory**", "**run commands**", "**run parameters**", "**container health check**", and "**privilege level**" can be set.
7. Click **Create a workload**. Now you created a workload.

### Viewing Job Status

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where Job status needs to be checked to enter the cluster management page.
4. Select "Workload" > "Job" to go to the Job information page. See the figure below:
![Job](https://main.qcloudimg.com/raw/0fa661e68d83d9cbb1f3228ad4988061.png)
5. To view the Job's details, click its name.

### Deleting a Job

A Job will keep existing Pods and not create new Pods after it is complete.You can view the logs of the completed Pods in *Logs*. Deleting a Job will clean up the Pods it created as well as the logs of those Pods.

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
- spec.completions: Number of times the Pod the Job creates to repeat.
- spec.parallelism: Number of Pods the Job runs in parallel.
- spec.template: Template of the configuration of the Pod the Job creates.

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
4. Run the following command to see if the job is successfully created.
```shell
kubectl get job
```
A message similar to the one below indicates that the job is successfully created.
```
NAME      DESIRED   SUCCESSFUL   AGE
job       1         0            1m
```

### Deleting a Job

Run the following command to delete a Job.
```
kubectl delete job [NAME]
```
