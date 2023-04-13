The `ls` command is used to query the list of buckets, objects in a bucket, and objects in a directory.

## Command Syntax
```plaintext
./coscli ls [cos://<bucket-name>[/prefix/]] [flag]
```

`ls` includes the following parameters:

| Parameter Format | Description | Example |
| ----------------- | -------------- | -------------------- |
| cos://&lt;bucket-name&gt; | Specifies the optional target bucket, which is accessible by using the bucket alias or bucket name configured in the configuration file as detailed in [Download and Installation Configuration](https://intl.cloud.tencent.com/document/product/436/43265). If you use the bucket name for access, you also need to include the `endpoint` flag. | Access with the bucket alias: cos://example-alias <br>Access with the bucket name: cos://examplebucket-1250000000    |
| /prefix/          | Specifies a directory (optional). | /picture/ |

`ls` includes the following optional flags:

| Flag Abbreviation | Flag Name   | Description                     |
| --------- | ----------- | ------------------------------------ |
| -h |  --help |   Views the usage of this command. |
|  None  | --include   | Includes specific objects.  |
|  None  | --exclude   | Excludes specific objects.    |
| -r        | --recursive | Specifies whether to traverse directories recursively and list all objects. |
|     None      | --limit       | Specifies the maximum quantity (0–1000) to be listed.  |

>? 
> - `--include` and `--exclude` support standard regular expressions. You can use regular expressions to filter objects that meet your requirements.
> - When using `zsh`, you may need to add double quotes at both ends of the `pattern` string.
```plaintext
./coscli ls cos://bucket1 -r --include ".*.mp4"
```
> - For other common options of this command (such as switching bucket and user account), see [Common Options](https://intl.cloud.tencent.com/document/product/436/46273).

## Examples


### Listing all buckets of the current account

```plaintext
./coscli ls
```

The returned information includes the bucket name, region, creation time, and total number of buckets. Below is an example:

```plaintext
           BUCKET NAME          |     REGION      |     CREATE DATE
--------------------------------+-----------------+-----------------------
  examplebucket-1250000000      | ap-nanjing      | 2022-01-01T00:00:00Z
--------------------------------+-----------------+-----------------------
                                  TOTAL BUCKETS:  |          1
                                ------------------+-----------------------
```

### Listing objects

#### Listing all objects in the `bucket1` bucket

```plaintext
./coscli ls cos://bucket1
```

The returned information includes the object key (the unique identifier of the object in the bucket), storage class, last update time, object size, and total number of objects. Below is an example:

```plaintext
        KEY      |   TYPE   |      LAST MODIFIED       |  SIZE
-----------------+----------+--------------------------+---------
        test.txt | STANDARD | 2022-01-01T00:00:00.000Z |   2  B
-----------------+----------+--------------------------+---------
                                   TOTAL OBJECTS:      |   1
                            ---------------------------+---------
```

#### Listing all objects and subdirectories in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli ls cos://bucket1/picture/
```

General listing only returns the data at the level of the query path, without expanding subpaths. Below is an example:

```plaintext
        KEY        |   TYPE   |      LAST MODIFIED       |  SIZE
-------------------+----------+--------------------------+---------
 picture/subfolder |      DIR |                          |   
  picture/pic1.png | STANDARD | 2022-01-01T00:00:00.000Z | 162  B
-------------------+----------+--------------------------+---------
                                   TOTAL OBJECTS:        |   2
                            -----------------------------+---------
```


#### Listing all objects in the `picture` directory in the `bucket1` bucket recursively

```plaintext
./coscli ls cos://bucket1/picture/ -r
```

If there are subpaths at the level of the query path, recursive listing will scan all subpaths and return all files under the level of the query path. Below is an example:

```plaintext
             KEY            |   TYPE   |      LAST MODIFIED       |  SIZE
----------------------------+----------+--------------------------+---------
 picture/subfolder/pic2.png |      DIR |                          |   
          picture/subfolder |      DIR |                          |   
           picture/pic1.png | STANDARD | 2022-01-01T00:00:00.000Z | 162  B
----------------------------+----------+--------------------------+---------
                                            TOTAL OBJECTS:        |   2
                                     -----------------------------+---------
```

#### Listing all MP4 objects in the `bucket1` bucket recursively

```plaintext
./coscli ls cos://bucket1 -r --include .*.mp4
```

#### Listing all non-MP4 objects in the `bucket1` bucket recursively

```plaintext
./coscli ls cos://bucket1 -r --exclude .*.mp4
```

#### Listing all non-JPG objects prefixed with `test` in the `picture` directory in the `bucket1` bucket

```plaintext
./coscli ls cos://bucket1/picture -r --include ^picture/test.* --exclude .*.jpg
```
