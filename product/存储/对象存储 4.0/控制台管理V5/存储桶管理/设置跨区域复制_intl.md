When cross-origin replication is enabled, objects in the source bucket can be automatically and asynchronously replicated to the target bucket in another region. When you perform operations on objects in the source bucket (such as adding objects and deleting objects), COS automatically replicates these operations to the target bucket. Cross-origin replication requires that the source bucket and the target bucket be in different available regions, and version control be enabled for both of them. You can enable or disable cross-origin replication based on your actual needs.

## Enabling Cross-origin Replication
### Procedure
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List** on the left navigation pane, and click the source bucket for which you need to configure cross-origin replication to enter the bucket details page.
![](https://main.qcloudimg.com/raw/b7edddd47cb89b06c02292dbda407b75.png)

2. Click **Basic Configuration** on the top to enter the Basic Configuration page of the bucket, scroll down to find **Cross-origin Replication**, and click the **New Rule** button on the right to set the cross-origin replication rule.
![](https://main.qcloudimg.com/raw/e5d37d4897c3095dcb362b489ccf9707.png)

3. Version control is required to be enabled for both the source bucket and the target bucket before you configure the cross-origin replication rule. Click **OK** after the rule is configured.
![](https://main.qcloudimg.com/raw/a0b825707606faba4db1141ff06bcebf.png)

The fields in the cross-origin replication rule configuration box are described as follows:
-  Scope: Refers to the scope of objects in the source bucket that need to be replicated. If not set, all objects in the bucket are replicated by default. If a prefix is specified, the objects with such a prefix are replicated (for example, to replicate files with the prefix of `logs/`, you should enter `logs/`).
-  Target Bucket: Refers to the bucket to which the objects are replicated. The bucket should be in a different region from the source bucket and should be one under the current account in the selected region.
-  Target Storage Class: Refers to the storage class of the objects replicated to the target bucket. It is the same with that of the objects in the source bucket by default. You can also select other storage class for the replicated objects in the target bucket, and Standard and Infrequent Access storage classes are supported.

>!
>- After configuring the rule, you can edit it in **Cross-origin Replication** on the Basic Configuration page of the bucket. You can enable or disable the rule, and modify the scope, target bucket, target storage class and other options.
>- If you set the scope to "entire bucket" at the first time setting up the cross-origin replication rule, you will not be able to add any rules or modify the scope to "specified prefix". In this case, you can delete the current rule and add a new rule.
>- If you set the scope to "specified prefix" at the first time setting up the cross-origin replication rule, you will not be able to modify the scope to "entire bucket". In this case, you can delete all the rules where the scope is set to "specified prefix" and then add new rules where the scope is set to "entire bucket".

## Disabling Cross-origin Replication
### Procedure

You can disable cross-origin replication by turning off the Status button or by deleting the rule.
- **Turning off the Status button**: Turning off the Status button in a rule will disable the rule, and suspend the cross-origin replication feature. In this case, the replicated data will be retained in the target bucket, and the incremental data in the source bucket will no longer be replicated.
- **Deleting the rule**: Delete the added rule in **Cross-origin Replication**. After the deletion, the configured cross-origin replication rule will be invalid, the replicated data will be retained in the target bucket, and the incremental data in the source bucket will not be replicated. To use the cross-origin replication rule again, you need to reconfigure it.
![](https://main.qcloudimg.com/raw/a9b306f08c0eabe43820bd76b487bade.png)

>!
>- A cross-origin replication operation in progress will be aborted when cross-origin replication is disabled and will not continue.
>- When cross-origin replication is enabled again for a bucket, replication is performed only for newly replicated objects after the time of enablement.

