This section describes running a Spark wordcount application in Python.
## 1.	Preparations for Development
- You need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) in COS for this job.
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating your EMR cluster, click the Spark component on the software configuration page, click "Enable COS" on the basic configuration page and then enter your SecretId and SecretKey. You can find your SecretId and SecretKey at [API Key Management](https://console.cloud.tencent.com/cam/capi). If you don’t have a SecretKey, click **Create Key** to create one.

## 2.	Data Preparations
Upload the to-be-processed file to COS first. If the file is in your local file system, upload it directly through the [COS Console](https://intl.cloud.tencent.com/document/product/436/13321); if it is in the EMR cluster, upload it by running the following Hadoop command:
```
[hadoop@10 hadoop]$ hadoop fs -put $testfile cosn:// $bucketname/
```
Here, $testfile is the full path with file name and $bucketname is your bucket name. After the upload is completed, you can check whether the file is available in COS.

## 3.	Running the Demo
First, you need to log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click "Log in" on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.

Run the following command on the EMR command-line interface to switch to the Hadoop user and go to the Spark installation directory `/usr/local/service/spark`:
```
[root@172 ~]# su hadoop
[hadoop@172 root]$ cd /usr/local/service/spark
```
Create a Python file named wordcount.py and add the following code:
```
from __future__ import print_function

import sys 
from operator import add
from pyspark.sql import SparkSession

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("Usage: wordcount <file>", file=sys.stderr)
        exit(-1)

    spark = SparkSession\
        .builder\
        .appName("PythonWordCount")\
        .getOrCreate()

    sc = spark.sparkContext

    lines = spark.read.text(sys.argv[1]).rdd.map(lambda r: r[0])
    counts = lines.flatMap(lambda x: x.split(' ')) \
                  .map(lambda x: (x, 1)) \
                  .reduceByKey(add)

    output = counts.collect()
    counts.saveAsTextFile(sys.argv[2])

    spark.stop()
```
Submit the job by running the following command:
```
[hadoop@10   spark]$   ./bin/spark-submit   --master yarn   ./wordcount.py 
cosn://$bucketname/$yourtestfile cosn:// $bucketname/$output
```
Here, $bucketname is your COS bucket name, $yourtestfile is the full path with test file name in the bucket, and $output is your output folder. **If the $output folder already exists before the command is executed, the program will fail.**

After the program is running automatically, you can find the output file in the target bucket:
```
[hadoop@172 spark]$ hadoop fs -ls cosn:// $bucketname/$output
Found 2 items
-rw-rw-rw- 1 hadoop Hadoop 0 2018-06-29 15:35 cosn:// $bucketname/$output /_SUCCESS
-rw-rw-rw- 1 hadoop Hadoop 2102 2018-06-29 15:34 cosn:// $bucketname/$output /part-00000
```
You can also look up the result by running the following command:
```
[hadoop@172 spark]$ hadoop fs -cat cosn:// $bucketname/$output /part-00000
(u'', 27)
(u'code', 1)
(u'both', 1)
(u'Hadoop', 1)
(u'Bureau', 1)
(u'Department', 1)
```
You can also output the result to HDFS by changing the output location in the command as follows:
```
[hadoop@10spark]$   ./bin/spark-submit   ./wordcount.py
cosn://$bucketname/$yourtestfile /user/hadoop/$output
```
Here, `/user/hadoop/` is the path in HDFS, which can be created on your own if not present.
After the job is completed, you can view the Spark execution log by running the following command:
```
[hadoop@10 spark]$  /usr/local/service/hadoop/bin/yarn logs -applicationId $yourId
```
Here, $yourId should be replaced with your job ID, which can be viewed in Yarn's WebUI.
