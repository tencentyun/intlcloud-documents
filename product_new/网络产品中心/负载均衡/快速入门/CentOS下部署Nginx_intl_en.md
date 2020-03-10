This document describes how to deploy Nginx projects on CentOS and is suitable for new individual users of Tencent Cloud.
## Software Version
The versions of software tools used in this document are as follows, which may be different from your software versions during actual operations.
- Operating system: CentOS 7.5
- Nginx: Nginx 1.16.1

## Installing Nginx
1. After completing the purchase, click **Log in** on the CVM details page to log in to the CVM instance and then enter your username and password to set up an Nginx environment. For more information on how to create a CVM instance, please see [Creating CVM Instances](https://cloud.tencent.com/document/product/213/4855).
```
# Install Nginx
yum -y install nginx  
# View Nginx version
nginx -v
# View Nginx installation directory
rpm -ql nginx
# Start Nginx
service nginx start
```
2. Access the public IP address of the CVM instance and if the following page appears, Nginx is successfully deployed:
![](https://main.qcloudimg.com/raw/8807f9fd819eb93d46c5646ba3572fac.png)
3. The default root directory of Nginx is `/usr/share/nginx/html`. Modify the `index.html` static page in the `html` directory to mark the specialness of this page. Relevant operations are as follows:
   1. Run the following command to enter the `index.html` static page in `html`:
```bash
vim /usr/share/nginx/html/index.html
```
   2. Press "i" to enter the editing mode and add the following in the `<body></body>` tag:
```bash
# You are recommended to enter directly under `<body>`
Hello nginx , This is rs-1!
URL is index.html
```
![](https://main.qcloudimg.com/raw/02e833dd08a6873d5d015f4531d24645.png)
   3. Press "Esc" and enter `:wq` to save the change.
4. CLB (formerly "Application CLB") can forward requests according to the real server path and deploy a static page in the `/image` path. Relevant operations are as follows:
   1. Run the following commands to create and enter an `image` directory:
```bash
mkdir /usr/share/nginx/html/image
cd /usr/share/nginx/html/image
```
   2. Run the following command to create an `index.html` static page in the `image` directory:
```
vim index.html
```
   3. Press "i" to enter the editing mode and add the following in the page:
```bash
Hello nginx , This is rs-1!
URL is image/index.html
```
   4. Press "Esc" and enter `:wq` to save the change.
 
>!The default port of Nginx is `80`. To change the port, please modify the configuration file and restart Nginx.

## Verifying the Nginx Service
Access the public IP and path of your CVM instance. If the deployed static page is displayed, Nginx has been successfully deployed.
- `index.html` page of `rs-1`:
![](https://main.qcloudimg.com/raw/ede62fecd2106869d53bf142ad51903e.png)
- `/image/index.html` page of `rs-1`:
![](https://main.qcloudimg.com/raw/f0f87422487177722291c2260cac9d35.png)
