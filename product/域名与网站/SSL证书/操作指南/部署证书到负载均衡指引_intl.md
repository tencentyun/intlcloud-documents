SSL certificates can be deployed to Cloud Load Balance (CLB) as follows:

### 1. Select a certificate
Apply for a certificate (see [DV Certificate Application](https://cloud.tencent.com/document/product/400/6814)) or select a certificate to upload, click **More**, and select **Deploy to CLB**.
![](https://mc.qcloudimg.com/static/img/f63593c744fe88e386ce1157526b468f/1.png)

### 2. Select an LB instance
Select only one LB instance based on the project and region (South China - Shenzhen Finance is not supported).
![](https://mc.qcloudimg.com/static/img/81157ad8528ad639623b32177e534624/123lb.jpg)

### 3. Create a listener
Go to the CLB console, open the **Create a Listener** pop-up window, switch the protocol port to HTTPS, select the specified server certificate, and then complete the rest configurations.
![](https://mc.qcloudimg.com/static/img/e997310524fd15288fca7c91ae7a2e6c/3.png)

### 4. Complete other configurations
Go on to complete other configurations to create a listener, and then you can achieve load balance with HTTPS.

