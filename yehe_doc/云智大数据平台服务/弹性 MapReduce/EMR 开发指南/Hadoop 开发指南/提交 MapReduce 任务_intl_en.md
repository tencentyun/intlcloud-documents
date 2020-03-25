This operation guide describes: 1. How to perform basic MapReduce job operations in command-line interfaces. 2. How to allow MapReduce jobs to access to the data stored in COS. For more information, please see the [community documentation](http://hadoop.apache.org/).

- The job submitted is a wordcount job. To count the words in a file, you need to upload the specified file in advance.
- The path of relevant software such as Hadoop is `/usr/local/service/`.
- The relevant logs are stored in `/data/emr`.

## 1. Preparations for Development
- You need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) in COS for this job.
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select **Enable COS** on the basic configuration page and then enter your SecretId and SecretKey. You can find your SecretId and SecretKey at [API Key Management](https://console.cloud.tencent.com/cam/capi). If you don't have a key, click **Create Key** to create one.

## 2. Logging in to an EMR Server
You need to log in to any server in the EMR cluster first before performing the relevant operations. A master node is recommended for this step. EMR is built on CVM instances running on Linux; therefore, using EMR in command line mode requires logging in to an CVM instance.

After creating the EMR cluster, select Elastic MapReduce in the console, find the cluster in cloud hardware management, click **Master Node** to select the resource ID of the master node. Then, you can enter the CVM Console and find the instance of the EMR cluster.

For more information on how to log in to a CVM instance, please see [Logging in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click **Login** on the right of the desired CVM instance to enter the login page. The default username is root, and the password is the one you set when creating the EMR cluster.

Once your credentials have been validated, you can access the EMR command-line interface. All Hadoop operations are under the Hadoop user. The root user is logged in by default when you log in to the EMR server, so you need to switch to the Hadoop user. Run the following command to switch users and go to the Hadoop folder:
```
[root@172 ~]# su hadoop
[hadoop@172 root]$ cd /usr/local/service/hadoop
[hadoop@172 hadoop]$
```

## 3. Data Preparations
You need to prepare a text file for counting. There are two ways to do so: **storing data in an HDFS cluster** and **storing data in COS**.

The first step is to upload a local file to the CVM instance of the EMR cluster with the scp or sftp service. Run the following command on the local command line:
```
scp $localfile root@public IP address:$remotefolder
```
Here, $localfile is the path and the name of your local file; root is the CVM instance username. You can look up the public IP address in the node information in the EMR or CVM Console; and $remotefolder is the path where you want to store the file in the CVM instance.

After the upload succeeds, you can check whether the file is in the corresponding folder on the command line of the EMR cluster.
```
[hadoop@172 hadoop]$ ls –l
```

### Storing data in HDFS
After uploading the data to the CVM instance, you can copy it to the HDFS cluster. The README.txt file in the `/usr/local/service/hadoop` directory is used here as an example. Copy the file to the Hadoop cluster by running the following command:
```
[hadoop@172 hadoop]$ hadoop fs -put README.txt /user/hadoop/
```
After the copy is completed, run the following command to view the copied file:
```
[hadoop@172 hadoop]$ hadoop fs -ls /user/hadoop
Output:
-rw-r--r-- 3 hadoop supergroup 1366 2018-06-28 11:39 /user/hadoop/README.txt
```
If there is no `/user/hadoop` folder in Hadoop, you can create it on your own by running the following command:
```
[hadoop@172 hadoop]$ hadoop fs –mkdir /user
```
For more Hadoop commands, please see [Common HDFS Operations](https://intl.cloud.tencent.com/document/product/1026/31124)


### Storing data in COS
There are two ways to store data in COS: **uploading through the COS Console from the local file system** and **uploading through Hadoop command from the EMR cluster**.

- When [uploading through the COS Console from the local file system](https://intl.cloud.tencent.com/document/product/436/13321), if the data file is already in COS, you can view it by running the following command:
 ```
 [hadoop@10 hadoop]$ hadoop fs -ls cosn://$bucketname/README.txt
-rw-rw-rw- 1 hadoop hadoop 1366 2017-03-15 19:09 cosn://$bucketname /README.txt
```
Replace $bucketname with the name and path of your bucket.

- To upload through Hadoop command from the EMR cluster, run the following command:
```
[hadoop@10 hadoop]$ hadoop fs -put README.txt cosn:// $bucketname /
[hadoop@10 hadoop]$ bin/hadoop fs -ls cosn:// $bucketname /README.txt
-rw-rw-rw- 1 hadoop hadoop 1366 2017-03-15 19:09 cosn://$bucketname /README.txt
```

## 4. Submitting a Job Through MapReduce
The job submitted this time is the wordcount routine that comes with the Hadoop cluster, which has already been compressed into a .jar package and uploaded to the created Hadoop cluster for direct call and use.

### Counting a text file in HDFS
Go to the `/usr/local/service/hadoop` directory as described in data preparations, and submit the job by running the following command:
```
[hadoop@10 hadoop]$ bin/yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount
/user/hadoop/README.txt /user/hadoop/output
```
> In the complete command above, `/user/hadoop/README.txt` is the input file to be processed, and `/user/hadoop/output` is the output folder. You should make sure that there is no output folder before submitting the command; otherwise, the submission will fail.

After the execution is completed, view the output file by running the following command:
```
[hadoop@10 hadoop]$ bin/hadoop fs -ls /user/hadoop/output
Found 2 items
-rw-r--r-- 3 hadoop supergroup 0 2017-03-15 19:52 /user/hadoop/output/_SUCCESS
-rw-r--r-- 3 hadoop supergroup 1306 2017-03-15 19:52 /user/hadoop/output/part-r-00000
```

View the statistics in part-r-00000 by running the following command:
```
[hadoop@10 hadoop]$ bin/hadoop fs -cat /user/hadoop/output/part-r-00000
(BIS),	1
(ECCN)	1
(TSU)	1
(see	1
5D002.C.1,	1
740.13)	1
<http://www.wassenaar.org/>	1
……
```

### Counting a text file in COS
Go to the `/usr/local/service/hadoop` directory and submit the job by running the following command:
```
[hadoop@10 hadoop]$ bin/yarn jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar  wordcount
cosn://$bucketname/README.txt /user/hadoop/output
```
The input file for the command is changed to `cosn:// $bucketname /README.txt`, which indicates to process the file in COS, where $bucketname is your bucket name and path. The result is still outputted to the HDFS cluster, but you can also choose to output to COS. The way to view the output is the same as above.

### Viewing job logs
```
# View job status
bin/mapred job -status jobid
# View job logs
yarn logs -applicationId id
```
