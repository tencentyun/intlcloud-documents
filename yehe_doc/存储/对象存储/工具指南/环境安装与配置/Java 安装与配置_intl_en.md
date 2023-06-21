Java Development Kit (JDK) is the SDK for Java. This document takes JDK 1.7 and 1.8 as examples to describe how to install and configure JDK under Windows and Linux systems.

## Windows

#### 1. Downloading a JDK

Go to the [Oracle  website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to download the desired JDK version.

#### 2. Installation

Install the JDK as instructed. You can specify the installation paths (C drive by default), for example, as `D:\Program Files\Java\jdk1.8.0_31` and `D:\Program Files\Java\jre1.8.0_31`.

#### 3. Configuration

After the installation is completed, right-click **Computer**, and then click **Properties** > **Advanced system settings** > **Environment Variables** > **System variables** > **New** to configure the software.
Variable name (N): **JAVA_HOME**   
Variable value (V): `D:\Program Files\Java\jdk1.8.0_31` (Configure according to your actual installation path).

Variable name (N): **CLASSPATH**   
Variable value (V): `.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;` (Note that the variable value begins with `.`).
Variable name (N): **Path**
Variable value (V): `%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`
#### 4. Testing
Test whether the configuration is successful: click **Start** (or shortcut: Win+R) > **Run** (enter `cmd`) > **OK** (or press Enter), then enter the command `javac` and press Enter. If messages such as command parameters and syntax are displayed, the environment variables are configured successfully.


## Linux
If openjdk is installed by using yum or apt-get command, the class library may be incomplete, thus leading to errors when you run relevant tools after the installation. Therefore, we recommend that you manually decompress and install JDK. Specific steps are as follows:

#### 1. Download a JDK
Go to the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  to download the desired JDK version to install.
>!The following uses `jdk-8u151-linux-x64.tar.gz` as an example. If you are using other versions, ensure that the extension is `.tar.gz`.

#### 2. Create a directory 

Run the following command to create the `java` directory in /usr/:
```shell
mkdir /usr/java
cd /usr/java 
```
Copy the downloaded `jdk-8u151-linux-x64.tar.gz` to the /usr/java/ directory. 

#### 3. Decompress the JDK

Run the following command to decompress the JDK:
```shell
tar -zxvf jdk-8u151-linux-x64.tar.gz 
```

#### 4. Set environment variables

Edit the /etc/profile file. Add the following content to the profile file and save it:
```shell
# set java environment
JAVA_HOME=/usr/java/jdk1.8.0_151        
JRE_HOME=/usr/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH 
```
>!`JAVA_HOME` and `JRE_HOME` should be configured according to the actual installation paths and JDK version.

Run the following command for the modifications to take effect:
```shell
source /etc/profile 
```

#### 5. Test
Run the following command to test the JDK installation:
```sh
java -version
```

If information about the Java version is displayed, the JDK is installed successfully.
```shell
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```
