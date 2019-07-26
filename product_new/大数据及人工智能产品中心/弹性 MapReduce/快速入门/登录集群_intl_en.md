
## Logging in Using a Remote Login Tool (on Windows)
This section uses Xshell as an example to describe how to log in to an EMR cluster with a password using a remote login tool on Windows.

### Applicable OS
Windows

### Logging in with a Password
1. Download PuTTY (a remote login tool on Windows) [here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) and install it.
2. Launch the PuTTY client, enter the following in the PuTTY Configuration window, and click **Open** to create a session as shown below:
 - **Host Name**: The public IP address of the EMR cluster, which can be viewed on the list page or details page in the [EMR Console](https://console.cloud.tencent.com/emr).
 - **Port**: The port number of the CVM instance, which has to be 22. (Please make sure that the port 22 in the CVM instance is opened. For more information, see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452) and [Network ACL](https://intl.cloud.tencent.com/document/product/215/5132)).
 - **Connect type**: Select **SSH**.
![](https://main.qcloudimg.com/raw/ffd939abf8af27a9dfba50707f421992.png)
3. In the PuTTY session window, enter the obtained admin account and press Enter.
4. Enter the obtained login password and press Enter to log in as shown below:
![](https://main.qcloudimg.com/raw/aa15c58c8528f41415a14f65ff7ab1bc.png)


## Log in Using SSH (on Linux or macOS)
This section describes how to log in to an EMR cluster using SSH on Linux or macOS.

### Applicable OS
Linux or macOS

### Logging in with a Password
1. On macOS, launch Terminal and run the following command. On Linux, run the following commands directly:
```
ssh <username>@<hostname or IP address>
```
 - username: The admin account, such as root.
 - hostname or IP address: The public IP address or custom domain name of your EMR cluster.
1. Enter the obtained password (only the input but not the output is displayed here) and press Enter to log in.


