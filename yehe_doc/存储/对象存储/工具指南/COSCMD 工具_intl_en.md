## Feature

With COSCMD tool, users can perform operations such as batch upload/download/deletion of objects using simple command line instructions.

>- If you use this tool to upload a file whose name already exists, the older file will be overwritten. File name duplication cannot be detected.

## Operating Environment

### System Environment

Windows, Linux, and macOS.

>
>
- Local characters should be in UTF-8 format, otherwise exceptions will occur when operating on files written in Chinese.
- Please make sure that the local time is in sync with UTC. The tool will malfunction if the time is significantly out of sync.

### Software Requirements

- Python 2.7/3.5/3.6.
- Latest Version of Pip

#### Installation and Configuration

- For more information about the installation and configuration of the environment, see [Python Installation and Configuration](https://intl.cloud.tencent.com/document/product/436/10866).
- For more information about the installation and configuration of pip, see [Installation](https://pip.pypa.io/en/stable/installing/).

## Download and Installation

### Installing Pip

Run the `pip` command to install:

```shell
pip install coscmd
```

 After the installation is completed, you can view information on the current version by running the `-v` or `--version` command.

### Updating Pip

Run the `pip` command to update:

```sh
pip install coscmd -U
```

> If the pip version number is greater than or equal to 10.0.0, a failure may occur when upgrading or installing dependent libraries. We recommend you use pip v9.x (pip install pip==9.0.0).

### Source Code Installation (Not Recommended)

Click [here](https://github.com/tencentyun/coscmd.git) to download the source code.

```shell
git clone https://github.com/tencentyun/coscmd.git
cd coscmd
python setup.py install
```

> With Python v2.6, we recommend you use this method because a failure is likely to occur when installing pip dependent libraries.

### Offline Installation

> Please ensure the two servers have the same version of Python, otherwise the installation will fail.

```sh
# Run the following command on a server with a public IP
mkdir coscmd-packages
pip download coscmd -d coscmd-packages
tar -czvf coscmd-packages.tar.gz coscmd-packages

# Copy the installer package to a server without a public IP and run the following command.
tar -xzvf coscmd-packages.tar.gz
pip install coscmd --no-index -f coscmd-packages
```

## Usage

### Viewing Help

You can view the tool's help information with the `-h` or `--help` command.

```shell
coscmd -h  //View information about the current version
```

The help information is as shown below:

```shell
usage: coscmd [-h] [-d] [-b BUCKET] [-r REGION] [-c CONFIG_PATH] [-l LOG_PATH]
              [-v]
              
              {info,restore,createbucket,signurl,listparts,mget,list,upload,deletebucket,abort,getbucketversioning,putbucketacl,getobjectacl,download,putobjectacl,copy,config,putbucketversioning,getbucketacl,delete}
              ...

an easy-to-use but powerful command-line tool. try 'coscmd -h' to get more
informations. try 'coscmd sub-command -h' to learn all command usage, likes
'coscmd upload -h'

positional arguments:
  {info,restore,createbucket,signurl,listparts,mget,list,upload,deletebucket,abort,getbucketversioning,putbucketacl,getobjectacl,download,putobjectacl,copy,config,putbucketversioning,getbucketacl,delete}
    config              Config your information at first
    upload              Upload file or directory to COS
    download            Download file from COS to local
    delete              Delete file or files on COS
    abort               Aborts upload parts on COS
    copy                Copy file from COS to COS
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

In addition, users can also enter `-h` after each command (with no parameter appended) to see how to use the command. For example:

```shell
coscmd upload -h  //View the usage of upload command
```

### Configuring Parameters

You need to configure parameters before using the COSCMD tool. Run the following command for configuration:

```shell
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

Generally, you only need simple configuration, as shown by the the sample below.

```shell
coscmd config -a AChT4ThiXAbpBDEFGhT4ThiXAbp**** -s WE54wreefvds3462refgwewe**** -b examplebucket-1250000000 -r ap-beijing
```

> Here, fields in "[]" are optional, while those in "<>" are required.

Parameters are configured as below:

| Option | Parameter Description | Required | Valid Value |
| :--------------- | :----------------------------------------------------------- | -------- | ------ |
| -a | Key ID, which can be obtained on the [API Key Management Page](https://console.cloud.tencent.com/cam/capi) | Yes | String |
| -s | Key, which can be obtained on the [API Key Management Page](https://console.cloud.tencent.com/cam/capi) | Yes | String |
| -t | Temporary key token - configure its x-cos-security-token header while using a temporary key. | No | String |
| -b | Name of the specified bucket, naming format is BucketName-APPID, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | Yes | String |
| -r | Region of the bucket; see [Regions and Access Domain Names](https://cloud.tencent.com/doc/product/436/6224) | Yes | String |
| -e | Configure the ENDPOINT of the request. After the ENDPOINT parameter is configured, the REGION parameter will be invalidated | No | String |
| -m | Multi-thread operation (5 by default, value range: 1-30) | No | Number |
| -p | Part size in multipart upload (in MB; 1 MB by default; value range: 1-1000) | No | Number |
| --do-not-use-ssl | Use the HTTP instead of HTTPS protocol | No | String |
| --anonymous | Anonymous operation (without signature) | No | String |

>
1. You can directly edit the `~/.cos.conf` file (which is a hidden file in `My Documents` on Windows). This file does not exist at first and is generated by the `coscmd config` command. You can also create it manually.
File content of the configured `.cos.conf` file is shown below:
```shell
 [common]
secret_id = AChT4ThiXAbpBDEFGhT4ThiXAbp****
secret_key = WE54wreefvds3462refgwewe****
bucket = examplebucket-1250000000
region = ap-beijing
max_thread = 5
part_size = 1
schema = https
```
2. Add `schema` in the configuration file to select `http/https`. The default value is `https`.
3. You can use the anonymous mode by selecting `True/False` in the `anonymous` item, i.e. the signature will be empty.



### Specifying the commands for bucket and region

- Specify a bucket by `-b <BucketName-APPID>`.
- The bucket name entered here must be in the format of BucketName-APPID.
- Specify a region by `-r <region>`.

```shell
# Command Format
coscmd -b <BucketName-APPID> -r <region> <action> ...
# Example - Create a bucket
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket
# Example - Upload a file
coscmd -b examplebucket-1250000000 -r ap-beijing upload exampleobject exampleobject

```

### Creating a bucket

- We recommend you use this command together with `-b <BucketName-APPID>` and `-r <region>`.

```shell
# Command Format
coscmd -b <BucketName-APPID> createbucket
# Example
coscmd createbucket
coscmd -b examplebucket-1250000000 -r ap-beijing createbucket

```

### Deleting a Bucket

- We recommend you use this command together with `-b <BucketName-APPID>` and `-r <region>`.

```shell
# Command Format
coscmd -b <BucketName-APPID> deletebucket
# Example
coscmd deletebucket
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket
coscmd -b examplebucket-1250000000 -r ap-beijing deletebucket -f

```

- Using the -f parameter will forcibly delete the bucket, including all files, history folders after versioning is turned on, and incomplete multipart uploads.

### Uploading a file or folder

- The command for file upload is as follows:

```shell
# Command Format
coscmd upload <localpath> <cospath>
# Example
# Upload the local /data/exampleobject file to the data/exampleobject path in COS
coscmd upload /data/exampleobject data/exampleobject 
coscmd upload /data/exampleobject data/
# Upload a file by specifying a header
# Specify the object type to upload an archived file
coscmd upload /data/exampleobject data/exampleobject -H "{'x-cos-storage-class':'Archive'}"
# Configuring the meta attribute
coscmd upload /data/exampleobject data/exampleobject -H "{'x-cos-meta-example':'example'}"
```

- The command for folder upload is as follows:

```shell
# Command Format
coscmd upload -r <localpath> <cospath>
# Example
coscmd upload -r /data/examplefolder data/examplefolder
# The storage path in COS is examplefolder2/examplefolder
coscmd upload -r /data/examplefolder examplefolder2/
# Upload to the bucket root directory
coscmd upload -r /data/examplefolder/ /
# Upload files synchronously and skip those with the same MD5
coscmd upload -rs /data/examplefolder data/examplefolder
# Ignore .txt and .doc files
coscmd upload -rs /data/examplefolder data/examplefolder --ignore *.txt,*.doc

```

 Replace parameters in "<>" with the path of the local file to be uploaded (localpath) and the storage path in COS (cospath).

>
>- When uploading a file, you need to complete the COS path name and the file (folder) name (refer to the example).
>- COSCMD supports resuming from upload breakpoints for large files. When multipart upload of large files fails, only the failed parts will be uploaded, rather than starting over during re-upload (make sure the directory and content of the re-uploaded files are consistent with the uploaded directory).
>- COSCMD performs MD5 verification on each part in multipart upload.
>- The `x-cos-meta-md5` header is carried by default when COSCMD uploads a file, and its value is the same as the file’s `MD5` value.
* Use -s parameter to upload files synchronously and skip those with the same MD5 (only if the source files in COS are uploaded using COSCMD v1.8.3.2 or above, carrying the x-cos-meta-md5 header by default).
>- When configuring the HTTP header using the -H parameter, make sure the format is JSON, such as `coscmd upload -H '{"x-cos-storage-class":"Archive","Content-Language":"zh-CN"}' <localpath> <cospath>`. For more headers, see [PUT Object](https://cloud.tencent.com/document/product/436/7749).
>- You can ignore a certain type of files using the --ignore parameter when uploading files. Multiple shell wildcard rules (separated by commas `,`) are supported. To ignore a specified file extension, `,` or `""` must be added at the end.
>- Currently, a single file of up to 40 TB can be uploaded.

### Downloading a file or folder

- The command for file download is as follows:

```shell
# Command Format
coscmd download <cospath> <localpath>
# Example
coscmd download data/exampleobject /data/exampleobject
coscmd download data/exampleobject /data/

```

- The command for folder download is as follows:

```shell
# Command Format
coscmd download -r <cospath> <localpath>
# Example
coscmd download -r data/examplefolder/ /data/examplefolder
coscmd download -r data/examplefolder/ /data/
# Download all the files in the current bucket root directory and overwrite local files
coscmd download -rf / /data/examplefolder
# Download all the files in the current bucket root directory synchronously and skip those with the same MD5
coscmd download -rs / /data/examplefolder
# Ignore .txt and .doc files
coscmd download -rs / /data/examplefolder --ignore *.txt,*.doc 

```

Replace parameters in "<>" with the path of the file to be downloaded in COS (cospath) and the local storage path (localpath).

>
>
>- The API `download` employs multipart download, which should be used since the old version `mget` API has been removed.
>- If a file with the same name exists locally, the download will fail. You need to use the `-f` parameter to overwrite the local file.
>- Use the `-s` or `--sync` parameter to skip identical files existed in the local folder when downloading a folder (provided that the downloaded files were uploaded via the upload API of COSCMD and the `x- cos-meta-md5` header was carried).
>- You can ignore a certain type of files using the --ignore parameter when downloading files. Multiple shell wildcard rules (separated by commas `,`) are supported. To ignore a specified file extension, `,` or `""` must be added at the end.

### Deleting a file or folder

- The command for file deletion is as follows:

```shell
# Command Format
coscmd delete <cospath>
# Example
coscmd delete data/exampleobject

```

- The command for folder deletion is as follows:

```shell
# Command Format
coscmd delete -r <cospath>
# Example
coscmd delete -r /data/examplefolder/
coscmd delete -r /
```

 Replace parameters in "<>" with the path of the file to be deleted in COS (cospath). You will be prompted to confirm this operation.

> For batch deletion, you need to enter `y` for confirmation. If the `-f` parameter is used, the file will be deleted directly with no confirmation needed.

### Viewing incomplete multipart uploads

- The command is as follows:

```shell
# Command Format
coscmd listparts <cospath>
# Example
coscmd listparts examplefolder/
```

### Clearing incomplete multipart uploads

- The command is as follows:

```shell
# Command Format
coscmd abort
# Example
coscmd abort
```

### Copying a file or folder

- The command for copying files is as follows:

```shell
# Command Format
coscmd copy <sourcepath> <cospath> 
# Example
# Copy the object in data/exampleobject in the bucket examplebucket2-1250000000 to data/examplefolder/exampleobject in the bucket examplebucket1-1250000000
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject
# Modify the storage type of a file to infrequent
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'STANDARD_IA'}"
# Modify the storage type of a file to archive
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy examplebucket2-1250000000.ap-beijing.myqcloud.com/data/exampleobject data/examplefolder/exampleobject -H "{'x-cos-storage-class':'Archive'}"
```

- The command for copying folders is as follows:

```shell
# Command Format
coscmd copy -r <sourcepath> <cospath>
# Example
# Copy the directory examplefolder in the bucket examplebucket2-1250000000 to the directory examplefolder in the bucket examplebucket1-1250000000
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder/ examplefolder
coscmd -b examplebucket1-1250000000 -r ap-guangzhou copy -r examplebucket2-1250000000.cos.ap-guangzhou.myqcloud.com/examplefolder/ examplefolder/

```

Replace parameters in "<>" with the path of the COS source file (sourcepath) and the path of the COS destination file (cospath) to be copied.

>
>- The sourcepath is in the format of `<BucketName-APPID>.cos.<region>.myqcloud.com/<cospath>`。
>- Use the -d parameter to configure the `x-cos-metadata-directive` header (value range: Copy and Replaced; Copy by default).
>- When configuring the HTTP header using the -H parameter, make sure the format is JSON, such as `coscmd copy -H -d Replaced '{"x-cos-storage-class":"Archive","Content-Language":"zh-CN"}' <localpath> <cospath>`. For more headers, see [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881).

### Querying file list

The command for querying is as follows:

```shell
# Command Format
coscmd list <cospath>

# Example
# Recursively query the list of all files in the bucket
coscmd list -ar
# Recursively query the list of all files prefixed with examplefolder
coscmd list examplefolder/  -ar
```

Replace parameter in "<>" with the path of the file list to be queried in COS (cospath).

- Use `-a` to query all files.
- Use `-r` to query files recursively. The number and total size of files are listed at the end of the returned result.
- Use `-n num` to configure the maximum number of files to be queried.

> If `<cospath>` is empty, the current bucket root directory will be queried by default.

### Displaying file information

The command is as follows:

```shell
# Command Format
coscmd info <cospath> 

# Example
coscmd info exampleobject
```

Replace parameters in "<>" with the path of the file to be displayed on COS (cospath).

### Getting signed download URLs

The command is as follows:

```shell
# Command Format
coscmd signurl <cospath>

# Example
coscmd signurl exampleobject
coscmd signurl exampleobject -t 100
```

Replace parameters in "<>" with the path of the file in COS for which you need to get the download URL (cospath).
Use `-t time` to configure the validity period of the signature to be queried (unit in seconds).

### Enabling and suspending versioning

The command is as follows:

```shell
# Command Format
coscmd putbucketversioning <status>

# Enable Versioning
coscmd putbucketversioning Enabled

## Suspend Versioning
coscmd putbucketversioning Suspended
```

Replace parameters in "<>" with the desired status of versioning.

>1. Once versioning is enabled for the bucket, it cannot return to the prior status (initial status). However, you can suspend versioning for the bucket so that subsequent uploads of objects will not generate multiple versions..

### Restoring an archived file

- The command for restoring files is as follows:

```shell
# Command Format
coscmd restore <cospath>
# Example
coscmd restore -d 3 -t Expedited exampleobject
```

- The command for restoring archived files in batches is as follows:

```shell
# Command Format
coscmd restore -r <cospath>
# Example
coscmd restore -r -d 3 -t Expedited examplefolder/
```

 Replace parameters in "<>" with the path of the file list to be queried in COS (cospath).

- Use `-d day` to configure the validity period of the temporary replica. Default value: 7.
- Use `-t tier` to specify the restoring type. Enumerated value: Expedited, Standard, and Bulk. Default value: Standard.

### Command for debugging mode

If `-d` or `-debug` is added before a command, detailed operation information will be displayed when executing on the command. Below is an example:

```shell
# Display the operation details of upload, command format is:
coscmd -d upload <localpath> <cospath>

# Example
coscmd -d upload exampleobject exampleobject
```

## FAQ

If you have any questions when using COSCMD, see [COSCMD FAQs](https://cloud.tencent.com/document/product/436/30744).
