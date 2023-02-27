## Feature Overview

COS FTP Server allows you to directly operate on COS objects and directories over FTP protocol, including uploading/downloading/deleting files and creating folders. This tool is developed with Python, which makes the installation easier.

## Feature Overview

**Upload mechanism**: streaming without saving uploaded files locally. It works as long as the working directory is configured using the standard FTP protocol, and no actual disk storage capacity is occupied.
**Download mechanism**: the downloaded file is directly streamed and returned to the client.
**Directory mechanism**: bucket serves as the root directory of the entire FTP Server, and multiple subdirectories can be created under a bucket.
**Binding to multi-buckets**: multiple buckets can be bound at the same time.
>? Binding to multi-buckets: Multiple buckets can be bound via different FTP Server working paths (`home_dir`). Therefore, ensure a unique `home_dir` is assigned to each bucket and user.
>
**Restriction on deletion**: the `delete_enable` option can be configured for each FTP user in the new FTP Server to identify whether the FTP user is allowed to delete files.
**Supported FTP commands:** `put`, `mput`, `get`, `rename`, `delete`, `mkdir`, `ls`, `cd`, `bye`, `quite`, and `size`.
**Unsupported FTP commands:** `append` and `mget` (The native `mget` command is not supported, but batch download is allowed on certain Windows clients, such as the FileZilla client.)

>? The FTP Server tool does not support checkpoint restart.
>

## Getting Started

#### Operating system

- OS: Linux. The [CVM](https://www.tencentcloud.com/document/product/213) of Tencent CentOS series is recommended. Windows systems are not supported for now.
- psutil-dependent Linux package: python-devel or python-dev, depending on the names of different Linux distributions. It is added using Linux package manager, such as `yum install python-devel` or `aptitude install python-dev`.
- Python interpreter version: Python 2.7. For more information on the installation and configuration, see [Python](https://intl.cloud.tencent.com/document/product/436/10866).
>? FTP Server does not support Python 3.
>
- Dependent packages:
 - [cos-python-sdk-v5](https://pypi.org/project/cos-python-sdk-v5/) (≥1.6.5)
 - [pyftpdlib](https://pypi.org/project/pyftpdlib/) (≥1.5.2)
 - [psutil](https://pypi.org/project/psutil/) (>=5.6.1)


#### Use restrictions

Applicable to COS XML version.

#### Installation and Operation

Download the FTP Server tool at [cos-ftp-server](https://github.com/tencentyun/cos-ftp-server-V5). The installation steps are as follows:

1. Enter the FTP Server directory, and run `setup.py` to install FTP Server and its dependent libraries (network required).
```bash
python setup.py install   # Your account should use sudo or have the root permission.
```
2. Copy the configuration sample file `conf/vsftpd.conf.example` and name it `conf/vsftpd.conf`. See [Configuration File](#conf) of this document to correctly configure bucket and user information.
3. Run `ftp_server.py` to start FTP Server.
```bash
python ftp_server.py
```
FTP Server can also be started in the following two ways:
 - Execute the `nohup` command to start it in the backend process:
```bash
nohup python ftp_server.py >> /dev/null 2>&1 &
```
 - Execute the `screen` command to run it at the backend (you need to install the screen tool):
```bash
screen -dmS ftp
screen -r ftp
python ftp_server.py
#Use the keyboard shortcut Ctrl + A + D to go back to the main screen.
```

#### Stop Operation

- If FTP Server is running directly or running at the backend with the `screen` command, you can stop it with the shortcut key combination `Ctrl+C`. 
- If FTP Server is started with the `nohup` command, you can stop it by the following way:
```bash
ps -ef | grep python | grep ftp_server.py | grep -v grep | awk '{print $2}' | xargs -I{} kill {}
```


<a id="conf"></a>
## Configuration File

The configuration sample file for FTP Server is `conf/vsftpd.conf.example`. Copy and name it vsftpd.conf, and then configure it as follows:
```conf
[COS_ACCOUNT_0]
cos_secretid = COS_SECRETID    # Replaced with your SECRETID
cos_secretkey = COS_SECRETKEY  # Replaced with your SECRETKEY
cos_bucket = examplebucket-1250000000
cos_region = region   # Replaced with your bucket region
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user0      # Replaced with the local path you want the FTP to mount to (which should be an actual existing path but not a soft link)
ftp_login_user_name=user0   # Replaced with a custom username
ftp_login_user_password=pass0   # Replaced with a custom password
authority=RW                # The user’s read and write permissions. R: read; W: write; RW: both.
delete_enable=true # true allows the FTP user to delete files by default; false prohibits the user to delete files.

[COS_ACCOUNT_1]
cos_secretid = COS_SECRETID    # Replaced with your SECRETID
cos_secretkey = COS_SECRETKEY  # Replaced with your SECRETKEY
cos_bucket = examplebucket-1250000000
cos_region = region   # Replaced with your bucket region
cos_protocol = https
#cos_endpoint = region.myqcloud.com
home_dir = /home/user1     # Replaced with the local path you want the FTP to mount to (which should be an existing path but not a soft link)
ftp_login_user_name=user1   # Replaced with a custom username
ftp_login_user_password=pass1   #Replaced with a custom password
authority=RW                # The user’s read and write permissions. R: read; W: write; RW: both.
delete_enable=false # true allows the FTP user to delete files by default; false prohibits the user to delete files.

[NETWORK]
# If the FTP Server is behind a gateway or NAT, you can use this section to specify the gateway's IP address or domain name as the FTP Server’s IP address.
masquerade_address = XXX.XXX.XXX.XXX
# The listening port for FTP Server is 2121 by default. Please note that your WAF needs to ALLOW this port (for example, if you deploy FTP Server on a Tencent Cloud CVM, you need to ALLOW this port in your CVM security group.)
listen_port = 2121			
# `passive_port` sets the available port range in Passive mode, with a default of [60000, 65535]. Note that your WAF (such as CVM security group) needs to ALLOW this range.
passive_port = 60000,65535      


[FILE_OPTION]
# By default, the maximum size of a single file is 200 G. We do not recommend going beyond the limit.
single_file_max_size = 21474836480

[OPTIONAL]
# For the following settings, take the default settings unless otherwise needed. Fill in an appropriate integer if necessary.
min_part_size       = default
upload_thread_num   = default
max_connection_num  = 512
max_list_file       = 10000                # The maximum number of files to be listed by `ls` command. It is not recommended to go beyond this limit. Otherwise, high latency of `ls` command will occur.
log_level           = INFO                 # Set the log output level.
log_dir             = log                  # Set the directory to store logs. Default: `log` under the `FTP Server` directory.
```


>?
>- To bind each user to a unique bucket, simply add the `[COS_ACCOUNT_X]` section.
The section for each `COS_ACCOUNT_X` is described as follows:
> - The username (`ftp_login_user_name`) and the home directory (`home_dir`) under each account must be unique, and the home directory must be a directory that exists in the system.
> - The number of users logging in to each COS FTP Server simultaneously cannot exceed 100.
> - `endpoint` and `region` will not take effect at the same time. To use the public cloud COS service, enter the `region` field correctly. The `endpoint` is commonly used in the privatized deployment environment. When both 'region` and `endpoint` are entered, `endpoint` will take precedence.
>- The OPTIONAL part in the configuration file is used to adjust the upload performance for advanced users. You can obtain an optimal uploading speed by reasonably adjusting the part size and the number of concurrent upload threads based on the server performance. General users can keep the default settings without adjustment.
Meanwhile, the limit option for the maximum number of connections is provided. If you do not want to set a limit to it, enter 0, meaning no limit to the maximum number of connections (a reasonable evaluation is required based on your server performance).
>- Generally, for the `masquerade_address` section in your configuration file, we recommend you specify the IP address that your client is using to connect to the COS FTP Server. If you have any questions, please see the FAQs about [FTP Server](https://intl.cloud.tencent.com/document/product/436/30588).
> - Assume that the FTP Server has more than one IP address, and after running the `ifconfig` command, you get a private ENI IP `10.xxx.xxx.xxx`, which is mapped to the public IP `119.xxx.xxx.xxx`. At this time, if the FTP Server does not explicitly set `masquerade_address` to the public IP (119.xxx.xxx.xxx) that the client uses to access the server, the FTP Server in Passive mode may use the private IP (10.xxx.xxx.xxx) to return packets to the client. As a result, the client is able to connect to the FTP Server, but cannot return data packets to the client properly. Therefore, generally speaking, we recommend you to set `masquerade_address` to the IP address that your client is using to connect to the Server.
>- In the configuration file, `listen_port` sets the listening port for the COS FTP Server, and is defaulted to 2121. `passive_port` sets the range of data channel listening ports for the COS FTP Server, and is defaulted to [60000, 65535]. When your client connects to the COS FTP Server, ensure that your WAF allows the ports configured in these two sections.

## Quick Practice

### Accessing COS FTP Server using Linux `ftp` command

1. Install the Linux FTP client.
```sh
yum install -y ftp
```
2. Open the Linux command line, and use the command `ftp [ip address] [port No.]` to connect to the COS FTP Server. Example:
```sh
ftp 192.xxx.xx.103 2121
```
 - In the `ftp` command, the IP field corresponds to the **masquerade_address** section in the sample configuration file `conf/vsftpd.conf.example`. In this example, the IP is set to `192.xxx.xx.103`.
 - In the `ftp` command, the port field corresponds to the **listen_port** section in the sample configuration file `conf/vsftpd.conf.example`. In this example, the port is set to `2121`.
3. Run the above command, and you can see **Name** and **Password** to be entered. Copy and paste the contents of the `ftp_login_user_name` and `ftp_login_user_passwordthe` sections for COS FTP Server, and the connection will succeed.
 - **Name**: Corresponds to **ftp_login_user_name** (requires configuration) in the sample configuration file `conf/vsftpd.conf.example`.
 - **Password**: Corresponds to **ftp_login_user_password** (requires configuration) in the sample configuration file `conf/vsftpd.conf.example`.

### Accessing COS FTP Server using FileZilla

1. Download and install [FileZilla client](https://filezilla-project.org/).
2. After configuring the access information for COS FTP Server on your FileZilla client, click **Quick Connect**.
 - **Host (H):** corresponds to **masquerade_address** in the sample configuration file `conf/vsftpd.conf.example`. In this example, the IP is set to `192.xxx.xx.103`.
>!If the COS FTP Server is behind a gateway or NAT, you can use this section to specify the gateway's IP address or domain name as the Server’s IP address.
 - **Username (U)**: Corresponds to **ftp_login_user_name** (requires configuration) in the sample configuration file `conf/vsftpd.conf.example`.
 - **Password (W):** Corresponds to **ftp_login_user_password** (requires configuration) in the sample configuration file `conf/vsftpd.conf.example`.
 - **Port (P):** Corresponds to **listen_port** in the sample configuration file `conf/vsftpd.conf.example`. In this example, the port is set to `2121`.



## FAQs

If any error occurs or you have any question on the upload limit while using FTP Server, see [FTP Server FAQs](https://intl.cloud.tencent.com/document/product/436/30588).
