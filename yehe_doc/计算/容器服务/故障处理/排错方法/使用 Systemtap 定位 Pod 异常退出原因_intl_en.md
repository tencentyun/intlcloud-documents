This article describes how to use SystemTap to troubleshoot pod issues.

## Preparations
Different operating systems have different methods for installing SystemTap and its dependencies. Pick one that suits you.

### Ubuntu
1. Run the following command to install SystemTap:
```bash
apt install -y systemtap
```
2. Run the following command to check for dependencies:
```
stap-prep
```
The following is a sample result:
```bash
Please install linux-headers-4.4.0-104-generic
You need package linux-image-4.4.0-104-generic-dbgsym but it does not seem to be available
 Ubuntu -dbgsym packages are typically in a separate repository
 Follow https://wiki.ubuntu.com/DebuggingProgramCrash to add this repository
apt install -y linux-headers-4.4.0-104-generic
```
3. The above result shows that you need to install dbgsym, which is not in the existing sources. Run the following command to add the third-party source:
```bash
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C8CAB6595FDFF622
    
    codename=$(lsb_release -c | awk  '{print $2}')
    sudo tee /etc/apt/sources.list.d/ddebs.list << EOF
    deb http://ddebs.ubuntu.com/ ${codename}      main restricted universe multiverse
    deb http://ddebs.ubuntu.com/ ${codename}-security main restricted universe multiverse
    deb http://ddebs.ubuntu.com/ ${codename}-updates  main restricted universe multiverse
    deb http://ddebs.ubuntu.com/ ${codename}-proposed main restricted universe multiverse
    EOF
    
    sudo apt-get update
```
4. Run the following command after adding the source:
```
stap-prep
```
The following is a sample result:
```bash
Please install linux-headers-4.4.0-104-generic
Please install linux-image-4.4.0-104-generic-dbgsym
```
5. Run the following command to install the prompted packages:
```bash
apt install -y linux-image-4.4.0-104-generic-dbgsym
```
```bash
apt install -y linux-headers-4.4.0-104-generic
```

### CentOS
1. Run the following command to install SystemTap:
```bash
yum install -y systemtap
```
2. For the purpose of this article, we assume that `debuginfo` is not added. Add the following to `/etc/yum.repos.d/CentOS-Debug.repo` and save.
```bash
[debuginfo]
name=CentOS-$releasever - DebugInfo
baseurl=http://debuginfo.centos.org/$releasever/$basearch/
gpgcheck=0
enabled=1
protect=1
priority=1
```
3. Run the following command to check for dependencies and install them:
> The following command installs `kernel-debuginfo`.
>
```
stap-prep
```
4. Run the following command to check if the node has multiple versions of `kernel-devel` installed:
```
rpm -qa | grep kernel-devel
```
The returned result is as follows:
```
kernel-devel-3.10.0-327.el7.x86_64
kernel-devel-3.10.0-514.26.2.el7.x86_64
kernel-devel-3.10.0-862.9.1.el7.x86_64
```
If there are multiple versions, keep the one that corresponds to the kernel version. For example, if the current kernel version is `3.10.0-862.9.1.el7.x86_64`, delete all version except `kernel-devel-3.10.0-862.9.1.el7.x86_64`.
>
>- You can use `uname -r` to view the kernel version. 
>- Make sure `kernel-debuginfo` and `kernel-devel` are both installed and their versions correspond to the kernel version.
>
```
rpm -e kernel-devel-3.10.0-327.el7.x86_64 kernel-devel-3.10.0-514.26.2.el7.x86_64
```


## Problem Analysis
You can use SystemTap to monitor a process in order to troubleshoot pod issues. This is how it works:
1. SystemTap translates the script into C code and calls gcc to compile the code into the Linux kernel module. It then uses `modprobe` to load the module into the kernel.
2. It uses the script to create kernel hooks and identify the causes of pod issues using the signals captured by the hooks.

### Troubleshooting

### Step 1: obtain the pids of the containers that restarted automatically in the pod due to exceptions
1. Run the following command to obtain the Container ID:
```
kubectl describe pod <pod name>
```
The returned result is as follows:
```bash
......
Container ID:  docker://5fb8adf9ee62afc6d3f6f3d9590041818750b392dff015d7091eaaf99cf1c945
......
Last State:     Terminated
	Reason:       Error
	Exit Code:    137
	Started:      Thu, 05 Sep 2019 19:22:30 +0800
	Finished:     Thu, 05 Sep 2019 19:33:44 +0800
```
2. <span id="getPid"></span>Run the following command to query the pid of the main container process using the obtained Container ID:
```bash
docker inspect -f "{{.State.Pid}}" 5fb8adf9ee62afc6d3f6f3d9590041818750b392dff015d7091eaaf99cf1c945
```
The returned result is as follows:
```
7942
```

### Step 2: narrow the scope using the container exit code
Use the `Exit Code` in the result of Step 1 to obtain the status code of the last container exit. For the purpose of this article, we will use 137 as an example. The analysis is as follows:
- If the process was killed by an external signal, the exit code should be between 129 and 255.
- An exit code of 137 indicates that the process was killed by `SIGKILL`. However, we still cannot determine the reason why the process exited.

### Step 3: use the SystemTap script to identify the reason
Assuming the issue is reproducible, you can use a SystemTap to troubleshoot the problem.
1. Create a file called `sg.stp`. Add the following content and save.
```bash
global target_pid = 7942
probe signal.send{
	if (sig_pid == target_pid) {
		printf("%s(%d) send %s to %s(%d)\n", execname(), pid(), sig_name, pid_name, sig_pid);
		printf("parent of sender: %s(%d)\n", pexecname(), ppid())
		printf("task_ancestry:%s\n", task_ancestry(pid2task(pid()), 1));
	}
}
```
> Substitute `pid` with the value of the main container process pid obtained in [Step 2](#getPid). For the purpose of this article, we will use 7942 as an example:
>
2. Run the following command to execute the script:
```bash
stap sg.stp
```
When the container process is killed, the script captures the event and outputs the following:
```yaml
pkill(23549) send SIGKILL to server(7942)
parent of sender: bash(23495)
task_ancestry:swapper/0(0m0.000000000s)=>systemd(0m0.080000000s)=>vGhyM0(19491m2.579563677s)=>sh(33473m38.074571885s)=>bash(33473m38.077072025s)=>bash(33473m38.081028267s)=>bash(33475m4.817798337s)=>pkill(33475m5.202486630s)
```
 
## Solution
By observing `task_ancestry`, you can see the parent processes of the stopped process. In the example above, you can see a strange process called `vGhyM0`. This usually indicates that there is a trojan in the system. Take the necessary steps to clean it so your containers can function properly.

