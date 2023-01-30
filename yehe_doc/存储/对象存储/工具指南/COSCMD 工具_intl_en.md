
## Feature Overview

COSCMD enables you to use simple command lines to batch-operate objects, such as upload, download, and delete.


## Operating Environments

#### Operating system

Windows, Linux, and macOS

> ?
> - Local characters should use UTF-8 encoding. Otherwise, exceptions will occur when you operate on Chinese files.
> - Ensure that the local time is in sync with UTC. If there is a large deviation between the two, COSCMD might not function properly.

#### Software dependency

- Python 2.7/3.5/3.6/3.9
- Latest version of pip
>?You are advised to install the latest version of Python (3.9.0) that is integrated with pip.

#### Installation and configuration

- For more information about the installation and configuration of the environment, see [Python](https://intl.cloud.tencent.com/document/product/436/10866).
- For more information about the installation and configuration of pip, see [Installation](https://pip.pypa.io/en/stable/installation/).


## Download and Installation

You can install COSCMD in the following three ways:

#### 1.1 Installing with pip 

Run the `pip` command to install COSCMD:
```plaintext
pip install coscmd
```
After the installation is complete, you can run the `-v` or `--version` command to view the version information.
>! After installing COSCMD in Windows, you need to add the `C:\python_install_dir` and `C:\python_install_dir\Scripts` paths to environment variables. 

#### 1.2 Upgrading with pip

After the installation is complete, you can run the following command to upgrade COSCMD:
```plaintext
pip install coscmd -U
```

#### 2. Installing with the source code (not recommended)

You can click [here](https://github.com/tencentyun/coscmd.git) to download the source code.

```plaintext
git clone https://github.com/tencentyun/coscmd.git
cd coscmd
python setup.py install
```

>!If your Python version is 2.6, installing the dependent libraries with pip may fail. Therefore, this installation method is recommended. 

#### 3. Installing from offline

>! Ensure that the two devices are installed with the same version of Python. Otherwise, the installation might fail.

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

Run the `-h` or `--help` command to view the information and usage of COSCMD.
```plaintext
coscmd -h  
```
The help information is as follows:
```plaintext
usage: coscmd [-h] [-d] [-s] [-b BUCKET] [-r REGION] [-c CONFIG_PATH]
              [-l LOG_PATH] [--log_size LOG_SIZE]
              [--log_backup_count LOG_BACKUP_COUNT] [-v]
              {config,upload,download,delete,abort,copy,move,list,listparts,info,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl,putbucketversioning,getbucketversioning,probe}
              ...

an easy-to-use but powerful command-line tool. try 'coscmd -h' to get more
informations. try 'coscmd sub-command -h' to learn all command usage, likes
'coscmd upload -h'

positional arguments:
  {config,upload,download,delete,abort,copy,move,list,listparts,info,restore,signurl,createbucket,deletebucket,putobjectacl,getobjectacl,putbucketacl,getbucketacl,putbucketversioning,getbucketversioning,probe}
    config              Config your information at first
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
  -s, --silence         Silence mode
  -b BUCKET, --bucket BUCKET
                        Specify bucket
  -r REGION, --region REGION
                        Specify region
  -c CONFIG_PATH, --config_path CONFIG_PATH
                        Specify config_path
  -l LOG_PATH, --log_path LOG_PATH
                        Specify log_path
  --log_size LOG_SIZE   specify max log size in MB (default 1MB)
  --log_backup_count LOG_BACKUP_COUNT
                        specify log backup num
  -v, --version         show program's version number and exit
```
In addition, you can enter `-h` after each command (with no parameter appended) to see how to use the command. For example:
```plaintext
coscmd upload -h  // View how to use the upload command
```

### Generating a configuration file

COSCMD will first read the necessary information from the configuration file before running. By default, COSCMD will read configuration items from `~/.cos.conf`.

>? Before the configuration, you need to go to the COS console to create a bucket (e.g., `configure-bucket-1250000000`) for parameter configuration and create a key.

The following is a sample configuration file:
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
>- `anonymous` can be set to `True` or `False`. If it is set to `True`, the anonymous mode is used (the signature is empty).
>- For more information about the parameter description, run the `coscmd config -h` command.
>

### Generating a configuration file via the `config` command



>!
>- We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.



You can run the `config` command to automatically generate a configuration file in `~/.cos.conf`. The command format is as follows:
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

>? Fields enclosed in "[]" are optional, and those in "<>" are required.
>

The parameters are described as follows:

| Option | Parameter Description | Valid Value | Required |
| ---------------- | ------------------------------------------------------------ | ------ | -------- |
| -a | Key ID, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi) | String | Yes |
| -s | Key, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi) | String | Yes |
| -t | Temporary key token, which needs to be specified in the `x-cos-security-token` header when a temporary key is used. | String | No |
| -b | Name of the specified bucket, formatted as `BucketName-APPID`. For more information, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). If this is your first time using COSCMD, you need to create a bucket in the COS console to configure COSCMD. | String | Yes |
| -r | Region of the bucket. For more information, see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224). | String | Yes |
| -e   | Endpoint of the request. Once you configure this parameter, the region parameter will be invalidated. If you use the default endpoint, this parameter is formatted as `cos.<region>.myqcloud.com`; if you use a global acceleration endpoint, the format is `cos.accelerate.myqcloud.com`. | String | No  |
| -m | Maximum number of threads in a multi-thread operation (default: 5; value range: 1-30) | Number | No |
| -p | Size of the multipart upload part, in MB (default: 1; value range: 1-1000) | Number | No |
| --do-not-use-ssl | Uses the HTTP protocol instead of HTTPS | String | No |
| --anonymous | Anonymous operation (without carrying a signature) | String | No |

The following sample shows how to use the `config` command:

```shell
coscmd config -a AChT4ThiXAbpBDEFGhT4ThiXAbp**** -s WE54wreefvds3462refgwewe**** -b configure-bucket-1250000000 -r ap-chengdu
```

## Common Commands

### Specifying a bucket and its region

If you do not specify the bucket and region in the commands, the commands take effect for the bucket that is used to configure COSCMD. To perform operations on another bucket, you need to specify the bucket and the region where the bucket resides.

>?
> - Use the `-b <BucketName-APPID>` parameter to specify the bucket name, which must be formatted as `BucketName-APPID`.
> - Use the `-r <region>` parameter to specify the region where the bucket resides. 

- Command syntax
```plaintext
coscmd -b <BucketName-APPID> -r <region> <action> ...
```
- Sample: creating a bucket named `examplebucket` that resides in the Beijing region
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
```
- Sample: uploading “picture.jpg” from D drive to the `examplebucket` bucket
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing upload D:/picture.jpg /
```

### Specifying the configuration file and log file paths

If you do not specify the configuration file path, `~/.cos.conf` will be used by default. Similarly, if you do not specify the log file path, `~/.cos.log` will be used by default.

>?
> - Use the `-c <conf_path>` parameter to specify the configuration file path. COSCMD will read configuration information from the path when running.
> - Use the `-l <log_conf>` parameter to specify the log file path. COSCMD will output the logs generated at runtime to the log files in the path.
>

- Command syntax
```plaintext
coscmd -c <conf_path> -l <log_conf> <action> ...
```
- Sample: setting the configuration file’s path to `/data/home/cos_conf` and the log path to `/data/home/cos_log`, and creating a bucket named `examplebucket` in the Beijing region
```plaintext
coscmd -c /data/home/cos_conf -l /data/home/cos_log -b examplebucket-1250000000 -r ap-beijing createbucket
```


### Running commands in debugging mode

If `-d` or `-debug` is added before a command, detailed operation information will be displayed when executing the command, as shown in the example below:

- Command syntax
```plaintext
coscmd -d upload <localpath> <cospath>
```

- Sample: outputting detailed information upon the upload
```plaintext
coscmd -d upload -rs D:/folder/ /
```

### Running commands in silence mode

You can prefix `-s` or `--silence` in each command so that no message will be output.

>?To run this command, the version should be at least 1.8.6.24.

- Command syntax
```plaintext
coscmd -s upload <localpath> <cospath>
```
- Sample:
```plaintext
coscmd -s upload D:/picture.jpg /
```

## Common Bucket Commands

### Creating a bucket

>?Specify `-b <BucketName-APPID>` and `-r <Region>` when you run the `coscmd createbucket` command; otherwise, an error may be reported. This is because if the bucket and region are not specified, this command takes effect for the bucket that is used to configure COSCMD.

- Command syntax
```plaintext
coscmd -b <BucketName-APPID> createbucket
```
- Sample: creating a bucket named `examplebucket` that resides in the Beijing region
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
```

### Deleting a bucket

>? `coscmd deletebucket` takes effect only for the bucket that is used to configure COSCMD. To delete another bucket, run the command with the `-b <BucketName-APPID>` and `-r <region>` parameters specified.

- Command syntax
```plaintext
coscmd -b <BucketName-APPID> deletebucket
```
- Sample: deleting empty buckets
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket
```
- Sample: forcibly deleting a non-empty bucket
```plaintext
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket -f
```
>! The `-f` parameter will forcibly delete the bucket, including all files, noncurrent folders (if versioning is enabled), and incomplete multipart uploads.

## Common Object Commands

### Uploading files

- Command syntax for uploading a file
```plaintext
coscmd upload <localpath> <cospath>
```
>! Replace "localpath" and "cospath" enclosed in "<>" with the path of the local file to upload and the COS storage path, respectively.
>
- Sample: uploading “picture.jpg” in D drive to the "doc" folder of COS
```plaintext
coscmd upload D:/picture.jpg doc/
```
- Sample: uploading “picture.jpg” in the "doc" folder in D drive to the "doc" folder of COS
```plaintext
coscmd upload D:/doc/picture.jpg doc/
```
- Sample: uploading a file to the ARCHIVE storage class to the "doc" directory of COS
```plaintext
coscmd upload D:/picture.jpg doc/ -H "{'x-cos-storage-class':'Archive'}"
```
>! When you set the HTTP header with the `-H` parameter, please use the JSON format, for example, `coscmd upload -H "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more information about the headers, see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).
>
- Sample: setting meta attributes and uploading a file to the “doc” folder of COS
```plaintext
coscmd upload D:/picture.jpg doc/ -H "{'x-cos-meta-example':'example'}"
```


### Uploading a folder

- Command syntax for uploading a folder
```plaintext
coscmd upload -r <localpath> <cospath>
```
>! Windows users are advised to use the `upload` command in cmd or PowerShell that comes with the system. Other tools, such as Git Bash, have a different command path resolution strategy than PowerShell and can cause users' files to be uploaded to an incorrect path.
>
- Sample: uploading the "doc" folder in D drive to the root directory of COS
```plaintext
coscmd upload -r D:/doc /
```
- Sample: uploading the "doc" folder in D drive to the "doc" folder of COS
```plaintext
coscmd upload -r D:/doc doc
```
- Sample: uploading files synchronously (files with the same name, MD5 checksum, and file size will be skipped)
```plaintext
coscmd upload -rs D:/doc doc
```
>! Use the `-s` parameter to upload files synchronously while skipping those with the same MD5 value (please note that the source files in COS must have been uploaded using COSCMD v1.8.3.2 or above; the `x-cos-meta-md5` header is included by default).
>
- Sample: uploading files synchronously (files with the same name and file size will be skipped)
```plaintext
coscmd upload -rs --skipmd5 D:/doc doc
```
>!The `-s` parameter allows synchronous upload, and the `--skipmd5` parameter can be used to skip files with the same name and same file size.
>
- Sample: uploading the folder synchronously and deleting files that are deleted in the "doc" folder in D drive
```plaintext
coscmd upload -rs --delete D:/doc /
```
- Sample: ignoring .txt and .doc files in the "doc" folder in D drive
```plaintext
coscmd upload -rs D:/doc / --ignore *.txt,*.doc
```
- Sample: ignoring .txt files in the "doc" folder in D drive
```plaintext
coscmd upload -rs D:/doc / --ignore "*.txt"
```
>! 
> - When uploading folders, you can ignore certain types of files by using the `--ignore` parameter, or filter certain types of files by using `--include`. Multiple shell wildcard rules (separated by commas `,`) are supported. To ignore a specified extension, `,` must be added at the end, or `""` must be used to enclose the extension. If `""` contains multiple comma-separated rules, the first rule prevails.
> - If you want to use `--ignore` to filter all files in a particular folder, you need to use an absolute path and use `""` to enclose the path, for example, `coscmd upload -rs D:/doc / --ignore "D:/doc/ignore_folder/*"`.
>
- Sample: uploading .txt and .doc files in the "doc" folder in D drive
```plaintext
coscmd upload -rs D:/doc / --include *.txt,*.doc
```
- Sample: uploading .txt files in the "doc" folder in D drive
```plaintext
coscmd upload -rs D:/doc / --include "*.txt"
```

> !
> - If the file to upload is larger than 10 MB, COSCMD will upload it with multipart upload. The command is `coscmd upload <localpath> <cospath>` (same as simple upload).
> - COSCMD supports checkpoint restart to resume the upload of large files. When the multipart upload of a large file fails, only the failed parts will be uploaded when the operation is resumed instead of starting over from scratch (please ensure that the directory and content of the re-uploaded file are consistent with the uploaded directory).
> - COSCMD performs MD5 verification on each part during multipart upload.
> - When COSCMD uploads a file, the `x-cos-meta-md5` header is carried by default, whose value is the file's MD5 checksum. If the command has carried the `--skipmd5` parameter, this header will not be carried.


### Querying a file list

The query command is as follows:
- Command syntax
```plaintext
coscmd list <cospath>
```
- Sample: recursively querying the list of all files prefixed with "doc/" in this bucket
```plaintext
coscmd list doc/
```
- Sample: recursively querying the file list, number of files, and the file sizes of a bucket
```plaintext
coscmd list -ar
```
- Sample: recursively querying the list of all files prefixed with "examplefolder"
```plaintext
coscmd list examplefolder/ -ar
```
- Sample: querying the historical versions of all files in a bucket
```plaintext
coscmd list -v
```

>?
> - Replace "cospath" enclosed in "<>" with the COS path of the file list to query. If `<cospath>` is empty, the root directory of the current bucket is queried.
> - Use `-a` to query all files.
> - Use `-r` to query files recursively. The number and total size of the files are listed at the end of the returned result.
> - Use `-n num` to set the maximum number of files to query.

### Viewing the file information

The command is as follows:

- Command syntax
```plaintext
coscmd info <cospath> 
```
- Sample: viewing the metadata of "doc/picture.jpg"
```plaintext
coscmd info doc/picture.jpg
```

>? Replace "cospath" enclosed in "<>" with the COS path of the file to display.


### Downloading a file or folder


#### Command syntax for downloading a file
```plaintext
coscmd download <cospath> <localpath>
```
>! Replace "cospath" and "localpath" enclosed in "<>" with the COS path of the file to download and the local storage path, respectively.
>
- Sample: downloading the "doc/picture.jpg" file in COS to "D:/picture.jpg"
```plaintext
coscmd download doc/picture.jpg D:/picture.jpg
```
- Sample: downloading the "doc/picture.jpg" file in COS to drive D
```plaintext
coscmd download doc/picture.jpg D:/
```
- Sample: downloading a specified version of "picture.jpg" to drive D
```plaintext
coscmd download picture.jpg --versionId MTg0NDUxMzc2OTM4NTExNTg7Tjg D:/
```

#### Command syntax for downloading a folder
```plaintext
coscmd download -r <cospath> <localpath>
```
- Sample: downloading the "doc" folder to "D:/folder/doc"
```plaintext
coscmd download -r doc D:/folder/
```
- Sample: downloading files in the root directory while ignoring those in the `doc` directory that is under the root directory
```plaintext
coscmd download -r / D:/ --ignore "doc/*"
```
- Sample: downloading all files in the root directory of the current bucket and overwriting local files
```plaintext
coscmd download -rf / D:/examplefolder/
```
>! If a file with the same name exists locally, the download will fail. In this case, you need to use the `-f` parameter to overwrite the local file.
>
- Sample: synchronously downloading all files in the root directory of the current bucket while skipping those with the same filename and MD5 checksum
```plaintext
coscmd download -rs / D:/examplefolder
```
>! Use the `-s` or `--sync` parameter to skip identical files that already exist locally when downloading a folder (provided that the downloaded files were uploaded via the COSCMD `upload` API and the `x- cos-meta-md5` header was included).
>
- Sample: synchronously downloading all files in the root directory of the current bucket while skipping those with the same filename and file size
```plaintext
coscmd download -rs --skipmd5 / D:/examplefolder
```
- Sample: synchronously downloading all files in the root directory of the current bucket and deleting local files that have been deleted in cloud
```plaintext
coscmd download -rs --delete / D:/examplefolder
```
- Sample: ignoring .txt or .doc files
```plaintext
coscmd download -rs / D:/examplefolder --ignore *.txt,*.doc
```
- Sample: ignoring .txt files
```plaintext
coscmd download -rs / D:/examplefolder --ignore "*.txt"
```
>! 
> - When uploading folders, you can ignore certain types of files by using the `--ignore` parameter, or filter certain types of files by using `--include`. Multiple shell wildcard rules (separated by commas `,`) are supported. To ignore a specified extension, `,` must be added at the end, or `""` must be used to enclose the extension. If `""` contains multiple comma-separated rules, the first rule prevails.
> - If you want to use `--ignore` to filter all files in a particular directory, you need to use an absolute path and use `""` to enclose the path, for example, `coscmd upload -rs D:/doc / --ignore "D:/doc/ignore_folder/*"`.
>
- Sample: filtering .txt and .doc files
```plaintext
coscmd download -rs / D:/examplefolder --include *.txt,*.doc
```
- Sample: filtering .txt files
```plaintext
coscmd download -rs / D:/examplefolder --include "*.txt"
```
>! Since the old `mget` API is disused, please use the `download` API for multipart downloads.


### Getting signed download URLs

- Command syntax
```plaintext
coscmd signurl <cospath>
```
- Sample: generating a signed URL for "doc/picture.jpg"
```plaintext
coscmd signurl doc/picture.jpg
```
- Sample: generating a signed URL that is effective for 100 seconds for "doc/picture.jpg"
```plaintext
coscmd signurl doc/picture.jpg -t 100
```

>?
> - Replace "cospath" enclosed in "<>" with the COS path of the file for which you need to get the download URL.
> - The `-t time` parameter sets the effective time (in seconds) of the URL signature. The default value is 10000.


### Deleting a file or folder

#### Command syntax for deleting a file
```plaintext
coscmd delete <cospath>
```
>! Replace "cospath" enclosed in "<>" with the COS path of the file to delete. You will be prompted to confirm this operation.

- Sample: deleting the "doc/exampleobject.txt" file
```plaintext
coscmd delete doc/exampleobject.txt
```
- Sample: deleting files with version IDs
```plaintext
coscmd delete doc/exampleobject.txt --versionId MTg0NDUxMzc4ODA3NTgyMTErEWN
```

#### Command syntax for deleting a folder
```plaintext
coscmd delete -r <cospath>
```
- Sample: deleting the `doc` folder
```plaintext
coscmd delete -r doc
```
- Sample: deleting the `folder/doc` folder
```plaintext
coscmd delete -r folder/doc
```
- Sample: deleting all files with version IDs in the `doc` directory
```plaintext
coscmd delete -r doc/ --versions
```
>?
>- You need to enter `y` to confirm a batch delete operation. You can skip this step if the `-f` parameter is used.
>- Note that the delete folder command will delete the current folder as well as the files in it. To delete a versioning-enabled file, you need to specify a version ID.

### Viewing incomplete multipart uploads

- Command syntax
```plaintext
coscmd listparts <cospath>
```
- Sample: listing incomplete multipart uploads prefixed with "doc/"
```plaintext
coscmd listparts doc/
```

### Aborting incomplete multipart uploads

- Command syntax
```plaintext
coscmd abort
```
- Sample: aborting all incomplete multipart uploads
```plaintext
coscmd abort
```

### Copying a file or folder

#### Command syntax for copying a file
```plaintext
coscmd copy <sourcepath> <cospath>
```
- Sample (intra-bucket replication): copying "picture.jpg" in the `examplebucket-1250000000` bucket to the "doc" folder
```plaintext
coscmd -b examplebucket-1250000000 -r ap-chengdu copy examplebucket-1250000000.ap-chengdu.myqcloud.com/picture.jpg doc/
```
- Sample (cross-bucket replication): copying "doc/picture.jpg" in the `examplebucket2-1250000000` bucket to "doc/examplefolder/" in the `examplebucket1-1250000000` bucket
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/
```
- Change the storage class of the file to STANDARD_IA.
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/ -H "{'x-cos-storage-class':'STANDARD_IA'}"
```
- Change the storage class of the file to ARCHIVE and rename it "photo.jpg".
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/doc/picture.jpg doc/examplefolder/photo.jpg -H "{'x-cos-storage-class':'Archive'}"
```

#### Command syntax for copying a folder
```plaintext
coscmd copy -r <sourcepath> <cospath>
```
- Sample: copying the `examplefolder` directory in the `examplebucket2-1250000000` bucket to the `doc` directory in the `examplebucket1-1250000000` bucket
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder doc/
```

> ?
> - Replace "sourcepath" and "cospath" enclosed in "<>" with the path of the COS file to copy and the COS destination path, respectively.
> - The source path is formatted as `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`.
> - Use the `-d` parameter to set the `x-cos-metadata-directive` header. Valid values are `Copy` (default) and `Replaced`.
> - When setting the HTTP header with the `-H` parameter, use the JSON format, for example, `coscmd copy -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more information about the headers, see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Moving a file or folder
>! In a `move` command, `<sourcepath>` and `<cospath>` cannot be the same. Otherwise, files will be deleted. The reason is that the `move` command copies files first and then deletes them, and the files in the `<sourcepath>` path are eventually deleted.
#### Command syntax for moving a file
```plaintext
coscmd move <sourcepath> <cospath> 
```
- Sample (intra-bucket movement): moving "picture.jpg" in the `examplebucket-1250000000` bucket to the "doc" folder 
```plaintext
coscmd -b examplebucket-1250000000 -r ap-chengdu move examplebucket-1250000000.ap-chengdu.myqcloud.com/picture.jpg doc/
```
- Sample (cross-bucket movement): moving "picture.jpg" in the `examplebucket2-1250000000` bucket to "doc/folder/" in the `examplebucket1-1250000000` bucket
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/picture.jpg doc/folder/
```
- Sample: changing the storage class of the file to STANDARD_IA
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/picture.jpg doc/folder/ -H "{'x-cos-storage-class':'STANDARD_IA'}"
```
- Sample: changing the storage class of the file to ARCHIVE
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'Archive'}"
```

#### Command syntax for moving a folder
```plaintext
coscmd move -r <sourcepath> <cospath>
```
- Sample: moving the "examplefolder" directory in the `examplebucket2-1250000000` bucket to the "doc" directory in the `examplebucket1-1250000000` bucket
```plaintext
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder doc/
```

> ?
> - Replace "sourcepath" and "cospath" enclosed in "<>" with the path of the COS file to move and the COS destination path, respectively.
> - The source path is formatted as `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`.
> - Use the `-d` parameter to set the `x-cos-metadata-directive` header. Valid values are `Copy` (default) and `Replaced`.
> - When setting the HTTP header with the `-H` parameter, use the JSON format, for example, `coscmd move -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more information about the headers, see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Setting object access permission

- Command syntax
```plaintext
coscmd putobjectacl --grant-<permissions> <UIN> <cospath>
```
- Sample: granting `100000000001` permission to read "picture.jpg"
```plaintext
coscmd putobjectacl --grant-read 100000000001 picture.jpg
```
- Sample: querying the file’s access permission
```plaintext
coscmd getobjectacl picture.jpg
```

### Enabling/Suspending versioning

- Command syntax
```plaintext
coscmd putbucketversioning <status>
```
- Sample: enabling versioning
```plaintext
coscmd putbucketversioning Enabled
```
- Sample: suspending versioning
```plaintext
coscmd putbucketversioning Suspended
```
- Sample: querying versioning
```plaintext
coscmd getbucketversioning
```

> !
>- Replace "status" enclosed in "<>" with the desired versioning status.
>- Once versioning is enabled for the bucket, it cannot return to the prior status (initial status). However, you can suspend versioning for the bucket so that subsequent uploads of objects will not generate multiple versions.

### Restoring an ARCHIVED file

- Command syntax for restoring an archived file
```plaintext
coscmd restore <cospath>
```
- Sample: restoring "picture.jpg" using the expedited retrieval mode (effective for 3 days)
```plaintext
coscmd restore -d 3 -t Expedited picture.jpg
```
- Command syntax for restoring archived files
```plaintext
coscmd restore -r <cospath>
```
- Sample: restoring the "examplefolder/" folder using the expedited retrieval mode (effective for 3 days)
```plaintext
coscmd restore -r -d 3 -t Expedited examplefolder/
```

>?
> - Replace "cospath" enclosed in "<>" with the COS path of the file list to query.
> - Use `-d <day>` to set the validity period of the temporary copy. Default value: `7`.
> - Use `-t <tier>` to specify the restoration mode. Enumerated values: `Expedited` (Expedited retrieval), `Standard` (Standard retrieval), and `Bulk` (bulk retrieval). Default value: `Standard`.

## FAQs

If you have any questions about COSCMD, see [COSCMD](https://intl.cloud.tencent.com/document/product/436/30586).



