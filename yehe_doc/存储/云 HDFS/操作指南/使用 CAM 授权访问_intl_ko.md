## CHDFS 정책 사전 설정
CHDFS 라이선스 정책 사전 설정은 다음과 같습니다. 

| 정책| 설명 |
|---------|---------|
| QcloudCHDFSReadOnlyAccess |  CHDFS 읽기 전용 액세스 권한 | 
| QcloudCHDFSFullAccess | CHDFS 관리 권한 |


#### CHDFS 라이선스 작업

| **Action**                 | **Resouce**                                                  | **설명**             |
| -------------------------- | ------------------------------------------------------------ | -------------------- |
| chdfs:CreateFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/*       |  CHDFS 생성            |
| chdfs:DeleteFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} |  CHDFS 삭제            |
| chdfs:ModifyFileSystem     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | CHDFS 속성 수정       |
| chdfs:DescribeFileSystem   | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} |  CHDFS 상세 정보 조회    |
| chdfs:DescribeFileSystems  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | CHDFS 리스트 조회        |
| chdfs:CreateMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | 마운트 포인트 생성           |
| chdfs:DeleteMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | 마운트 포인트 삭제           |
| chdfs:ModifyMountPoint     | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | 마운트 포인트 속성 수정       |
| chdfs:DescribeMountPoint   | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | 마운트 포인트 상세 정보 조회   |
| chdfs:DescribeMountPoints  | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | 마운트 포인트 리스트 조회       |
| chdfs:AssociateAccessGroups   | qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | 권한 그룹 리스트 바인딩  |
| chdfs:DisassociateAccessGroups| qcs::chdfs:${region-id}:uin/${account-uin}:mountpoint/${mount-point-id} | 권한 그룹 리스트 바인딩 해제  |
| chdfs:CreateAccessGroup | qcs::chdfs:${region-id}:uin/${account-uin}:vpc/${vpc-id} 또는 qcs::chdfs:${region-id}:uin/${account-uin}:unVpcId/${unVpcId} | 권한 그룹 생성 |
| chdfs:DeleteAccessGroup    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 권한 그룹 삭제           |
| chdfs:ModifyAccessGroup    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 권한 그룹 속성 수정       |
| chdfs:DescribeAccessGroup  | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 권한 그룹 상세 정보 조회  |
| chdfs:DescribeAccessGroups | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 권한 그룹 리스트 조회       |
| chdfs:CreateAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id}  |권한 규칙 일괄 생성     |
| chdfs:DeleteAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessrule/${access-rule-id} | 권한 규칙 일괄 삭제     |
| chdfs:ModifyAccessRules    | qcs::chdfs:${region-id}:uin/${account-uin}:accessrule/${access-rule-id} | 권한 규칙 속성 일괄 수정 |
| chdfs:DescribeAccessRules  | qcs::chdfs:${region-id}:uin/${account-uin}:accessgroup/${access-group-id} | 권한 규칙 리스트 조회     |
| chdfs:CreateLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | 라이프사이클 규칙 일괄 생성 |
| chdfs:DeleteLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:lifecyclerule/${life-cycle-rule-id} | 라이프사이클 규칙 일괄 삭제 |
| chdfs:ModifyLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:lifecyclerule/${life-cycle-rule-id} | 라이프사이클 규칙 속성 일괄 수정 |
| chdfs:DescribeLifeCycleRules | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | 라이프사이클 규칙 리스트 조회  |
| chdfs:CreateRestoreTasks    | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | 복구 작업 일괄 생성    |
| chdfs:DescribeRestoreTasks  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | 복구 작업 리스트 조회    |
| chdfs:ModifyResourceTags    | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id}  | 리소스 태그 리스트 수정    |
| chdfs:DescribeResourceTags  | qcs::chdfs:${region-id}:uin/${account-uin}:filesystem/${file-system-id} | 리소스 태그 리스트 조회     |


## CHDFS 라이선스 정책 예시
서브 계정에 CHDFS 관리 시스템 읽기 전용 권한을 부여하는 정책 예시는 다음과 같습니다.  
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

서브 계정에 CHDFS 조회 권한을 부여하는 정책 예시는 다음과 같습니다.  
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
