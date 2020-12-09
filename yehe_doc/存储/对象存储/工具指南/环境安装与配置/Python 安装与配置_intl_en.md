This document uses Python 2.7.13 as an example to demonstrate how to install and configure Python in Windows and Linux.


## Windows 
#### 1. Download
Go to the [Python official website](https://www.python.org/downloads/) and download an appropriate version. In this example, we download [Python 2.7.13](https://www.python.org/ftp/python/2.7.13/python-2.7.13.amd64.msi).

#### 2. Install
Double click the Python installer package, and install Python as instructed.

#### 3. Configure environment variables
(1) Once Python is installed, restart your computer as instructed.
(2) Right-click on the "Computer" or "My Computer" desktop icon, and select **Properties** > **Advanced system settings** > *Environment Variables*. In **System variables**, locate **Path**, or click **New** to create a variable named as such.
(3) Click **Edit** > **Edit Text**, and add `;C:\Python27` (replace it with your own Python installation path) to the end of the “Path”.
(4) Click **OK**.


#### 4. Test whether the configuration is successful
Click **Start** (or shortcut: Win+R) > **Run** (enter `cmd`) > **OK** (or press Enter), enter the Python command in the pop-up window, and press Enter. If Python version information appears, Python 2.7 has been installed successfully.

## Linux
#### 1. Check the Python version 
Linux’s yum comes with Python, so check the default Python version first.
```sh
python -V
```
If it comes with Python 2.7 or above, ignore the following steps. Otherwise (for example, if it comes with Python 2.6.6), enter the following command:
```plaintext
yum groupinstall "Development tools"
```

#### 2. Install the component used to compile Python
```sh
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel
```

#### 3. Download and decompress Python 2.7 
```sh
wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tar.xz
tar xf Python-2.7.12.tar.xz
```

#### 4. Compile and install Python
```plaintext
cd Python-2.7.12 //Enter the directory
./configure -prefix=/usr/local
make && make install //Install
make clean 
make distclean
```

#### 5. Direct the Python command to Python 2.7
```shell
mv /usr/bin/python /usr/bin/python2.6.6
ln -s /usr/local/bin/python2.7 /usr/bin/python
```

#### 6. Test whether the configuration is successful
```sh
python
```
If the information appears as shown below, Python 2.7 has been installed successfully.
![112046](//mc.qcloudimg.com/static/img/0eb560566c1f67e302e75b1dcb515d98/image.png)

>!If permission problems occur, try to add `sudo` to the beginning of your command.