## Overview

A CronJob object is similar to a line in a crontab (cron table) file. It periodically runs a Job according to the specified schedule. For more information about the format, see cron's documentation.
The cron format is as follows:
```
# File format description
# --minute (0 - 59)
# | --hour (0 - 23)
# | | --day (1 - 31)
# | | | --month (1 - 12)
# | | | | --week (0 - 6)
# | | | | |
# * * * * *
```

## Operation Guide for CronJobs in the Console

### Creating a CronJob

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where CronJob needs to be created to enter the cluster management page.
4. Select "Workload" > "CronJob" to go to the CronJob information page. See the figure below:
![CronJob](https://main.qcloudimg.com/raw/881d1fd3e52cfc6fa421f22820c09419.png)
5. Click **Create** to go to the "Create a workload" page. See the figure below:
![Create a workload](https://main.qcloudimg.com/raw/cc40dbd25618e72c92e47b0397443e7d.png)
6. Set the CronJob parameters based on actual needs. Key parameters are as follows:
 - Workload name: Custom.
 - Namespace: Select based on actual needs.
 - Type: Select "CronJob (running according to a cron schedule)".
 - Run policy: Set the periodic run policy of the Job based on the cron format.
 - Job settings
    - Repetitions: The number of times the Job-managed Pod needs to be repeated.
    - Parallelism: The number of Pods that the Job runs in parallel.
    - Restart policy: The restart policy after a container in the Pod exits exceptionally.
        - Never: Do not restart the container until all containers in the Pod exit.
        - OnFailure: The Pod continues to run and the container will be restarted.
 - In-Pod containers: Set one or more different containers for a Pod of the CronJob based on actual needs.
    - Name: Custom.
    - Image: Select based on actual needs.
    - Image tag: Enter based on actual needs.
    - CPU/memory limits: Set the CPU and memory limit according to [Kubernetes' resource limits](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/) to improve the robustness of the business.
    - Advanced settings: Parameters such as "**working directory**", "**run commands**", "**run parameters**", "**container health check**", and "**privilege level**" can be set.
7. Click **Create a workload**. Now you successfully created a workload.

### Viewing CronJob Status

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page.
3. Click the ID of the cluster where CronJob status needs to be checked to enter the cluster management page.
4. Select "Workload" > "CronJob" to go to the CronJob information page. See the figure below:
![CronJob](https://main.qcloudimg.com/raw/adee4e9199660c39f61fc091273d3999.png)
5. Click the name of the CronJob for which to view the status to view its details.

## Using kubectl to Manipulate CronJobs

<span id="YAMLSample"></span>
### YAML Sample

```Yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox
            args:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure
```
- kind: This identifies the CronJob resource type.
- metadata: Basic information such as CronJob name and Label.
- metadata.annotations: An additional description of the CronJob. You can set additional enhancements to TKE through this parameter.
- spec.schedule: The cron policy run by the CronJob.
- spec.jobTemplate: The Job template run by cron.

### Creating a CronJob

#### Method 1

1. See the [YAML sample](#YAMLSample) to prepare the CronJob YAML file.
2. Install kubectl and connect to a cluster.
3. Run the following command to create the CronJob YAML file.
```shell
kubectl create -f CronJob YAML filename
```
For example, to create a CronJob YAML file named cronjob.yaml, run the following command:
```shell
kubectl create -f cronjob.yaml
```

#### Method 2

1. Quickly create a CronJob by running the `kubectl run` command.
For example, to quickly create a CronJob that does not need to write full configuration information, run the following command:
```shell
kubectl run hello --schedule="*/1 * * * *" --restart=OnFailure --image=busybox -- /bin/sh -c "date; echo Hello"
```
2. Run the following command to see if you successfully created a CronJob.
```shell+-
kubectl get cronjob [NAME]
```
A message similar to the one below indicates that you successfully created the item.
```
NAME      SCHEDULE    SUSPEND   ACTIVE    LAST SCHEDULE   AGE
cronjob   * * * * *   False     0         <none>          15s
```

### Deleting a CronJob
>!
> - Before running this deletion command, please confirm whether there is a Job being created; if yes, running this command will terminate that Job.
> - When you run this deletion command, created Jobs and completed Jobs will not be terminated or deleted.
> - To delete a Job created by CronJob, please do so manually.

Run the following command to delete a CronJob.
```
kubectl delete cronjob [NAME]
```


