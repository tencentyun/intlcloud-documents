With the batch operation feature in COS, you can specify an operation on a specified list of objects in a bucket. To do so, you have two options: either create an inventory of the objects via the inventory feature or list the desired objects in a CSV file as formatted in the inventory. Those objects will then be batch operated as specified in COS.

For more information, see [Inventory Overview](https://www.tencentcloud.com/document/product/436/30622).

At present, the batch operation feature only supports the following operations:

- [Batch copying objects](https://intl.cloud.tencent.com/document/product/436/32960)
- [Batch restoring archived objects](https://intl.cloud.tencent.com/document/product/436/34075)

You can use the batch operation feature in the COS console. For more information, see [Batch Operation](https://intl.cloud.tencent.com/document/product/436/32956).



## How It Works

To perform a batch operation, you need to create a batch operation job first, which contains all the information needed to perform the specified operation on the object list. You can use an inventory as an object list.

After you provide an inventory file and start the created batch operation job, the batch operation feature will execute the specified operation on the objects in the inventory sequentially. During job execution, you can monitor the execution status in the COS console or choose to output a job report after the job is completed. The job report provides details about each operation in the job.

> !The batch operation feature is only applicable to objects in the current bucket. If you want to batch operate on the objects in another bucket, please enable the batch operation feature for that bucket.

## Object Inventory

An object inventory is a list of all the objects to be operated on. To create a batch operation job, you need to provide an object inventory first to tell COS what objects it should operate on. You need to put the object inventory file in the bucket and provide information such as the filename, ETag, and VersionID (if applicable). You can create an object inventory in the following two ways:

- **COS inventory feature**: This feature outputs an object inventory in CSV format. For more information, see [Inventory Overview](https://www.tencentcloud.com/document/product/436/30622). If your object inventory contains version ID information, COS will batch operate on the objects with the corresponding version ID.
- **CSV file configuration**: Every row in the CSV file must contain the bucket name and the name and version ID (if versioning is enabled for the bucket) of an object for batch operation. If versioning has never been enabled, you can skip the version ID information. The CSV file can be configured as follows:
```plaintext
examplebucket-appid, exampleobject, PZ9ibn9D5lP6p298B7S9_ceqx1n5EJ0p
examplebucket-appid, exampleobject, jbo9_jhdPEyB4RrmOxWS0kU0EoNrU_oI
```

> !
> - If versioning is or was once enabled for your bucket, and you want to perform a batch operation on the specified version of the object, you must provide object version ID information in the object inventory.
> - If versioning is or was once enabled for your bucket, but you don't specify a version ID in the inventory, COS will operate on the latest version of the object by default.
> - If you uploaded an object with the same name as an object to be operated on before creating a job, COS will operate on the object on the latest version by default rather than the version when the object inventory was created. To avoid this issue, you can enable versioning and specify the version ID in the object inventory.
> - An object inventory can contain all the objects in a bucket. However, note that it takes longer to operate on a large number of objects.
> 

## Batch Operation Job

This section describes how to create a batch operation job and how the system will respond after creation.

When creating a batch operation job, you need to provide the following information:

| Type | Description |
|---------|---------|
| Operation | You need to specify which operation is to be performed on objects. Corresponding parameters can be configured for each operation, and COS will perform the operation on the objects in the inventory sequentially as configured. |
| Object inventory | An object inventory is a list of all the objects to be operated on. You can create an object inventory through the inventory feature. For more information, see [Inventory Overview](https://www.tencentcloud.com/document/product/436/30622). You can also list desired objects in a CSV file as formatted in the inventory. |
| Priority | You can set priority to identify the precedence of the current batch operation job over other jobs. Job priority does not directly determine the order in which jobs will be completed. If you want to control the order of multiple jobs, you need to check the job execution status on your own and start the next job after the current one is completed. |
| Rule permission | After creating a batch operation job, you need to make sure that your account has the corresponding IAM permission to perform the operation. For example, if you have created a batch operation job to execute `PUT Object-copy`, you should make sure that your account has the `Get Object` permission in the source bucket and the `PUT Object` permission in the destination bucket. In addition, for all batch operation jobs, you should have permission to read the object inventory and write into the job report. For more information on permission configuration, see [Overview](https://intl.cloud.tencent.com/document/product/436/18023) and [Bucket Policy](https://intl.cloud.tencent.com/document/product/436/45235). |
| Job report | If you want to output a job report after a batch operation job is completed, you need to enter the corresponding parameters when creating the job, so that the system can correctly output the job report to the specified destination bucket. The required information includes the bucket to store the job report, job report format, and whether all job information should be included. The file prefix of the job report is optional. |
| Job description (optional) | You can enter 256-byte job description for your created batch operation job to keep track of it. The job description will be displayed in the COS console and can be used to sort or filter jobs. You can enter same job description for similar jobs (e.g., syncing and copying log data weekly) to manage them in a centralized manner.

