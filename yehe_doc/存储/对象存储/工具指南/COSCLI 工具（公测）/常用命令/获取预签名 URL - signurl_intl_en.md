The `signurl` command is used to get the pre-signed URL of an object, through which the object can be accessed anonymously.

## Command Format

```plaintext
./coscli signurl cos://<bucketAlias>/<key> [flag]
```

>? For more information on `bucketAlias`, please see [Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>

The `signurl` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | ---------------------------- |
| -h        | --help        | Outputs help information                      |
| -c        | --config-path | Specifies the path of the configuration file to be used          |
| -t        | --time        | Sets the URL expiration time, which is 1000s by default |

## Example

### Getting the pre-signed URL of `picture.jpg` in `bucket1` bucket

```plaintext
./coscli signurl cos://bucket1/picture.jpg
```

### Getting the pre-signed URL of `picture.jpg` in `bucket2` bucket and setting the URL expiration time to 1314 seconds

```plaintext
./coscli signurl cos://bucket2/picture.jpg --time 1314
```

