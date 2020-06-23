## 1. What is the Linux server Load Average?

Load is used for measuring the workload of a server, that is, the length of the queue of tasks to be executed by the CPU. The greater the value, the more processes that are currently running or waiting to be executed..

## 2. How can I check Linux server load?

You can run the `w`, `top`, `uptime`, and `procinfo` commands or access the file `/proc/loadavg` to view the load.
Please refer to "Installing Software in Linux Environment" for the instructions on how to install procinfo tool. 

## 3. What should I do when the server load is too high?

The server load/load average is displayed based on the length of the process queue. When the server load is high (we recommend viewing the 15-minute average), it may be caused by insufficient CPU resources, I/O read/write bottleneck, insufficient memory resources, or the intensive computing tasks. We recommend you run the `vmstat`, `iostat`, and `top` commands to locate the reason for the high load, and optimize processes. 

## 4. How do I check server memory usage?

You can check it by running the `free`, `top` (after running, you can press `shift+m` to sort the memory), `vmstat`, and `procinfo` commands or accessing the file `/proc/meminfo`. 

## 5. How do I check the memory usage of a single process?

You can check it by running the `top -p PID`, `pmap -x PID`, and `ps aux|grep PID` commands or accessing the `/proc/$process_id (process PID) /status` file, for example, the `/proc/7159/status` file. 

## 6. How do I check services and ports that are in use?

You can check it by running the `netstat -tunlp`, `netstat -antup`, and `lsof -i:PORT` commands. 

## 7. How do I check server process information?

You can check it by running the `ps auxww|grep PID`, `ps -ef`, `lsof -p PID`, and `top -p PID` commands. 

## 8. How do I stop a process?

You can run `kill -9 PID` (PID indicates the process ID) and `killall program name` (for example, killall cron) to stop the process.
To stop a zombie process, you need to kill the parent process by running `kill -9 ppid` (ppid indicates the parent process ID, which can be queried by running `ps -o ppid PID`, for example, ps -o ppid 32535). 

## 9. How do I locate a zombie process?

You can run `top` to view the total of zombie processes, and run `ps -ef | grep defunct | grep -v grep` to locate a specific zombie process. 

## 10. Why can't I enable the server port?

You need to check the operating system and the application to ensure a port is enabled.
Only the `root` user can enable ports below 1024 on the Linux operating system. Run `sudo su -` to obtain root privileges before doing so.
For application issues such as port conflict or misconfiguration, use application startup logs to troubleshoot. Tencent Cloud system uses port 36000. 

## 11. What are the commands commonly used for checking the performance of a Linux server?
<table class="t">
<tbody><tr>
<th width="100"><b>Command Name</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td>top
</td><td>top is a task manager program that monitors the overall performance of the system.<br>
<p>This command can be used to display information such as system load, process, CPU, memory and paging. Use `shift+m` and `shift+p` to sort processes by memory usage and CPU usage.
</p>
</td></tr>
<tr>
<td>vmstat
</td><td>vmstat is a computer system monitoring tool that collects and displays summary information about CPU, processes, memory paging and IO.<br>
<p>For example, vmstat 3 10 outputs results every 3 seconds and is executed 10 times.
</p>
</td></tr>
<tr>
<td>iostat
</td><td>iostat is a computer system monitor tool that collects and displays statistics of CPU and IO.<br>
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
</td><td>lsof reports a list of all open files, which is useful in Linux system management.<br>
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
</td><td>ps is a process query command that displays information related to the processes.<br>
<p>Commonly used command parameter combinations are `ps -ef` and `ps aux`. Use `ps -A -o` to output custom fields. <br>
For example:<br>
`ps -A -o pid,stat,uname,%cpu,%mem,rss,args,lstart,etime |sort -k6,6 -rn` outputs results according to the listed fields and sorts by the 6th field.
<br>
`ps -A -o comm |sort -k1 |uniq -c|sort -k1 -rn|head` lists the process with the largest number of running instances.
</p>
</td></tr></tbody></table>

Other commonly used commands and files: `free -m`, `du`, `uptime`, `w`, `/proc/stat`, `/proc/cpuinfo`, and `/proc/meminfo`. 

##12. What can I do when Cron does not work?
Use the following steps to troubleshoot:
1. Verify whether crontab is running normally.
 1. Run `crontab -e` to add the following test item.
```
 \*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &
```
 2. Check the `/tmp/crontest` file. 
In case of any problem, run `ps aux|grep cron` to look for pid of cron, run `kill -9 PID` to terminate the cron process, and then run `/etc/init.d/cron start` to restart cron. 
2. Verify whether absolute path is used in the cron script.
3. Check whether you used the right account to execute cron. Also check if the account is included in `/etc/cron.deny`.
4. Check the execution permission of the script, script directory and log file permission.
5. We recommended that you run the script in the background. Append an "&" to the script entry, for example, `\*/1 \* \* \* \* /bin/date >> /tmp/crontest 2>&1 &`.

## 13. How do I setup a startup task for my CVM instance?

Linux kernel startup sequence is as follows:
1. Start the `/sbin/init` process.
2. Run the init initial scripts in sequence.
3. Run the level script `/etc/rc.d/rc\*.d`, where the value of \* means running mode, which can be queried in `/etc/inittab`.
4. Run `/etc/rc.d/rc.local`.

> The configuration of startup task can be made in the `S\*\*rclocal` file in `/etc/rc.d/rc\*.d` or in `/etc/rc.d/rc.local`. 

## 14. Why is the server hard drive read-only?

Common reasons for a read-only hard disk are as follows:
- The disk space is full
You can run `df -m` to check the disk usage, and then delete unnecessary files to free disk space. (Deleting non-third party files is not recommended. Check the files before you delete them). 
- Disk inode resources are all occupied
You can run `df -i` to view and confirm relevant processes. 
- Hardware fault

If none of the above works, please call the hot line 95716 or submit a ticket. 

## 15. How do I view Linux system logs?

- The storage path for system-level log files is `/var/log`.
- The commonly used system log is `/var/log/messages`.

## 16. How do I find large files in the file system?

You can find them by following these steps:
1. Run `df` to query the disk partition usage, for example, `df -m`.
2. Run `du` to query the size of a specific folder, for example, `du -sh ./\*`, `u -h --max-depth=1|head -10`.
3. Run `ls` to list the files and file sizes, for example, `ls -lSh`.
You can also directly check the size of files under a specific directory by using the `find` command, for example, `find / -type f -size +10M -exec ls -lrt {} \`.

## 17. How do I check the version of an operating system?

You can run the following commands to query the system version:
- uname -a
- cat /proc/version
- cat /etc/issue 

## 18. Why are Chinese displayed as garbage characters in a terminal?

The server itself does not impose restrictions on the display language. Therefore, this most likely is a client problem. If you are using secureCRT, try to change settings in **Options** -> **Session Options** -> **Appearance**. If you are using other terminal software, google for a solution.
If this problem appears in a pure Linux shell, run `export` to check user environment variables such as LANG and LC_CTYPE.

## 19. How do I configure a connection timeout using SecureCRT?

You can configure the following settings so that the connection to your CVM instance is stable:
1. Open SecureCRT and select **Options**.
2. Select **Session Options** and click **Terminal**.
3. Select **Send protocol NO-OP** in **Anti-idle** on the right and set the time to “every 120 seconds”. 

## 20. Why isn't disk space on a Linux server freed after a file is deleted?

**Cause:**

You log in to your Linux CVM instance and delete a file using `rm`. Then you check disk space using `df` but the amount of free disk space is the same. This is because when the file is deleted, another process happens to be accessing the file, the space occupied by the deleted file will not be immediately freed at the time you check the disk space.

**Solution:**

1. Run `lsof |grep deleted` with root privilege and find the PID of the process which is using the deleted file.
2. Kill the process with `kill -9 PID`. 


## 21. How do I delete files on a Linux server?
You can run `rm` to delete files, but which are unrecoverable. Use this command with care.
Format of `rm`: `rm (option) (parameter)`.
- Options:
**-d**: directly deletes all hardwired data contained, and then the directory.
**-f**: forcibly deletes a file or directory.
**-i**: asks the user before deleting an existing file or directory.
**-r** or **-R**: deletes all files and sub-directories under a specific directory recursively.
**--preserve-root**: does not recurse on the root directory.
**-v**: displays the detailed execution of the commands.
- Parameter: specifies the file or file list to be deleted. If the parameter contains a directory, add the `-r` or `-R` option.
- Example:
	- Run `rm test.txt` to delete the `test.txt` file.
	- Run `rm -r test` to delete the `test` directory.
	- Run `rm -r *`to delete all files and sub-directories under the current directory.
