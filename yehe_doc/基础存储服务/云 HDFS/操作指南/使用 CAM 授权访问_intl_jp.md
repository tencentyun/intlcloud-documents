## CHDFSのプリセットポリシー
CHDFSのプリセット権限ポリシーは次のとおりです。

| ポリシー| 説明 |
|---------|---------|
| QcloudCHDFSReadOnlyAccess | CHDFSの読み取り専用アクセス権限 | 
| QcloudCHDFSFullAccess | CHDFS権限の管理 |


#### CHDFS権限付与の操作

| **Action**                 | **Resouce**                                                  | **説明**             |
| -------------------------- | ------------------------------------------------------------ | -------------------- |
| chdfs:CreateFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/*       | CHDFSの作成            |
| chdfs:DeleteFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | CHDFSの削除            |
| chdfs:ModifyFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | CHDFSの属性変更        |
| chdfs:DescribeFileSystem   | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | CHDFSの詳細情報の確認    |
| chdfs:DescribeFileSystems  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | CHDFSリストの確認       |
| chdfs:CreateMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | マウントポイントの作成           |
| chdfs:DeleteMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | マウントポイントの削除           |
| chdfs:ModifyMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | マウントポイントの属性変更       |
| chdfs:DescribeMountPoint   | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | マウントポイントの詳細情報の確認   |
| chdfs:DescribeMountPoints  | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | マウントポイントリストの確認       |
| chdfs:AssociateAccessGroups   | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | 権限グループリストのバインド  |
| chdfs:DisassociateAccessGroups| qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | 権限グループリストのバインド解除 |
| chdfs:CreateAccessGroup    | qcs::chdfs:${region-id}:uin/${account-uin}:vpc/${vpc-id}<br>またはqcs::chdfs:${region-id}:uin/${account-uin}:unVpcId/${unVpcId}     | 権限グループの作成           |
| chdfs:DeleteAccessGroup    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 権限グループの削除           |
| chdfs:ModifyAccessGroup    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 権限グループの属性変更       |
| chdfs:DescribeAccessGroup  | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 権限グループの詳細情報の確認  |
| chdfs:DescribeAccessGroups | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 権限グループリストの確認       |
| chdfs:CreateAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id}  | 権限ルールの一括作成     |
| chdfs:DeleteAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessrule/${access-rule-id} | 権限ルールの一括削除     |
| chdfs:ModifyAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessrule/${access-rule-id} | 権限ルールの属性の一括変更 |
| chdfs:DescribeAccessRules  | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 権限ルールリストの確認     |
| chdfs:CreateLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | ライフサイクルルールの一括作成 |
| chdfs:DeleteLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:lifecyclerule/${life-cycle-rule-id} | ライフサイクルルールの一括削除 |
| chdfs:ModifyLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:lifecyclerule/${life-cycle-rule-id} | ライフサイクルルール属性の一括変更 |
| chdfs:DescribeLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | ライフサイクルルールリストの確認  |
| chdfs:CreateRestoreTasks    | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | リストアタスクの一括作成    |
| chdfs:DescribeRestoreTasks  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | リストアタスクリストの確認    |
| chdfs:ModifyResourceTags    | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | リソースタグリストの変更    |
| chdfs:DescribeResourceTags  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | リソースタグリストの確認     |


## CHDFS権限付与ポリシーの例
サブアカウントにCHDFS制御システムの読み取り専用アクセス権限を付与するためのポリシーの例は、次のとおりです。
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": [
			"name/chdfs:Describe*"
		],
		"resource": [
	 		"*"
		]
	}]
}
```

サブアカウントにCHDFSを確認する権限を付与するためのポリシーの例は、次のとおりです。
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": [
 			"name/chdfs:DescribeFileSystem"
  		],
		"resource": [
			"qcs::chdfs::uin/ownerUin:filesystem/fileSystemId"
		]
	}]
}
```
