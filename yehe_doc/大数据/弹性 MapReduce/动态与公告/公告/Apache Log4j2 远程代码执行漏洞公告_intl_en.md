## Vulnerability Description
-----
Recently, Tencent Cloud has noticed that the remote code execution vulnerability in Apache Log4j 2 has been disclosed. There is a JNDI injection vulnerability in Log4j 2, which can be triggered when the program logs the user-input data. It can be exploited to run any code on the target server. For more information on the vulnerability, see [here](https://s.tencent.com/research/report/144).

## Impact
-----
Components in EMR such as Flink, Hive, Ranger, Presto, Oozie, Knox, Storm, and Druid are affected by this vulnerability. If you are affected, fix it as instructed below.

## Solution
-----

Replace the Log4j 2 package with a safe version.
Affected versions: Apache Log4j2 2.0–2.15.0-rc1.
Safe versions: Apache Log4j 2.17.1.

## Fix Command
-----
1. Run the fix command in the standard EMR directory:
<table>
<thead>
<tr>
<th>wget https://image-repo-gz-1259353343.cos.ap-guangzhou.myqcloud.com/user-patches/common/fix-log4j2.sh -O fix-log4j2.sh && bash -x fix-log4j2.sh /usr/local/service
</th>
</tr>
</thead>
</table >
2. Fix the JAR packages in the cache directory when running the task.
	- Make sure that there are no problematic JAR packages in the submitted task; otherwise, they will be cached again in the task submitted next time.
	- Directly delete the problematic JAR packages in the directory.
<table>
<thead>
<tr>
<th>/data/emr/yarn/local/filecache/<br>
   /data/emr/yarn/local/usercache/<br>
   /data1/emr/yarn/local/filecache/<br>
   /data1/emr/yarn/local/usercache/<br>
   /data2/emr/yarn/local/filecache/<br>
   /data2/emr/yarn/local/usercache/</th>
</tr>
</thead>
</table >
The above lists the information of only three data disks, where the number following `/data` is the data disk index. You need to clear the corresponding files in the `/data` directory of all data disks.
3. Run the following command to fix non-standard directories (directories other than `/usr/local/service`).
 <table>
<thead>
<tr>
<th>EXTRA_DISRUPTOR_DIR=/path/to/other bash fix-log4j2.sh /path/to/other</th>
</tr>
</thead>
</table >
4. Fix in other scenarios.
Upgrade the six JAR packages related to the vulnerability: log4j-api, log4j-core, log4j-jul, log4j-slf4j-impl, log4j-web, and disruptor. If such a package doesn't exist, you don't need to replace it.

## Service Restart and Grayscale Fix
-----
1. Perform a fix on a node in the cluster.
	- Restart the Flink, Spark, Hive, Ranger, Presto, Oozie, Storm, Impala, Knox, and Druid services on the node.
	- Restart all resident tasks, including Flink, Storm, and Spark tasks.
2. After confirming that everything is OK by restarting the services on the node, perform the fix on other nodes.


## Fix Process

-----
1. Place the six fixed JAR packages in the `fix-log4j` directory of the execution directory. 
2. Search for problematic packages in the target directory and replace the found ones with the six fixed JAR packages. The problematic JAR packages in the `tar.gz` and `war` packages, as well as the cache package in the `/user/hadoop/share` path on HDFS will be replaced at the same time.
	- Replace `log4j-api,log4j-core,log4j-jul,log4j-slf4j-impl,log4j-web 2.0–2.17.1` with the 2.17.1 version.
	- Replace the versions earlier than `disruptor-3.4.2.jar` with the 3.4.2 version. Note that the disruptor needs to be replaced only for certain components.

## Rollback Steps for Service Problems
-----
You need to copy the problematic JAR packages back and delete the added latest JAR packages.
1. Decompress the backup file.
<table>
<thead>
<tr>
<th>cd fix-log4j2<br>tar zxvf rm_if_no_need_to_rollback.tar.gz.1639576622
</th>
</tr>
</thead>
</table >
Here, `1639576622` is a temporarily generated timestamp, and you need to find the corresponding file for decompression.
2. Copy the backup file back.
<table>
<thead>
<tr>
<th> cp -r ./root/fix-log4j2/emr_fix_log4j_bak_10812_1639576622/usr/local/service/* /usr/local/service/</th>
</tr>
</thead>
</table >
Here, `10812_1639576622` is the number temporarily generated during execution, and you need to find the corresponding file for copying.
3. Delete the added latest Log4j JAR packages.
<table>
<thead>
<tr>
<th> find /usr/local/service/ -name log4j-api-2.17.1.jar | xargs -n1 -I{} rm -f {}<br>
  find /usr/local/service/ -name log4j-web-2.17.1.jar | xargs -n1 -I{} rm -f {}<br>
      find /usr/local/service/ -name log4j-jul-2.17.1.jar | xargs -n1 -I{} rm -f {}<br>
 find /usr/local/service/ -name log4j-slf4j-impl-2.17.1.jar | xargs -n1 -I{} rm -f {}<br>
   find /usr/local/service/ -name log4j-core-2.17.1.jar | xargs -n1 -I{} rm -f {}</th>
</tr>
</thead>
</table >
4. To roll back in the `/path/to/other` directory, replace `/usr/local/service/` with `/path/to/other`.

