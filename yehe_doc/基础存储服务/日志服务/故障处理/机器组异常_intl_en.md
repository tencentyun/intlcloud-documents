
## Error Description

The installed LogListener may go wrong when you are configuring server groups. In this case, LogListener neither connects to the CLB console nor uploads logs normally. The exception status is shown in the figure below:

![](https://main.qcloudimg.com/raw/cffaee990badc81785d85714169d848b.png)

## Troubleshooting Steps

> The troubleshooting described here is only applicable to LogListener 2.2.4 and later versions. For troubleshooting applicable to earlier versions, see [LogListener Installation Exception](https://intl.cloud.tencent.com/document/product/614/35675).

#### 1. Check LogListener by running the `check` command.

```sh
sudo /etc/init.d/loglistenerd check
```

If LogListener is running normally, the `check` command outputs the results as shown below:

![1574426236479](https://main.qcloudimg.com/raw/56ead9b5deb1652b21d37663ee429a40.png)

If you see different results, the possible causes may include:

#### LogListener process exception
  Start LogListener if it is not started. 
  ![1574428021070](https://main.qcloudimg.com/raw/122b75a2e79a9c2eaaeb9ff47ad4ac02.png)

#### LogListener heartbeat exception
Many causes may lead to LogListener heartbeat exception. The most common causes include:
- Key error
     Check whether the key information of LogListener is correct. Go to the installation directory `etc` of LogListener and run the following command.
     ```shell
cd loglistener-2.2.4/etc && sudo cat loglistener.conf
     ```
     ![1574428504494](https://main.qcloudimg.com/raw/745dc55f11812878c4fb54f6fc9488bc.png)
- Network error
     ```shell
telnet <cls domain name> 80
     ```
     Confirm whether the network is connected. For the domain name of CLS, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). If the network is properly connected, you will see the results below. 
![](https://main.qcloudimg.com/raw/d9efbce1be5cbfa89b94fa406966b58c.jpg)


#### 2. Check IP configurations

Check whether the IP address of the server group is the same obtained during the installation of LogListener. To check the IP address of LogListener, run the following command:

```plaintext
sudo /etc/init.d/loglistenerd check
```

![1574424826850](https://main.qcloudimg.com/raw/e56df118de33285ad666435fe77c3751.png)

Log in to the [Cloud Log Service Console](https://console.cloud.tencent.com/cls), and click **Server Group** in the left sidebar to go to the **Server Group Management** page, check the IP address of the server group. The IP address must be the same as that for LogListener.
![](https://main.qcloudimg.com/raw/ea8e833b596e1cf000f4f58f8f99dd29.png)

