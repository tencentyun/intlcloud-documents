## Overview
GitLab is a Ruby-based open-source version management system. It provides the code management tool Git and the self-hosted Git repository to support your Web access to public and private projects. This document describes how to install and use GitLab on Tencent Cloud CVM.



## Software
- GitLab: Community Edition 14.6.2 
- The CVM instance used in this document needs to be configured with:
	- vCPU: 2 cores
	- Memory: 4 GB
	- Linux operating system: this document uses CentOS 8.2 and 7.9 as an example.

## Prerequisites
- You have purchased a Linux CVM instance.
- The security group rules for the Linux instance have already been configured. Open the port 80. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

## Directions
### Installing GitLab
1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command based on the operating system to install the dependency package:
<dx-tabs>
::: CentOS 8.2
```
yum install -y curl policycoreutils-python-utils openssh-server
```
:::
::: CentOS 7.9
```
yum install -y curl policycoreutils-python openssh-server
```
:::
</dx-tabs>
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
7. Press **i** to enter the editing mode. Delete `#` before `inet_interfaces = all`, and add `#` before `inet_interfaces = localhost`, as shown below: 
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
For more information about how to obtain the public IP address of the instance, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
12. In a local browser, visit the public IP address that you have obtained. If the following page appears, GitLab has been installed successfully.
<img src="https://qcloudimg.tencent-cloud.cn/raw/abaf3b700a58ed5b4a1e13e9d82eaf7e.png"/>


### Setting admin account password
1. Get the default password of the admin account.
 Log in to the instance and run the following command to get the login password of the `root` admin account:
```
cat /etc/gitlab/initial_root_password
```
Get the password as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/01bfa701452cc470fbdbfb82ab294237.png)
2. Log in to GitLab.
In the local browser, access the public IP of your CVM instance to enter the GitLab login page. Enter your `root` account and the obtained password.
3. Change the admin account password.
As the file saving the default password will be deleted automatically 24 hours after GitLab runs with the first configuration, change the login password of the `root` account as soon as possible.
 1. Select the user profile photo in the top-right corner of the page and select **Preferences** in the pop-up menu.
 2. On the **User Settings** page, select **Password** on the left sidebar.
 3. Enter the currently used and new passwords for confirmation on the page and click **Save Password** as shown below:
 ![](https://qcloudimg.tencent-cloud.cn/raw/25adb5b68d48873392684d1a1030bbe1.png)

### Creating projects
1. Log in with the `root` account and set login password.
2. Create a private project as instructed. This document uses `test` as an example in the following figure:
![](https://qcloudimg.tencent-cloud.cn/raw/a6d85a83b86a44c1f39dbd363a3311ce.png)
3. After creating the project successfully, click **Add SSH Key** in the prompt at the top of the page.
4. On the **SSH Keys** page, add a SSH key by performing the following steps:
 1. [Get the key](#getKey) for the PC to be managed by the project and paste it in the `Key` field.
 2. Enter the key name in the `Title` field.
 3. Click **Add key** to add a key as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/504b7a69215471516f7ace36bb5606af.png)
If the result is similar to the following figure, the key has been added successfully:
![](https://qcloudimg.tencent-cloud.cn/raw/2d46dcb48b51243ce4fc91b319b3ede3.png)
5. [](id:Step5)Return to the project homepage and click **Clone** to record the project address as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9edb130321b5df140cfc863c73f6837d.png)


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
git clone "Project address"
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
git push
```
Go back to the test project page. You can now see the file on the page, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0440c9a53b3a93d056119fd47f39638e.png)

## Related Operations
### Getting key[](id:getKey)
1. On the PC to be managed by the project, run the following command to install Git.
```
yum install -y git
```
2. Run the following command to generate the key file ".ssh/id_rsa". During the key file generation process, press **Enter** to keep the default configurations.
```
ssh-keygen
```
3. Run the following command to view and record the key information.
```
cat .ssh/id_rsa.pub
```
