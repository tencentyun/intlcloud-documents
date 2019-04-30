## Introduction

All the tools and demos are stored in the [Github repository](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/OOTB-XML).

This document introduces user's application server and user's application client.

## Setting Up a User's Application Server
In this example, the user's application server only provides a temporary key. "cos\_signer\_lite" is a temporary key service based on the flask service framework and is written in python3. You can run it on your own machine or virtual machine to provide the temporary key service for your COS terminal (Android/iOS) SDK.
>!This project is only used for demonstration and cannot be used in a production environment. You can use the temporary key API of the COS server SDK in a production environment.

### Configure the environment

"cossign" only supports Python3. It provides you with a temporary key service, and you can install it directly using the pip command.
```
pip3 install cossign
```

### Enable the service
After the installation is completed, you can execute the following command to enable the temporary key service.
```
cossign --secret_id your_secret_id --secret_key your_secret_key --port 5000
```
>?The default port is 5000. You are not required to specify a port when executing the command.
>The key information can be found in the [Cloud API Key Console](https://console.cloud.tencent.com/cam/capi).


### Test the service
You can test the service by accessing `http://your_server_ip:5000/sign` in a browser or executing the following command.
```
curl http://your_server_ip:5000/sign
```    
If the following result is returned, the service has run successfully.
```
{
 "code":0,
 "message":"",
 "codeDesc":"Success",
 "data":{
  "credentials":{
   "sessionToken":"634aa09dccc3274045ba413ec081c1df64007f0a30001",
   "tmpSecretId":"AKIDwxHZGTUvXAfcbLaOedJUQuwBXWUXG4m3",
   "tmpSecretKey":"kriDdZsOuuF9zrZPlSAVVG0Sg4RXZu6M"},
  "expiredTime":1530515889}
 }
```

### Troubleshooting guide
If an error occurs during the creation of a temporary key, refer to the following guide for troubleshooting.
1. **Problem:** `comment not found pip3` is reported while running the installation command `pip3 install flask`.    
**Analysis:** Python 3 is not installed, or the installation path of Python 3 is not correctly set.
**Solution:** Install Python 3 based on your system, or check the path settings.

2. **Problem:** After the service is started, the error `URLError: urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed` is reported while obtaining a temporary key.
**Solution:** This problem is common in MAC OS X system. You can install the certifi module. For more information, see [Stack Overflow FAQ](https://stackoverflow.com/questions/27835619/urllib-and-ssl-certificate-verify-failed-error/42334357#42334357).

## Setting Up a User's Application Client
### Configure the client
Modify the file QCloudCOSXMLDemo/QCloudCOSXMLDemo/TestCommonDefine.h, enter the APPID and the deployed address used to obtain the temporary key, and then execute the following command.
```
pod install
```
After executing the command, open QCloudCOSXMLDemo.xcworkspace to view the Demo.
### Run the Demo
#### Query the bucket list and create a bucket
1. All the available regions are displayed after the demo App is opened, as shown below.    
![](https://main.qcloudimg.com/raw/c7cdd4171e7ab4314299df399954942c.png)

2. Select a region, and all the buckets in the region under the current account are displayed, as shown below.  
![](https://main.qcloudimg.com/raw/9dae084c02f2e19cc6682588cada1e28.png)

You can also create a bucket under the current region by tapping the **Create Bucket** button in the upper right corner, as shown below. 
![](https://main.qcloudimg.com/raw/fefd8a545c2a0924d3d60722b8d2affb.png)


#### Upload a file
You can conduct an upload test by tapping **Photos** -> **Upload** -> **Pause** -> **Resume** -> **Cancel** at the bottom in turn, as shown below. 
![](https://main.qcloudimg.com/raw/7050892158c428a9c5470eb472680844.png)

#### Download a file
Go to the download interface, and all the files in the current bucket are displayed. Tap **Download** to have a test, as shown below.
![](https://main.qcloudimg.com/raw/25fc6b09c7b6f3da7f1a427ecabb4ecb.png)

