LogListener is a log collector provided by Cloud Log Service (CLS). You can install and deploy it on a machine to collect logs quickly.

## Installation Environment

LogListener supports only Linux 64-bit operating systems and does not support Windows now. It is compatible with mainstream Linux operating system versions. If LogListener is incompatible with the Linux operating system version you use, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

| Parameter | Set Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| CentOS (64-bit)                                               | CentOS_6.8_64-bit, CentOS_6.9_64-bit, CentOS_7.2_64-bit, CentOS_7.3_64-bit, CentOS_7.4_64-bit, CentOS_7.5_64-bit, CentOS_7.6_64-bit, CentOS_8.0_64-bit |
| Ubuntu (64-bit) | Ubuntu Server_14.04.1_LTS_64-bit, Ubuntu Server_16.04.1_LTS_64-bit, Ubuntu Server_18.04.1_LTS_64-bit |
| Debian (64-bit) | Debian_8.2_64-bit, Debian_9.0_64-bit |
| openSUSE (64-bit) | openSUSE_42.3_64-bit |


## Installation and startup

### 1. Downloading and installing LogListener

Download links of the latest version LogListener: [Download by public network](https://mirrors.tencent.com/install/cls/loglistener-linux-x64-2.6.2.tar.gz), [Download by private network](http://mirrors.tencentyun.com/install/cls/loglistener-linux-x64-2.6.2.tar.gz)

Download the LogListener installation package and decompress it to the installation path (`/usr/local/` in this example). Then go to the LogListener directory `loglistener/tools` and run the following installation command.
- Operation command for the public network:
```plaintext
wget https://mirrors.tencent.com/install/cls/loglistener-linux-x64-2.6.2.tar.gz  && tar -zxvf loglistener-linux-x64-2.6.2.tar.gz -C /usr/local && cd /usr/local/loglistener-2.6.2/tools && ./loglistener.sh install
```
- Operation command for the private network:
```plaintext
wget http://mirrors.tencentyun.com/install/cls/loglistener-linux-x64-2.6.2.tar.gz  && tar -zxvf loglistener-linux-x64-2.6.2.tar.gz -C /usr/local && cd /usr/local/loglistener-2.6.2/tools && ./loglistener.sh install
```

### 2. Initializing LogListener

In the `loglistener/tools` path, run the following command to initialize LogListener as the root user. By default, a private network is used to access the service:
```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-xxxxxx
```
>?You need to replace **-secretid**, **-secretkey**, **-region**, and **-network** in the command with the actual values. For more information, please see [Parameter description](#parameterdescription) below.

<span id="parameterdescription"></span>

#### Parameters

| Parameter    | Description                                                     |
| --------- | ------------------------------------------------------------ |
| secretid  | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi). Used to identify who calls the API. |
| secretkey | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi). Used to encrypt signature strings and verify server-side signature strings. |
| region    | [Region](https://intl.cloud.tencent.com/document/product/614/18940) where CLS resides. Enter a region abbreviation here, such as `ap-beijing` or `ap-guangzhou`. |
| network   | Type of the network through which LogListener accesses the service by domain name. Valid values are: intra (private network) and internet (public network). The default value is intra.|
| ip        | Machine IP. If this parameter is left empty, LogListener will automatically get the local IP address. |
| label     | Machine group label, which is required if you want to identify the machine group. Multiple tags should be separated by comma. |

A private network domain name is used by default:

![](https://main.qcloudimg.com/raw/ea417c6d60ab21e52984d04c1364b30d.png)

If you need to access the service by domain name through the public network, run the following command to set the network parameter `internet` explicitly:

```plaintext
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf0xxxxxxxxxxxx -region ap-xxxxxx -network internet
```

![](https://main.qcloudimg.com/raw/653ebe0400dca5b21b3e25d01f93cb5b.png)
> ?
>- We recommend that you use a collaborator key if the collaborator has been assigned with the CLS read/write permission by the root account.
> - `region` indicates the region of the CLS you use, instead of the region where your business machine resides.
>- If your CVM instance and logset are in the same region, we recommend you access the service domain name over the private network; otherwise, use the public network.
> - For details about log collection, please see [Granting a Sub-account Permissions for CLS](https://intl.cloud.tencent.com/document/product/614/39023).
> 

### 3. Starting LogListener

After LogListener is successfully installed, run the following command to start it:
```plaintext
/etc/init.d/loglistenerd start
```
![](https://main.qcloudimg.com/raw/184d6cc3308206b14288372da59a99a0.png)

## Common LogListener Operations

> ? The operation commands used in this document are only applicable to LogListener v2.2.4 and later versions. For operation commands applicable to earlier versions, see [Earlier-Version LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/35674).

### 1. Checking the LogListener version

```plaintext
/etc/init.d/loglistenerd -v
```

### 2. Viewing LogListener help documentation

```plaintext
/etc/init.d/loglistenerd -h
```

### 3. Managing LogListener process

```plaintext
/etc/init.d/loglistenerd (start|restart|stop) # Start, restart, stop
```

### 4. Checking LogListener process status

```plaintext
/etc/init.d/loglistenerd status
```

LogListener normally runs two processes:
![](https://main.qcloudimg.com/raw/134c3ffc885d09903f86412edc18b9a9.png)

### 5. Checking LogListener heartbeat and configuration

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

#### Reusing the breakpoint file (logs are not repeatedly collected)

1. Run the stop command to stop the existing LogListener.
2. Back up the breakpoint file directory (`loglistener/data`) on the earlier version; for example, back up the legacy breakpoint file to the `/tmp/loglistener-backup` directory.
<dx-codeblock>
:::  plaintext
cp -r loglistener-2.2.3/data /tmp/loglistener-backup/
:::
</dx-codeblock>
3. Run the uninstallation command to uninstall the existing LogListener.
4. Download the latest version of LogListener, install and initialize it with relevant commands.
5. Copy the breakpoint file directory backed up in step 2 to the new LogListener directory.
```plaintext
cp -r /tmp/loglistener-backup/data loglistener-<version>/
```
 You can change the value of `<version>`. For example:
```plaintext
cp -r /tmp/loglistener-backup/data loglistener-2.2.8/
```
6. Run the start command to start the latest version of LogListener.



#### Not reusing the breakpoint file (logs may be repeatedly collected)

1. Run the stop command to stop the existing LogListener.
2. Run the uninstallation command to uninstall the earlier version of LogListener.
3. Download the latest version of LogListener, install and initialize it with relevant commands.
4. Run the start command to start the latest version of LogListener.
