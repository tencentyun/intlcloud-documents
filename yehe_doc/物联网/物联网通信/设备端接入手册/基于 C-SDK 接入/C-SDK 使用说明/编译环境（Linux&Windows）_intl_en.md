## Linux (Ubuntu)

>?The Ubuntu version used for demonstration in this document is v16.04.

1. **Install the necessary software**
The SDK requires CMake v3.5 or above. The CMake version installed by default is low. If compilation fails, [download](https://cmake.org/download/) and install the specific version of CMake as instructed in [Installation Instructions](https://gitlab.kitware.com/cmake/cmake).
```
$ sudo apt-get install -y build-essential make git gcc cmake
```
2. **Modify the configuration**
Modify the `CMakeLists.txt` file in the root directory of the SDK and make sure that the following options exist (with a key-authenticated device as example):
```
set(BUILD_TYPE                   "release")
set(COMPILE_TOOLS                "gcc") 
set(PLATFORM 	                "linux")
set(FEATURE_MQTT_COMM_ENABLED ON)
set(FEATURE_AUTH_MODE "KEY")
set(FEATURE_AUTH_WITH_NOTLS OFF)
set(FEATURE_DEBUG_DEV_INFO_USED  OFF)  
```
3. **Run the script for compilation**
 1. Below is a complete compilation library and demo:
```
./cmake_build.sh 
```
 2. The output library files, header files, and samples are in the `output/release` folder.
After the complete compilation, if you only need to compile the demo, then run the following code:
```
./cmake_build.sh samples
```
4. **Enter the device information**
Enter the information of the device created on the IoT Hub platform (with a key-authenticated device as example) in `device_info.json` in the root directory of the SDK. Below is the sample code:
```
"auth_mode":"KEY",	
"productId":"S3EUVBQAZW",
"deviceName":"test_device",	
"key_deviceinfo":{    
    "deviceSecret":"vX6PQqazsGsMyf5SMfs6OA6y"
}
```
5. **Run the demo**
The demo output is in the `output/release/bin` folder. For example, to run the `data_template_sample` demo, enter `./output/release/bin/data_template_sample`.


## Windows

#### Getting and installing Visual Studio 2019

1. Download [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/) and install it. In this document, the downloaded and installed version is v16.2 Community.
![](https://main.qcloudimg.com/raw/2fd5a35c66683b62f09a93575ad29036.png)
2. Select **Desktop development with C++** and **C++ CMake tools for Windows**.
![](https://main.qcloudimg.com/raw/45914188fe5b51fc8b89cca7d9d03f02.png)

#### Compilation and running

1. Run Visual Studio, select **Open a local folder**, and select the downloaded SDK for C directory.
![](https://main.qcloudimg.com/raw/b245adf8ccfe14f78c862d62516ec3c8.png)
2. Enter the information of the device created in the IoT Hub console (with a key-authenticated device as example) in `device_info.json`. Below is the sample code:
```
"auth_mode":"KEY",	
"productId":"S3EUVBQAZW",
"deviceName":"test_device",	
"key_deviceinfo":{    
    "deviceSecret":"vX6PQqazsGsMyf5SMfs6OA6y"
}
```
3. Double-click `CMakeLists.txt` in the root directory and make sure that the platform is set to **Windows** and the compilation tool is set to **MSVC** in the compilation toolchain.
![](https://main.qcloudimg.com/raw/d4ef02feb3304c99dbfb02fe37996870.png)
```cmake
# Compilation toolchain
   #set(COMPILE_TOOLS "gcc") 
   #set(PLATFORM 	  "linux")
    
   set(COMPILE_TOOLS "MSVC") 
   set(PLATFORM 	  "windows")
```	 
4. Visual Studio will automatically build the CMake cache. Just wait for the build to complete.
![](https://main.qcloudimg.com/raw/52f0f35974ad0503b6f45a09f69420ac.jpg)
5. After the cache is generated, select **Build** > **Build All**.
![](https://main.qcloudimg.com/raw/dc985f71fdb4b882ce2d12d01c5b7e73.png)
6. Select the corresponding demo for running, which should correspond to the user information.
![](https://main.qcloudimg.com/raw/5c3f0fe31182b8dc7b805ce7578ae0ad.jpg)

