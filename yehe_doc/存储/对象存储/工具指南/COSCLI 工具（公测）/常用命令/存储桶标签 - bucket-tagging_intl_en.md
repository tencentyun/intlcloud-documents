The `bucket-tagging` command is used to create (modify), get, and delete bucket tags. One bucket can have up to 50 tags.

## Command Syntax

```plaintext
./coscli bucket-tagging --method [method] cos://<bucket-name> [tag_key]#[tag_value]
```


`bucket-tagging` includes the following parameters:

| Parameter Format | Description | Example |
| --------- | ------------- | ------------------------ |
| cos://&lt;bucket-name&gt; | Specifies the target bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias <br>Access with the bucket name: cos://examplebucket-1250000000    |

The `bucket-tagging` command contains the following optional flags:

| Flag Abbreviation | Flag Name | Description |
|----|----|----|
| -h |  --help |   Views the usage of this command. |
| None |--method| Specifies the operation to be performed, including `put` (adding tags), `get` (querying tags), and `delete` (deleting tags). |

>? For other common options of this command (such as switching bucket and user account), see [Common Options](https://www.tencentcloud.com/document/product/436/46273).
>


## Adding or Modifying Bucket Tag

A bucket tag is represented by a key-value pair. Only the bucket owner and users with the `PutBucketTagging` permission can add or modify bucket tags. Error message “403 AccessDenied” will be returned for other users.

### Command syntax

```plaintext
./coscli bucket-tagging --method put cos://bucketAlias key1#value1 key2#value2
```
Here, `key#value` represents the tag key-value pair separated by `#`. If the bucket does not have a tag, this command will add the specified tag to the bucket; otherwise, it will overwrite the original tag.

### Example

To configure two tags with the keys of 1 and 2 as well as values of 111 and 222 respectively for the bucket with alias `example-alias`, run the following command:

```plaintext
./coscli bucket-tagging --method put cos://exmaple-alias 1#111 2#222
```

## Querying Bucket Tags
### Command syntax

```plaintext
./coscli bucket-tagging --method get cos://bucketAlias
```

### Example

```plaintext
./coscli bucket-tagging --method get cos://exmaple-alias
```

The following output shows that the bucket with alias `example-alias` has two tags with the keys of 1 and 2 as well as values of 111 and 222 respectively.

```plaintext
  KEY | VALUE  
------+--------
    1 |   111  
    2 |   222 
```

## Deleting Bucket Tags

### Command syntax

```plaintext
./coscli bucket-tagging --method delete cos://bucketAlias
```

### Example

```plaintext
./coscli bucket-tagging --method delete cos://exmaple-alias
```
