## Feature Description

COSCMD enables you to perform batch object operations such as upload/download/delete by using simple command lines.

## Operating Environment

#### System environment

Windows, Linux, and macOS.

> ?
> - Please make sure that local characters are in UTF-8 format; otherwise, exceptions will occur when operating on Chinese files.
> - Please also make sure that local time is in sync with UTC, as COSCMD will malfunction when there is a large deviation between the two.

#### Software requirements

- Python 2.7/3.5/3.6.
- Latest version of pip.

#### Installation and configuration

- For more information on the installation and configuration of the environment, please see [Python](https://intl.cloud.tencent.com/document/product/436/10866).
- For more information on the installation and configuration of pip, please see [Installation](https://pip.pypa.io/en/stable/installing/).

## Download and Installation

#### Installing pip

Run the `pip` command to install:

```plaintext
pip install coscmd
```

 After installation is complete, you can view the version information by running the `-v` or `--version` command.

#### Updating pip

Run the `pip` command to update:

```plaintext
pip install coscmd -U
```

> ! If the pip version number is greater than or equal to 10.0.0, a failure may occur when upgrading or installing dependent libraries. We recommend using pip v9.x (pip install pip==9.0.0).

#### Installation through source code (not recommended)

Click [here](https://github.com/tencentyun/coscmd.git) to download the source code.

```plaintext
git clone https://github.com/tencentyun/coscmd.git
cd coscmd
python setup.py install
```

> !For Python v2.6, we recommend using this method as it is easy for a failure to occur when installing pip dependent libraries.

#### Offline installation

> ! Please make sure that the same version of Python is installed on the two devices; otherwise, the installation will fail.

```sh
# Run the following commands on a device that is connected to the internet
mkdir coscmd-packages
pip download coscmd -d coscmd-packages
tar -czvf coscmd-packages.tar.gz coscmd-packages

# Copy the installation package to a device that is not connected to the internet and run the following commands
tar -xzvf coscmd-packages.tar.gz
pip install coscmd --no-index -f coscmd-packages
```

## Directions

### Viewing help information

You can view the tool's help information with the `-h` or `--help` command.

```plaintext
coscmd -h  // View information on the current version
```

The help information is as shown below:

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
    mget                Download file from COS to local
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

In addition, you can also enter `-h` after each command (with no parameter appended) to see how to use the command. For example:

```plaintext
coscmd upload -h  // View how to use the upload command
```

### Configuring parameters

You need to configure certain parameters before using COSCMD. Run the following command to begin configuration:

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

Generally, you only need to perform simple configurations, as shown in the sample below.

```shell
coscmd config -a AChT4ThiXAbpBDEFGhT4ThiXAbp**** -s WE54wreefvds3462refgwewe**** -b examplebucket-1250000000 -r ap-beijing
```

> ?Here, fields enclosed in "[]" are optional, while those in "<>" are required.

The parameters are as detailed below:

| Option | Parameter Description | Required | Valid Value |
| :--------------- | :----------------------------------------------------------- | -------- | ------ |
| -a | Key ID, which can be obtained on the [API Key Management Page](https://console.cloud.tencent.com/cam/capi) on the console | Yes | String |
| -s | Key, which can be obtained on the [API Key Management Page](https://console.cloud.tencent.com/cam/capi) on the console | Yes | String |
| -t | Temporary key token, which should be specified in the `x-cos-security-token` header if a temporary key is used | No | String |
| -b | Name of the specified bucket in the format: `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | Yes | String |
| -r | Bucket region. For more information, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | Yes | String |
| -e               | `ENDPOINT` of the request. Once configured, the `REGION` parameter will be invalidated. The format of this parameter is `cos.<region>.myqcloud.com` for default endpoint domain names and `cos.accelerate.myqcloud.com` for global acceleration endpoint domain names | No | String |
| -m | Maximum number of threads in a multi-thread operation (default value: 5; value range: 1–30) | No | Number |
| -p | Part size in MB in a multipart operation (default value: 1 MB; value range: 1–1000) | No | Number |
| --do-not-use-ssl | Specifies to use HTTP instead of HTTPS protocol | No | String |
| --anonymous | Anonymous operation (i.e. one that does not carry a signature) | No | String |

> ?
> 1. You can directly edit the `~/.cos.conf` file (which is a hidden file in **My Documents** on Windows). This file does not exist at first and is generated by the `coscmd config` command. You can also create it manually.
The file content of the configured `.cos.conf` file is as shown below:
```plaintext
 [common]
secret_id = AChT4ThiXAbpBDEFGhT4ThiXAbp****
secret_key = WE54wreefvds3462refgwewe****
bucket = examplebucket-1250000000
region = ap-beijing
max_thread = 5
part_size = 1
schema = https
```
> 2. You can add `schema` in the configuration file to select `http/https`. The default value is `https`.
> 3. You can use anonymous mode (i.e., the signature is kept empty) by selecting `True/False` for the `anonymous` item.



### Using commands to specify a bucket and region

- Specify a bucket with `-b <BucketName-APPID>`.
- The bucket name entered here must be in the format of `BucketName-APPID`.
- Specify a region with `-r <region>`.

```plaintext
# Command format
coscmd -b <BucketName-APPID> -r <region> <action> ...
# Sample - Create a bucket
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
# Sample - Upload a file
coscmd -b examplebucket-1250000000 -r ap-beijing upload exampleobject exampleobject
```

### Creating bucket

- We recommend using this command in conjunction with `-b <BucketName-APPID>` and `-r <region>`.

```plaintext
# Command format
coscmd -b <BucketName-APPID> createbucket
# Sample
coscmd createbucket
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
```

### Deleting a bucket

- We recommend using this command in conjunction with `-b <BucketName-APPID>` and `-r <region>`.

```plaintext
# Command format
coscmd -b <BucketName-APPID> deletebucket
# Sample
coscmd deletebucket
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket -f
```

- Using the `-f` parameter will forcibly delete the bucket, including all files, noncurrent folders (if versioning is enabled), and incomplete multipart uploads.

### Uploading a file or folder

- The command for uploading a file is as follows:

```plaintext
# Command format
coscmd upload <localpath> <cospath>
# Sample
# Upload the local `/data/exampleobject` file to the `data/exampleobject` path in COS
coscmd upload /data/exampleobject data/exampleobject 
coscmd upload /data/exampleobject data/
# Upload the file by specifying the header
# Specify the object type to upload an archived file
coscmd upload /data/exampleobject data/exampleobject -H "{'x-cos-storage-class':'Archive'}"
# Configure metadata
coscmd upload /data/exampleobject data/exampleobject -H "{'x-cos-meta-example':'example'}"
```

- The command for uploading a folder is as follows:

```plaintext
# Command format
coscmd upload -r <localpath> <cospath>
# Sample
coscmd upload -r /data/examplefolder data/examplefolder
# The storage path in COS is `examplefolder2/examplefolder`
coscmd upload -r /data/examplefolder examplefolder2/
# Upload to the bucket root directory
coscmd upload -r /data/examplefolder/ /
# Upload files synchronously while skipping those with the same MD5 value
coscmd upload -rs /data/examplefolder data/examplefolder
# Upload files synchronously while deleting those that have been deleted locally
coscmd upload -rs --delete /data/examplefolder data/examplefolder
# Ignore .txt and .doc files
coscmd upload -rs /data/examplefolder data/examplefolder --ignore *.txt,*.doc
```

 Replace parameters enclosed in "<>" with the path of the local file to be uploaded (localpath) as well as the COS storage path (cospath).

> !
> - When uploading a file, you need to enter the COS path plus the name of the file and/or folder (please see the samples for details).
> - COSCMD supports checkpoint restart to resume the upload of large files. When the multipart upload of a large file fails, only the parts that failed to upload will be uploaded when the operation is resumed instead of starting over from scratch (please ensure that the file content of the re-uploaded directory is the same as that of the uploaded directory).
> - COSCMD performs MD5 verification on each part during multipart upload.
> - The `x-cos-meta-md5` header is included by default when COSCMD uploads a file, and its value is the same as the file's MD5 value.
> - Use the `-s` parameter to upload files synchronously while skipping those with the same MD5 value (please note that the source files in COS must have been uploaded by using COSCMD v1.8.3.2 or above; the `x-cos-meta-md5` header is included by default).
> - When setting the HTTP header using the `-H` parameter, please make sure that it is in JSON format, such as `coscmd upload -H "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more headers, please see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).
> - You can ignore certain types of files by using the `--ignore` parameter when uploading folders. Multiple shell wildcard rules (separated by commas `,`) are supported. To ignore a specified file extension, `,` must be added at the end, or `""` must be added to enclose the file extension.
> - Currently, a single file of up to 40 TB can be uploaded.

### Downloading a file or folder

- The command for downloading a file is as follows:

```plaintext
# Command format
coscmd download <cospath> <localpath>
# Sample
coscmd download data/exampleobject /data/exampleobject
coscmd download data/exampleobject /data/
```

- The command for downloading a folder is as follows:

```plaintext
# Command format
coscmd download -r <cospath> <localpath>
# Sample
coscmd download -r data/examplefolder/ /data/examplefolder
coscmd download -r data/examplefolder/ /data/
# Download all the files in the current bucket root directory and overwrite local files
coscmd download -rf / /data/examplefolder
# Download all the files in the current bucket root directory synchronously while skipping those with the same MD5 value
coscmd download -rs / /data/examplefolder
# Download all the files in the current bucket root directory synchronously while deleting existing local files that have been deleted in the cloud
coscmd download -rs --delete / /data/examplefolder
# Ignore .txt and .doc files
coscmd download -rs / /data/examplefolder --ignore *.txt,*.doc
```

Replace parameters enclosed in "<>" with the COS path (cospath) of the file to be downloaded as well as the local storage path (localpath).

> !
> - Since the old `mget` API is no longer in use, please use the `download` API for multipart downloads.
> - If a file with the same name exists locally, the download will fail. In this case, you need to use the `-f` parameter to overwrite the local file.
> - Use the `-s` or `--sync` parameter to skip identical files that already exist locally when downloading a folder (provided that the downloaded files were uploaded through the COSCMD upload API and the `x- cos-meta-md5` header was included).
> - You can ignore certain types of files by using the `--ignore` parameter when downloading folders. Multiple shell wildcard rules (separated by commas `,`) are supported. To ignore a specified file extension, `,` must be added at the end, or `""` must be added to enclose the file extension.

### Deleting a file or folder

- The command for deleting a file is as follows:

```plaintext
# Command format
coscmd delete <cospath>
# Sample
coscmd delete data/exampleobject

```

- The command for deleting a folder is as follows:

```plaintext
# Command format
coscmd delete -r <cospath>
# Sample
coscmd delete -r /data/examplefolder/
coscmd delete -r /
```

 Replace parameters enclosed in "<>" with the COS path (cospath) of the file to be deleted. You will be prompted to confirm this operation.

> !You need to enter `y` to confirm a batch deletion operation. This step can be skipped if the `-f` parameter is used.

### Viewing incomplete multipart uploads

- The command is as follows:

```plaintext
# Command format
coscmd listparts <cospath>
# Sample
coscmd listparts examplefolder/
```

### Clearing incomplete multipart uploads

- The command is as follows:

```plaintext
# Command format
coscmd abort
# Sample
coscmd abort
```

### Copying a file or folder

- The command for copying a file is as follows:

```plaintext
# Command format
coscmd copy <sourcepath> <cospath> 
# Sample
# Copy the object `data/exampleobject` in the bucket `examplebucket2-1250000000` to `data/examplefolder/exampleobject` in the bucket `examplebucket1-1250000000`
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject
# Change the storage class of the file to `STANDARD_IA`
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'STANDARD_IA'}"
# Change the storage class of the file to `ARCHIVE`
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'Archive'}"
```

- The command for copying a folder is as follows:

```plaintext
# Command format
coscmd copy -r <sourcepath> <cospath>
# Sample
# Copy the directory `examplefolder` in the bucket `examplebucket2-1250000000` to the directory `examplefolder` in the bucket `examplebucket1-1250000000`
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder/ examplefolder
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder/ examplefolder/

```

Replace parameters enclosed in "<>" with the path of the COS source file (sourcepath) to be copied as well as the path of the COS destination file (cospath) to be copied to.

> ?
> - The `sourcepath` is in the format of `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`.
> - Use the `-d` parameter to set the `x-cos-metadata-directive` header (valid values: Copy, Replaced; default value: Copy).
> - When setting the HTTP header by using the `-H` parameter, please make sure that it is in JSON format, such as `coscmd copy -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more headers, please see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Moving a file or folder

- The command for moving a file is as follows:

```plaintext
# Command format
coscmd move <sourcepath> <cospath> 
# Sample
# Move the object `data/exampleobject` in the bucket `examplebucket2-1250000000` to `data/examplefolder/exampleobject` in the bucket `examplebucket1-1250000000`
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject
# Change the storage class of the file to `STANDARD_IA`
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'STANDARD_IA'}"
# Change the storage class of the file to `ARCHIVE`
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'Archive'}"
```

- The command for moving a folder is as follows:

```plaintext
# Command format
coscmd move -r <sourcepath> <cospath>
# Sample
# Move the directory `examplefolder` in the bucket `examplebucket2-1250000000` to the directory `examplefolder` in the bucket `examplebucket1-1250000000`
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder/ examplefolder
coscmd -b examplebucket1-1250000000 -r ap-guangzhou move -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder/ examplefolder/

```

Replace parameters enclosed in "<>" with the path of the COS source file (sourcepath) to be moved as well as the path of the COS destination file (cospath) to be moved to.

> ?
> - The `sourcepath` is in the format of `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`.
> - Use the `-d` parameter to set the `x-cos-metadata-directive` header (valid values: copy, Replaced; default value: copy).
> - When setting the HTTP header by using the `-H` parameter, please make sure that it is in JSON format, such as `coscmd move -H -d Replaced "{'x-cos-storage-class':'Archive','Content-Language':'zh-CN'}" <localpath> <cospath>`. For more headers, please see [PUT Object - copy](https://intl.cloud.tencent.com/document/product/436/10881).


### Querying a file list

The query command is as follows:

```plaintext
# Command format
coscmd list <cospath>

# Sample
# Recursively query the list of all files in the bucket
coscmd list -ar
# Recursively query the list of all files prefixed with `examplefolder`
coscmd list examplefolder/  -ar
```

Replace parameters enclosed in "<>" with the COS path (cospath) of the file list to be queried.

- Use `-a` to query all files.
- Use `-r` to query files recursively. The number and total size of the files will be listed at the end of the returned result.
- Use `-n num` to set the maximum number of files to be queried.

>?If `<cospath>` is empty, the current bucket root directory will be queried by default.

### Displaying file information

The command is as follows:

```plaintext
# Command format
coscmd info <cospath> 

# Sample
coscmd info exampleobject
```

Replace parameters enclosed in "<>" with the COS path (cospath) of the file to be displayed.

### Getting signed download URL

The command is as follows:

```plaintext
# Command format
coscmd signurl <cospath>

# Sample
coscmd signurl exampleobject
coscmd signurl exampleobject -t 100
```

Replace parameters enclosed in "<>" with the COS path (cospath) of the file for which you need to get the download URL.
Use `-t time` to configure the validity period in seconds of the query signature.

### Enabling/Suspending versioning

The command is as follows:

```plaintext
# Command format
coscmd putbucketversioning <status>

# Enable versioning
coscmd putbucketversioning Enabled

# Suspend versioning
coscmd putbucketversioning Suspended
```

Replace parameters enclosed in "<>" with the desired versioning status.

> !Once versioning is enabled for a bucket, this operation cannot be reversed (i.e., versioning cannot be disabled). However, you can suspend versioning for the bucket so that subsequent object uploads will not generate multiple versions.

### Restoring an archived file

- The command for restoring a file is as follows:

```plaintext
# Command format
coscmd restore <cospath>
# Sample
coscmd restore -d 3 -t Expedited exampleobject
```

- The command for restoring archived files in batches is as follows:

```plaintext
# Command format
coscmd restore -r <cospath>
# Sample
coscmd restore -r -d 3 -t Expedited examplefolder/
```

 Replace parameters enclosed in "<>" with the COS path (cospath) of the file list to be queried.

- Use `-d day` to configure the validity period of the temporary copy. Default value: 7.
- Use `-t tier` to specify the restoration type. Enumerated values: Expedited, Standard, Bulk. Default value: Standard.

### Running commands in debugging mode

If `-d` or `-debug` is added before a command, detailed operation information will be displayed when the command is executed as shown in the example below:

```plaintext
# Display upload details by using a command in the following format:
coscmd -d upload <localpath> <cospath>

# Sample
coscmd -d upload exampleobject exampleobject
```

## FAQs

If you have any questions about COSCMD, please see [COSCMD FAQs](https://intl.cloud.tencent.com/document/product/436/30586).
