## Creating Repository
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
- app_id: `APPID` of your Tencent Cloud account.
- access_key_id: `SecretId` of your TencentCloud API key.
- access_key_secret: `SecretKey` of your TencentCloud API key.
- bucket: COS bucket name, **which cannot contain the `-{appId}` suffix**.
- region: COS bucket region, **which must be the same region as that of the ES cluster**.  For more information about regions, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091).
- base_path: backup directory.   

## Listing Repository Information
You can use `GET _snapshot` to get the repository information. You can also get the information of a specified repository by running `GET _snapshot/my_cos_backup`.

## Creating Snapshot Backup

### Backing up all indexes
Back up all indices in the ES cluster to the repository `my_cos_backup` and name it `snapshot_1`.
```
PUT _snapshot/my_cos_backup/snapshot_1
```
This command will be returned immediately and executed asynchronously in the background until the end. If you want to block the execution of the snapshot creating command, you can add the `wait_for_completion` parameter. **The duration of the command execution depends on the index size.**
```
PUT _snapshot/my_cos_backup/snapshot_1?wait_for_completion=true
```

### Backing up specified index
You can specify the index to be backed up when creating a snapshot. **If the value of the `indices` parameter is multiple indices, they should be separated by `, ` with no spaces.**
```
PUT _snapshot/my_cos_backup/snapshot_2
{
    "indices": "index_1,index_2"
}
```

## Querying Snapshot
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

## Deleting Snapshot
Delete the specified snapshot:
```
DELETE _snapshot/my_cos_backup/snapshot_1
```

>If there are uncompleted snapshots, the snapshot deleting command will still be executed and cancel the creation of such snapshots.

## Restoring from Snapshot
1. Restore all indices backed up in the snapshot to the ES cluster:
```
POST _snapshot/my_cos_backup/snapshot_1/_restore
```
 - If snapshot_1 contains 5 indices, then all of them will be restored to the ES cluster.   
 - You can also rename the indices through an additional option which allows you to match the index name by pattern and provide a new name through the restoration process. Use this option if you want to restore old data to verify the content or perform other operations without replacing existing data.

2. Restore a single index from a snapshot and provide an alternate name:
```
POST /_snapshot/my_cos_backup/snapshot_1/_restore
{
    "indices": "index_1",
    "rename_pattern": "index_(.+)",
    "rename_replacement": "restored_index_$1"
}
```
 - indices: only restores the index "index_1" and ignores other indices in the snapshot.
 - rename_pattern: finds the index being restored that can be matched by the specified pattern.
 - rename_replacement: renames the matching index to an alternate name.   

## Querying Snapshot Restoration Status
You can check the status of snapshot restoration and monitor the progress by running the `_recovery` command.   
1. You can call the following API separately in the index specified for restoration:
```
GET index_1/_recovery
```
2. This command will return the restoration status of each shard of the specified index.
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
 - type: this describes the nature of the restoration, i.e., this shard is restored from a snapshot.
 - source: the hash describes the specific snapshot and repository as the source of restoration.
 - percent: this describes the status of restoration. The particular shard has now restored 94% of the files, so it will be completely restored soon.   

The output lists all the indices that are being restored and all the shards in them. Each shard contains statistics such as start/stop time, duration, percentage of restoration, and number of bytes transferred.

## Canceling Snapshot Restoration
```
DELETE /restored_index_1
```
If `restored\_index\_1` is being restored, this deleting command will stop the restoration and delete all data that has been restored to the cluster.
