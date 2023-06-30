## Scenario
Ghost is a free and open source blogging platform written in JavaScript and distributed under the MIT License, designed to simplify the process of online publishing for individual bloggers as well as online publications. This article describes how to setup Ghost on a CVM. 

To setup Ghost, you should be familiar with Linux and its common commands, such as [Install Software via Apt-get under Ubuntu Environment](https://intl.cloud.tencent.com/document/product/213/2123).

## Software
This article uses the following software:
- Linux operating system. This article uses Ubuntu 20.04.
- Nginx 1.18.0 is used to provide web service.
- MySQL 8.0.25 is used for database.
- Node.js 14.17.0 is our runtime environment.
- Ghost 4.6.4


##  Prerequisites
You should have a Linux CVM. If you have not purchased one yet, see [Getting Started with Linux CVMs](http://intl.cloud.tencent.com/document/product/213/2936).
- A domain name that points to your CVM. If the domain name is used for Mainland China service, ICP filing is required.



## Directions

### Step 1 Logging in to a Linux instance
- [Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Logging In to a Linux Instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Step 2 Create a new user
1. After logging in, switch to `root`. Refer to [this article](https://intl.cloud.tencent.com/document/product/213/17278) for details.
2. Run the following command to create a user named `user`.
>Do not use `ghost` as the username. It causes conflicts with Ghost-CLI. 
>
```
adduser user
```
 1. Input and confirm password as prompted. Password is not shown by default. Press **Enter** to continue.
 2. Input user information. Or press **Enter** to skip them and continue.
 3. Input **Y** to confirm and press **Enter** to complete the process, as shown below:
 ![](https://main.qcloudimg.com/raw/66ca399607b89f2653668eb4b0cb71f5.png)
3. Run the following command to add user privileges.
```
usermod -aG sudo user
```
4. Run the following command to switch to user `user`.
```
su user
```

### Step 3 Update installed packages
Run the following commands to update installed packages.
>Input the password for `user` as prompted and press **Enter** to start.
>
```
sudo apt-get update
```
```
sudo apt-get upgrade -y
```

### Step 4 Environment setup
#### Install Nginx
Run the following command to install Nginx.
```
sudo apt-get install -y nginx 
```

#### Install and configure MySQL
1. Run the following command to install MySQL.
```
sudo apt-get install -y mysql-server 
```
2. Run the following command to connect to MySQL.
```
sudo mysql
```
3. <span id="database"></span>Run the following command to create a database for Ghost named `ghost_data`.
```
CREATE DATABASE ghost_data;
```
4. <span id="sercet"></span>Run the following command to set a password for the database user `root`.
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
```
5. Run the following command to quit MySQL.
```
\q
```

#### Install Node.js
1. Run the following command to set a default Node.js version to be used.
```
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash
```
2. Run the following command to install Node.js.
```
sudo apt-get install -y nodejs
```

#### Install Ghost-CLI
Run the following command to install Ghost-CLI which helps configuring Ghost.
```
sudo npm install ghost-cli@latest -g
```

### Step 5 Install and configure Ghost
1. Run the following commands.
```
sudo mkdir -p /var/www/ghost
```
```
sudo chown user:user /var/www/ghost
```
```
sudo chmod 775 /var/www/ghost
```
```
cd /var/www/ghost
```
2. Run the following command to install Ghost.
```
ghost install
```
3. Use the following image to complete the installation process.
![](https://main.qcloudimg.com/raw/6c3a3b9d083dfb253285f47d81e928b5.png)
 1. **Enter your blog URL**: input your domain name in the format of `http://your_domain_name`.
 2. **Enter your MySQL hostname**: input your database address. Use `localhost` in this case and press **Enter**.
 3. **Enter your MySQL username**: input the username you use to connect to MySQL. Use `root` in this case and press **Enter**.
 4. **Enter your MySQL password**: input the corresponding password you set [earlier](#secret) and press **Enter**.
 5. **Enter your database name**: input the name of the database you created for Ghost [in the previous step](#database). Use `ghost_data` and press **Enter**.
 6. Input **Y** or **n** to complete the configuration.
 The admin URL appears on the bottom of the screen.
4. Open a browser window on your local machine and visit the admin URL to start configuring your blog.
Click **Create your account** to create an admin account.
![](https://main.qcloudimg.com/raw/e2eeacd71eec4c27660eeb4797f83f2a.png)
5. Input desired information and click **Last step**, as shown below:
![](https://main.qcloudimg.com/raw/a7a81f16b811bdceeb429116ee23081c.png)
6. You can invite others to create blogs, or skip this step.
7. Go to the administration page to manage blogs, as shown below: 
![](https://main.qcloudimg.com/raw/fd9071dba9748ce8125f8597be0d248a.png)
Once finished, use a browser to visit your domain name `www.xxxxxxxx.xx` to see your blog, as shown below:
![](https://main.qcloudimg.com/raw/055decab4524eb9f2f5602fbd0502c7c.png)

## FAQ
If you encounter a problem when using CVM, refer to the following documents for troubleshooting based on your actual situation.
- For issues regarding CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues regarding the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues regarding CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).
