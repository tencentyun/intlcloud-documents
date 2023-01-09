
>! This document provides an operation guide for LogListener 2.2.4 and earlier. We recommend that you update to the latest version as this document may no longer be maintained. For information on how to install the latest version, see the [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).

#### Starting LogListener

Go to the installation directory `loglistener` and start LogListener by running the following script:

```plaintext
cd loglistener/tools; ./start.sh
```

#### Stopping LogListener

Go to the installation directory `loglistener` and stop LogListener by running the following script:

```shell
cd loglistener/tools; ./stop.sh
```

#### Checking LogListener process status

Go to the installation directory `loglistener` and check the status of the LogListener processes by running the following command:

```shell
cd loglistener/tools; ./p.sh
```

![](https://main.qcloudimg.com/raw/1d69aa323f09dfe2105b7d60a41137b7.png)
Normally, there are three processes:

```shell
bin/loglistenerm -d                                #Daemon process
bin/loglistener --conf=etc/loglistener.conf        #Main process    
bin/loglisteneru -u --conf=etc/loglistener.conf    #Update process
```

#### Uninstalling LogListener

Go to the installation directory `loglistener` and uninstall LogListener by running the following command:

```shell
cd loglistener/tools; ./uninstall.sh
```

#### Checking LogListener heartbeat and configuration

Go to the installation directory `loglistener` and check the heartbeat and configuration of LogListener by running the following command:

```shell
cd loglistener/tools; ./check.sh
```
