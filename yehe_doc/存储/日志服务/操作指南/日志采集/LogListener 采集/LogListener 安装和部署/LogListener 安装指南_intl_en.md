LogListener is a log collector provided by CLS. You can install and deploy it on a server to collect logs quickly.

## Installation Environment

LogListener supports only Linux 64-bit operating systems and does not support Windows now. It is compatible with mainstream Linux operating system versions. If LogListener is incompatible with the Linux operating system version you use, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

| OS &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Compatible Versions                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| CentOS (64-bit)                                               | CentOS_6.8_64-bit, CentOS_6.9_64-bit, CentOS_7.2_64-bit, CentOS_7.3_64-bit, CentOS_7.4_64-bit, CentOS_7.5_64-bit, CentOS_7.6_64-bit, CentOS_8.0_64-bit |
| Ubuntu (64-bit) | Ubuntu Server_14.04.1_LTS_64-bit, Ubuntu Server_16.04.1_LTS_64-bit, Ubuntu Server_18.04.1_LTS_64-bit |
| Debian (64-bit) | Debian_8.2_64-bit, Debian_9.0_64-bit |
| openSUSE (64-bit) | openSUSE_42.3_64-bit |
| TencentOS Server                                             | TencentOS Server 3.1, TencentOS Server 2.4                   |

## Supported Features

Key features supported by different LogListener versions are as listed below. For more information, see [LogListener Updates](https://intl.cloud.tencent.com/document/product/614/40005).

| LogListener Version | Supported Feature  | Feature Description | Documentation |
| ---------------- | ------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| v2.8.0           | GBK encoding for collection; optimization of the escape character in JSON extraction mode    | LogListener can collect GBK-encoded log text.                    | -                                                            |
| v2.7.4   | Host name collection (`hostname`)    | LogListener collects and reports the machine host name as a default field and displays \_\_HOSTNAME\_\_ as a key, such as \_\_HOSTNAME\_\_:VM-108-centos.   | -   |
| v2.6.4   | Combined parsing to customize complex log parsing rules   | You can use LogListener's combined parsing mode to parse logs. This mode allows you to enter JSON code in the console to customize the log parsing pipeline logic.   | [Combined Parsing Format](https://intl.cloud.tencent.com/document/product/614/42742)   |
| v2.6.0   | CVM batch deployment   | You can select CVM instances in the console and batch distribute LogListener deployment tasks through an API to automatically complete LogListener installation and deployment (including `accesskey`, ID, and region configuration).   | [Deploying LogListener on CVMs in Batches](https://www.tencentcloud.com/document/product/614/42133)   |
| v2.5.4 | LogListener service logs | LogListener service logs are used to record the operation, collection, and monitoring activities of LogListener, and you can configure visual graphs to display such log data. | [LogListener Service Logs](https://intl.cloud.tencent.com/document/product/614/40232) |
| v2.5.2 | Uploading parsing-failed logs | Parsing-failed logs can be uploaded, using `LogParseFailure` as the key name (`Key`) and the raw log content as the key value (`Value`). |  -                                                            |
| v2.5.0 | LogListener auto-upgrade |  Users can set a time period for Agent auto-upgrade or select specific machine groups to upgrade manually. | [LogListener Upgrade Guide](https://intl.cloud.tencent.com/document/product/614/40233) |
| v2.4.5 | Multi-line log extraction with regex | The extraction mode of **Multi-line - Full regular expression** is added to LogListener collection configuration rules for log collection. | [Full Regular Expression (Multi-Line)](https://intl.cloud.tencent.com/document/product/614/39590) |



## Installation and startup


### 1. Downloading and installing LogListener


Download links of the latest version LogListener: [Download via public network](https://mirrors.tencent.com/install/cls/loglistener-linux-x64.tar.gz), [Download via private network](http://mirrors.tencentyun.com/install/cls/loglistener-linux-x64.tar.gz)
Download the LogListener installation package and decompress it to the installation path (`/usr/local/` in this example). Then, go to the LogListener directory `/usr/local/loglistener/tools` and run the installation command.
>?No version number extensions are added to the installation package of LogListener on v2.8.3 and later. The latest version will be installed with `loglistener-linux-x64` by default. To install a specific version, specify the version number, for example, replace `loglistener-linux-x64` with `loglistener-linux-x64-2.8.0` to install the 2.8.0 version.

- Operation command for the public network:
```plaintext
wget http://mirrors.tencent.com/install/cls/loglistener-linux-x64.tar.gz && tar zxvf loglistener-linux-x64.tar.gz  -C /usr/local/ && cd /usr/local/loglistener/tools && ./loglistener.sh install
```
- Operation command for the private network:
```plaintext
wget http://mirrors.tencentyun.com/install/cls/loglistener-linux-x64.tar.gz && tar zxvf loglistener-linux-x64.tar.gz  -C /usr/local/ && cd /usr/local/loglistener/tools && ./loglistener.sh install
```

### 2. Initializing LogListener

In the case of the `/usr/local/` installation path, go to the `/usr/local/loglistener/tools` path and run the following command to initialize LogListener as the root user (by default, the private network is used to access the service):
```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-xxxxxx
```
>?You need to replace **-secretid**, **-secretkey**, **-region**, and **-network** in the command with the actual values. For more information, please see [Parameter description](#parameterdescription) below.
<span id="parameterdescription"></span>

#### Parameter description

| Parameter    | Description                                                     |
| --------- | ------------------------------------------------------------ |
| secretid  | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi). Used to identify who calls the API. |
| secretkey | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi). Used to encrypt signature strings and verify server-side signature strings. |
| region    | [Region](https://intl.cloud.tencent.com/document/product/614/18940) where CLS resides. Enter a region abbreviation here, such as `ap-beijing` or `ap-guangzhou`. |
| network   | Type of the network through which LogListener accesses the service by domain name. Valid values: `intra` (private network), `internet` (public network). Default value: `intra` |
| IP        | Machine IP. If this parameter is left empty, LogListener will automatically get the local IP address. |
| label     | Machine group label, which is required if you want to identify the machine group. Multiple labels should be separated by comma. |

A private network domain name is used by default:

![](https://main.qcloudimg.com/raw/ea417c6d60ab21e52984d04c1364b30d.png)

If you need to access the service by domain name through the public network, run the following command to set the network parameter `internet` explicitly:
```plaintext
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf0xxxxxxxxxxxx -region ap-xxxxxx -network internet
```

![](https://main.qcloudimg.com/raw/653ebe0400dca5b21b3e25d01f93cb5b.png)
> ?
>- We recommend that you use a collaborator key if the collaborator has been assigned the CLS read/write permission by the root account.
> - `region` indicates the region of the CLS you use, instead of the region where your business machine resides.
> - If your CVM instance and logset are in the same region, we recommend you access the service domain name over the private network; otherwise, use the public network.
> - For more information on log collection permissions, see [Access Policy Templates](https://intl.cloud.tencent.com/document/product/614/45004).
>

### 3. Starting LogListener
- LogListener is on v2.8.3 or later and the operating system has systemd.
```plaintext
systemctl start loglistenerd
```
- LogListener is earlier than v2.8.3, or LogListener is on v2.8.3 or later but the operating system does not have systemd.
```plaintext
/etc/init.d/loglistenerd start
```
![](https://main.qcloudimg.com/raw/184d6cc3308206b14288372da59a99a0.png)

## Common LogListener Operations

>? The operation commands used in this document are applicable only to LogListener v2.2.4 and later versions. For operation commands applicable to earlier versions, see [Earlier-Version LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/35674).
>

### 1. Checking the LogListener version

```plaintext
/etc/init.d/loglistenerd -v
```
### 2. Viewing LogListener help documentation
```plaintext
/etc/init.d/loglistenerd -h
```
### 3. Managing LogListener process
- LogListener is on v2.8.3 or later and the operating system has systemd.
```plaintext
systemctl (start|restart|stop)  loglistenerd # Start, restart, stop
```
- LogListener is earlier than v2.8.3, or LogListener is on v2.8.3 or later but the operating system does not have systemd.
```plaintext
/etc/init.d/loglistenerd (start|restart|stop) # Start, restart, stop
```

### 4. Checking LogListener process status
```plaintext
/etc/init.d/loglistenerd status
```
LogListener normally runs two processes:
![](https://qcloudimg.tencent-cloud.cn/raw/52e273d05e6afc4946849429daf95c8d.png)

### 5. Checking LogListener heartbeat and configuration

```plaintext
/etc/init.d/loglistenerd check
```
![](https://main.qcloudimg.com/raw/82430a9cb1aa364d2abfbc47ebae5ef5.png)

## Uninstalling LogListener

In the case of the `/usr/local/` installation path, go to the `/usr/local/loglistener/tools` path and run the uninstallation command as the admin:

```plaintext
./loglistener.sh uninstall
```

## Manually Updating LogListener

#### Reusing the breakpoint file (logs are not repeatedly collected)

1. Run the stop command to stop the existing LogListener.
2. Back up the breakpoint file directory (`loglistener/data`) on the earlier version; for example, back up the legacy breakpoint file to the `/tmp/loglistener-backup` directory.
<dx-codeblock>
:::  plaintext
cp -r loglistener-2.2.3/data /tmp/loglistener-backup/
:::
</dx-codeblock>
3. Run the uninstallation command to uninstall the existing LogListener.
4. Download the latest version of LogListener. Then, install and initialize it with relevant commands.
5. Copy the breakpoint file directory backed up in step 2 to the new LogListener directory.
```plaintext
cp -r /tmp/loglistener-backup/data loglistener-<version>/
```
 Change the value of `<version>` as required. The following is an example:
```plaintext
cp -r /tmp/loglistener-backup/data loglistener-2.8.2/
```
6. Run the start command to start the latest version of LogListener.

#### Not reusing the breakpoint file (logs may be repeatedly collected)

1. Run the stop command to stop the existing LogListener.
2. Run the uninstallation command to uninstall the earlier version of LogListener.
3. Download the latest version of LogListener. Then, install and initialize it with relevant commands.
4. Run the start command to start the latest version of LogListener.
