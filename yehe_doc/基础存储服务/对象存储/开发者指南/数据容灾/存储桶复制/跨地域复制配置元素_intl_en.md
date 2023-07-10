## Basic Structure

Each COS bucket can have one cross-region replication rule, which is configured and edited in XML language in the following basic structure:

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
	<Rule>
	...
	</Rule>
</ReplicationConfiguration>
```

Here, `<Role>` indicates the identity of the cross-region replication initiator, and `<Rule>` the configured cross-region replication rule. Each rule contains the following:

- Status: Indicates whether the rule is enabled or disabled.
- ID: Indicates the specific rule name.
- Prefix: Indicates the prefix matching policy, which cannot be overlapped; otherwise, an error will be returned. When the prefix is empty, all objects in the bucket will be replicated. When the prefix has a value, only objects with the specified prefix value will be replicated.
- Destination: Indicates the destination bucket information, including `Bucket` and `StorageClass` elements:
	1. Bucket: Name and region of the destination bucket.
	2. StorageClass: Storage class of objects after being replicated to the destination bucket.

## Rule Description

### Object replication elements

#### Replicating all objects in a bucket

Specify an empty `<Prefix>` so that all objects in the bucket are replicated under the cross-region replication rule.

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

#### Replicating only objects with the specified prefix in a bucket

Specify a prefix so that only objects with the specified prefix in the bucket are replicated under the cross-region replication rule. For example, you can replicate objects with the prefix `logs/`:

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix>logs</Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

### Destination bucket elements

#### Destination bucket region and name

By modifying the `<Bucket>` parameter, you can specify a bucket in another region as the destination bucket. Note that the source and destination buckets must be in different regions under the same account.

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:cn-south::sevenyousouthtest-7319456</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

#### Object storage class in the destination bucket

By modifying the `<StorageClass>` parameter, you can specify the storage class of objects after they are replicated to the destination bucket. Copies are stored in the storage class of source objects by default. COS currently supports two storage classes for object copies: STANDARD and STANDARD_IA. If you want to store copies in ARCHIVE, you need to enable lifecycle in the destination bucket to implement object management.

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:cn-south::sevenyousouthtest-7319456</Bucket>
            <StorageClass>Standard</StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

