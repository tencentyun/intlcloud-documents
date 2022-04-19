The `signurl` command is used to get the pre-signed URL of an object, through which the object can be accessed anonymously.

## Command Syntax

```plaintext
./coscli signurl cos://<bucketAlias>/<key> [flag]
```

>? 
>- For more information on `bucketAlias`, see [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>- For more general options for this command (such as switching buckets or user accounts), see [General Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

The `signurl` command contains the following optional flags:

| Flag Abbreviation | Flag Name     | Purpose                         |
| --------- | ------------- | ---------------------------- |
| -t        | --time        | Sets the URL expiration time, which is 1000s by default |

## Examples

### Getting the pre-signed URL of `picture.jpg` in `bucket1` bucket

```plaintext
./coscli signurl cos://bucket1/picture.jpg
```

### Getting the pre-signed URL of `picture.jpg` in `bucket2` bucket and setting the URL expiration time to 1314s

```plaintext
./coscli signurl cos://bucket2/picture.jpg --time 1314
```

