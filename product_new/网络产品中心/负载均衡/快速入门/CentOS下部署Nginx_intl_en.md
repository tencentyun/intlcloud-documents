This document describes how to deploy Nginx projects on CentOS. It is suitable for new individual users of Tencent Cloud.
## Software Version
The versions of software tools used in this document are as follows, which may be different from your software versions during actual operations.
- Operating system: CentOS 7.5
- Nginx: Nginx 1.12.2

## Installing Nginx
1. After purchased the service, click **Log in** on the CVM details page to log in to the CVM instance. And then enter your username and password to set up an Nginx environment. For more information on how to launch a CVM instance, see [Creating CVM Instances](http://intl.cloud.tencent.com/document/product/213/4855).
```
# Install n=Nginx:
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
3. The default root directory of Nginx is `/usr/share/nginx/html`. Modify the index.html static page in the `html` directory to mark the specialness of this page.
```
vim /usr/share/nginx/html/index.html
# Enter the following on the page:
Hello nginx , This is rs-1!
URL is index.html
```
4. Cloud Load Balancer (former “Application Load Balancer”) can forward requests according to the real server path and deploy a static page in the `/image` path. The command is as follows:
```
# Create a directory Image
mkdir /usr/share/nginx/html/image
cd /usr/share/nginx/html/image
vim index.html
# Enter the following on the page:
Hello nginx , This is rs-1!
URL is image/index.html
```
> The default port of Nginx is `80`. To change the port, please modify the configuration file and restart Nginx.

## Verify the Nginx service
Access the public IP and path of your CVM instance. If the deployed static page is displayed, Nginx has been successfully deployed.
- `index.html` page of `rs-1`:
![](https://main.qcloudimg.com/raw/ede62fecd2106869d53bf142ad51903e.png)
- `/image/index.html` page of `rs-1`:
![](https://main.qcloudimg.com/raw/f0f87422487177722291c2260cac9d35.png)
