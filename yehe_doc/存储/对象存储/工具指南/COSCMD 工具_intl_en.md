## Feature

COSCMD enables you to use simple command lines to batch-operate objects, such as upload, download, and delete.


## Operating Environment

#### System environment

Windows, Linux, and macOS

> ?
> - Local characters should use UTF-8 encoding. Otherwise, exceptions will occur when you operate on Chinese files.
> - Ensure that the local time is in sync with UTC. If there is a large deviation between the two, COSCMD might not function properly.

#### Software requirements

- Python 2.7/3.5/3.6/3.9
- Latest version of pip
>?You are advised to install the latest version of Python (3.9.0) that is integrated with pip.

#### Installation and configuration

- For more information about the installation and configuration of the environment, please see [Python](https://intl.cloud.tencent.com/document/product/436/10866).
- For more information about the installation and configuration of pip, please see [Installation](https://pip.pypa.io/en/stable/installing/).


## Download and Installation

You can install COSCMD in the following three ways:

#### 1.1 Installing with pip 

Run the `pip` command to install COSCMD:

```plaintext
pip install coscmd
```

 After the installation is complete, you can run the `-v` or `--version` command to view the version information.

#### 1.2 Upgrading with pip

After the installation is complete, you can run the following command to upgrade COSCMD:

```plaintext
pip install coscmd -U
```

> ! If the pip version number is greater than or equal to 10.0.0, a failure may occur when you are upgrading or installing dependent libraries. You are advised to use pip v9.x (pip install pip==9.0.0). If you have installed the latest Python version (for example, 3.9.0), pip has been integrated and does not need to be installed again.

#### 2. Installing with the source code (not recommended)

You can click [here](https://github.com/tencentyun/coscmd.git) to download the source code.

```plaintext
git clone https://github.com/tencentyun/coscmd.git
cd coscmd
python setup.py install
```

> !If your Python version is 2.6, installing the dependent libraries with pip may fail. Therefore, this installation method is recommended. 

#### 3. Installing from offline

> ! Ensure that the two devices are installed with the same version of Python. Otherwise, the installation might fail.

```sh
# Run the following commands on a device that is connected to the Internet
mkdir coscmd-packages
pip download coscmd -d coscmd-packages
tar -czvf coscmd-packages.tar.gz coscmd-packages

# Copy the installation package to a device that is not connected to the Internet and run the following commands
tar -xzvf coscmd-packages.tar.gz
pip install coscmd --no-index -f coscmd-packages
```

## Parameter Configuration

### Viewing the help option

You can run the `-h` or `--help` command to view the information and usage of COSCMD.

```plaintext
coscmd -h  // View information about the current version
```

The help information is as follows:

```plaintext
usage: coscmd [-h] [-d] [-b BUCKET] [-r REGION] [-c CONFIG_PATH] [-l LOG_PATH]
              [-v]
              
              {info,restore,createbucket,signurl,listparts,mget,list,upload,deletebucket,abort,getbucketversioning,putbucketacl,getobjectacl,download,putobjectacl,copy,config,putbucketversioning,getbucketacl,delete}
              ...

An easy-to-use but powerful command-line tool. Try 'coscmd -h' to get more
information. Try 'coscmd sub-command -h' to learn the usage of all commands, for example
'coscmd upload -h'

positional arguments:
  {info,restore,createbucket,signurl,listparts,mget,list,upload,deletebucket,abort,getbucketversioning,putbucketacl,getobjectacl,download,putobjectacl,copy,config,putbucketversioning,getbucketacl,delete}
    config              Config your information first
    upload              Upload file or directory to COS
    download            Download file from COS to local
    delete              Delete file or files on COS
    abort               Aborts upload parts on COS
    copy                Copy file from COS to COS
	move                move file from COS to COS
    list                List files on COS
    listparts           List upload parts
    info                Get the information of file on COS
    restore             Restore
    signurl             Get download url
    createbucket        Create bucket
    deletebucket        Delete bucket
    putobjectacl        Set object acl
    getobjectacl        Get object acl
    putbucketacl        Set bucket acl
    getbucketacl        Get bucket acl
    putbucketversioning
                        Set the versioning state
    getbucketversioning
                        Get the versioning state
	probe               Connection test

optional arguments:
  -h, --help            show this help message and exit
  -d, --debug           Debug mode
  -b BUCKET, --bucket BUCKET
                        Specify bucket
  -r REGION, --region REGION
                        Specify region
  -c CONFIG_PATH, --config_path CONFIG_PATH
                        Specify config_path
  -l LOG_PATH, --log_path LOG_PATH
                        Specify log_path
  -v, --version         show program's version number and exit
```

In addition, you can enter `-h` after each command (with no parameter appended) to see how to use the command. For example:

```plaintext
coscmd upload -h  // View how to use the upload command
```

### Basic configuration items

Certain parameters need to be configured before you use COSCMD. You can run the following commands for the configuration:

> ?In the following commands, fields enclosed in "[]" are optional, and those in "<>" are required.

```plaintext
coscmd config [OPTION]...<FILE>...
			  [-h] --help
			  [-a] <SECRET_ID>
			  [-s] <SECRET_KEY>
			  [-t] <TOKEN>
			  [-b] <BucketName-APPID>
              [-r] <REGION> | [-e] <ENDPOINT>
              [-m] <MAX_THREAD>
              [-p] <PART_SIZE>
              [--do-not-use-ssl]
              [--anonymous]   
```

The following table describes these parameters:

| Option | Parameter Description | Valid Value | Required |
| ---------------- | ------------------------------------------------------------ | ------ | -------- |
| -a | Key ID, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi) | String | Yes |
| -s | Key, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi) | String | Yes |
| -t | Temporary key token, which needs to be specified in the `x-cos-security-token` header when a temporary key is used. | String | No |
| -b | Name of the specified bucket, formatted as `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). If this is your first time using COSCMD, you need to create a bucket in the COS console to configure COSCMD. | String | Yes |
| -r | Region of the bucket. For more information, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| -e   | ENDPOINT of the request. Once configured, the `REGION` parameter will be invalidated. If you use the default endpoint, this parameter is formatted as `cos.<region>.myqcloud.com`; if you use a global acceleration endpoint, the format is `cos.accelerate.myqcloud.com`. | String | No  |
| -m | Maximum number of threads in a multi-thread operation (default: 5; value range: 1-30) | Number | No |
| -p | Size of the multipart upload part, in MB (default: 1; value range: 1-1000) | Number | No |
| --do-not-use-ssl | Uses the HTTP protocol instead of HTTPS | String | No |
| --anonymous | Anonymous operation (without carrying a signature) | String | No |

### Quick configuration

If you only need to perform basic operations, you can refer to the following operation example for a quick configuration.

>?Before the configuration, you need to go to the COS console to create a bucket (e.g., `configure-bucket-1250000000`) for parameter configuration and create a key.

```shell
coscmd config -a AChT4ThiXAbpBDEFGhT4ThiXAbp**** -s WE54wreefvds3462refgwewe**** -b configure-bucket-1250000000 -r ap-chengdu
```


### Modifying the configuration file

In the Windows OS, you can directly edit the `.cos.conf` file, which is hidden in **My Documents**. This file does not exist at first and is generated by the `coscmd config` command. You can also create it manually.

The file content of the configured `.cos.conf` file is as follows:
```plaintext
[common]
secret_id = AKIDA6wUmImTMzvXZNbGLCgtusZ2E8mG****
secret_key = TghWBCyf5LIyTcXCoBdw1oRpytWk****
bucket = configure-bucket-1250000000
region = ap-chengdu
max_thread = 5
part_size = 1
retry = 5
timeout = 60
schema = https
verify = md5
anonymous = False
```

>?
>- `schema` can be set to `http` or `https` (default).
>- `anonymous` can be set to `True` or `False`. If set to `True`, the anonymous mode is used (the signature is empty).
>- For more information about the parameter description, please run the `coscmd config -h` command.

## Common Bucket Commands

### Specifying a bucket and its region

If you do not specify the bucket and region in the commands, the commands take effect for the bucket that is used to configure COSCMD. To perform operations on another bucket, you need to specify the bucket and the region where the bucket resides.

>?
>- Use the `-b <BucketName-APPID>` parameter to specify the bucket name, which must be formatted as `BucketName-APPID`.
>- Use the `-r <region>` parameter to specify the region where the bucket resides.

```plaintext
#Command syntax
coscmd -b <BucketName-APPID> -r <region> <action> ...
#Example: Create a bucket named `examplebucket` that resides in the Beijing region.
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
#Example: Upload a file (picture.jpg) from D drive to the `examplebucket` bucket.
coscmd -b examplebucket-1250000000 -r ap-beijing upload D:/picture.jpg /
```

### Creating a bucket

>?Please specify `-b <BucketName-APPID>` and `-r <region>` when you run the `coscmd createbucket` command; otherwise, an error may be reported. This is because if the bucket and region are not specified, this command takes effect for the bucket that is used to configure COSCMD.

```plaintext
#Command syntax
coscmd -b <BucketName-APPID> createbucket
#Example: Create a bucket named `examplebucket` that resides in the Beiijng region.
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
```

### Deleting a bucket

>?`coscmd deletebucket` takes effect only for the bucket that is used to configure COSCMD. To delete another bucket, run the command with the `-b <BucketName-APPID>`and `-r <region>` parameters specified.

```plaintext
#Command syntax
coscmd -b <BucketName-APPID> deletebucket
#Example
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket -f
```

>!The `-f` parameter will forcibly delete the bucket, including all files, noncurrent folders (if versioning is enabled), and incomplete multipart uploads.


## Common Object Commands

### Uploading a file or folder

- The command for uploading a file is as follows:

```plaintext
#Command syntax
coscmd upload <localpath> <cospath>
#Example
#Upload picture.jpg in D drive to the "doc" directory of COS.
coscmd upload D:/picture.jpg doc/
#Upload picture.jpg in the "doc" folder in D drive to the "doc" directory of COS.
coscmd upload D:/doc/picture.jpg doc/
#Upload the file by specifying the header.
#Upload a file to the ARCHIVE storage class to the "doc" directory of COS.
coscmd upload D:/picture.jpg doc/ -H "{'x-cos-storage-class':'Archive'}"
#Configure the meta attribute.
coscmd upload D:/picture.jpg doc/ -H "{'x-cos-meta-example':'example'}"
```

- The command for uploading a folder is as follows:

```plaintext
#Command syntax
coscmd upload -r <localpath> <cospath>
#Example: Upload the "doc" folder in D drive to the root directory of COS.
coscmd upload -r D:/doc /
#Upload the folder to the "doc" directory of COS.
coscmd upload -r D:/doc doc
#Upload the folder synchronously while skipping those with the same MD5 value.
coscmd upload -rs D:/doc doc
#Upload the folder synchronously and delete files that are deleted in the "doc" folder in D drive.
coscmd upload -rs --delete D:/doc /
#Ignore uploading files whose extension is .txt or .doc in the "doc" folder in D drive.
coscmd upload -rs D:/doc / --ignore *.txt,*.doc
```



> !
> - Replace "localpath" and "cospath" enclosed in "<>" with the path of the local file to upload and the COS storage path, respectively.
> - If the file to upload is larger than 10 MB, COSCMD will upload with multipart upload. The command is `coscmd upload <localpath> <cospath>` (same as simple upload).
> - COSCMD supports checkpoint restart to resume the upload of large files. When the multipart upload of a large file fails, only the failed parts will be uploaded when the operation is resumed instead of starting over from scratch (please ensure that the directory and content of the re-uploaded file are consistent with the uploaded directory).
> - COSCMD performs MD5 verification on each part during multipart upload.
> - The `x-cos-meta-md5` header is included by default when COSCMD uploads a file, and its value is the same as the file’s MD5 value.
> - Use the `-s` parameter to upload files synchronously while skipping those with the same MD5 value (please note that the source files in COS must have been uploaded using COSCMD v1.8.3.2 or above; the `x-cos-meta-md5` header is included by default).
> - When you set the HTTP header with the `-H` parameter, please use the JSON format (for example, `coscmd upload -H "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more information about the headers, please see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).
> - When uploading folders, you can ignore certain types of files by using the `--ignore` parameter. Multiple shell wildcard rules (separated by commas `,`) are supported. To ignore a specified extension, `,` must be added at the end, or `""` must be used to enclose the extension.
> - Currently, a single file of up to 40 TB can be uploaded.


### Querying a file list

The query command is as follows:

```plaintext
#Command syntax
coscmd list <cospath>
#Example
coscmd list doc/
#Recursively query the file list, number of files, and the file sizes of a bucket.
coscmd list -ar
#Recursively query the list of all files prefixed with "examplefolder".
coscmd list examplefolder/ -ar
#Query the historical versions of all files in a bucket.
coscmd list -v
```

>?
>- Replace "cospath" enclosed in "<>" with the COS path of the file list to query. If `<cospath>` is empty, the root directory of the current bucket is queried.
>- Use `-a` to query all files.
>- Use `-r` to query files recursively. The number and total size of the files are listed at the end of the returned result.
>- Use `-n num` to set the maximum number of files to query.


### Viewing the file information

The command is as follows:

```plaintext
#Command syntax
coscmd info <cospath> 

#Example
coscmd info doc/picture.jpg
```

>?Replace "cospath" enclosed in "<>" with the COS path of the file to query.


### Downloading a file or folder

- The command for downloading a file is as follows:

```plaintext
#Command syntax
coscmd download <cospath> <localpath>
#Example
coscmd download doc/ D:/
coscmd download doc/folder/ D:/
#Download picture.jpg with a specified version ID to D drive.
coscmd download picture.jpg --versionId MTg0NDUxMzc2OTM4NTExNTg7Tjg D:/
```

- The command for downloading a folder is as follows:

```plaintext
#Command syntax
coscmd download -r <cospath> <localpath>
#Example
coscmd download -r doc D:/
coscmd download -r doc D:/folder/
#Download files in the root directory while ignoring those in the "doc" directory that is under the root directory.
coscmd download -r / D:/ --ignore doc/*
#Download all files in the root directory of the current bucket and overwrite local files.
coscmd download -rf / D:/examplefolder/
#Synchronously download all files in the root directory of the current bucket while skipping those with the same MD5 value.
coscmd download -rs / D:/examplefolder
#Synchronously download all files in the root directory of the current bucket and delete local files that have been deleted in cloud.
coscmd download -rs --delete / D:/examplefolder
#Ignore files with the .txt or .doc extension.
coscmd download -rs / D:/examplefolder --ignore *.txt,*.doc
```


> !
> - Replace "cospath" and "localpath" enclosed in "<>" with the COS path of the file to download and the local storage path, respectively.
> - Since the old `mget` API is no longer in use, please use the `download` API for multipart downloads.
> - If a file with the same name exists locally, the download will fail. In this case, you need to use the `-f` parameter to overwrite the local file.
> - Use the `-s` or `--sync` parameter to skip identical files that already exist locally when downloading a folder (provided that the downloaded files were uploaded via the COSCMD `upload` API and the `x- cos-meta-md5` header was included).
> - When downloading folders, you can ignore certain types of files by using the `--ignore` parameter. Multiple shell wildcard rules (separated by commas `,`) are supported. To ignore a specified extension, `,` must be added at the end, or `""` must be used to enclose the extension.


### Getting signed download URLs

The command is as follows:

```plaintext
#Command syntax
coscmd signurl <cospath>

#Example
coscmd signurl doc/picture.jpg
coscmd signurl doc/picture.jpg -t 100
```

>?
>- Replace "cospath" enclosed in "<>" with the COS path of the file for which you need to get the download URL.
>- Use `-t time` to set the effective period (in seconds) of the query signature.


### Deleting a file or folder

- The command for deleting a file is as follows:

```plaintext
#Command syntax
coscmd delete <cospath>
#Example
coscmd delete doc/exampleobject.txt
#Delete a file with a specified version ID.
coscmd delete doc/exampleobject.txt --versionId MTg0NDUxMzc4ODA3NTgyMTErEWN
```

- The command for deleting a folder is as follows:

```plaintext
#Command syntax
coscmd delete -r <cospath>
#Example
coscmd delete -r doc
coscmd delete -r folder/doc
#Delete all files with version IDs in the "doc" directory.
coscmd delete -r doc/ --versions
```

>?
>- Replace "cospath" enclosed in "<>" with the COS path of the file to delete. You will be prompted to confirm this operation.
>- You need to enter `y` to confirm a batch delete operation. You can skip this step if the `-f` parameter is used.
>- Note that the delete folder command will delete the current folder as well as the files in it. To delete a versioning-enabled file, you need to specify a version ID.


### Viewing incomplete multipart uploads

- The command is as follows:

```plaintext
#Command syntax
coscmd listparts <cospath>
#Example
coscmd listparts doc/
```

### Clearing incomplete multipart uploads

- The command is as follows:

```plaintext
#Command syntax
coscmd abort
#Example
coscmd abort
```

### Copying a file or folder

- The command for copying a file is as follows:

```plaintext
#Command syntax
coscmd copy <sourcepath> <cospath> 
#Example
#Intra-bucket replication: Copy picture.jpg in the `examplebucket-1250000000` bucket to the "doc" folder.
coscmd -b examplebucket-1250000000 -r ap-chengdu copy examplebucket-1250000000.ap-chengdu.myqcloud.com/picture.jpg doc/
#Cross-bucket replication: Copy doc/picture.jpg in the `examplebucket2-1250000000` bucket to doc/examplefolder/ in the `examplebucket1-1250000000` bucket.
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/
#Change the storage class of the file to STANDARD_IA.
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/ -H "{'x-cos-storage-class':'STANDARD_IA'}"
#Change the storage class of the file to ARCHIVE and rename it "photo.jpg".
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/photo.jpg -H "{'x-cos-storage-class':'Archive'}"
```

- The command for copying a folder is as follows:

```plaintext
#Command syntax
coscmd copy -r <sourcepath> <cospath>
#Example
#Copy the "examplefolder" directory in the `examplebucket2-1250000000` bucket to the "doc" directory in the `examplebucket1-1250000000` bucket.
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder doc/
```



> ?
> - Replace "sourcepath" and "cospath" enclosed in "<>" with the path of the COS file to copy and the COS destination path, respectively.
> - The source path is formatted as `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`.
> - Use the `-d` parameter to set the `x-cos-metadata-directive` header. Valid values are `Copy` (default) and `Replaced`.
> - When setting the HTTP header with the `-H` parameter, please use the JSON format (for example, `coscmd copy -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more information about the headers, please see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Moving a file or folder

- The command for moving a file is as follows:

```plaintext
#Command syntax
coscmd move <sourcepath> <cospath> 
#Example
#Intra-bucket movement: Move picture.jpg in the `examplebucket-1250000000` bucket to the "doc" directory.
coscmd -b examplebucket-1250000000 -r ap-chengdu move examplebucket-1250000000.ap-chengdu.myqcloud.com/picture.jpg doc/
#Cross-bucket movement: Move picture.jpg in the `examplebucket2-1250000000` bucket to doc/folder/ in the `examplebucket1-1250000000` bucket.
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/picture.jpg doc/folder/
#Change the storage class of the file to STANDARD_IA.
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/picture.jpg doc/folder/ -H "{'x-cos-storage-class':'STANDARD_IA'}"
#Change the storage class of the file to ARCHIVE.
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'Archive'}"
```

- The command for moving a folder is as follows:

```plaintext
#Command syntax
coscmd move -r <sourcepath> <cospath>
#Example
#Move the "examplefolder" directory in the `examplebucket2-1250000000` bucket to the "doc" directory in the `examplebucket1-1250000000` bucket.
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder doc/
```



> ?
> - Replace "sourcepath" and "cospath" enclosed in "<>" with the path of the COS file to move and the COS destination path, respectively.
> - The source path is formatted as `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`.
> - Use the `-d` parameter to set the `x-cos-metadata-directive` header. Valid values are `Copy` (default) and `Replaced`.
> - When setting the HTTP header with the `-H` parameter, please use the JSON format (for example, `coscmd move -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more information about the headers, please see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Setting object access permission

The command is as follows:
```plaintext
#Command syntax
coscmd putobjectacl --grant-<permissions> <UIN> <cospath>
#Grant account `100000000001` the read permission on picture.jpg.
coscmd putobjectacl --grant-read 100000000001 picture.jpg
#Query the file access permission.
coscmd getobjectacl picture.jpg
```

### Enabling/Suspending versioning

The command is as follows:

```plaintext
#Command syntax
coscmd putbucketversioning <status>
#Enable versioning.
coscmd putbucketversioning Enabled
#Suspend versioning.
coscmd putbucketversioning Suspended
#Query versioning.
coscmd getbucketversioning
```

> !
>- Replace "status" enclosed in "<>" with the desired versioning status.
>- Once versioning is enabled for the bucket, it cannot return to the prior status (initial status). However, you can suspend versioning for the bucket so that subsequent uploads of objects will not generate multiple versions.

### Restoring an ARCHIVED file

- The command is as follows:

```plaintext
#Command syntax
coscmd restore <cospath>
#Example
coscmd restore -d 3 -t Expedited picture.jpg
```

- The command for restoring ARCHIVED files in batches is as follows:

```plaintext
#Command syntax
coscmd restore -r <cospath>
#Example
coscmd restore -r -d 3 -t Expedited examplefolder/
```

>?
>- Replace "cospath" enclosed in "<>" with the COS path of the file list to query.
>- Use `-d <day>` to set the effective period of the temporary copy. Default value: `7`.
>- Use `-t <tier>` to specify the restoration mode. Enumerated values: `Expedited`, `Standard` (default), and `Bulk`.

### Running commands in debugging mode

If `-d` or `-debug` is added before a command, detailed operation information will be displayed when executing the command, as shown in the example below:

```plaintext
#Display upload details using a command in the following syntax:
coscmd -d upload <localpath> <cospath>

#Example
coscmd -d upload D:/picture.jpg /
```

## FAQ

If you have any questions about COSCMD, please see [COSCMD Tool](https://intl.cloud.tencent.com/document/product/436/30586).
