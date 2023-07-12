### Why cannot a single file be uploaded to multiple topics?

LogListener adopts the policy that a single file can be uploaded to only one topic.
For example, if you have two files `topicA` and `topicB` and you configure the two files as follows:
- Set the collection path for `topicA` to `/data/log/\*\*/\*.log`.
- Set the collection path for `topicB` to `/data/log/test/\*\*/\*.log`, `/data/log/\*\*/test\*.log`, `/data/log/\*\*/\*.log`, or other collection paths similar to that of `topicA`.

In this scenario, though a file matches two collection paths, the file will be uploaded to only one of the topics. Therefore, it is recommended that different log topics be used to collect logs of different business types and that you configure collection paths as accurately as possible. If you need to upload a file to different topics, use soft links. You can create different soft links for the same file so that it can be collected to different topics via different soft links.


### How do I configure collection paths?

Currently, the required collection path format is: Path prefix + "/\*\*/" + Wildcard filename, for example, `/data/log + /\*\*/ + \*.log ==> /data/log/\*\*/\*.log`.

When setting a wildcard collection path, you need to set the collection path (prefix) as accurately as possible so that LogListener can provide service more efficiently. If the prefix of the collection path is incorrectly set, a large number of paths may be matched by the collection path. As a result, LogListener enters the abnormal status and cannot work.

For example, if the collection path is set to `//\*\*/\*.log`, where the prefix is "/", LogListener will scan the entire root directory and cannot work.


### What is the recommended log rotation scheme?

For log rotation, it is recommended that the file name after rotation not be matched by the wildcard collection path.

For example, assume that the collection path is `/var/log/xxxx/\*\*/\*.log` and the log file to be collected is `test.log`. When `test.log` is rotated to `test.2021-07-13.4.log`, LogListener can identify that `test.2021-07-13.4.log` is the rotated file of `test.log` and still label it as `test.log`. Therefore, the checkpoint files stored by LogListener do not include the collection record of the `test.2021-07-13.4.log` file.

However, when LogListener is restarted, LogListener will scan files according to `/var/log/xxxx/\*\*/\*.log` and detect that the `test.2021-07-13.4.log` file matches the matching rule but has no collection record. Then LogListener considers the file a new file and collects it.

Therefore, it is recommended not to match rotated files when matching the wildcard collection path to avoid the case where LogListener collects the rotated files after LogListener restarts.

The recommended log rotation scheme is as follows: if you need to collect `test.log`, you are advised to name the file after rotation to `test.log.2021-07-13.xxx` so that it will not be matched by `\*.log`.

### What should be noted about the LogListener upgrade?

During the iteration of LogListener, the API parameters of the collection path are modified. The collection paths set in versions earlier than v2.2.8 are not supported in the latest version.
Therefore, if you are to upgrade a version earlier than v2.2.8, you need to configure the collection paths again as wildcard paths in the console after LogListener is upgraded.


### How do I configure the regular expression collection mode during LogListener collection configuration?

When configuring collection in the console, if you select a collection mode related to regular expressions, although the console provides a tool for extracting regular expression key-value indexes, the tool does not provide automatic generation of regular expressions for Chinese content. If you need to extract regular expressions from Chinese text, you can write your own regular expressions and verify them in the console or using other third-party tools.


### What can I do if no log is uploaded when I access CLS through the LogListener for the first time?

The LogListener configuration may be incorrect. The common cases are as follows:
- The configured server domain name does not match. As a result, LogListener cannot obtain the collection configuration of the current region, and no collection service is running.
- LogListener is added to the IP machine group, but LogListener is configured with label information. As a result, the collection configuration cannot be pulled from the current region, and no collection service is running.
- The secret ID or key configured in LogListener is incorrect, or the permission is insufficient. As a result, logs cannot be uploaded.
- Environment problem (for example, the public network access is not enabled in the VPC subnet). If cross-region upload is configured, the configuration does not take effect. In fact, LogListener still communicates with the local server.
- Generally, in this case, you can log in to LogListener, go to the LogListener installation directory, and run the `./bin/check` command to check the following information:
 - Whether the domain name is correct.
 - Whether heartbeats are reported properly.
 - Whether collection configuration is pulled properly.


### Log collection failed due to mixed usage of machine groups. What should I do?

At present, machine groups are divided into two categories, and their usage methods are independent of each other:
- IP machine group: a machine IP must be manually added to the machine group in the console, and the `group_label` field in `loglistener.conf` on the corresponding machine must be empty.
- Label machine group: the machine group label is set in the console, and the `group_label` field in `loglistener.conf` on the corresponding machine must be set to the same label.

The above two usage methods are incompatible. If they are used together, LogListener will not be able to pull the correct collection configuration, resulting in no collection.


### In what situations will LogListener collect logs?

When a group of files queue for LogListener collection, the first file in the queue is collected first, and only when the end of the first file is read at a certain time, the position of the first file is given up. That is, not all files can enjoy the collection resources equally in a unit of time.

If the writing speed of a single file is always greater than the collection speed, and the latest position of the file cannot be consumed due to the slow collection speed, the file occupies collection resources for a long time, and as a result other files cannot be collected.


### What should I do in the case of topic collection blocking?

In a certain period of time, if the generation speed of a single file is greater than the collection speed, LogListener will continue to collect this file, and the collection of other files will be blocked.

### What are the rules for filters?

The filter rule is collection after matching, not discarding after matching. LogListener does not collect logs that do not match.


### How do I use non-root permission to start LogListener?

You are advised to use the root permission to start LogListener. If you need to use LogListener with non-root permission, see "Configuring Non-Root Permission to start LogListener".


### How do I pin the LogListener process to a CPU?

For the CPU pinning, use the taskset tool and run the `taskset -cp ${cpu number} ${pid>}` command.

### How do I control the high memory and resource usage of LogListener?

- We recommend that you upgrade LogListener to the latest version and set `memory_tight_mode = true`.
- Use CGroup to control CPU and MEM usage.

### Does LogListener support log collection via a soft link?

Yes. But LogListener earlier than version 2.3.0 does not collect those log files in soft links, or in shared file directories of NFS, CIFS, etc.

### Can LogListener upload data to multiple log topics?

- Yes, provided that these log topics are in the same region.
- A log file will only be collected into one log topic.

### Are machines automatically added to a machine group when LogListener is initialized?

Yes, provided that you configure the machine group by machine ID. For more information, please see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

### In what situations will LogListener upload logs?

 - More than 4 MB logs are cached.
 - More than 10,000 logs are cached.
 - LogListener finishes reading a file.

### What does the maximum performance of LogListener mean?

 - Collecting logs with full text in a single line: 115 MB/sec.
 - Collecting logs with full text in multi lines: 40 MB/sec.
 - Collecting JSON logs: 25 MB/sec.
 - Collecting CSV logs: 50 MB/sec.
 - Collecting full RegEx logs: 18 Mb/sec, depending on the regex complexity.


### How do I modify the LogListener configuration after the server IP address is changed?

- If you configure the machine group by machine ID, you don’t need to modify the LogListener configuration. This method is recommended when the server IP frequently changes. For more information, see [Configuring the machine group by machine ID](https://intl.cloud.tencent.com/document/product/614/17412#.E9.80.9A.E8.BF.87.E9.85.8D.E7.BD.AE.E6.9C.BA.E5.99.A8.E6.A0.87.E8.AF.86.E5.88.9B.E5.BB.BA.E6.9C.BA.E5.99.A8.E7.BB.84).
- If you configure the machine group by IP address, modify the configuration as follows:
  a. Add the new IP address to the `group_ip` field in the configuration file.
```shell
sed -i '' "s/group_ip *=.*/group_ip = ${group_ip}/" etc/loglistener.conf
```
 b. Restart LogListener.
```shell
 /etc/init.d/loglistenerd restart
```
 c. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview?region=ap-guangzhou) and select **Machine Group Management** on the left sidebar. Locate the machine group to which the server binds and click **Edit**. In the pop-up window, replace the old IP address with the new one, and click **OK**.
