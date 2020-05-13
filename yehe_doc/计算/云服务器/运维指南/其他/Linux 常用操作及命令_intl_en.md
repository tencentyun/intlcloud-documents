## 1. What is the server Load Average?

Load is used for measuring the workload of a server, that is, the length of the queue of tasks to be executed by the CPU. The greater the value, the more processes that are currently running or waiting to be executed.

## 2. How can I check my server load?

You can run `w`, `top`, `uptime`, and `procinfo` or use the file `/proc/loadavg` to check your server load.
Refer to documentation on how to install software on Linux for the instructions on how to install procinfo. 

## 3. What should I do when the server load is too high?

Server load/load average is based on the length of the process queue. When the server load is high (we recommend that you use a 15-minute average as the reference), it may be caused by reasons such as insufficient CPU resources, I/O read/write bottleneck, insufficient memory resources, or the intensive computing tasks. Use `vmstat`, `iostat`, and `top` to identify the reason for the high load and optimize the corresponding processes. 

## 4. How do I check server memory usage?

You can check your memory usage using `free`, `top` (after running, you can press `shift+m` to sort the memory), `vmstat`, and `procinfo` or the file `/proc/meminfo`. 

## 5. How do I check the memory occupied by a single process?

You can check this using `top -p PID`, `pmap -x PID`, and `ps aux|grep PID` or the `/proc/$process_id (process PID) /status` file, such as, /proc/7159/status. 

## 6. How do I check which services and ports are in use?

You can check using `netstat -tunlp`, `netstat -antup`, and `lsof -i:PORT`. 

## 7. How do I check server process information?

You can check using `ps auxww|grep PID`, `ps -ef`, `lsof -p PID`, and `top -p PID`. 

## 8. How do I stop a process?

You can run `kill -9 PID` (PID is the process ID) and `killall program name` (for example, killall cron) to stop the process.
To stop a zombie process, you need to kill the parent process by running `kill -9 ppid` (ppid is the parent process ID, which can be queried by running `ps -o ppid PID`, for example, ps -o ppid 32535). 

## 9. How do I find a zombie process?

You can run `top` to view the total number of zombie processes, and run `ps -ef | grep defunct | grep -v grep` to find the information of a specific zombie process. 

## 10. Why can't I enable a server port?

You need use the operating system or the application to cehck if a port is enabled.
For ports below 1024, you need to be `root` to use it. Use `sudo su -` to obtain root privileges before doing so.
For application issues such as port conflict or misconfiguration, use application startup logs to troubleshoot. Tencent Cloud system uses port 36000. 

## 11. What are the commands commonly used for checking the performance of a Linux server?
<table class="t">
<tbody><tr>
<th width="100"><b>Command name</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td>top
</td><td>top is a task manager program that displays information about CPU and memory utilization.<br>
<p>This command can be used to display information such as system load, process, CPU, memory and paging. Use `shift+m` and `shift+p` to sort processes by memory usage and CPU usage.
</p>
</td></tr>
<tr>
<td>vmstat
</td><td>vmstat is a computer system monitoring tool that collects and displays summary information about operating system memory, processes, interrupts, paging and block I/O.<br>
<p>For example, vmstat 3 10 outputs results every 3 seconds and is executed 10 times.
</p>
</td></tr>
<tr>
<td>iostat
</td><td>iostat is a computer system monitor tool used to collect and show operating system storage input and output statistics.<br>
<p>For example, iostat -dxmt 10 outputs detailed information about IO in MB every 10 seconds.
</p>
</td></tr>
<tr>
<td>df
</td><td>df is a standard Unix command used to display the amount of available disk space for file systems on which the invoking user has appropriate read access.<br>
<p>For example: df -m displays the disk space usage in MB.
</p>
</td></tr>
<tr>
<td>lsof
</td><td>lsof is short for list open files, which is used to report a list of all open files and the processes that opened them.<br>
<p>For example:<br>
lsof -i: 36000 displays the processes using Port 36000.
<br>
lsof -u root displays the programs run by root.
<br>
lsof -c php-fpm displays the files opened by php-fpm process.
<br>
lsof php.ini displays the processes for which php.ini is opened.
</p>
</td></tr>
<tr>
<td>ps
</td><td>ps, short for Process Status, is a command line utility that is used to display or view information related to the processes running in a Linux system.<br>
<p>Commonly used command parameter combinations are ps -ef and ps aux. Use ps -A -o to output custom fields.<br>
For example:<br>
`ps -A -o pid,stat,uname,%cpu,%mem,rss,args,lstart,etime |sort -k6,6 -rn` outputs results according to the listed fields and sorts by the 6th field.
<br>
`ps -A -o comm | sort -k1 | uniq -c | sort -k1 -rn | head` lists the process with the largest number of running instances.
</p>
</td></tr></tbody></table>

Other commonly used commands and files: `free -m`, `du`, `uptime`, `w`, `/proc/stat`, `/proc/cpuinfo`, and `/proc/meminfo`. 

##12. What do I do when Cron does not work?
Use the following steps to troubleshoot:
1. Verify whether crontab is running normally.
 1. Run `crontab -e` to add the following test item.
```
 \*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &
```
 2. Observe the `/tmp/crontest` file. 
In case of any problems, run `ps aux|grep cron` to look for the pid of cron and use `kill -9 PID` to terminate the cron process. Then restart cron with `/etc/init.d/cron start`. 
2. Verify whether absolute path is used in the cron script.
3. Check whether you used the right account to execute cron. Also check if the account is included in /etc/cron.deny.
4. Check the execution permission of the script, script directory and log file permission.
5. We recommended that you run the script in the background. Append an "&" to the script entry, for example, `\*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &`.

## 13. How do I setup a startup task for my CVM instance?

Linux kernel startup sequence is as follows:
1. Start the `/sbin/init` process.
2. Run the init initial scripts in sequence.
3. Run the level script `/etc/rc.d/rc\*.d`, where the value of \*means running mode, which can be queried in `/etc/inittab`.
4. Run `/etc/rc.d/rc.local`.

> The configuration of startup task can be made in the `S\*\*rclocal` file in `/etc/rc.d/rc\*.d` or in `/etc/rc.d/rc.local`. 

## 14. Why is the server hard drive read-only?

Common reasons for a read-only hard disk are as follows:
- The disk space is full
You can use the `df-m` command to check the disk usage, and then delete unnecessary files to free disk space. (Deleting non-third party files is not recommended. Check the files before you delete them). 
- Disk inode resources are all occupied
You can run `df -i` to view and confirm relevant processes. 
-  Hardware fault

If you still cannot identify the reason using the above methods, please call the hot line 95716 or submit a ticket. 

## 15. How do I view system logs?

- The storage path for system-level log files is `/var/log`.
- The commonly used system log is `/var/log/messages`.

## 16. How do I find large files in the file system?

You can find them by following these steps:
1. Run `df` to query the disk partition usage, for example, df -m.
2. Run `du` to query the size of a specific folder, for example, du -sh ./\*, du -h --max-depth=1|head -10.
3. Run `ls` to list the files and file sizes, for example, ls -lSh.
You can also directly check the size of files under a specific directory by using the `find` commands, for example, find / -type f -size +10M -exec ls -lrt {} \;

## 17. How do I check the version of an operating system?

You can run the following commands to query the system version:
- uname -a
- cat /proc/version
- cat /etc/issue 

## 18. Why are Chinese displayed as garbage characters in a terminal?

The server itself does not impose restrictions on the display language. Therefore, this most likely is a client problem. If you are using secureCRT, try to change settings in **Options** -> **Session Options** -> **Appearance**. If you are using other terminal software, google for a solution.
If this problem appears in a pure Linux shell, use the export command to check user environment variables such as LANG and LC_CTYPE.

## 19. How do I configure connection timeout using SecureCRT?

You can configure the following settings so that the connection to your CVM instance is stable:
1. Open SecureCRT and select **Options**.
2. Select **Session Options** and click **Terminal**.
3. Select **Send protocol NO-OP** in **Anti-idle** and set the time to **every 120 seconds**. 

## 20. Why isn't disk space freed after a file is deleted?

**Cause**:

You log in to your CVM instance and delete a file using `rm`. Then you check disk space using `df` but the amount of free disk space is the same. What happened? This is because when the file is deleted, another process happens to be accessing the file, the space occupied by the deleted file will not be immediately freed at the time you check the disk space.

**Solution**:

1. Run `lsof |grep deleted` with root privilege and find the PID of the process which is using the deleted file.
2. Kill the process with `kill -9 PID`. 
