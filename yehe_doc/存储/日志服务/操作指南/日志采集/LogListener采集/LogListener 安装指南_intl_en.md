LogListener is a log collector provided by Tencent Cloud Log Service (CLS). You can install and deploy it on a server to collect logs quickly.

  

## Installation environment

LogListener supports only Linux 64-bit operating systems and does not support Windows for the moment. It is compatible with mainstream Linux operating system versions. If LogListener is incompatible with the Linux operating system version you use, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

   <table>
   <thead>
   <tr>
   <th>Operating System</th>
   <th>Compatible Version</th>
   </tr>
   </thead>
   <tbody><tr>
   <td nowrap="nowrap">CentOS (64-bit)</td>
   <td>CentOS_6.8_64, CentOS_6.9_64, CentOS_7.2_64, CentOS_7.3_64, CentOS_7.4_64, CentOS_7.5_64, CentOS_7.6_64</td>
   </tr>
   <tr>
   <td>Ubuntu (64-bit)</td>
   <td>Ubuntu Server_14.04.1_LTS_64, Ubuntu Server_16.04.1_LTS_64, Ubuntu Server_18.04.1_LTS_64</td>
   </tr>
   <tr>
   <td>Debian (64-bit)</td>
   <td>Debian_8.2_64, Debian_9.0_64</td>
   </tr>
   <tr>
   <td nowrap="nowrap">openSUSE (64-bit)</td>
   <td>openSUSE_42.3_64</td>
   </tr>
   </tbody></table>





## Installation and startup

### 1. Downloading and installing LogListener

Download address of the latest version of LogListener: [Download LogListener](https://loglistener-1254077820.cos.ap-shanghai.myqcloud.com/loglistener-linux-x64-2.2.8.tar.gz).

Download the LogListener installation package and decompress it to the installation path (`/usr/local/` in this example). Then go to the LogListener directory `loglistener/tools` and run the following installation command:

```shell
wget https://loglistener-1254077820.cos.ap-shanghai.myqcloud.com/loglistener-linux-x64-2.2.8.tar.gz && tar -zxvf loglistener-linux-x64-2.2.8.tar.gz -C /usr/local && cd /usr/local/loglistener-2.2.8/tools && ./loglistener.sh install
```

   

### 2. Initializing LogListener

In the `loglistener/tools` path, run the following command to initialize LogListener as the root user (by default, a private network is used to access the service):

```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-shanghai
```

A private network domain name is used by default:

![](https://main.qcloudimg.com/raw/a1a4077fa9b1dc43f0ac20dc3f3b0025.png)

If you need to access the service by domain name through the public network, run the following command to set the network parameter `internet` explicitly:

```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf0xxxxxxxxxxxx -region ap-shanghai -network internet
```

![](https://main.qcloudimg.com/raw/15e1dbf3058f6eb5110dfd2ca646bb6d.png)

   

#### Parameter description

| Parameter    | Description                                                     |
| --------- | ------------------------------------------------------------ |
| secretid  | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi). Used to identify who calls the API. |
| secretkey | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi). Used to encrypt signature strings and verify server-side signature strings. |
| region    | [Region](https://intl.cloud.tencent.com/document/product/614/18940) where CLS resides. |
| network   | Type of the network through which LogListener accesses the service by domain name. Valid values are: intra (private network) and internet (public network). The default value is intra.|

>
>
> - It is recommended that you use a collaborator key, and the root account should grant the read/write permission of CLS to the collaborator.
> - `region` indicates the region of the CLS you use, instead of the region where your business server resides.
> - If your CVM and logset are in the same region, it is recommended that you use your private network to access the service by domain name.

### 3. Starting LogListener

After LogListener is successfully installed, run the following command to start it:

```shell
/etc/init.d/loglistenerd start
```

![](https://main.qcloudimg.com/raw/a68d1df534898ed99c35f25199840fa4.png)

## Working with LogListener 

> The operation commands used in this document are only applicable to LogListener-2.2.4 and later versions. 

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

Run the initialization command in the `loglistener/tools` directory as an administrator:

```shell
./loglistener.sh init -secretid AKIDPEtPyKabfW8Z3Uspdz83xxxxxxxxxxxx -secretkey whHwQfjdLnzzCE1jIf09xxxxxxxxxxxx -region ap-beijing

```

#### Uninstalling LogListener

Run the uninstallation command in the `loglistener/tools` directory as an administrator:

```shell
./loglistener.sh uninstall

```

#### Checking LogListener process status

```shell
/etc/init.d/loglistenerd status 

```

LogListener normally runs three processes:
![](https://main.qcloudimg.com/raw/7ae93d3ee7e9b57cf264466e87da351e.png)

#### Checking LogListener heartbeat and configuration

```shell
/etc/init.d/loglistenerd check

```

![](https://main.qcloudimg.com/raw/98115f6529f3a43c17d6b75fc767d17f.png)

   

## Manually updating LogListener

- Reusing the breakpoint file (logs are not repeatedly collected)

  1. Run the stop command to stop the earlier version of LogListener.
  2. Download the latest version of LogListener.
  3. Run commands to install and initialize the latest version.
  4. Copy the breakpoint file directory (`loglistener/data`) from the earlier version of LogListener to the directory of the latest version of LogListener. For example, to copy the breakpoint file of LogListener-2.2.3 to the latest version (for example, 2.2.6), run the following command:
  ```shell
  cp -r loglistener-2.2.3/data loglistener-2.2.8/
  ```
  5. Run the start command to start the latest version.
  6. Run the uninstallation command to uninstall the earlier version.

- Not reusing the breakpoint file (logs may be repeatedly collected)

  1. Run the stop command to stop the earlier version of LogListener.
  2. Download the latest version of LogListener.
  3. Run commands to install and initialize the latest version.
  4. Run the start command to start the latest version of LogListener.
  5. Run the uninstallation command to uninstall the earlier version of LogListener.
