## Overview of Task-based Modeling

Task-based modeling provides model building capabilities in a wizard-like training task submission method and supports task submission based on multiple algorithm sources. It allows you to directly bind mainstream high-performance, distributed training frameworks through code package to quickly submit and start training tasks. The following uses a simple PyTorch MPI job as an example to demonstrate how to quickly create a task in task-based modeling.
## Data Preparations
### Dataset
This document uses the MNIST database available [here](https://tencent-cloud-product-release-1258877907.cos.ap-guangzhou.myqcloud.com/TI-ONE-release/TIONE%E5%85%AC%E6%9C%89%E4%BA%91%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8-%E5%8B%BF%E5%88%A0/ti-images.zip).
### Code package
The training script in this document is written by using the PyTorch framework. Its code package can be downloaded [here](https://tencent-cloud-product-release-1258877907.cos.ap-guangzhou.myqcloud.com/TI-ONE-release/TIONE%E5%85%AC%E6%9C%89%E4%BA%91%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8-%E5%8B%BF%E5%88%A0/mnist.pytorch.zip).
## Directions
### Step 1 of task creation
1. Go to **Training** > **Task-based Modeling** and click **New Task** to enter the task creation wizard.

![](https://qcloudimg.tencent-cloud.cn/raw/194bb4af4e6b76d69bd090f4905d7298.png)

1. Enter the following information on the basic information page:

   - Task Name: mnist_train
   - Training Framework: select **Built-in framework / PyTorch / 1.9-py3.6-cuda11.1-gpu**.
   - Training Mode: select **MPI**.
   - Billing Mode: select **Pay-as-You-Go**.
   - Spec: select **8C40G V100*1**.
   - Node Count: select **1**.
   - Tag and Description: optional

   After entering the required information, click **Next** to go to the task configuration page.

![](https://qcloudimg.tencent-cloud.cn/raw/f40bdb4a0dfeffd009b711fea19f1521.png)

### Step 2 of task creation

Enter the following information on the task configuration page:

1. Algorithm Source:

   - Code Package: click **Select**. In the COS pop-up window, select the target bucket, click **Upload Folder** in the bottom-left corner, upload the `mnist.pytorch` folder generated after decompressing the code package to the bucket, and select the path of the code package.
   - Startup Commands: enter `sh start.sh`.

![](https://qcloudimg.tencent-cloud.cn/raw/20d6f01ce319820ef8ac8fc27a0a909a.png)

2. Data Source: select **COS**.

   - Mapping Path: enter `train`.
   - Dataset Path: click **Select**. In the COS pop-up window, select the target bucket, click **Upload Folder** in the bottom-left corner, upload the `ti-images` folder generated after decompressing the dataset, and select the folder path as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/bf2e6ae479fe3c05384418259965ffa2.png)

![](https://qcloudimg.tencent-cloud.cn/raw/b9cd316c7b34404b575134b79c37c5c9.png)

3. Tuning Parameter: none.

4. Training Output: click **Select**. In the COS pop-up window, select the target bucket path for saving the training output data as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/9e372ceee98928936105a675b265ab4a.png)

1. CLS Log: toggle it off.
2. VPC: select **Do not use VPC**.

After completing the configuration, view the hourly rate of the training task at the bottom of the page and click **OK**.

![](https://qcloudimg.tencent-cloud.cn/raw/4da928c725228a855418f3f20e9b8a49.png)