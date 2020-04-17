## Overview

All the tools and demos are stored in the [GitHub repository](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/OOTB-XML). This document describes the user application server and user application client separately:

## Setting up a User's Application Server
In this example, the user's application server only provides a temporary key. `cos\_signer\_lite` is a temporary key service based on the flask service framework and is written in Python 3. You can run it on your own machine or CVM instance to provide the temporary key service for your COS SDK for Android/iOS.
>This project is only used for demonstration and cannot be used in a production environment. You can use the temporary key API of the COS server SDK in a production environment.

### Configuring the environment

`cossign` only supports Python 3. It provides you with a temporary key service, and you can install it directly by using the pip command.
```sh
pip3 install cossign
```

### Start the service
After the installation is completed, you can run the following command to enable the temporary key service.
```sh
cossign --secret_id your_secret_id --secret_key your_secret_key --port 5000
```

>
>- The default port is 5000. You are not required to specify a port when running the command.
>- The key information can be found in the [TencentCloud API Key Console](https://console.cloud.tencent.com/cam/capi).


### Testing the service
You can test the service by visiting `http://your_server_ip:5000/sign` in a browser or running the following command.
```sh
curl http://your_server_ip:5000/sign
```
If the following result is returned, the service has run successfully.
```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success",
	"data": {
		"credentials": {
			"sessionToken": "634aa09dccc3274045ba413ec081c1df64007f0a30001",
			"tmpSecretId": "AKIDwxHZGTUvXAfcbLaOedJUQuwBXWUXG4m3",
			"tmpSecretKey": "kriDdZsOuuF9zrZPlSAVVG0Sg4RXZu6M"
		},
		"expiredTime": 1530515889
	}
}
```

### Troubleshooting guide
If an error occurs during the creation of a temporary key, please refer to the following guide for troubleshooting.
1. **Problem:** `comment not found pip3` is displayed when I run the installation command `pip3 install flask`.    
**Analysis:** Python 3 is not installed, or the installation path of Python 3 is not correctly set.
**Solution:** Install Python 3 based on your system version or check the path settings.

2. **Problem:** After the service is started, the error `URLError: urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed` is displayed when I try to get a temporary key.
**Solution:** This problem is common on macOS X. You can install the `certifi` module. For more information, please see [Stack Overflow FAQ](https://stackoverflow.com/questions/27835619/urllib-and-ssl-certificate-verify-failed-error/42334357#42334357).

## Setting up a User's Application Client
### Configuring the client
Modify the `QCloudCOSXMLDemo/QCloudCOSXMLDemo/TestCommonDefine.h` file, enter the `APPID` and the deployed address used to get the temporary key, and then run the following command.
```sh
pod install
```
After running the command, open `QCloudCOSXMLDemo.xcworkspace` to view the demo.

### Running the demo
#### Querying the bucket list and creating a bucket
1. All the available regions are displayed after the demo application is opened .    
2. Select a region and all the buckets in the region under the current account will be displayed.  
You can also create a bucket in the current region by tapping **Create Bucket** in the top-right corner. 


#### Uploading a file
You can conduct an upload test by tapping **Photos** -> **Upload** -> **Pause** -> **Resume** -> **Cancel** at the bottom in turn. 

#### Downloading a file
Go to the download page and all the files in the current bucket will be displayed. Tap **Download** to have a test.
