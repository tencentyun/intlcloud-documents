The `hash` command is used to calculate the hash value of a local file or get the hash value of a file in COS.

## Command Syntax


```plaintext
./coscli hash <object-name> [flag]
```

>? 
>- For more information on `bucketAlias`, see [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>- For more general options for this command (such as switching buckets or user accounts), see [General Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

The `hash` command contains the following optional flags:

| Flag Abbreviation | Flag Full Name     | Description                         |
| --------- | ------------- | -------------------------------------- |
|     None      | --type        | Hash type, which can be MD5 or CRC64 (default) |

## Examples

### Calculating the CRC64 value of local file

```plaintext
./coscli hash ~/test.txt
```

### Getting the MD5 value of COS file

```plaintext
./coscli hash cos://bucket1/example.txt --type=md5
```
