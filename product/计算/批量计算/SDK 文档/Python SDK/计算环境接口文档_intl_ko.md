## 개발 준비
- [Python SDK](https://cloud.tencent.com/document/sdk/Python)를 다운로드 및 설치합니다.
- 처음 Batch Compute을 사용할 경우, [시작 전 준비](https://cloud.tencent.com/document/product/599/10807)를 참조하십시오.
- 더 많은 컴퓨팅 환경 구성 매개변수를 알아보려면 [컴퓨팅 환경 생성 API 문서](https://cloud.tencent.com/document/product/599/12691)를 참조하십시오.

## 시작 가이드

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 입구 모듈 가져오기
from QcloudApi.qcloudapi import QcloudApi

# 공통 구성
module = 'batch'

config = {
    'Region': 'ap-beijing',
    'secretId': '나의 secretId',
    'secretKey': '나의 secretKey',
}

service = QcloudApi(module, config)
```

## 컴퓨팅 환경 생성

```
try:
    action = 'CreateComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        "ComputeEnv": {
            "EnvName": "Cluster-A",  # 컴퓨팅 환경 이름
            "EnvDescription": "first cluster",  # 컴퓨팅 환경 설명
            "EnvType": "MANAGED",
            "MountDataDisks": [
                {
                    "FileSystemType": "NTFS",
                    "LocalPath": J://",  # 데이터 디스크 탑재 포인트
                    }
                ],
            "EnvData": {
                "InstanceType": "S2.SMALL1",  # 인스턴스 유형
                "ImageId": "img-er9shcln",  # 이미지 ID
                "LoginSettings": {
                    "Password": "B1[habcdB1[habcd"  # 로그인 비밀번호
                    },
                "InternetAccessible": {
                    "PublicIpAssigned": "TRUE",  # 공인 IP
                    "InternetMaxBandwidthOut": 50  # 공중망 대역폭
                    },
                "SystemDisk": {
                    "DiskType": "LOCAL_BASIC",  # 시스템 디스크 유형
                    "DiskSize": 50  # 시스템 디스크 크기
                    },
                "DataDisks": [
                    {
                        "DiskType": "LOCAL_BASIC",  # 데이터 디스크 유형
                        "DiskSize": 50  # 데이터 디스크 크기
                        }
                    ]
                },
            "DesiredComputeNodeCount": 1  # 컴퓨팅 노드 수
            },
        "Placement": {
            "Zone": "ap-beijing-2"  # 가용 영역
            },
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
 더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 생성 API 문서](https://cloud.tencent.com/document/product/599/12691)를 참조하십시오.
## 컴퓨팅 환경 수정

```
try:
    action = 'ModifyComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "env-cc44pzme",  # 컴퓨팅 환경 ID
        'DesiredComputeNodeCount': 100,  # 예상 노드 수
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
 더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 수정 API 문서](https://cloud.tencent.com/document/product/599/13637)를 참조하십시오.

 ## 컴퓨팅 클러스터 삭제

```
try:
    action = 'DeleteComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "env-cc44pzme",  # 컴퓨팅 환경 ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
 더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 삭제 API 문서](https://cloud.tencent.com/document/product/599/12692)를 참조하십시오.

 ## 컴퓨팅 환경 생성 정보 보기

```
try:
    action = 'DescribeComputeEnvCreateInfo'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "",  # 컴퓨팅 환경 ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
 더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 생성 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/14604)를 참조하십시오.

 ## 컴퓨팅 환경 정보 보기

```
try:
    action = 'DescribeComputeEnv'
    action_params = {
        'Version': '2017-03-12',
        'EnvId': "",  # 컴퓨팅 환경 ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/12694)를 참조하십시오.

## 컴퓨팅 환경 목록 보기

```
try:
    action = 'DescribeComputeEnvs'
    action_params = {
        'Version': '2017-03-12',
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [컴퓨팅 환경 목록 보기 API 문서](https://cloud.tencent.com/document/product/599/12695)를 참조하십시오.
