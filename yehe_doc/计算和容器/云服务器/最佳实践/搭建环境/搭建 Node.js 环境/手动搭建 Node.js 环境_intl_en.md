## Overview
This article describes how to deploy Node.js on a CVM and create a sample project.

To do this, you need to be familiar with common Linux commands such as [Installing Software via YUM in a CentOS Environment](https://intl.cloud.tencent.com/document/product/213/2046) and understand the versions of the installed software.
<dx-alert infotype="explain" title="">
It's recommended that you can configure the Node.js environment through the image environment of Tencent Cloud marketplace, and it may take a long time to set up the Node.js environment manually.
</dx-alert>



## Software
Setting up Node.js involves:
- CentOS: a distribution of the Linux operating system. We use CentOS 7.6 in this article.
- Node.js: a JavaScript runtime environment. We use Node.js 10.16.3 and Node.js 6.9.5 in this article.
- npm: a package manager for JavaScript. We use npm 6.9.0 in this article to manage multiple Node.js versions.

## Prerequisites
You have purchased a Linux CVM.

## Directions
### Step 1: log in to a Linux instance
[Log in to the Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use any of the following login methods you are comfortable with:
- [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
- [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)


### Step 2: Installing Node.js
1. Run the following command to download the Node.js 64-bit install package for Linux.
```
wget https://nodejs.org/dist/v10.16.3/node-v10.16.3-linux-x64.tar.xz
```
<dx-alert infotype="explain" title="">
Visit the [Node.js official website](https://nodejs.org/download/) for more information.
</dx-alert>
2. Run the following command to decompress the install package.
```
tar xvf node-v10.16.3-linux-x64.tar.xz
```
3. Run the following commands to create symbolic links.
```
ln -s /root/node-v10.16.3-linux-x64/bin/node /usr/local/bin/node
```
```
ln -s /root/node-v10.16.3-linux-x64/bin/npm /usr/local/bin/npm
```
Once created, you are able to use node and npm commands in any CVM directory.
4. Run the following commands to view Node.js and npm versions.
```
node -v
```
```
npm -v
```

### Step 3: Installing multiple Node.js versions (optional)


<dx-alert infotype="explain" title="">
This process allows you to install multiple Node.js versions. Developers can use this to quickly switch among versions.
</dx-alert>


1. Run the following command to install git.
```
yum install -y git
```
2. Run the following command to download the NVM source code and check for the newest version.
```
git clone git://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```
3. Run the following to configure NVM environment variables.
```
echo ". ~/.nvm/nvm.sh" >> /etc/profile
```
4. Run the following command to read system environment variables.
```
source /etc/profile
```
5. Run the following commands to view all Node.js versions.
```
nvm list-remote
```
6. Run the following commands to install multiple Node.js versions.
```
nvm install v6.9.5
```
```
nvm install v10.16.3
```
7. Run the following command to view all installed Node.js versions.
```
nvm ls
```
If the following appears, then the installation is successful and the current version in use is Node.js 10.16.3.
![](https://main.qcloudimg.com/raw/a315fe51314357fb44ec725f20c101ed.png)
8. Run the following command switch to another version.
```
nvm use v6.9.5
```
The following information will appear:
![](https://main.qcloudimg.com/raw/817fd96fef77f818e65ce41a3723e5bc.png)

### Step 4: Creating a sample project
1. Run the following commands to create a file named `index.js` under the root path.
```
cd ~
```
```
vim index.js
```
2. Press **i** to enter edit mode and input the following in the `index.js` file:
```
const http = require('http');
const hostname = '0.0.0.0';
const port = 7500;
const server = http.createServer((req, res) => { 
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello World\n');
}); 
server.listen(port, hostname, () => { 
    console.log(`Server running at http://${hostname}:${port}/`);
});
```
<dx-alert infotype="explain" title="">
This article uses port 7500 in the `index.js` file. You can use other ports as needed.
</dx-alert>
3. Click **Esc**, enter **:wq**, and press **Enter** to save and close the file.
4. Run the following command to execute the Node.js project we just created.
```
node index.js
```
5. Open a browser window on your local machine and visit the following URL to check if the project has been executed successfully.
```
http://CVM_Public_IP:Port
```
If the following appears, Node.js is installed successfully.
![](https://main.qcloudimg.com/raw/5b72798dc9e988eee8d8186055aa45e9.png)


## FAQs
If you encounter a problem when using CVM, refer to the following documents for troubleshooting:
- CVM login: [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- CVM network: [IP Address](https://intl.cloud.tencent.com/document/product/213/17285) and [Port](https://intl.cloud.tencent.com/document/product/213/2502).
- CVM disks: [System and Data Disks](https://intl.cloud.tencent.com/zh/document/product/213/17351).

