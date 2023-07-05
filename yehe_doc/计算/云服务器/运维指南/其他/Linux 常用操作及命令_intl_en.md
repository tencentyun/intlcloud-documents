### What is the Linux server load average?

Load is used to measure the workload of a server; that is, the length of the queue of tasks to be executed by the CPU. The greater the value, the more processes that are currently running or waiting to be executed.

### How can I check the Linux server load?

You can run the `w`, `top`, `uptime`, and `procinfo` commands or access the `/proc/loadavg` file to view the load.
Please refer to "Installing Software in the Linux Environment" for instructions on how to install the procinfo tool. 

### What should I do when the server load is too high?

The server load/load average is displayed based on the length of the process queue. A high server load (we recommend referencing the 15-minute average) may be caused by insufficient CPU resources, I/O read/write bottlenecks, insufficient memory resources, or intensive computing tasks. We recommend you run the `vmstat`, `iostat`, and `top` commands to identify the reason for the high load and optimize the processes. 

### How do I check the server memory usage?

You can check the server memory usage by running the `free`, `top` (after running, you can press `shift+m` to sort the memory), `vmstat`, and `procinfo` commands or by accessing the `/proc/meminfo` file. 

### How do I check the memory usage of a single process?

You can check the memory usage of a single process by running the `top -p PID`, `pmap -x PID`, and `ps aux|grep PID` commands or by accessing the `/proc/$process_id (process PID) /status` file (for example, the `/proc/7159/status` file). 

### How do I check the services and ports that are currently in use?

You can check the services and ports that are currently in use by running the `netstat -tunlp`, `netstat -antup`, and `lsof -i:PORT` commands. 

### How do I check the server process information?

You can check the server process information by running the `ps auxww|grep PID`, `ps -ef`, `lsof -p PID`, and `top -p PID` commands. 

### How do I stop a process?

You can run `kill -9 PID` (PID indicates the process ID) and `killall program name` (for example, killall cron) to stop a process.
To stop a zombie process, you need to kill the parent process by running `kill -9 ppid` (ppid indicates the parent process ID, which can be queried by running `ps -o ppid PID` (for example, ps -o ppid 32535)). 

### How do I locate a zombie process?

You can run `top` to view the total of zombie processes, and run `ps -ef | grep defunct | grep -v grep` to locate a specific zombie process. 

### Why can't I enable the server port?

You need to check the operating system and the application to ensure a port is enabled.
Only the `root` user can enable ports below 1024 on the Linux operating system. Run `sudo su -` to obtain root permissions before enabling the server port.
For application issues such as port conflicts or configuration problems, use the application startup logs to troubleshoot them. The Tencent server system uses port 36000. 

### What are the commands commonly used to check the performance of a Linux server?
<table class="t">
<tbody><tr>
<th width="100"><b>Command Name</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td>top
</td><td>top is a task manager program that monitors the overall performance of the system.<br>
<p>This command can be used to display information such as the system load, the process, the CPU, the memory, and paging. Use `shift+m` and `shift+p` to sort the processes by memory usage and CPU usage.
</p>
</td></tr>
<tr>
<td>vmstat
</td><td>vmstat is a computer system monitoring tool mainly used for virtual memory that collects and displays summary information about CPU, processes, memory paging, and IO.<br>
<p>For example, vmstat 3 10 outputs results every 3 seconds and is executed 10 times.
</p>
</td></tr>
<tr>
<td>iostat
</td><td>iostat is a computer system monitoring tool that collects and displays statistics about CPU and IO.<br>
<p>For example, iostat -dxmt 10 outputs detailed information about IO in MB every 10 seconds.
</p>
</td></tr>
<tr>
<td>df
</td><td>df is a command used to display the amount of available disk space.<br>
<p>For example: df -m displays the disk space usage in MB.
</p>
</td></tr>
<tr>
<td>lsof
</td><td>lsof reports a list of all open files, which is very useful for Linux system management.<br>
<p>For example:<br>
lsof -i: 36000 displays the processes using port 36000.
<br>
lsof -u root displays the programs run by root.
<br>
lsof -c php-fpm displays the files opened by the php-fpm process.
<br>
lsof php.ini displays the processes for which php.ini is opened.
</p>
</td></tr>
<tr>
<td>ps
</td><td>ps is a process query command that displays information related to the processes.<br>
<p>Commonly used command parameter combinations are `ps -ef` and `ps aux`. Use `ps -A -o` to output custom fields. <br>
For example:<br>
`ps -A -o pid,stat,uname,%cpu,%mem,rss,args,lstart,etime |sort -k6,6 -rn` outputs results according to the listed fields and sorts them using the 6th field.
<br>
`ps -A -o comm |sort -k1 |uniq -c|sort -k1 -rn|head` lists the process with the largest number of running instances.
</p>
</td></tr></tbody></table>

Other commonly used commands and files: `free -m`, `du`, `uptime`, `w`, `/proc/stat`, `/proc/cpuinfo`, and `/proc/meminfo`. 

### What do I do when Cron doesn’t work?
Follow the steps below to troubleshoot this problem:
1. Verify whether crontab is running normally.
 1. Run `crontab -e` to add the following test item.
```
 \*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &
```
 2. Check the `/tmp/crontest` file. 
If there are any problems, run `ps aux|grep cron` to look for the pid of cron, run `kill -9 PID` to terminate the cron process, and then run `/etc/init.d/cron start` to restart cron. 
2. Verify whether the script path in the cron entry is an absolute path.
3. Check whether you used the right account to execute cron. Also, check whether the account is included in `/etc/cron.deny`.
4. Check the execution permission of the script, the script directory, and the log file permission.
5. We recommend that you run the script in the background by adding an "&" at the end of the script entry. For example, `\*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &`.

### How do I set up a startup task for my CVM instance?

The Linux kernel startup sequence is as follows:
1. Start the `/sbin/init` process.
2. Run the init initial scripts in sequence.
3. Run the level script `/etc/rc.d/rc\*.d`, where the value of \* means the running mode, which can be queried in `/etc/inittab`.
4. Run `/etc/rc.d/rc.local`.

>? The startup task can be configured in `/etc/rc.d/rc.local` or in the `S\*\*rclocal` file in `/etc/rc.d/rc\*.d`. 

### Why is the server disk read-only?

Common reasons for a read-only server disk are as follows:
- The disk space is full
You can run `df -m` to check the disk usage and then delete unnecessary files to free disk space. (We do not recommend you delete non-third party files. Please check the files before you delete them). 
- Disk inode resources are all occupied
You can run `df -i` to view and confirm relevant processes. 
- There is a hardware failure

If none of the above works, please [submit a ticket](https://console.tencentcloud.com/workorder/category). 

### How do I view Linux system logs?

- The storage path for system-level log files is `/var/log`.
- The commonly used system log is `/var/log/messages`.

### How do I find large files in the file system?

You can find them by following the steps below:
1. Run `df` to query the disk partition usage (for example, `df -m`).
2. Run `du` to query the size of a specific folder (for example, `du -sh ./\*`, `du -h --max-depth=1|head -10`).
3. Run `ls` to list the files and file sizes (for example, `ls -lSh`).
You can also directly check the size of files under a specific directory by using the `find` command (for example, `find / -type f -size +10M -exec ls -lrt {} \`).

### How do I check the version of a server’s operating system?

You can run the following commands to check the version of a server’s operating system:
- uname -a
- cat /proc/version
- cat /etc/issue 

### Why are Chinese characters displayed as unintelligible code in the Linux terminal?

The server itself does not impose restrictions on the display language. Therefore, this is most likely a client problem. If you are using secureCRT, try to change the settings in **Options** -> **Session Options** -> **Appearance**. If you are using other terminal software, please search on Google for solutions.
If this problem appears in a pure Linux shell, run `export` to check the user environment variables such as LANG and LC_CTYPE.

### How do I configure a connection timeout using SecureCRT?

You can configure the following settings so that the connection to your CVM instance remains stable when connecting to CVM via SecureCRT:
1. Open SecureCRT and select **Options**.
2. Select **Session Options** and click **Terminal**.
3. Select **Send protocol NO-OP** in the **Anti-idle** box on the right and set the time to “every 120 seconds”. 

### Why isn't disk space on a Linux server freed after a file is deleted?

**Cause:**

After logging in to your Linux CVM instance and deleting a file using `rm`, you may find that the available disk space does not increase when you use `df` to check the disk space. This is because when the file is deleted, if another process happens to be accessing the file, the space occupied by the deleted file will not be immediately freed at the time you check the disk space.

**Solution:**

1. Run `lsof |grep deleted` using the root permission and find the PID of the process that is using the deleted file.
2. Kill the process using `kill -9 PID`. 


### How do I delete files on a Linux server?
You can run `rm` to delete files. Files deleted with this command cannot be recovered. Therefore, please use this command with caution.
Format of `rm`: `rm (option) (parameter)`.
- Options:
**-d**: directly deletes all hardwired data contained in the directory to be deleted, and then deletes the directory itself.
**-f**: forcibly deletes a file or a directory.
**-i**: asks the user before deleting an existing file or directory.
**-r** or **-R**: deletes all files and sub-directories under a specific directory together using recursive processing.
**--preserve-root**: does not implement recursive operations on the root directory.
**-v**: displays the detailed execution processes of the commands.
- Parameter: specifies the file or file list to be deleted. If the parameter contains a directory, add the `-r` or `-R` option.
- Example:
	- Run `rm test.txt` to delete the `test.txt` file.
	- Run `rm -r test` to delete the `test` directory.
	- Run `rm -r *` to delete all files and sub-directories under the current directory.
