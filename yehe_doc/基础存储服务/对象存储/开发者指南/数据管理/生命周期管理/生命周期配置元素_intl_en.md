## Basic Structure

A lifecycle configuration is specified as XML and consists of one or more lifecycle rules. The structure is as follows:

```xml
<LifecycleConfiguration>
	<Rule>
		<ID>**your lifecycle name**</ID>
        <Status>Enabled</Status>
        <Filter>
            <And>
            	<Prefix>projectA/</Prefix>
                <Tag>
                	<Key>key1</Key>
                    <Value>value1</Value>
                </Tag>
            </And>
        </Filter>
        **transition/expiration actions**
	</Rule>
	<Rule>
		...
	</Rule>
</LifecycleConfiguration>
```

Each rule contains the following:

- ID (optional): Indicates the content of the rule and is customizable.
- Status: Indicates whether the rule is enabled or disabled.
- Filter: Identifies objects to which the rule applies.
- Action: Specifies actions (operations) that need to be performed on objects that match the above description.
- Time: `Days` (after the object's last modified date) or `Date` based on which actions are performed on objects.

## Rule Description

### Filter element

#### For all objects in bucket

Specify an empty filter, in which case the rule applies to all objects in the bucket.

```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### Based on object key prefix

Specify a prefix-based filter so that the rule applies only to objects with the specified prefix. For example, you can filter out objects by the prefix `logs/`:

```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
           <Prefix>logs/</Prefix>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### Based on object tag

Specify a filter based on `key` and `value` so that the rule applies only to objects with the specified tag. For example, you can filter out objects by tags `key=type` and `value=image`:
```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
           <Tag>
              <Key>type</Key>
              <Value>image</Value>
           </Tag>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

#### Using multiple filters

In COS, you can combine multiple filters by using `AND`. For example, you can filter out objects by the prefix `logs/` as well as tags `key=type` and `value=image`:
```xml
<LifecycleConfiguration>
    <Rule>
        <Filter>
            <And>
            	<Prefix>logs/</Prefix>
                <Tag>
              		<Key>type</Key>
              		<Value>image</Value>
           	 </Tag>
            </And>
        </Filter>
        <Status>Enabled</Status>
        **transition/expiration actions**
    </Rule>
</LifecycleConfiguration>
```

### Action element

Specify one or more predefined actions in a lifecycle rule so that these actions will be performed when any objects meet the rule.

#### Transition action

Specify the `Transition` action to transition objects from one storage class to another. For a versioning-enabled bucket, this action applies to the current object version. You can set the transition date to as short as 0 days. For example, you can transition objects to the ARCHIVE storage class in 30 days:

```xml
<Transition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</Transition>
```

#### Deletion upon expiration

Specify the `Expiration` action to delete expired objects. For a versioning-disabled bucket, expired objects will be permanently deleted. For a versioning-enabled bucket, expired objects are **added with a `DeleteMarker`** and become the current version. For example, you can delete objects that expire in 30 days:
```xml
<Expiration>
	<Days>30</Days>
</Expiration>
```

#### Incomplete multipart upload


>! You cannot specify object tags and clear incomplete multipart uploads at the same time in the same lifecycle rule.
>

Specify the `AbortIncompleteMultipartUpload` action to delete multipart upload tasks with the specified `UploadId` if they are not successfully completed within the predefined time period. Then, these tasks cannot be resumed or indexed. For example, you can abort multipart upload tasks not successfully completed within 7 days:
```xml
<AbortIncompleteMultipartUpload>
   <DaysAfterInitiation>7</DaysAfterInitiation>
</AbortIncompleteMultipartUpload>
```

#### Non-current object

In a versioning-enabled bucket, the `Transition` action only applies to objects of the latest version, and the `Expiration` action only results in adding delete markers to the objects. Therefore, COS provides the following actions for objects of non-current versions:

Specify the `NoncurrentVersionTransition` action to transition non-current objects to another storage class at the specified time. For example, you can transition non-current objects to the `ARCHIVE` storage class in 30 days:

```xml
<NoncurrentVersionTransition>
	<StorageClass>ARCHIVE</StorageClass>
    <Days>30</Days>
</NoncurrentVersionTransition>
```

Specify the `NoncurrentVersionExpiration` action to delete non-current objects at the specified time. For example, you can delete non-current objects in 30 days:
```xml
<NoncurrentVersionExpiration>
	<Days>30</Days>
</NoncurrentVersionExpiration>
```

Specify the `ExpiredObjectDeleteMarker` action to clear the remaining delete markers. You can set it to `true` or `false`. This action is triggered by the `NoncurrentVersionExpiration` action. If this feature is enabled, when lifecycle execution deletes the last historical version in the lifecycle of an object, COS will automatically delete the remaining delete markers.

The details are as follows. If the `NoncurrentVersionExpiration` action is in effect:
- If there is only one delete marker left, COS will automatically delete the last delete marker regardless of whether `ExpiredObjectDeleteMarker` is enabled.
- If there are multiple delete markers left, COS will check whether `ExpiredObjectDeleteMarker` is enabled (`true`), and if so, COS will automatically delete the remaining delete markers; otherwise, COS will not delete them.


```xml
<ExpiredObjectDeleteMarker>
	<Days>true|false</Days>
</ExpiredObjectDeleteMarker>
```

### Time element

#### Based on number of days

`Days` refers to the number of days since an object was last modified.
- For example, if an object is set to be transitioned to the `ARCHIVE` storage class in 0 days, when the object is uploaded at 2018-01-01 23:55:00 GMT+8, it will be added to the transition queue at 2018-01-02 00:00:00 GMT+8 and transitioned before 2018-01-02 23:59:59 GMT+8.
- For example, if an object is set to be deleted upon expiration in 1 day, when the object is uploaded at 2018-01-01 23:55:00 GMT+8, it will be added to the expiration queue at 2018-01-03 00:00:00 GMT+8 and deleted before 2018-01-03 23:59:59 GMT+8.

#### Based on specific date

Perform the predefined action on all eligible objects based on the filter on the specified `Date`. The date must be in the ISO 8601 format, and the time is always 00:00 GMT+8.
For example, use `2018-01-01T00:00:00+08:00` for January 1, 2018.


