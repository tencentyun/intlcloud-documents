The `hash` command is used to calculate the hash value of a local file or get the hash value of a file in COS.

## Command Format


```plaintext
./coscli hash <object-name> [flag]
```

>? For more information on `bucketAlias`, please see [Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>

The `hash` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | -------------------------------------- |
| -h        | --help        | Outputs help information                      |
| -c        | --config-path | Specifies the path of the configuration file to be used          |
|     None      | --type        | Hash type, which can be MD5 or CRC64 (default) |

## Example

### Calculating the CRC64 value of local file

```plaintext
./coscli hash ~/test.txt
```

### Getting the MD5 value of COS file

```plaintext
./coscli hash cos://bucket1/example.txt --type=md5
```
