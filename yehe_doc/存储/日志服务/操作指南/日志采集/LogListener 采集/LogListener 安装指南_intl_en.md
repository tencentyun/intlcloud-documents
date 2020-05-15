LogListener is a dedicated log collector provided by Tencent Cloud Log Service (CLS). You can install and deploy it on a server to collect logs quickly.

## Installation environment

LogListener supports only Linux 64-bit operating systems and does not support Windows for the moment. It is compatible with mainstream Linux operating system versions. If LogListener is incompatible with the Linux operating system version you use, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

| Operating System &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Compatible Versions
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| CentOS (64-bit)                                               | CentOS_6.8_64-bit, CentOS_6.9_64-bit, CentOS_7.2_64-bit, CentOS_7.3_64-bit, CentOS_7.4_64-bit, CentOS_7.5_64-bit, CentOS_7.6_64-bit |
| Ubuntu (64-bit)                                                | Ubuntu Server_14.04.1_LTS_64-bit, Ubuntu Server_16.04.1_LTS_64-bit, Ubuntu Server_18.04.1_LTS_64-bit |
| Debian (64-bit)                                                | Debian_8.2_64-bit, Debian_9.0_64-bit                              |
| openSUSE (64-bit)                                              | openSUSE_42.3_64-bit                                          |





## Installation and Startup

### 1. Downloading and installing LogListener

Download the latest version of LogListener from [Download LogListener](https://loglistener-1254077820.cos.ap-shanghai.myqcloud.com/loglistener-linux-x64-2.2.8.tar.gz).

Download the LogListener installation package and decompress it to the installation path (`/usr/local/` in this example). Go to the directory `loglistener/tools` of LogListener and run the following command to install it:

```shell
wget https://loglistener-1254077820.cos.ap-shanghai.myqcloud.com/loglistener-linux-x64-2.2.8.tar.gz && tar -zxvf loglistener-linux-x64-2.2.8.tar.gz -C /usr/local && cd /usr/local/loglistener-2.2.8/tools && ./loglistener.sh install
```

### 2. Initializing LogListener

In the `loglistener/tools` path, run the following command to initialize LogListener as the `root` user (by default, a private network is used to access the service):
```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-xxxxxx
```

>You need to enter the parameters of **-secretid**, **-secretkey**, **-region**, and **-network** in the command. For details, see [Parameter description](#parameterdescription) given below.

<span id="parameterdescription"></span>

#### Parameter description

| Parameter    | Description                                                     |
| --------- | ------------------------------------------------------------ |
| secretid | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi). Used to identify who calls the API. |
| secretkey | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi). Used to encrypt signature strings and verify server-side signature strings. |
| region    | [Region](https://intl.cloud.tencent.com/document/product/614/18940) where CLS resides. You need to enter region abbreviations, such as ap-beijing and ap-guangzhou.  |
| network   | Type of the network through which LogListener accesses the service by domain name. Valid value: intra (private network) and internet (public network). Default value: intra.|

A domain name of the private network is used by default:

![](https://main.qcloudimg.com/raw/ea417c6d60ab21e52984d04c1364b30d.png)

If you need to access the service by domain name through the public network, run the following command to set the network parameter `internet` explicitly:

```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf0xxxxxxxxxxxx -region ap-xxxxxx -network internet
```

![](https://main.qcloudimg.com/raw/653ebe0400dca5b21b3e25d01f93cb5b.png)



>
> - We recommend you use a collaborator key, and the root account should grant the read/write permission of CLS to the collaborator.
> - `region` indicates the region of the CLS you use, instead of the region where your business server resides.
> - We recommend you use your private network to access the service by domain name if your CVM and logset are in the same region, otherwise, use the public network.

### 3. Starting LogListener

After LogListener is successfully installed, run the following command to start it:

```shell
/etc/init.d/loglistenerd start
```

![](https://main.qcloudimg.com/raw/184d6cc3308206b14288372da59a99a0.png)

## Working with LogListener

> The operation commands used here are only applicable to LogListener-2.2.4 and later versions. For operation commands applicable to earlier versions, see [Installation Guide for Earlier LogListener Versions ](https://intl.cloud.tencent.com/document/product/614/35674).

#### Checking the LogListener version

```shell
/etc/init.d/loglistenerd -v
```

#### Starting LogListener

```shell
/etc/init.d/loglistenerd start
```

#### Restarting LogListener

```shell
/etc/init.d/loglistenerd restart
```

#### Stopping LogListener

```shell
/etc/init.d/loglistenerd stop
```

#### Initializing LogListener

Run the following command in the `loglistener/tools` directory as the `root` user to initialize LogListener:

```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-xxxxxx
```

#### Uninstalling LogListener

Run the following command in the `loglistener/tools` directory as the `root` user to uninstall LogListener:

```shell
./loglistener.sh uninstall
```

#### Checking LogListener process status

```shell
/etc/init.d/loglistenerd status 
```

LogListener normally runs three processes:

![](https://main.qcloudimg.com/raw/6300054d2089484f2af5399082f9b880.png)

#### Checking LogListener heartbeat and configuration

```shell
/etc/init.d/loglistenerd check
```

![](https://main.qcloudimg.com/raw/82430a9cb1aa364d2abfbc47ebae5ef5.png)


## Manually updating LogListener

- Reusing the breakpoint file (logs are not repeatedly collected)
1. Run the stop command to stop the earlier version of LogListener.
2. Back up the breakpoint file directory (`loglistener/data`) on the earlier version. For example, back up the legacy breakpoint file to the directory `/tmp/loglistener-backup`.
```shell
cp -r loglistener-2.2.3/data /tmp/loglistener-backup/
```
3. Run the uninstallation command to uninstall the earlier version.
4. Download the latest version of LogListener, and run commands to install and initialize it.
5. Run the following command to copy the breakpoint file directory backup from Step 2 to the directory of the latest version.
```shell
cp -r /tmp/loglistener-backup/data loglistener-2.2.8/
```
6. Run the start command to start the latest version.

#### Not reusing the breakpoint file (logs may be repeatedly collected)
1. Run the stop command to stop the earlier version of LogListener.
2. Run the uninstallation command to uninstall the earlier version.
3. Download the latest version of LogListener, and run commands to install and initialize it.
4. Run the start command to start the latest version of LogListener.
