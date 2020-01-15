Here we use Python 2.7 as an example to demonstrate the installation and configuration of Python in Windows and Linux.

## Windows
### 1. Download
Go to the [Python official website](https://www.python.org/downloads/) and download an appropriate version. In this example, we download [Python 2.7.13](https://www.python.org/ftp/python/2.7.13/python-2.7.13.amd64.msi).
### 2. Install
Double click the Python installer package, and install Python as instructed.
### 3. Configure environment variables
After installation, right click **Computer**, click **Properties** -> **Advanced system settings** -> **Environment Variables** -> **System variables (S)** to find "Path" (if it does not exist, create one). Add the Python installation path `;C:\Python27` (change it to your installation path) to the end of "Variable value", and click **OK** to save.

### 4. Test whether the configuration is successful
Click **Start** (or shortcut: Win+R) -> **Run** (enter `cmd`) -> **OK** (or press Enter), enter the `Python` command in the pop-up window, and press Enter.

## Linux
### 1. Check the Python version 
Linux’s yum comes with Python. So check the default Python version first.
```
python -V
``` 
If it comes with Python 2.7 or above, ignore the following steps. Otherwise (for example, if it comes with Python 2.6.6), enter the following command:
```
yum groupinstall "Development tools"
```
### 2. Install the component used to compile Python
```
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel
```
### 3. Download and decompress Python 2.7 
```
wget https://www.python.org/ftp/python/2.7.12/Python-2.7.12.tar.xz
tar xf Python-2.7.12.tar.xz
```
### 4. Compile and install Python
```
cd Python-2.7.12 //Enter the directory
./configure –prefix=/usr/local
make && make install //Install
make clean 
make distclean
```
### 5. Direct the system Python command to Python 2.7
```
mv /usr/bin/python /usr/bin/python2.6.6
ln -s /usr/local/bin/python2.7 /usr/bin/python
```
### 6. Test whether the configuration is successful
```
python
```
If the following message appears, Python 2.7 is installed and configured successfully:
![112046](//mc.qcloudimg.com/static/img/0eb560566c1f67e302e75b1dcb515d98/image.png)
> <font color="#0000cc">**Note:**</font>
If permission-related errors occur, try to add sudo before command.
