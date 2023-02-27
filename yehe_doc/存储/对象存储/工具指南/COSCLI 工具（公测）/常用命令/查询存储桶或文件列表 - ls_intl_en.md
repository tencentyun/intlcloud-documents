The `ls` command is used to query the list of buckets, objects in a bucket, and objects in a directory.

## Command Syntax

```plaintext
./coscli ls [cos://bucketAlias[/prefix/]]
```

>? 
>- For more information on `bucketAlias`, see [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265).
>- For other common options of this command (such as switching bucket and user account), see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).
>

`ls` includes the following optional parameters:

| Parameter Format | Description | Example |
| ----------------- | -------------- | -------------------- |
| cos://bucketAlias | Specifies a bucket. | cos://bucket1          |
| /prefix/          | Specifies a directory. | /picture/ |




## Examples


### Listing all buckets of the current account

```plaintext
./coscli ls
```

### Listing objects

#### Listing all objects in the `bucket1` bucket

```plaintext
./coscli ls cos://bucket1
```

#### Listing all objects and subdirectories in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli ls cos://bucket1/picture/
```


