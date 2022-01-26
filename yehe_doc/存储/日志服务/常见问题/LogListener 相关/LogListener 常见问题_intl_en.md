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

### Are servers automatically added to a server group when LogListener is initialized?

Yes, provided that you [Server Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

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

- If you configure the machine group by machine ID, you don’t need to modify the LogListener configuration. This method is recommended when the server IP frequently changes. For more information, see [Configuring the machine group by machine ID](https://intl.cloud.tencent.com/document/product/614/17412#configuring-the-server-group-by-server-id).
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
