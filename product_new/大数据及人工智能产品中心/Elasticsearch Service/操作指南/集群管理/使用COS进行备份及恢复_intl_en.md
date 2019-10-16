## Creating a Repository
You can create a repository by running the following command:
```
PUT _snapshot/my_cos_backup
{
    "type": "cos",
    "settings": {
        "app_id": "xxxxxxx",
        "access_key_id": "xxxxxx",
        "access_key_secret": "xxxxxxx",
        "bucket": "xxxxxx",
        "region": "ap-guangzhou",
        "compress": true,
        "chunk_size": "500mb",
        "base_path": "/"
    }
}
```
- app_id: APPID of your Tencent Cloud account.
- access_key_id: SecretId of your TencentCloud API key.
- access_key_secret: SecretKey of your TencentCloud API key.
- bucket: Name of the COS bucket.
- region: Region of the COS bucket. It is recommended to select the same region as the ES cluster.
- base_path: Backup directory.   

## Listing Repository Information
You can get the repository information by running the following command:
```
GET _snapshot
```

You can also get the information of the specified repository by running `GET _snapshot/my_cos_backup`.


## Creating a Snapshot Backup

### Backing up All Indices
Back up all indices in the ES cluster to the repository `my_cos_backup` and name it `snapshot_1`.
```
PUT _snapshot/my_cos_backup/snapshot_1
```
This command will be returned immediately and executed asynchronously in the background until the end.   
If you want to block the execution of the snapshot creating command, you can add the `wait_for_completion` parameter:
```
PUT _snapshot/my_cos_backup/snapshot_1?wait_for_completion=true
```

>The duration of the command execution depends on the index size.

### Backing up the Specified Index
You can specify the index to be backed up when creating a snapshot:
```
PUT _snapshot/my_cos_backup/snapshot_2
{
    "indices": "index_1,index_2"
}
```

>If the value of the parameter "indices" is multiple indices, they should be separated by `, ` with no spaces.

## Querying a Snapshot
Query the information of a single snapshot:
```
GET _snapshot/my_cos_backup/snapshot_1
```
This command will return the information about the snapshot:
```
{
    "snapshots": [
        {
            "snapshot": "snapshot_1",
            "uuid": "zUSugNiGR-OzH0CCcgcLmQ",
            "version_id": 5060499,
            "version": "5.6.4",
            "indices": [
                "index_1",
                "index_2"
            ],
            "state": "SUCCESS",
            "start_time": "2018-05-04T11:44:15.975Z",
            "start_time_in_millis": 1525434255975,
            "end_time": "2018-05-04T11:45:29.395Z",
            "end_time_in_millis": 1525434329395,
            "duration_in_millis": 73420,
            "failures": [],
            "shards": {
                "total": 3,
                "failed": 0,
                "successful": 3
            }
        }
    ]
}
```

## Deleting a Snapshot
Delete the specified snapshot:
```
DELETE _snapshot/my_cos_backup/snapshot_1
```

>If there are uncompleted snapshots, the snapshot deleting command will still be executed and cancel the creation of such snapshots.

## Restoring from a Snapshot
Restore all indices backed up in the snapshot to the ES cluster:
```
POST _snapshot/my_cos_backup/snapshot_1/_restore
```
If snapshot_1 contains 5 indices, then all of them will be restored to the ES cluster.   
You can also rename the indices through an additional option. This option allows you to match the index name by pattern and provide a new name through the restoration process. Use this option if you want to restore old data to verify the content or perform other operations without replacing existing data.
Restore a single index from a snapshot and provide an alternate name:
```
POST /_snapshot/my_cos_backup/snapshot_1/_restore
{
    "indices": "index_1",
    "rename_pattern": "index_(.+)",
    "rename_replacement": "restored_index_$1"
}
```
- indices: Only restore the index "index_1" and ignore other indices in the snapshot.
- rename_pattern: Find the index being restored that can be matched by the specified pattern.
- rename_replacement: Rename the matching index to an alternate name.   

## Querying Snapshot Restoration Status
You can check the status of snapshot restoration and monitor the progress by running the `_recovery` command.   
You can call the following API separately in the index specified for restoration:
```
GET index_1/_recovery
```
This command will return the restoration status of each shard of the specified index:
```
{
    "sonested": {
        "shards": [
            {
                "id": 1,
                "type": "SNAPSHOT",
                "stage": "INDEX",
                "primary": true,
                "start_time_in_millis": 1525766148333,
                "total_time_in_millis": 8718,
                "source": {
                    "repository": "my_cos_backup",
                    "snapshot": "snapshot",
                    "version": "5.6.4",
                    "index": "index_1"
                },
                "target": {
                    "id": "TlzmxJHwSqyv4rhyQfRkow",
                    "host": "10.0.0.6",
                    "transport_address": "10.0.0.6:9300",
                    "ip": "10.0.0.6",
                    "name": "node-1"
                },
                "index": {
                    "size": {
                        "total_in_bytes": 1374967573,
                        "reused_in_bytes": 0,
                        "recovered_in_bytes": 160467084,
                        "percent": "11.7%"
                    },
                    "files": {
                        "total": 132,
                        "reused": 0,
                        "recovered": 20,
                        "percent": "15.2%"
                    },
                    "total_time_in_millis": 8716,
                    "source_throttle_time_in_millis": 0,
                    "target_throttle_time_in_millis": 0
                },
                "translog": {
                    "recovered": 0,
                    "total": 0,
                    "percent": "100.0%",
                    "total_on_start": 0,
                    "total_time_in_millis": 0
                },
                "verify_index": {
                    "check_index_time_in_millis": 0,
                    "total_time_in_millis": 0
                }
            }
        ]
    }
}
```
- type: This describes the nature of the restoration, i.e., this shard is restored from a snapshot.
- source: The hash describes the specific snapshot and repository as the source of restoration.
- percent: This describes the status of restoration. The particular shard has now restored 94% of the files, so it is almost finished.   

The output lists all the indices that are being restored and all the shards in them. Each shard contains statistics such as start/stop time, duration, percentage of restoration, and number of bytes transferred.

## Canceling Snapshot Restoration
```
DELETE /restored_index_1
```
If restored\_index\_1 is being restored, this deleting command will stop the restoration and delete all data that has been restored to the cluster.
