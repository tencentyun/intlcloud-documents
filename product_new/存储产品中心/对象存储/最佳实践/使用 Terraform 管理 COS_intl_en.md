## Overview

Terraform is an open-source automated resource orchestration tool that uses code to manage and maintain IT resources.

Tencent Cloud began to use Terraform for resource orchestration in 2017. Up to now, Terraform is fully supported by more than 10 basic products of Tencent Cloud ranging from computing and storage to networks and databases. This document describes how to use Terraform to manage COS.

## Installing Terraform

Terraform is easy to install. For more information on how to install it, see the "Installing Terraform" section in [Tencent Cloud Terraform User Guide (I)](https://cloud.tencent.com/developer/article/1473713).

## Using Terraform to Manage COS 

#### 1. Initialize
(1) Create a working directory, such as `terraform-test`.
(2) Create or prepare a Tencent Cloud account for Terraform and get the SecretID and SecretKey.
(3) Compile a `provider` configuration file, write your account information such as SecretID and SecretKey to the `provider.tf` configuration file, and save it under the working directory (terraform-test). Below is a sample `provider.tf` configuration file:
```
provider "tencentcloud" {
	secret_id  = "AKIDdFUUEjgud7WpujygoiNsENJ1UigO****"
	secret_key = "yjFWbN4oJbeQwDG4e0AKN9f191f4****"
	region     = "ap-beijing"
}
```

> ?Fore more information on other configurations, see the "Configuring a Tencent Cloud `provider` File" section in [Tencent Cloud Terraform User Guide (I)](https://cloud.tencent.com/developer/article/1473713).

(4) Run the `init` command to initialize the working directory (e.g., terraform-test). Below is an example:
```
[root@tigger terraform-test]#terraform init
```

If the following message is printed, the initialization is successful.
```sh
Terraform has been successfully initialized!
```

>Each Terraform project needs a working directory in which all operations are performed. Some Terraform commands can specify a working directory in the parameters. For more information, see [Tencent Cloud Terraform User Guide (III)](https://cloud.tencent.com/developer/article/1482560). If no working directory is specified, the current directory will be used as the working directory by default.

#### 2. Create a bucket
(1) Compile a `resource` configuration file to define the resource. If you want to create a private bucket named `examplebucket-1250000000`, run the following sample code:
```
resource "tencentcloud_cos_bucket" "mycos" {
  bucket = "examplebucket-1250000000"     # Bucket name in the format of BucketName-APPID
  acl    = "private"  # The ACL permission is private
}
```

>During actual operations, be sure to replace the suffix of the bucket name with your real APPID; otherwise, COS will refuse to create a bucket.

Use a `*.tf` configuration file starting with `resource` to define the resource.
- tencentcloud_cos_bucket: Describes the resource type as a bucket. For more information on other resource types, see the left column [here](https://www.terraform.io/docs/providers/tencentcloud/r/cos_bucket.html).
- mycos: Describes the resource name which is customizable.

If you want to create a bucket that supports static websites, run the following sample code:

```
resource "tencentcloud_cos_bucket" "examplebucket2" {
  bucket = "examplebucket2-1250000000"

  website {
    index_document = "index.html"
    error_document = "error.html"
  }
}
```

If you want to set up CORS, run the following sample code:

```
resource "tencentcloud_cos_bucket" "examplebucket3" {
  bucket = "examplebucket3-1250000000"
  acl    = "public-read-write"

  cors_rules {
    allowed_origins = ["http://*.abc.com"]
    allowed_methods = ["PUT", "POST"]
    allowed_headers = ["*"]
    max_age_seconds = 300
    expose_headers  = ["Etag"]
  }
}
```

> Terraform can be used to manage the attributes of COS buckets such as website, ACL, cors_rules, and lifecycle_rules. For more information, see the "Argument Reference" section [here](https://www.terraform.io/docs/providers/tencentcloud/r/cos_bucket.html).

(2) Run the `terraform apply` command to deploy the resource and create a bucket named examplebucket-1250000000. You can log in to the [COS Console](https://console.cloud.tencent.com/cos5) to view the newly created bucket examplebucket-1250000000.

> If a bucket named examplebucket-1250000000 already exists, Terraform will delete the existing bucket first and then create an empty bucket.

Typically, before running the `terraform apply` command, you can run the `terraform plan` command first, which allows you to verify whether the execution plan can work as expected without changing the actual resource or status.

#### 3. Create an object resource

(1) Compile a `resource` configuration file to define the resource. If you want to upload the `picture.jpg` file to the `examplebucket-1250000000` bucket, run the following sample code:
```
resource "tencentcloud_cos_bucket_object" "myobject" {
  bucket = "examplebucket-1250000000"  # Bucket name in the format of BucketName-APPID
  key    = "picture.jpg"   # Object key
  source = "D:\folder\picture.jpg"  # Path to the file to be uploaded, which should contain the path and the filename
}
```

(2) Run the `terraform apply` command to deploy the resource and upload picture.jpg.

> 
> - Terraform can be used to manage the attributes of COS objects such as upload, ACL, content, ETag, and storage_class. For more information, see the "Argument Reference" section [here](https://www.terraform.io/docs/providers/tencentcloud/r/cos_bucket_object.html).
> - Currently, Terraform does not support downloading objects, because Terraform is designed to be a resource orchestration tool that focuses on the orchestration and deployment of cloud resources.

#### 4. Query a resource

4.1. Run the `terraform show` command to view the information of all resources (i.e., metadata of all buckets and objects).

To query the specific information of the specified bucket or object, you need to compile a configuration file and then run the `terraform apply` command.

4.2. Query detailed bucket information.

(1) Compile a `data source` configuration file to define refined query criteria. If you want to query the buckets prefixed with `example`, run the following sample code:
```
data "tencentcloud_cos_buckets" "cos_buckets" {
  bucket_prefix      = "example"  # Bucket prefix
  result_output_file = "mytestpath"  # Filename of the saved query result
}
```

Use a `*.tf` configuration file prefixed with `data` to define the query criteria.

- tencentcloud_cos_buckets: Describes the resource type as a bucket. For more information, see the left column [here](https://www.terraform.io/docs/providers/tencentcloud/d/cos_buckets.html).
- cos_buckets: Describes the resource name which is customizable.

(2) Run the `terraform apply` command to perform a query. The query result will be saved in the `mytestpath` file.

> For more information on how to query the information of the attributes of a bucket, see the "Argument Reference" section [here](https://www.terraform.io/docs/providers/tencentcloud/d/cos_buckets.html).

4.3. Query detailed object information.

(1) Compile a `data source` configuration file to define refined query criteria. If you want to query the metadata of the `picture.jpg` object, run the following sample code:

```
data "tencentcloud_cos_bucket_object" "mycos" {
  bucket             = "examplebucket-1250000000"  # Bucket name in the format of BucketName-APPID
  key                = "picture.jpg"  # Object key
  result_output_file = "mytestpath"  # Filename of the saved query result
}

```

(2) Run the `terraform apply` command to perform a query. The query result will be saved in the `mytestpath` file.

> For more information on how to query the information of the attributes of an object, see the "Argument Reference" section [here](https://www.terraform.io/docs/providers/tencentcloud/d/cos_bucket_object.html).

#### 5. Delete a resource

Run the `terraform destroy` command to delete all resources under the working directory.

To delete a specific bucket or object, you need to delete the configuration information which defines the bucket or object resource from the configuration file and then run the `terraform apply` command. You are recommended to use the `terraform show` to check the deletion result.

