The `hash` command is used to calculate the hash value of a local file or get the hash value of a file in COS.

## Command Syntax


```plaintext
./coscli hash <object-name> [flag]
```

`hash` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
| &lt;object-name&gt; | Specifies the target file, which can be a local path or a COS file path. The COS path is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Local path: ~/example.txt <br>COS file path specified with the bucket alias: cos://bucketalias/example.txt <br>COS file path specified with the bucket name: cos://examplebucket-1250000000/example.txt |

The `hash` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Description                         |
| --------- | ------------- | -------------------------------------- |
| -h |  --help |   Views the usage of this command. |
|     None      | --type        | Hash type, which can be MD5 or CRC64 (default) |

>? For other common options of this command (such as switching bucket and user account), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).
>

## Examples

### Calculating the CRC64 value of local file

```plaintext
./coscli hash ~/test.txt
```

### Getting the MD5 value of COS file

```plaintext
./coscli hash cos://bucket1/example.txt --type=md5
```
