## Introduction
This article describes how to set up a Java Web environment on a Linux CVM.

This requires you to be familiar with common Linux commands, such as [Installing Software via YUM in a CentOS Environment](https://intl.cloud.tencent.com/document/product/213/2046), and understand the versions of the installed software.

## Software
These are the software involved:
- CentOS is a distribution of the Linux operating system. We use CentOS 7.6 in this article.
- Apache Tomcat provides a "pure Java" HTTP web server environment in which Java code can run. We use Apache Tomcat 8.5.47.
- JDK, or Java Development Kit, is an implementation of the Java Platform. We use JDK 1.8.0_221 in this article.


## Prerequisites
Setting up a Java Web environment requires a Linux CVM. If you have not purchased one yet, see [Getting Started with Linux CVMs](http://intl.cloud.tencent.com/document/product/213/2936).

## Directions
### Step 1: Logging in to a Linux instance
- [Log in to a Linux instance using WebShell (recommended)](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are comfortable with:
- [Log in to a Linux instance using remote login software](https://intl.cloud.tencent.com/document/product/213/32502).
- [Log in to a Linux Instance using SSH](https://intl.cloud.tencent.com/document/product/213/32501)


### Step 2: Installing JDK
1. Download the JDK installation file. Go to the [Java SE download page](https://www.oracle.com/technetwork/java/javase/downloads/index.html) to select a version and download it.
>Download the JDK file, save it locally, and upload it to your CVM. Otherwise, decompressing the file will result in errors.
> - If you are using Windows, use [WinSCP](https://intl.cloud.tencent.com/document/product/213/2131) to upload the file.
> - If you are using MacOS or Linux, use [SCP](https://intl.cloud.tencent.com/document/product/213/2133) to upload the file.
>
2. Run the following command to create a directory for JDK installation.
```
mkdir /usr/java
```
3. Run the following command to decompress JDK to the directory.
```
tar xzf jdk-8u221-linux-x64.tar.gz -C /usr/java
```
4. Run the following command to open `profile`.
```
vim /etc/profile
```
5. Press **i** to enter edit mode. Start a new line after `export PATH USER ...` and add the following:
```
export JAVA_HOME=/usr/java/jdk1.8.0_221 (replace 1.8.0_221 with your JDK version number)
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```
The result should be as follows:
![](https://main.qcloudimg.com/raw/a4d0466eca6c4c0ef219f571b7d165de.png)
6. Press **Esc** and input **:wq** to save the file and go back.
7. Run the following command to read system environment variables.
```
source /etc/profile
```
8. Run the following command to check if JDK is installed properly.
```
java -version
```
If the following appears, the installation was successful.
![](https://main.qcloudimg.com/raw/f12cfeed5d8aa15cccb9836637e9555f.png)

### Step 3: Installing Tomcat
1. Run the following command to download Tomcat source codes. Select a version that suits you.
>Refer to the [Apache Tomcat official website](https://tomcat.apache.org/) for more information.
>
```
wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.47/bin/apache-tomcat-8.5.47.tar.gz
```
2. Run the following command to decompress the file.
```
tar xzf apache-tomcat-8.5.47.tar.gz
```
3. Run the following command to move the directory that contains Tomcat to `/usr/local/tomcat/`.
```
mv apache-tomcat-8.5.47 /usr/local/tomcat/
```
4. Run the following command to open `server.xml`.
```
vim /usr/local/tomcat/conf/server.xml
```
5. Find `<Host … appBase="webapps”>` and press **i** to enter edit mode. Replace `appBase="webapps"` with the following:
```
appBase="/usr/local/tomcat/webapps"
```
6. Press **Esc** and input **:wq** to save the file and go back.
7. Run the following command to create a file named `setenv.sh`.
```
vi /usr/local/tomcat/bin/setenv.sh
```
8. Press **Enter** to enter edit mode and input the following to set JVM memory variables.
```
JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8' 
```
9. Press **Esc** and input **:wq** to save the file and go back.
10. Run the following command to start Tomcat.
```
/usr/local/tomcat/bin/startup.sh
```
If the following appears, Tomcat has been successfully started.
![](https://main.qcloudimg.com/raw/64bdd25e734db46464655f15acae4c2f.png)

## Verifying the Environment Configuration
1. Run the following command to create a test file.
```
echo Hello World! > /usr/local/tomcat/webapps/ROOT/index.jsp
```
2. Open a browser window on your local machine and visit the following URL to check whether the environment configuration was successful.
```
http://[Public IP address of the CVM instance]:8080
```
If the following results appear, the environment configuration was successful.
![](https://main.qcloudimg.com/raw/359b7119e9e7d81e2e2728dabd57456a.png)

## FAQ
If you encounter a problem when using CVM, refer to the following documents for troubleshooting based on your actual situation.
- For issues about CVM login, see [Password Login and SSH Key Login](https://intl.cloud.tencent.com/document/product/213/18120) and [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
- For issues about the CVM network, see [IP Addresses](https://intl.cloud.tencent.com/document/product/213/17285) and [Ports and Security Groups](https://intl.cloud.tencent.com/document/product/213/2502).
- For issues about CVM disks, see [System and Data Disks](https://intl.cloud.tencent.com/document/product/213/17351).
