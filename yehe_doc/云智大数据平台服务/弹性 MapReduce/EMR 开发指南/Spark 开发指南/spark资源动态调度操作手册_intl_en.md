## Preparations for Development

Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, you need to select the spark_hadoop component on the software configuration page.

Spark is installed in the `/usr/local/service/` path (`/usr/local/service/spark`) in the CVM instance for the EMR cluster.

## Copying the JAR Package

You need to copy `spark-<version>-yarn-shuffle.jar` to the `/usr/local/service/hadoop/share/hadoop/yarn/lib` directory of all nodes in the cluster.

### Method 1. Use the SSH Console

1. On the left sidebar, select **Component Management** and click the **YARN** component to enter the YARN component management page.
![](https://main.qcloudimg.com/raw/82cbab09e1ca217e813c751dda026391.png)
2. On the YARN component management page, select **Role Management** and confirm the IP of the node where NodeManager resides.
![](https://main.qcloudimg.com/raw/81c6513609cdf77bd89505eaa14fba77.png)
3. Log in to the nodes where NodeManager resides one by one.
 - You need to log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.intl.cloud.tencent.com/document/product/213/5436). Here, you can log in by using XShell.
 - Use SSH to log in to other nodes where NodeManager resides. The used command is `ssh $user@$ip`, where `$user` is the login username, and `$ip` is the remote server IP (i.e., IP address confirmed in step 2).
![](https://main.qcloudimg.com/raw/d83d844103c4a6050a83700fadaf79dd.png)
 - Verify that the switch is successful.
![](https://main.qcloudimg.com/raw/30f0578b2cc19daebbdd82df8d95c13e.png)

4. Search for the path of the `spark-<version>-yarn-shuffle.jar` file.
![](https://main.qcloudimg.com/raw/4927797f6ff300662f14dd3d0ae3b22a.png)
5. Copy `spark-<version>-yarn-shuffle.jar` to `/usr/local/service/hadoop/share/hadoop/yarn/lib`.
![](https://main.qcloudimg.com/raw/fab8b0abf34de2f4608924e9982f28ac.png)
6. Log out and switch to other nodes.
![](https://main.qcloudimg.com/raw/a9d4b368807a974b618202af0173357c.png)

### Method 2. Use batch deployment script

You need to log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.intl.cloud.tencent.com/document/product/213/5436). Here, you can log in by using XShell.

Write the following Shell script for batch file transfer. When there are many nodes in a cluster, to avoid entering the password for multiple times, you can use sshpass for file transfer. sshpass provides password-free transfer to eliminate your need to enter the password repeatedly; however, the password plaintext is prone to disclosure and can be found with the `history` command.

1. Install sshpass for password-free transfer.
```
[root@172 ~]# yum install sshpass
```
Write the following script:
```
#!/bin/bash
nodes=(ip1 ip2 … ipn) # List of IPs of all nodes in the cluster separated by spaces
len=${#nodes[@]}
password=<your password>
file=" spark-2.3.2-yarn-shuffle.jar "
source_dir="/usr/local/service/spark/yarn"
target_dir="/usr/local/service/hadoop/share/hadoop/yarn/lib"
echo $len
for node in ${nodes[*]}
do
     echo $node;
     sshpass -p $password scp "$source_dir/$file"root@$node:"$target_dir";
done
```
2. Transfer files in a non-password-free manner.
Write the following script:
```
#!/bin/bash
nodes=(ip1 ip2 … ipn) # List of IPs of all nodes in the cluster separated by spaces
len=${#nodes[@]}
password=<your password>
file=" spark-2.3.2-yarn-shuffle.jar "
source_dir="/usr/local/service/spark/yarn"
target_dir="/usr/local/service/hadoop/share/hadoop/yarn/lib"
echo $len
for node in ${nodes[*]}
do
       echo $node;
       scp "$source_dir/$file" root@$node:"$target_dir";
done
```

## Modifying YARN Configuration
1. On the YARN component management page, select "Configuration Management". Select the configuration file `yarn-site.xml` and select cluster as the dimension (modifications of configuration items in the cluster dimension will be applied to all nodes in the cluster).
![](https://main.qcloudimg.com/raw/d84c5b5e5b3d3509276f16e9b9deeb9e.png)
2. Modify the `yarn.nodemanager.aux-services` configuration item and add `spark_shuffle`.
![](https://main.qcloudimg.com/raw/d264a6708b76c10d3239dd2eb50a09a8.png)
3. Add the configuration item `yarn.nodemanager.aux-services.spark_shuffle.class` and set it to `org.apache.spark.network.yarn.YarnShuffleService`.
![](https://main.qcloudimg.com/raw/83993fcd50f163befd89dde88de4edae.png)
4. Add the configuration item `spark.yarn.shuffle.stopOnFailure` and set it to `false`.
![](https://main.qcloudimg.com/raw/c068045128997e8006c977ef7f622b6d.png)
5. Save and distribute the settings. Restart the YARN component for the configuration to take effect.

## Modifying Spark Configuration
1. In **Component Management**, find the Spark component and select **Configure** in the **Operation** column.
![](https://main.qcloudimg.com/raw/505a7650875913b419106602b0ba4b9a.png)
2. Select the configuration file **spark-defaults.conf**, click **Modify Configuration**, and create configuration items as shown below:
![](https://main.qcloudimg.com/raw/325a2334537b0b1a32cd4c6e358a52c4.png)
<table>
<tr>
<th>Configuration Item</th>
<th>Value</th>
<th>Remarks</th>
</tr>
<tr>
<td>spark.shuffle.service.enabled</td>
<td>true</td>
<td>It starts the shuffle service.</td>
</tr>
<tr>
<td>spark.dynamicAllocation.enabled</td>
<td>true</td>
<td>It starts dynamic resource allocation.</td>
</tr>
<tr>
<td>spark.dynamicAllocation.minExecutors</td>
<td>1</td>
<td>It specifies the minimum number of executors allocated for each application.</td>
</tr>
<tr>
<td>spark.dynamicAllocation.maxExecutors</td>
<td>30</td>
<td>It specifies the maximum number of executors allocated for each application.   </td>
</tr>
<tr>
<td>spark.dynamicAllocation.initialExecutors</td>
<td>1</td>
<td>Generally, its value is the same as that of `spark.dynamicAllocation.minExecutors`. </td>
</tr>
<tr>
<td>spark.dynamicAllocation.schedulerBacklogTimeout</td>
<td>1s</td>
<td>If there are pending jobs backlogged for more than this duration, new executors will be requested.</td>
</tr>
<tr>
<td>spark.dynamicAllocation.sustainedSchedulerBacklogTimeout</td>
<td>5s</td>
<td>If the queue of pending jobs still exists, it will be triggered again once every several seconds. The number of executors requested per round grows exponentially compared to the previous round.</td>
</tr>
<tr>
<td>spark.dynamicAllocation.executorIdleTimeout</td>
<td>60s</td>
<td>If an executor has been idle for more than this duration, it will be deleted by the application.</td>
</tr>
</table>

3. Save and distribute the configuration and restart the component.

## Testing Dynamic Scheduling of Spark Resources
### 1. Resource configuration description of the testing environment
In the testing environment, there are two nodes where NodeManager is deployed, and each node has a 4 CPU cores and 8 GB memory. The total resources of the cluster are 8 CPU cores and 16 GB memory.
### 2. Testing job description
#### Test 1
- In the EMR Console, enter the `/usr/local/service/spark` directory, switch to the "hadoop" user, and run `spark-submit` to submit a job. The data needs to be stored in HDFS.
```
[root@172 ~]# cd /usr/local/service/spark/
[root@172 spark]# su hadoop
[hadoop@172 spark]$  hadoop fs -put ./README.md /
[hadoop@172 spark]$ spark-submit --class org.apache.spark.examples.JavaWordCount --master yarn-client --num-executors 10 --driver-memory 4g --executor-memory 4g --executor-cores 2 ./examples/jars/spark-examples_2.11-2.3.2.jar /README.md /output
```
- In the "Application" panel of the WebUI of the YARN component, you can view the container and CPU allocation before and after the configuration.
![](https://main.qcloudimg.com/raw/8b929f19b8bf42b161817ae4a3effa85.png)
- Before dynamic resource scheduling is configured, at most 3 CPUs can be allocated.
![](https://main.qcloudimg.com/raw/e09ddfe7a396414a7741e951aa154ec8.png)
- After dynamic resource scheduling is configured, up to 5 CPUs can be allocated.

Conclusion: after dynamic resource scheduling is configured, the scheduler will allocate more resources based on the real-time needs of applications.

#### Test 2

- In the EMR Console, enter the `/usr/local/service/spark` directory, switch to the "hadoop" user, and run `spark-sql` to start the interactive SparkSQL Console, which is set to use most of the resources in the testing cluster. Configure dynamic resource scheduling and check resource allocation before and after the configuration.
```
[root@172 ~]# cd /usr/local/service/spark/
[root@172 spark]# su hadoop
[hadoop@172 spark]$ spark-sql --master yarn-client --num-executors 5 --driver-memory 4g --executor-memory 2g --executor-cores 1
```
- Use the example for calculating the pi that comes with Spark 2.3.0 as the testing job. When submitting the job, set the number of executors to 4, the driver memory to 4 GB, the executor memory to 4 GB, and the number of executor cores to 2.
```
[root@172 ~]# cd /usr/local/service/spark/
[root@172 spark]# su hadoop
[hadoop@172 spark]$ spark-submit --class org.apache.spark.examples.SparkPi --master yarn-client --num-executors 5 --driver-memory 4g --executor-memory 4g --executor-cores 2 examples/jars/spark-examples_2.11-2.3.2.jar 500
```
![](https://main.qcloudimg.com/raw/80f77735e7e6a90c7752562fe38f24e6.png)
- The resource utilization when only the SparkSQL job is running is 90.3%.
![](https://main.qcloudimg.com/raw/ea7f6348bd1359ede90341bd1cb87397.png)
- After the SparkPi job is submitted, the resource utilization of SparkSQL becomes 27.8%.

Conclusion: although the SparkSQL job applies for a large amount of resources during submission, no analysis jobs are executed; therefore, there are a lot of idle resources actually. When the idle duration exceeds the limit set by `spark.dynamicAllocation.executorIdleTimeout`, idle executors will be released, and other jobs will get resources. In this test, the cluster resource utilization of the SparkSQL job decreases from 90% to 28%, and idle resources are allocated to the pi calculation job; therefore, automatic scheduling is effective.

>The value of the configuration item `spark.dynamicAllocation.executorIdleTimeout` affects the speed of dynamic resource scheduling. In the test, it is found that the resource scheduling duration is basically the same as this value. You are recommended to adjust this value based on your actual needs for optimal performance.
