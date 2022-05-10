The `bucket-tagging` command is used to create (modify), get, and delete bucket tags.

## Command Options
The `bucket-tagging` command contains the following optional flags:

| Flag Abbreviation | Flag Name | Description |
|----|----|----|
|-m|--method| Specifies the operation to be performed, including PUT, GET, and DELETE  |

>? For other common options of this command (such as switching bucket and user account), see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

## Adding or Modifying Bucket Tag

A bucket tag is represented by a key-value pair. Only the bucket owner and users with the `PutBucketTagging` permission can add or modify bucket tags. Error message “403 AccessDenied” will be returned for other users.

### Command format

```plaintext
./coscli bucket-tagging --method put cos://<BucketName-APPID> key1#value1 key2#value2
```
Here, `key#value` represents the tag key-value pair separated by `#`. If the bucket does not have a tag, this command will add the specified tag to the bucket; otherwise, it will overwrite the original tag.

### Example

To configure two tags for the bucket `exmaplebucket-1250000000` with the keys of 1 and 2 as well as values of 111 and 222 respectively, run the following command:

```plaintext
./coscli bucket-tagging --method put cos://exmaplebucket-1250000000 1#111 2#222
```

## Querying Bucket Tags
### Command format

```plaintext
./coscli bucket-tagging --method get cos://<BucketName-APPID>
```

### Example

```plaintext
./coscli bucket-tagging --method get cos://exmaplebucket-1250000000
```

The following output shows that `exmaplebucket-1250000000` has two tags with the keys of 1 and 2 as well as values of 111 and 222 respectively.

```plaintext
  KEY | VALUE  
------+--------
    1 |   111  
    2 |   222 
```

## Deleting Bucket Tags

### Command format
```plaintext
./coscli bucket-tagging --method delete cos://<BucketName-APPID>
```


### Example

```plaintext
./coscli bucket-tagging --method delete cos://exmaplebucket-1250000000
```
