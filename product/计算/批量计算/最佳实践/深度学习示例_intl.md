## Quick Start
This document illustrates how to write a multilayer perceptron (MLP) BP algorithm based on a Scikit-learn machine learning library and then predict the probability of winning and losing between two football teams by modeling historical international football matches, team rankings, physical and skill metrics of players and the FIFA 2018 group match results. The steps are as follows:
### I. Making a Custom Image
1. See [Creating a Custom Image](https://intl.cloud.tencent.com/document/product/213/4942) for creation steps.
2. Install the dependency package. Take Centos 7.2 64-bit as an example:
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

### II. Downloading the Package
Click [Download application package](https://main.qcloudimg.com/raw/40b6eb7103072ca549e398ca39783f21.gz) and upload the downloaded package to [COS](https://intl.cloud.tencent.com/document/product/436). By specifying the COS address for the package, Batch will download the package to the CVM instance before the job starts and then automatically decompress and execute it.

### III. Creating a Task Template Named "fifa-predict"
1. Log in to the [Batch Console](), click **Task template** in the left navigation bar, select the target region and click **Create**.

2. Configure basic information. Below is an example:

  ![](https://main.qcloudimg.com/raw/adbdbc31286ef4d58d3ade44570cf832.png)
  * Name: fifa-predict;
  * Description: Data training and prediction;
  * Resource configuration: S2.SMALL1 (1 core, 1 GB memory); Internet bandwidth is postpaid;
  * Number of resources: Number of concurrent renderings; for example, 3 for training 3 neural network models concurrently;
  * Timeout: Default value;
  * Number of retries: Default value;
  * Image: Custom image ID, e.g. img-i64lx84h

3. Configure application information. Below is an example:

  ![](https://main.qcloudimg.com/raw/1203aa789d6666d7b63db9d643f1bb38.png)
  * Execution method: PACKAGE;
  * Package address: COS as an example, `cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`;
  * Stdout log: For formats, see [Entering COS or CFS Path](https://cloud.tencent.com/document/product/599/13996);
  * Stderr log: Same as Stdout Log;
  * Command line: `python predict.py "Japan" "Senegal"`.

4. Lost of teams: 'Russia', 'Saudi Arabia', 'Egypt', 'Uruguay', 'Portugal', 'Spain', 'Morocco', 'Iran', 'France', 'Australia', 'Peru', 'Denmark', 'Argentina', 'Iceland', 'Croatia', 'Nigeria', 'Brazil', 'Switzerland', 'Costa Rica', 'Serbia', 'Germany', 'Mexico', 'Sweden', 'Korea Republic', 'Belgium', 'Panama', 'Tunisia', 'England', 'Poland', 'Senegal', 'Colombia', 'Japan'.

5. Configure the storage mapping (skipped).

6. Preview the task's JSON file and click **Save** after confirming it is correct.

### IV. Creating a Task Template Named "fifa-merge"
1. Log in to the [Batch Console](), click **Task template** in the left navigation bar, select the target region and click **Create**.

2. Configure basic information. Below is an example:
![](https://main.qcloudimg.com/raw/3f79fc57b16a7a3c6d5d1083e86576e2.png)
  * Name: fifa-merge;
  * Description: Aggregation of prediction data;
  * Resource configuration: S2.SMALL1 (1 core, 1 GB memory); Internet bandwidth is postpaid;
  * Number of resources: 1;
  * Timeout: Default value;
  * Number of retries: Default value;
  * Image: Custom image ID, e.g. img-i64lx84h

3. Configure application information. Below is an example:
![](https://main.qcloudimg.com/raw/7c08ee74a2dadbea3ef0bc3b94788694.png)
  * Execution method: PACKAGE;
  * Package address: COS as an example, `cos://barrygz-1251783334.cosgz.myqcloud.com/fifa/fifa.2018.tar.gz`;
  * Stdout log: For formats, see [Entering COS or CFS Path](https://intl.cloud.tencent.com/document/product/599/13996);
  * Stderr log: Same as Stdout Log;
  * Command line: `python merge.py /data`.

4. Configure the storage mapping.
![](https://main.qcloudimg.com/raw/eb1b1dd75a45c81ae4b7089b36f7adc9.png)
 - Input path mapping > COS/CFS path: Enter the Stdout log path of the "fifa-predict" template.
 - Input path mapping > Local path: /data.

5. Preview the task's JSON file and click **Save** after confirming it is correct.

### V. Submitting a Job
1. Click **Job** in the left navigation bar, select the target region and click **Create**.

2. Configure basic job information. Below is an example:
  * Job name: fifa;
  * Priority: Default value;
  * Description: fifa 2018 model.

3. Select the **fifa-predict** and **fifa-merge** tasks on the left on the task flow page and move the tasks onto the canvas on the right using the mouse. Click the **fifa-predict** task anchor and drag it to the **fifa-merge** task.
![](https://main.qcloudimg.com/raw/d92616232f162679f03edfb4b7e32188.png)

4. Turn on **Task details** to the right of the task flow, confirm the configuration is correct and click **Finish**.

5. Query the job state. For more information, see [Querying Information]().
![](https://main.qcloudimg.com/raw/7f2fac7290ca2c51f0203e7b01821354.png)

6. Query the learning result. For more information, see [Viewing Object Information]().
![](https://main.qcloudimg.com/raw/1f8434915088871fa540ff7b754f84a1.png)

## What Can I Do Next?
This document illustrates a simple machine learning job to show the most basic capabilities of Batch. You can continue to test the advanced capabilities according to the Console User Guide.
- **Rich CVM configuration items**: Batch provides a wide variety of CVM configuration items, so you can customize the CVM configuration based on the specific business scenario.
- **Remote storage mapping**: Batch optimizes storage access and simplifies access to remote storage services into local file system operations.
- **Concurrent multi-model training**: Batch supports specifying of the number of concurrent instances which are distinguished through [Environment Variables](https://intl.cloud.tencent.com/document/product/599/11752) with each instance reading different training data for concurrent modeling.
