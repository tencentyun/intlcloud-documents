LogListener is a log collection client provided by Tencent Cloud's Cloud Log Service (CLS). You can install and deploy it on the target server to collect logs quickly and in real time.

## Supported Environment

LogListener supports the following Linux 64-bit operating systems:

- CentOS
- Debian
- SUSE
- OpenSUSE
- Ubuntu

## Installation Procedure

#### 1. Downloading LogListener

The download address of the latest version of LogListener is as follows: [Download LogListener](https://main.qcloudimg.com/raw/8656fcadd12ab9689674df09b510b52b/loglistener.2.2.2.tar.gz).

#### 2. Installing LogListener

Decompress the downloaded installer package. The installation decompression path is `/usr/local/`. Execute the commands as follows:

```shell
tar -zxvf [Installer package] -C /usr/local/ && cd /usr/local/loglistener/tools
```

Enter the installation directory of LogListener `/loglistener/tools`, and execute the following commands with root permission:

```shell
./install.sh [SecretId] [SecretKey] [region]
```
![](https://main.qcloudimg.com/raw/17fdde2321ae56551ee05f82b84fabd3.png)
Parameter Sample:
```shell
./install.sh AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX ap-guangzhou 
```

| Parameter Name    | Type Description                                                     |
| --------- | ------------------------------------------------------------ |
| SecretId  | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi), which is used to identify the API caller |
| SecretKey | Part of the [Cloud API key](https://console.cloud.tencent.com/cam/capi), which is used to encrypt signature strings and verify server-side signature strings |
| region    | [Region](https://intl.cloud.tencent.com/document/product/614/18940) of the log service |

>?
> - It is recommended to use a collaborator key, and the collaborator should be granted the read-write permission of CLS by the root account.
> - The field "region" is where CLS is available instead of the region in which your business server resides.
> - The installation script uses `rc.local` to ensure that the client starts normally upon server restart.

## Working with LogListener

###  Launching LogListener

You can launch the LogListener by running the following script:

```shell
cd /usr/local/loglistener/tools; ./start.sh
```

### Stopping LogListener

You can stop the LogListener by running the following script:

```shell
cd /usr/local/loglistener/tools; ./stop.sh
```

### Viewing the Processes

You can view the processes of LogListener using the following command:

```shell
cd /usr/local/loglistener/tools; ./p.sh
```
![](https://main.qcloudimg.com/raw/9c326c49e85f761a82aadd8ead1f1a59.png)
Normally, there are three processes:

```shell
bin/loglistenerm -d                                # Daemon
bin/loglistener --conf=etc/loglistener.conf        # Main process     
bin/loglisteneru -u --conf=etc/loglistener.conf    # Update process
```

### Uninstalling LogListener

You can uninstall the LogListener using the following command:

```shell
cd /usr/local/loglistener/tools; ./uninstall.sh
```

>!Uninstalling LogListener deletes the auto-restart tool from `rc.local`.

## Updating LogListener

We recommend that you update LogListener to the latest version. **Full RegEx collection is not supported for LogListner of versions earlier than 2.2.2.** You can view the LogListener version information in `loglistener/version.txt`.

-  If your LogListener version is later than 2.0.0 but earlier than 2.2.2, the following updating procedures apply:
 1. Download a new installer package.
 2. Decompress the new compressed package to the installation directory (the same level as the directory of LogListener).
 3. After the decompression, restart LogListener to complete the update process.
-  If your LogListener version is earlier than 2.0.0, update it manually by following the procedures below:
 1. Stop the earlier version of LogListener.
 2. Back up the earlier version of LogListener.
 3. Download and install the latest LogListener.

