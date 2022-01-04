The `mb` command is used to create a bucket.

## Command Syntax

```plaintext
./coscli mb cos://<BucketName-APPID> -r <Region> [flag]
```

`mb` includes the following optional flags:

| Flag Abbreviation | Flag Full Name   | Description                     |
| --------- | ------------- | ------------------------ |
| -h        | --help      | Outputs help information.       |
| -c        | --config-path | Path of the configuration file to use |
| -r        | --region      | Region of the bucket   |

>! To use the `md` command to create a bucket in COSCLI, you need to run the `config add` command to update the bucket configuration in the configuration file after running the `md` command successfully.
>

## Examples

```plaintext
// Create the bucket3 bucket.
./coscli mb cos://bucket3-1250000000 -r ap-chengdu
// Update the configuration file.
./coscli config add -b bucket3-1250000000 -r ap-chengdu -a bucket3
// After the update, you can access the bucket at cos://bucket3.
```
