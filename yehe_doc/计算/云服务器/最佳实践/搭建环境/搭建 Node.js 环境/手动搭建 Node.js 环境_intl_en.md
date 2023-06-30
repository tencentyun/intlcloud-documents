## Introduction
This article describes how to deploy Node.js on a CVM and create a sample project.

To do this, you need to be familiar with common Linux commands such as [Installing Software via YUM in a CentOS Environment](https://intl.cloud.tencent.com/document/product/213/2046) and understand the versions of the installed software.

## Software
Setting up Node.js involves:
- CentOS: a distribution of the Linux operating system. We use CentOS 7.6 in this article.
- Node.js: a JavaScript runtime environment. We use Node.js 10.16.3 and Node.js 6.9.5 in this article.
- npm: a package manager for JavaScript. We use npm 6.9.0 in this article to manage multiple Node.js versions.

## Prerequisites
To set up Node.js, you need a Linux CVM. If you have not purchased one yet, see [Getting Started with Linux CVMs](http://intl.cloud.tencent.com/document/product/213/2936).

## Directions
### Step 1: Logging in to a Linux instance
[Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux Instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)


### Step 2: Installing Node.js
1. Run the following command to download the Node.js 64-bit install package for Linux.
```
wget https://nodejs.org/dist/v10.16.3/node-v10.16.3-linux-x64.tar.xz
```
>Visit the [Node.js official website](https://nodejs.org/download/) for more information.
>
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
>This process allows you to install multiple Node.js versions. Developers can use this to quickly switch among versions.
>
1. Run the following command to install git.
```
yum install -y git
```
2. Run the following command to download the NVM source code and check for the newest version.
```
git clone https://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
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
The following appears:
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
    if (res.statusCode === 200) {
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello World\n');
}); 
server.listen(port, hostname, () => { 
    console.log(`Server running at http://${hostname}:${port}/`);
});
```
>This article uses port 7500 in the `index.js` file. You can use other ports as needed.
>
3. Press **Esc** and input **:wq** to save the file and go back.
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


## FAQ
If you encounter a problem when using CVM, refer to the following documents for troubleshooting based on your actual situation.
- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).

