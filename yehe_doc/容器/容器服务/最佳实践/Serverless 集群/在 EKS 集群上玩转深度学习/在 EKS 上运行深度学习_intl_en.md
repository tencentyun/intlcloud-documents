## Overview

This series of documents describe how to deploy deep learning in EKS from direct TensorFlow deployment to subsequent Kubeflow deployment and are intended to provide a comprehensive scheme for implementing container-based deep learning.


## Prerequisites

This document proceeds to run a deep learning task in EKS by using a self-built cluster after the steps in [Building Deep Learning Container Image](https://intl.cloud.tencent.com/document/product/457/42059) are completed.
The self-built image has been uploaded to the image repository `ccr.ccs.tencentyun.com/carltk/tensorflow-model`, which can be directly pulled for use with no rebuild required.



## Directions


### Creating EKS cluster

Please create an EKS cluster as instructed in [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
>?As you need to run a GPU-based training task, when creating a cluster, please pay attention to the supported resources in the AZ of the selected container network and be sure to select an AZ that supports GPU as shown below:
![](https://main.qcloudimg.com/raw/58034799229973690611ef067cec37b5.png)


### Creating CFS file system (optional)

The container will be automatically deleted, and the resources will be automatically released after the task ends. Therefore, to persistently store models and data, we recommend you mount an external storage service such as [CBS](https://intl.cloud.tencent.com/document/product/362), [CFS](https://intl.cloud.tencent.com/document/product/582), and [COS](https://intl.cloud.tencent.com/document/product/436).

In this example, CFS is used as an NFS disk to persistently store data with frequent reads and writes.

#### Creating CFS file system

1. Log in to the [CFS](https://console.cloud.tencent.com/cfs/fs) console and enter the **File System** page.
2. Click **Create**. On the **Create File System** page that pops up, select the file system type and click **Next: Detailed Settings**.
3. On the **Detailed Settings** page, set the relevant configuration items. For more information on CFS types and configurations, please see [Creating File Systems and Mount Targets](https://intl.cloud.tencent.com/document/product/582/9132).
![](https://main.qcloudimg.com/raw/60f6718380420de728392c6a93cf6fd9.png)
>!The CFS file system must be created in the region of the cluster.
4. After confirming that everything is correct, click **Buy Now** and make the payment to create a file system.


#### Getting file system mount information

1. On the **File System** page, click the ID of the file system whose sub-target path needs to be obtained to enter the file system details page.
2. Select the **Mount Target Info** tab and get the file system mount information next to **Mount to Linux** as shown below:
![](https://main.qcloudimg.com/raw/ff3df7a80f7a5755b0dc54062b661056.png)
>?Note down the IPv4 address in the mount target details, such as `10.0.0.161:/`, which will be used as the NFS path in subsequent mount configuration.



### Creating training task

This task uses the MNIST handwritten digit recognition dataset and two-layer CNN as an example. The sample image is the [self-built image](https://console.cloud.tencent.com/tke2/registry/user/self/detail/tag?rid=5&reponame=carltk%2Ftensorflow-model) created in the previous chapter. If you need to use a custom image, please see [Creating Deep Learning Container Image](https://intl.cloud.tencent.com/document/product/457/42059). Two task creation methods are provided below:

<dx-tabs>
::: Console
Taking the essence of the deep learning task into account, Job node deployment is used as an example in this document. For more information on how to deploy a Job, please see [Job Management](https://intl.cloud.tencent.com/document/product/457/30665).
The following is the example of deployment in the console:

1. In the **Volume (optional)** configuration item, select **Using NFS disk** and enter the name and IPv4 address of the CFS file system created previously as shown below:
![](https://main.qcloudimg.com/raw/88778dcc49791bb5114b24b987152d51.png)
2. In the **Mount Target** configuration item in **Containers in the Pod**, select the volume and configure the mount target as shown below:
![](https://main.qcloudimg.com/raw/d433dada54f0f2bd3c186e0c2e039268.png)
[](id:precautions)
>!
>- As the dataset may need to be downloaded online, you need to configure the public network access for the cluster. For more information, please see [Public Network Access](https://intl.cloud.tencent.com/document/product/457/42062).
>- After selecting a GPU model, when setting the request and limit, you need to assign the container CPU and memory resources meeting the [resource specifications](https://intl.cloud.tencent.com/document/product/457/34057). The actual values do not need to be accurate down to the ones place.
  When configuring in the console, you can also delete the default configuration and leave it empty to configure "unlimited" resources, which also have the corresponding billing specifications. This approach is recommended.
>- The container running command is inherited from Docker's `CMD` field, whose preferred form is `exec`. If you do not call the `shell` command, there will be no normal shell processing. Therefore, if you want to run a command in the `shell` form, you need to add `"sh"` and `"-c"` at the beginning.
  When you enter multiple commands and parameters in the console, each command should take a line (subject to the line break)
:::
::: kubectl
You can also use a YAML file to create a task.
1. Prepare a YAML file. Below is the sample file `gpu_pod.yaml`:
<dx-codeblock>
:::  yaml
apiVersion: v1
kind: Pod
metadata: 
    name: tf-cnn
    annotations: 
    #eks.tke.cloud.tencent.com/cpu: "8"
    #eks.tke.cloud.tencent.com/gpu-count: "1"
    eks.tke.cloud.tencent.com/gpu-type: T4
    #eks.tke.cloud.tencent.com/mem: 32Gi
spec: 
    containers: 
  - name: tf-cnn
    image: hkccr.ccs.tencentyun.com/carltk/tensorflow-model:latest # Training task image
    env:  
    - name: MODEL_DIR
      value: /tf/model
    - name: DATA_DIR
      value: /tf/data
    command: 
      - "sh"
      - "-c"
      # Script that triggers the training task
      - "python3 official/vision/image_classification/mnist_main.py \ 
        --model_dir=$MODEL_DIR \
        --data_dir=$DATA_DIR \
        --train_epochs=5 \
        --distribution_strategy=one_device \
        --num_gpus=1 \
        --download"
    resources: 
      limits: 
        #cpu: "8" 
        #memory: 32Gi
        nvidia.com/gpu: "1" 
      requests: 
        #cpu: "8"
        #memory: 32Gi
        nvidia.com/gpu: "1" 
    volumeMounts: 
    - name: tf-model-cfs
      mountPath: /tf
    volumes:  
  - name: tf-model-cfs   # Persistently store the training results to CFS
    nfs:  
      path: /            # Enter the root directory of the CFS file system here
      server: 10.0.1.8   # Enter the IPv4 address of the created CFS file system
    restartPolicy: OnFailure
:::
</dx-codeblock>
2. Run the following command to complete deployment:
```sh
kubectl create -f [yaml_name]
```
<dx-alert infotype="notice" title="">
In addition to the [precautions](#precautions) mentioned above for directions in the console, you also need to pay attention to the following:

- You need to use `annotations` to declare resource assignment in the YAML file. For more information, please see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162). You also should note that different GPU models correspond to different CPU and memory options. We recommend you enter the values as needed.
- Here, NFS is used as the data volume. If you want to use other data volumes for persistent storage, please see [Instructions for Other Storage Volumes](https://intl.cloud.tencent.com/document/product/457/30678).
- You can **reserve** `eks.tke.cloud.tencent.com/gpu-type` only with **no other items** needed in annotations. If `/gpu-count` is specified, then `cpu` and `mem` must also be specified. (In this document, we **recommend you not add other items**, which will not affect the actual effect. If you enter other items without following the specifications, OOM errors may occur.)
- For `nvidia.com/gpu` in GPU scheduling, **only `limits` is required**. If only `annotations` is specified, an error will be reported that no cards are found. If only `limits` is specified, its values will be considered as the `request`. If `request` is also specified, its value must be the same as that of `limits`. For more information, please see [Schedule GPUs](https://kubernetes.io/zh/docs/tasks/manage-gpus/scheduling-gpus/) (here, **adding the `cpu` and `memory` settings in `request` and `limits` is also not recommended** as detailed above).
</dx-alert>
:::
</dx-tabs>





### Viewing running result

You can view the running result either in the console or on the command line:

<dx-tabs>
::: Console
After creating a Job, you will be redirected to the Job management page by default. You can also enter the page as follows:
1. Log in to the TKE console and click **Elastic Container** > **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** on the left sidebar.
2. In the elastic cluster list, click the ID of the cluster whose events you want to view to enter the cluster management page.
3. Select **Workload** > **Job** and click the newly created Job in the Job list.
	- Select the **Event** tab to view events as shown below:
	![](https://main.qcloudimg.com/raw/95eb57fa00729e0a4362fad69922ea0c.png)
	- Select the **Log** tab to view logs as shown below:
	![](https://main.qcloudimg.com/raw/7b426961d27dbc10a4c3e9df82a7dcc8.png)
	![](https://main.qcloudimg.com/raw/1c62f6739885af581885ad43a55c15d7.png)
:::
::: Command line
You can run commands to view events or logs:
- Run the following command to view events:
```sh
kubectl describe pod [name]
```
See the figure below:
![](https://main.qcloudimg.com/raw/65020975db4da78481d1453034346ede.png)
- Run the following command to output logs continuously:
```sh
kubectl logs -f [pod_name]
```
See the figure below:
![](https://main.qcloudimg.com/raw/f38ed0501b8a0fdda2049d11b9c477e4.png)
![](https://main.qcloudimg.com/raw/1cc1ffe53e8c03951fe70ccf53b8d8c6.png)
As EKS containers will be terminated after use, you can view logs only when the Pod is in **Running** status. For the solution, please see [Log Collection](https://intl.cloud.tencent.com/document/product/457/42063).

#### Viewing storage
If you have configured NFS as instructed above, you can go to the mount target to view NFS storage:
1. Run the following command to enter the relevant mount directory to check whether it exists:
```shell
cd /mound_data
```
See the figure below:
![](https://main.qcloudimg.com/raw/dc20d01b4b200e12520d901c5c087305.png)
2. Enter the `model` directory and view whether there is relevant data in it as shown below:
![](https://main.qcloudimg.com/raw/7850fee6d7bffdfb7aa25c96b2f6dee7.png)
3. Enter the `data` directory and view whether there is relevant data in it as shown below:
![](https://main.qcloudimg.com/raw/c70c91fe9911cc71234740905f233616.png)
:::
</dx-tabs>





## Relevant Operations

### Using GPU to deploy deep learning task in TKE

Deployment in TKE is almost the same as that in EKS. Taking deployment through kubectl with a YAML file as an example, TKE has the following differences:

- When creating a TKE node, you should select a node with GPU. For more information, please see [Using a GPU Node](https://intl.cloud.tencent.com/document/product/457/30656).
- As the node has built-in GPU resources, `annotations` and `resources` are not needed. Practically, you can reserve `annotations`, which TKE will not process. We recommend you comment out `resources`, as it may cause unreasonable resource requirements.




## FAQs

If you encounter any problems when performing this practice, please see [FAQs](https://intl.cloud.tencent.com/zh/document/product/457/42062) for troubleshooting.
