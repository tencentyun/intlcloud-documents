LogListener is a log collector provided by Cloud Log Service (CLS). You can install and deploy it on a server to collect logs quickly.

## Installation Environment

LogListener supports only Linux 64-bit operating systems and does not support Windows now. It is compatible with mainstream Linux operating system versions. If LogListener is incompatible with the Linux operating system version you use, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

| OS &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Compatible Versions                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| CentOS (64-bit)                                               | CentOS_6.8_64-bit, CentOS_6.9_64-bit, CentOS_7.2_64-bit, CentOS_7.3_64-bit, CentOS_7.4_64-bit, CentOS_7.5_64-bit, CentOS_7.6_64-bit, CentOS_8.0_64-bit |
| Ubuntu (64-bit) | Ubuntu Server_14.04.1_LTS_64-bit, Ubuntu Server_16.04.1_LTS_64-bit, Ubuntu Server_18.04.1_LTS_64-bit |
| Debian (64-bit) | Debian_8.2_64-bit, Debian_9.0_64-bit |
| openSUSE (64-bit) | openSUSE_42.3_64-bit |


## Installation and Startup

### 1. Downloading and installing LogListener

Download link of the latest version LogListener: [download via the public network](https://mirrors.tencent.com/install/cls/loglistener-linux-x64-2.5.8.tar.gz)、[download via the private network](http://mirrors.tencentyun.com/install/cls/loglistener-linux-x64-2.5.8.tar.gz)

Download the LogListener installation package and decompress it to the installation path (`/usr/local/` in this example). Then go to the LogListener directory `loglistener/tools` and run the following installation command:
```plaintext
wget https://mirrors.tencentyun.com/install/cls/loglistener-linux-x64-2.5.8.tar.gz && tar -zxvf loglistener-linux-x64-2.5.8.tar.gz -C /usr/local && cd /usr/local/loglistener-2.5.8/tools && ./loglistener.sh install
```


### 2. Initializing LogListener

In the `loglistener/tools` path, run the following command to initialize LogListener as the root user. By default, a private network is used to access the service:
```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-xxxxxx
```
>?You need to replace **-secretid**, **-secretkey**, **-region**, and **-network** in the command with the actual values. For more information, please see [Parameter description](#parameterdescription) below.

<span id="parameterdescription"></span>

#### Parameter description

| Parameter    | Description                                                     |
| --------- | ------------------------------------------------------------ |
| secretid  | Part of a [TencentCloud API key](https://console.cloud.tencent.com/cam/capi), which is used to identify the API requester |
| secretkey | Part of a [TencentCloud API key](https://console.cloud.tencent.com/cam/capi), which is used to encrypt the strings to create a signature so that Tencent Cloud server can validate the identity of the requester. |
| region    | [Region](https://intl.cloud.tencent.com/document/product/614/18940) where CLS resides. Enter a region abbreviation here, such as `ap-beijing` or `ap-guangzhou`. |
| network   | Type of the network through which LogListener accesses the service by domain name. Valid values: intra (private network), internet (public network). Default value: intra.|
| ip        | Server IP. If this parameter is left empty, LogListener will automatically get the local IP address. |
| label     | Server group tag, which is required if you want to identify the server group. Multiple tags should be separated by comma. |

A private network domain name is used by default:

![](https://main.qcloudimg.com/raw/ea417c6d60ab21e52984d04c1364b30d.png)

If you need to access the service by domain name through the public network, run the following command to set the network parameter `internet` explicitly:

```plaintext
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf0xxxxxxxxxxxx -region ap-xxxxxx -network internet
```

![](https://main.qcloudimg.com/raw/653ebe0400dca5b21b3e25d01f93cb5b.png)
> ?
> - It is recommended to use a collaborator key if the collaborator is granted the read and write permission of CLS by the root account.
> - `region` indicates the region of your CLS, instead of the region where your business server resides.
>- If your CVM instance and logset are in the same region, we recommend you access the service domain name over the private network; otherwise, use the public network.

### 3. Starting LogListener

After LogListener is successfully installed, run the following command to start it:
```plaintext
/etc/init.d/loglistenerd start
```
![](https://main.qcloudimg.com/raw/184d6cc3308206b14288372da59a99a0.png)

## Common LogListener Operations

> ? The operation commands used in this document are only applicable to LogListener-2.2.4 and later versions. For operation commands applicable to earlier versions, see [Earlier-Version LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/35674).

### 1. Check LogListener version

```plaintext
/etc/init.d/loglistenerd -v
```

### 2. View LogListener help documentation

```plaintext
/etc/init.d/loglistenerd -h
```

### 3. Manage LogListener process

```plaintext
/etc/init.d/loglistenerd (start|restart|stop) # Start, restart, stop
```

### 4. Check LogListener process status

```plaintext
/etc/init.d/loglistenerd status
```

LogListener normally runs two processes:
![](https://main.qcloudimg.com/raw/134c3ffc885d09903f86412edc18b9a9.png)

### 5. Check LogListener heartbeat and configuration

```plaintext
/etc/init.d/loglistenerd check
```

![](https://main.qcloudimg.com/raw/82430a9cb1aa364d2abfbc47ebae5ef5.png)


## Uninstalling LogListener

In the `loglistener/tools` directory, run the uninstallation command as the admin:

```plaintext
./loglistener.sh uninstall
```

## Manually Updating LogListener

#### Breakpoint file reused (logs will not be repeatedly collected)

1. Run the stop command to stop the existing LogListener.
2. Back up the breakpoint file directory (`loglistener/data`) on the earlier version; for example, back up the legacy breakpoint file to the `/tmp/loglistener-backup` directory.
<dx-codeblock>
:::  plaintext
cp -r loglistener-2.2.3/data /tmp/loglistener-backup/
:::
</dx-codeblock>

3. Run the uninstallation command to uninstall the existing LogListener.
4. Download the latest version of LogListener and install and initialize it with relevant commands.
5. Copy the breakpoint file directory backed up in step 2 to the new LogListener directory.
```plaintext
cp -r /tmp/loglistener-backup/data loglistener-<version>/
```
 You can change the value of  `<version>`. For example:
```plaintext
cp -r /tmp/loglistener-backup/data loglistener-2.2.8/
```
6. Run the start command to start the latest version of LogListener.



#### Breakpoint file not reused (logs may be repeatedly collected)

1. Run the stop command to stop the existing LogListener.
2. Run the uninstallation command to uninstall the earlier version of LogListener.
3. Download the latest version of LogListener and install and initialize it with relevant commands.
4. Run the start command to start the latest version of LogListener.
