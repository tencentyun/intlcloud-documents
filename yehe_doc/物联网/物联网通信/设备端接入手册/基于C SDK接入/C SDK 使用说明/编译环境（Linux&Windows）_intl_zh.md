## Linux（Ubuntu）环境

>?本文演示使用 Ubuntu 的版本为16.04。

1. **必要软件安装**
SDK 需要 cmake 版本在3.5以上，默认安装的 cmake 版本较低，若编译失败，请单击 [下载](https://cmake.org/download/) 并参考 [安装说明](https://gitlab.kitware.com/cmake/cmake) 进行 cmake 特定版本的下载与安装。
```
$ sudo apt-get install -y build-essential make git gcc cmake
```
2. **配置修改**
修改 SDK 根目录下的 CMakeLists.txt 文件，并确保以下选项存在（以密钥认证设备为例）：
```
set(BUILD_TYPE                   "release")
set(COMPILE_TOOLS                "gcc") 
set(PLATFORM 	                "linux")
set(FEATURE_MQTT_COMM_ENABLED ON)
set(FEATURE_AUTH_MODE "KEY")
set(FEATURE_AUTH_WITH_NOTLS OFF)
set(FEATURE_DEBUG_DEV_INFO_USED  OFF)  
```
3.  **执行脚本编译**
 1. 完整编译库和示例如下：
```
./cmake_build.sh 
```
 2. 输出的库文件，头文件及示例在`output/release`文件夹中。
在一次完整编译之后，若只需要编译示例，则执行以下代码：
```
./cmake_build.sh samples
```
4. **填写设备信息**
将在腾讯云物联网平台创建的设备的设备信息（以密钥认证设备为例），填写到 SDK 根目录下 device_info.json 中，示例代码如下：
```
"auth_mode":"KEY",	
"productId":"S3EUVBQAZW",
"deviceName":"test_device",	
"key_deviceinfo":{    
    "deviceSecret":"vX6PQqazsGsMyf5SMfs6OA6y"
}
```
5. **运行示例**
示例输出位于`output/release/bin`文件夹中，例如运行 data_template_sample 示例，输入`./output/release/bin/data_template_sample`即可。


## Windows 环境

#### 获取和安装 Visual Studio 2019开发环境

1. 请访问 [Visual Studio 下载网站](https://visualstudio.microsoft.com/zh-hans/downloads/)，下载并安装 Visual Studio 2019，本文档下载安装的是16.2版本 Community。
![](https://main.qcloudimg.com/raw/394078661873f4464e7c2bf2836aa6a2.png)
2. 选择【使用 C++ 的桌面开发】，并确保勾选【用于 Windows 的 C++ CMAKE 工具】。
![](https://main.qcloudimg.com/raw/2c5ea21e32ed3a6375d41370c6b521d9.png)

#### 编译并运行

1. 运行 Visual Studio，选择【打开本地文件夹】，并选择下载的 C SDK 目录。
![](https://main.qcloudimg.com/raw/94a3bbcf421836a46198a0413003ff2c.png)
2. 将在腾讯云物联网通信控制台创建的设备的设备信息（以密钥认证设备为例），填写到 device_info.json 中，示例代码如下：
```
"auth_mode":"KEY",	
"productId":"S3EUVBQAZW",
"deviceName":"test_device",	
"key_deviceinfo":{    
    "deviceSecret":"vX6PQqazsGsMyf5SMfs6OA6y"
}
```
3. 双击打开根目录的 CMakeLists.txt，并确认编译工具链中设置的平台为 **Windows** 和编译工具为 **MSVC**。
![](https://main.qcloudimg.com/raw/d4ef02feb3304c99dbfb02fe37996870.png)
```cmake
# 编译工具链
   #set(COMPILE_TOOLS "gcc") 
   #set(PLATFORM 	  "linux")
    
   set(COMPILE_TOOLS "MSVC") 
   set(PLATFORM 	  "windows")
```
4. Visual Studio 会自动生成 cmake 缓存，请等待 cmake 缓存生成完毕。
![](https://main.qcloudimg.com/raw/e32548904810ed92ecd52cd5803d23ff.png)
5. 缓存生成完毕后，选择【生成】>【全部生成】。
![](https://main.qcloudimg.com/raw/8afc803e904f2e06eaa8948d1a8c1b81.png)
6. 选择相应的示例运行，示例应与用户信息相对应。
![](https://main.qcloudimg.com/raw/c02877b0975625858b9fe51cb9c4114c.png)

