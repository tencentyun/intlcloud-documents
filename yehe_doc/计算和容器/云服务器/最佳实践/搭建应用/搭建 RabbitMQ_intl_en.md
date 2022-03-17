## Overview
RabbitMQ is an open-source message broker based on the Advanced Message Queuing Protocol (AMQP). It features usability, scalability, and high availability with an Erlang-programmed server, and supports multiple clients including Python, Ruby, .NET, Java, JMS, C, PHP, ActionScript, XMPP, STOMP, and AJAX. This document describes how to deploy RabbitMQ on Tencent Cloud CVM.

## Software
This document uses the following software as an example to deploy RabbitMQ:
- Linux: Linux operating system. This document uses CentOS 7.7 as an example.
- RabbitMQ Server: open-source message broker. This document uses RabbitMQ Server 3.6.9 as an example.
- Erlang: programming language. This document uses Erlang 19.3 as an example.


## Prerequisites
- You have purchased a Linux CVM.
- The security group rules for the Linux instance have already been configured. Open the ports 80, 5672 and 15672. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

## Directions
### Installing Erlang
1. [Log in to a Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:
	- [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
2. Run the following command to install dependencies.
```
yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
```
3. Run the following command to download the Erlang installation package.
```
wget http://erlang.org/download/otp_src_19.3.tar.gz
```
4. Run the following command to decompress the Erlang installation package.
```
tar xzf otp_src_19.3.tar.gz
```
5. Run the following command to create the erlang folder.
```
mkdir /usr/local/erlang
```
6. Run the following commands in sequence to compile and install Erlang.
```
cd otp_src_19.3
```
```
./configure --prefix=/usr/local/erlang --without-javac
```
```
make && make install
```
7. Run the following command to open the profile configuration file.
```
vi /etc/profile
```
8. Press **i** to enter the edit mode, and append the following at the end of the file.
```
export PATH=$PATH:/usr/local/erlang/bin
```
9. Press **Esc** and enter **:wq** to save and close the file.
10. Run the following command for the environment variable to take effect immediately.
```
source /etc/profile
```

### Installing RabbitMQ Server
1. Run the following command to download the RabbitMQ Server installation package.
```
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_9/rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
This document uses downloading RabbitMQ 3.6.9 from the RabbitMQ official website as an example. If the download link has expired, or if you want to use other RabbitMQ versions, go to [rabbitmq-server](https://github.com/rabbitmq/rabbitmq-server/releases) and learn more about the installation.
10. Run the following command to import the signature key.
```
rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
```
11. Run the following commands in sequence to install RabbitMQ Server.
```
cd
```
```
yum install rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
12. Run the following commands in sequence to enable RabbitMQ autostart and start RabbitMQ.
```
systemctl enable rabbitmq-server
```
```
systemctl start rabbitmq-server
```
13. Run the following command to delete the default guest account of RabbitMQ.
```
rabbitmqctl delete_user guest
```
14. <span id="Step6"></span>Run the following command to create an account.
```
rabbitmqctl add_user Username Password
```
15. Run the following command to set the new account as the admin account.
```
rabbitmqctl set_user_tags Username administrator
```
16. Run the following command to grant the admin account all permissions.
```
rabbitmqctl set_permissions -p / Username ".*" ".*" ".*"
```


### Verifying installation
1. Run the following command to open the Web management page of RabbitMQ.
```
rabbitmq-plugins enable rabbitmq_management
```
2. Open a browser and visit:
```
http://Instance public IP:15672
```
For more information about how to obtain the public IP address of the instance, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
If you see the following page, it indicates that RabbitMQ has been successfully installed.
![](https://main.qcloudimg.com/raw/aacb15db11b5cf80dd6b7ba1dc80d331.png)
3. Log in to RabbitMQ with the admin account created in [Step 6](#Step6) and access the RabbitMQ management page, as shown below:
![](https://main.qcloudimg.com/raw/7f8d24062541be6ba8b271483343b20a.png)

