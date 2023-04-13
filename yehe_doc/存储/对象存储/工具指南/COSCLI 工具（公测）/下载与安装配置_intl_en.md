COSCLI provides binary packages for Windows, macOS, and Linux, which can be used after simple installation and configuration.

## Download Address

| GitHub Address | Tencent Cloud Address                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Windows](https://github.com/tencentyun/coscli/releases/download/v0.13.0-beta/coscli-windows.exe) | [Windows](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-windows.exe) |
| [Mac](https://github.com/tencentyun/coscli/releases/download/v0.13.0-beta/coscli-mac) | [Mac](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-mac) |
| [Linux](https://github.com/tencentyun/coscli/releases/download/v0.13.0-beta/coscli-linux) | [Linux](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-linux) |

>? The current version is v0.13.0-beta. To get the latest and earlier versions and changelog of the tool, see [Releases](https://github.com/tencentyun/coscli/releases).

## Installation

### Windows

1. [Download COSCLI for Windows](https://github.com/tencentyun/coscli/releases/download/v0.13.0-beta/coscli-windows.exe).
2. Move the downloaded COSCLI executable file to the `C:\Users\<username>` directory.
3. Rename `coscli-windows.exe` to `coscli.exe`.
4. Press `Windows + R` to launch the `Run` program.
5. In the dialog box, enter `cmd` and press `Enter` to open the command line window.
6. Enter `coscli --version` in the command line window. If the following information is printed out, the installation is successful:
>? On Windows, the method for using COSCLI may vary slightly by command line client. If COSCLI does not work properly after `coscli [command]` is entered, try `./coscli [command]`.
>
```
coscli version v0.13.0-beta
```

### macOS

1. Run the following command to download COSCLI:
```bash
wget https://github.com/tencentyun/coscli/releases/download/v0.13.0-beta/coscli-mac
```
2. Run the following command to rename the file:
```bash
mv coscli-mac coscli
```
3. Run the following command to modify the file execution permission:
```bash
chmod 755 coscli
```
4. Enter the command line `./coscli --version`. If the following information is printed out, the installation is successful:
```
coscli version v0.13.0-beta
```
>? When you use COSCLI on macOS, if the `Unable to open "coscli" because the developer cannot be verified` prompt is displayed, go to `Settings > Security & Privacy > General` and select `Open COSCLI anyway`, and then COSCLI can be used properly.


### Linux

1. [Download COSCLI for Linux](https://github.com/tencentyun/coscli/releases/download/v0.13.0-beta/coscli-linux) or run the following command to download COSCLI:
```bash
wget https://github.com/tencentyun/coscli/releases/download/v0.13.0-beta/coscli-linux
```
2. Run the following command to rename the file:
```bash
mv coscli-linux coscli
```
3. Run the following command to modify the file execution permission:
```bash
chmod 755 coscli
```
4. Enter `./coscli --version` in the command line window. If the following information is printed out, the installation is successful:
```
coscli version v0.13.0-beta
```


## Parameter Configuration


>!
>- We recommend that you use the tool through a temporary key as instructed in [Generating and Using Temporary Keys](https://www.tencentcloud.com/document/product/436/14048) for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to limit the scope of permission on the permanent key.


When using COSCLI for the first time, you need to initialize the configuration file, which contains the following two parts:

1. To authorize COSCLI to access your Tencent Cloud account, you need to configure the secret ID, secret key, and temporary key token.
2. To add an alias for a common bucket, you need to configure its name, region, and alias. Then, you can use the alias to perform bucket operations without entering the bucket name and region information. After adding configurations for multiple common buckets, you can perform cross-bucket or cross-domain operations more easily. If you don't need to configure common bucket information, press `Enter` to skip.

COSCLI will automatically call `./coscli config init` to generate a configuration file in `~/.cos.yaml` when used for the first time. You can complete the configuration interactively on the command line. You can also run the `./coscli config init` command later to interactively generate a configuration file in another location. Then, you can use `./coscli config show` to view the location and parameter information of the configuration file.

The configuration items in the configuration file are as described below:

<span id="alias"></span>

| Configuration Item        | Description                                                         |
| ------------- | ------------------------------------------------------------ |
| Secret ID     | `SecretId`. We recommend that you use a sub-account key and follow the principle of least privilege to reduce risks. For more information on how to obtain a sub-account key, see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675). |
| Secret Key     | `SecretKey`. We recommend that you use a sub-account key and follow the principle of least privilege to reduce risks. For more information on how to obtain a sub-account key, see [Access Key](https://intl.cloud.tencent.com/document/product/598/32675). |
| Session Token | Temporary key token, which should be specified if a temporary key is used; otherwise, press `Enter` to skip it. For more information on temporary key, see [Accessing COS Using a Temporary Key](https://intl.cloud.tencent.com/document/product/436/45242). |
|  protocol   |  Network transfer protocol, which is HTTPS by default. If you want to change it to HTTP, directly modify it in the configuration file. |
| APPID        | `APPID` is the account you get after successfully registering your Tencent Cloud account. It is automatically assigned by the system and can be obtained from [Account Information](https://console.cloud.tencent.com/developer). The full name of a bucket consists of `Bucket Name` and `APPID` in the format of `<BucketName-APPID>`. For more information on bucket naming conventions, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). |
| Bucket Name   | Bucket name, which forms the full name of the bucket together with the `APPID` in the format of `<BucketName-APPID>`. For more information on bucket naming conventions, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). |
| Bucket Endpoint | Bucket endpoint in the format of `cos.<region>.myqcloud.com`, where `<region>` is the bucket region such as `ap-guangzhou` and `ap-beijing`. For the list of regions supported by COS, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). |
| Bucket Alias  | Bucket alias, which can be used to replace `BucketName-APPID` after configuration to shorten required commands. If it is not configured, its value will be the value of `BucketName-APPID`. |
| OFS Bucket | Metadata acceleration bucket flag, which indicates whether the [metadata acceleration](https://intl.cloud.tencent.com/document/product/436/43305) feature is enabled for the bucket. Currently, metadata acceleration is in free beta test. To try it out, [contact us](https://intl.cloud.tencent.com/contact-sales). You can check the [Message Center](https://console.cloud.tencent.com/message) or see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) to stay up to date with the latest billing plan.


COSCLI will ask you to configure the information of only one bucket during the initial configuration. If you want to configure multiple buckets, you can run the `./coscli config add` command later to add the information of more buckets. If you want to modify the configuration file or learn more about operations on the configuration file, see [Generating and Modifying Configuration Files - config](https://intl.cloud.tencent.com/document/product/436/43251) or run the `./coscli config --help` command to view commands related to the configuration file.

Before starting to use commands, you can quickly check how to use COSCLI by running the command `./coscli --help`.

### Other configuration methods

In addition to interactively generating a configuration file by running `./coscli config init`, you can also manually write a YAML configuration file for COSCLI as shown below:

```yaml
cos:
  base:
    secretid: XXXXXXXXXXXXXXX
    secretkey: XXXXXXXXXXXXXXXXX
    sessiontoken: ""
    protocol: https
  buckets:
  - name: examplebucket1-1250000000
    alias: bucket1
    region:       ap-shanghai
    endpoint: cos.ap-shanghai.myqcloud.com
    ofs: false
  - name: examplebucket2-1250000000
    alias: bucket2
    region: ap-guangzhou
    endpoint: cos.ap-guangzhou.myqcloud.com
    ofs: false
  - name: examplebucket3-1250000000
    alias: bucket3
    region: ap-chengdu
    endpoint: cos.ap-chengdu.myqcloud.com
    ofs: false
```


>! By default, COSCLI reads configuration items from `~/.cos.yaml`. If you want to use the custom configuration file, select `-c （--config-path）` after running commands. The strings (`secretid`/`secretkey`/`sessiontoken`) stored in the configuration file are encrypted.

