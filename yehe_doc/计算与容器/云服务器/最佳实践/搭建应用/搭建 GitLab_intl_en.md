## Overview
GitLab is a Ruby-based open-source version management system. It provides the code management tool Git and the self-hosted Git repository to support your Web access to public and private projects. This document describes how to install and use GitLab on Tencent Cloud CVM.



## Software
The CVM instance needs to be configured with:
- vCPU: 2 cores
- Memory: 4 GB
- Linux operating system: this document uses CentOS 7.7 as an example

## Prerequisites
- A Linux CVM is required to install GitLab. If you have not purchased a Linux CVM yet, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
- The security group rules for the Linux instance have already been configured. Open the port 80. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

## Directions
### Installing GitLab
1. See [Log in to Linux Instances Using the Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:
 - [Log in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Log in to Linux Instances via a SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
2. Run the following command to install dependencies.
```
yum install -y curl policycoreutils-python openssh-server
```
3. Run the following commands in sequence to enable SSH service autostart and start the SSH service.
```
systemctl enable sshd
```
```
systemctl start sshd
```
4. Run the following command to install Postfix.
```
yum install -y postfix
```
5. Run the following command to enable Postfix service autostart.
```
systemctl enable postfix
```
6. Run the following command to open Postfix’s configuration file main.cf.
```
vim /etc/postfix/main.cf
```
7. Press  **i** to enter the editing mode. Delete `#` before `inet_interfaces = all`, and add `#` before `inet_interfaces = localhost`, as shown below: 
![](https://main.qcloudimg.com/raw/57fa73bdcd05343b5dcee24e47b5f09a.png)
8. Press **Esc** and enter **:wq** to save and close the file.
9. Run the following command to start Postfix.
```
systemctl start postfix
```
10. Run the following command to add the GitLab software repository.
```
 curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```
11. Run the following command to install GitLab.
```
sudo EXTERNAL_URL="Public IP address of the instance" yum install -y gitlab-ce
```
For more information about how to obtain the public IP of the instance, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
12. In a local browser, visit the public IP address that you have obtained. If the following page appears, GitLab has been installed successfully.
>!Configure the password for your GitLab account here.
>
![](https://main.qcloudimg.com/raw/791f5250c2bca059369a141c047f2c21.png)


### Creating projects
1. In a local browser, visit the public IP address of your CVM to access the GitLab login page. Enter your `root` account and the configured password, as shown below:
![](https://main.qcloudimg.com/raw/c0639741b40c1fa33d41434c0222c13b.png)
2. Create a private project as instructed. This document uses `test` as an example in the following figure:
![](https://main.qcloudimg.com/raw/912805dfffcba06558d3adbe8b33b4bc.png)
3. After the project is created, click **Add SSH Key** at the top of the page.
4. On the **SSH Keys** page, add a SSH key by performing the following steps:
 1. [Get the key](#getKey) for the PC to be managed by the project and paste it in the `Key` field.
 2. Enter the key name in the `Title` field.
 3. Click **Add key** as shown below:
![](https://main.qcloudimg.com/raw/c8d21821f0d6919a650cf36d43666f06.png)
If the result is similar to the following figure, the key has been added successfully:
![](https://main.qcloudimg.com/raw/6908a9710bd01d57c01892b31247bc02.png)
5. <span id="Step5"></span>On the project homepage, click **clone** to record the project address, as shown below:
![](https://main.qcloudimg.com/raw/972726ec33e5a92c0a778a700ae9b4b0.png)


### Cloning projects
1. Run the following command on the managed PC to configure the username of the Git repository.
```
git config --global user.name "username" 
```
2. Run the following command to configure the email for the username.
```
git config --global user.email "xxx@example.com" 
```
3. Run the following command to clone the project. Replace the project address with the actual values obtained in [Step 5](#Step5).
```
git clone “Project address”
```
After the project is successfully cloned, the same directory and all project files will be generated on your local computer.

### Uploading files
1. Run the following command to access the project directory.
```
cd test/
```
2. Run the following command to create the target file to be uploaded to GitLab. This document uses the test.sh file as an example.
```
echo "test" > test.sh
```
3. Run the following command to add the test.sh file to the index.
```
git add test.sh
```
4. Run the following command to submit the test.sh to the local repository.
```
git commit -m "test.sh"
```
5. Run the following command to synchronize the test.sh file with the GitLab server.
```
git push -u origin master
```
Go back to the test project page. You can now see the file on the page, as shown below:
![](https://main.qcloudimg.com/raw/e208c7a0f7399e4a42a1bb3d17a89c1c.png)

## Relevant Operations
### Getting the key<span id="getKey"></span>
1. On the PC to be managed by the project, run the following command to install Git.
```
yum install -y git
```
2. Run the following command to generate the key file “.ssh/id_rsa”. During the key file generation process, press **Enter** to keep the default configurations.
```
ssh-keygen
```
3. Run the following command to view and record the key information.
```
cat .ssh/id_rsa.pub
```
