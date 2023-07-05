## Quick Start
This document describes how to write a multilayer perceptron (MLP) BP algorithm based on a Scikit-learn machine learning library to predict the probability of winning and losing between two football teams by modeling historical international football matches, team rankings, physical and skill metrics of players, and the FIFA 2018 group match results. Below are the detailed directions.

### Step 1. Make a custom image<span id="Step1"></span>
1. For creation steps, please see [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
2. Install the dependency package. Take CentOS 7.2 64-bit as an example:
```
yum -y install gcc
yum -y install python-devel
yum -y install tkinter
yum -y install python-pip
pip install --upgrade pip
pip install pandas
pip install numpy
pip install matplotlib
pip install seaborn
pip install sklearn
pip install --upgrade python-dateutil
```

### Step 2. Download the application package
Click [here](https://main.qcloudimg.com/raw/40b6eb7103072ca549e398ca39783f21.gz) to download the application package and upload it to [COS](https://intl.cloud.tencent.com/zh/document/product/436). Specify the COS endpoint of the package, BatchCompute will download the package to the CVM instance before the job starts and automatically decompress and execute it.

### Step 3. Create a "fifa-predict" task template
1. Log in to the BatchCompute Console and select **[Task Template](https://console.cloud.tencent.com/batch/task)** on the left sidebar.
2. Select the target region at the top on the "Task Template" page and click **Create**.
3. Click **Create** to enter the "New task template" page and create a template as shown below:
![](https://main.qcloudimg.com/raw/adbdbc31286ef4d58d3ade44570cf832.png)
  * **Name**: fifa-predict.
  * **Description**: data training and prediction.
  * **Compute environment type**: select as needed. **Auto compute environment** is selected in this example.
  * **Resource configuration**: S2.SMALL1 (1 core 1 GB memory). Public network bandwidth is pay-as-you-go.
  * **Image**: custom image ID. Please select the one created in [step 1](#Step1).
  * **Resource quantity**: number of concurrent renderings, such as 3, which means to train 3 neural network models concurrently.
  * **Timeout threshold and number of retry attempts**: keep the default values.
3. Click **Next** to configure the program information as shown below:
![](https://main.qcloudimg.com/raw/1203aa789d6666d7b63db9d643f1bb38.png)
  * **Execution method**: PACKAGE.
  * **Package address**: using COS as an example: `cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`.
  * **Stdout log**: for more information on the format, please see [Entering COS & CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996).
  * **Stderr log**: same as Stdout log.
  * **Command line**: `python predict.py "Japan" "Senegal"`.
Team list: 'Russia', 'Saudi Arabia', 'Egypt', 'Uruguay', 'Portugal', 'Spain', 'Morocco', 'Iran', 'France', 'Australia', 'Peru', 'Denmark', 'Argentina', 'Iceland', 'Croatia', 'Nigeria', 'Brazil', 'Switzerland', 'Costa Rica', 'Serbia', 'Germany', 'Mexico', 'Sweden', 'Korea Republic', 'Belgium', 'Panama', 'Tunisia', 'England', 'Poland', 'Senegal', 'Colombia', 'Japan'.
4. Skip the storage mapping configuration step and click **Next**.
5. Preview the task's JSON file and click **Save** after confirming that everything is correct.

### Step 4. Create a "fifa-merge" task template
1. Log in to the BatchCompute Console and select **[Task Template](https://console.cloud.tencent.com/batch/task)** on the left sidebar.
2. Select the target region at the top on the "Task Template" page and click **Create**.
3. Click **Create** to enter the "New task template" page and create a template as shown below:
![](https://main.qcloudimg.com/raw/3f79fc57b16a7a3c6d5d1083e86576e2.png)
  * **Name**: fifa-merge.
  * **Description**: aggregation of prediction data.
  * **Compute environment type**: select as needed. **Auto compute environment** is selected in this example.
  * **Resource configuration**: S2.SMALL1 (1 core 1 GB memory). Public network bandwidth is pay-as-you-go.
  * **Image**: custom image ID. Please select the one created in [step 1](#Step1).
  * **Resource quantity**: 1.
  * **Timeout threshold and number of retry attempts**: keep the default values.
3. Click **Next** to configure the program information as shown below:
![](https://main.qcloudimg.com/raw/7c08ee74a2dadbea3ef0bc3b94788694.png))
  * **Execution method**: PACKAGE.
  * **Package address**: using COS as an example: `cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`.
  * **Stdout log**: for more information on the format, please see [Entering COS & CFS Paths](https://intl.cloud.tencent.com/document/product/599/13996).
  * **Stderr log**: same as Stdout log.
  * **Command line**: `python merge.py /data`.
4. Click **Next** to configure the storage mapping as shown below:
![](https://main.qcloudimg.com/raw/eb1b1dd75a45c81ae4b7089b36f7adc9.png)
 - **Input path mapping > COS/CFS path**: enter the Stdout log path of the "fifa-predict" template.
 - **Input path mapping > Local path**: `/data`.
5. Preview the task's JSON file and click **Save** after confirming that everything is correct.

### Step 5. Submit a job
1. Click **Job** on the left sidebar to enter the "Job" list page.
2. On the "Job" list page, select the target region at the top and click **Create**.
2. Enter the "New job" page and configure job information as shown below:
  * **Job name**: fifa.
  * **Priority**: default value.
  * **Description**: fifa 2018 model.
4. Select the **fifa-predict** and **fifa-merge** tasks on the left on the task flow page and drag them to the canvas on the right. Click the **fifa-predict** task anchor and drag it to the **fifa-merge** task.
![](https://main.qcloudimg.com/raw/d92616232f162679f03edfb4b7e32188.png)
5. Enable **Task information** on the right on the task flow page, confirm that the configuration is correct, and click **Complete**.
5. Query the job running information. For more information, please see [Information Query](https://intl.cloud.tencent.com/document/product/599/14567).
![](https://main.qcloudimg.com/raw/7f2fac7290ca2c51f0203e7b01821354.png)
6. Query the rendering result. For more information, please see [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326).
![](https://main.qcloudimg.com/raw/1f8434915088871fa540ff7b754f84a1.png)

## Subsequent Operations
This document illustrates a simple machine learning job to demonstrate basic BatchCompute capabilities. You can continue to test the advanced capabilities of BatchCompute as instructed in the Console User Guide.
- **Various CVM configurations**: BatchCompute provides a variety of CVM configuration options. You can customize your own CVM configuration based on your business scenario.
- **Remote storage mapping**: BatchCompute optimizes storage access and simplifies access to remote storage services into operations in the local file system.
- **Concurrent multi-model training**: With BatchCompute, you can specify the number of concurrent instances and use [environment variables](https://intl.cloud.tencent.com/document/product/599/11752) to separate instances and read different training data for concurrent modeling.



