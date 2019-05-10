## 개발 준비
- [Python SDK](https://cloud.tencent.com/document/sdk/Python)를 다운로드 및 설치합니다.
- 처음 Batch Compute을 사용할 경우, [시작 전 준비](https://cloud.tencent.com/document/product/599/10807)를 참조하십시오.
- 더 많은 작업 구성 매개변수를 알아보려면 [작업 제출 API 문서](https://cloud.tencent.com/document/product/599/12683)를 참조하십시오.

## 시작 가이드

```
#!/usr/bin/python
# -*- coding: utf-8 -*-

# 클라우드 API 입구 모듈 가져오기
from QcloudApi.qcloudapi import QcloudApi

# 공통 구성
module = 'batch'

config = {
    'Region': 'ap-guangzhou',  # 대상 지역
    'secretId': '나의 secretId',
    'secretKey': '나의 secretKey',
}

service = QcloudApi(module, config)
```

## 작업 제출

```
try:
    action = 'SubmitJob'
    action_params = {
        'Version': '2017-03-12',
        'Job': {
            'JobName': 'batch-job', # 작업 이름
            'JobDescription': 'batch job',  # 작업 설명
            'Priority': '1',  # 작업 우선 순위
            'Tasks': [
                {
                    'TaskName': 'task1',  # 태스크 이름
                    'TaskInstanceNum':  1,  # 태스크 인스턴스 수
                    'FailedAction': 'FAST_INTERRUPT',  # 실패 작업 처리 방식
                    'Application': {
                        'DeliveryForm': 'LOCAL',  # 프로그램 패키지 출처
                        'Command': 'echo hello',  # 명령행
                        },
                    'EnvId': 'env-gbyctcy9',  # 컴퓨팅 환경 ID
                    'RedirectInfo': {
                        'StdoutRedirectPath': 'cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stdout/',  # 표준 출력 저장 경로
                        'StderrRedirectPath': 'cos://bucketgz-1251783334.cos.ap-guangzhou.myqcloud.com/stderr/',  #표준 오류 저장 경로
                        }
                    }
                ]
            },
        'Placement': {
            'Zone': 'ap-guangzhou-2'  # 가용 영역
            },
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [작업 제출 API 문서](https://cloud.tencent.com/document/product/599/12683)를 참조하십시오.

## 작업 종료

```
try:
    action = 'TerminateJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # 작업 ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [작업 종료 API 문서](https://cloud.tencent.com/document/product/599/12689)를 참조하십시오.

## 작업 삭제

```
try:
    action = 'DeleteJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # 작업 ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [작업 삭제 API 문서](https://cloud.tencent.com/document/product/599/12682)를 참조하십시오.

## 작업의 제출 정보 보기

```
try:
    action = 'DescribeJobSubmitInfo'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # 작업 ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [작업의 제출 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/12687)를 참조하십시오.

## 작업 정보 보기

```
try:
    action = 'DescribeJob'
    action_params = {
        'Version': '2017-03-12',
        'JobId': 'job-8kwnzki7',  # 작업 ID
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [작업 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/12685)를 참조하십시오.

## 작업 목록 보기

```
try:
    action = 'DescribeJobs'
    action_params = {
        'Version': '2017-03-12'
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [작업 목록 보기 API 문서](https://cloud.tencent.com/document/product/599/12686)를 참조하십시오.

## 태스크 정보 보기

```
try:
    action = 'DescribeTask'
    action_params = {
        'Version': '2017-03-12',
	'JobId': 'job-8kwnzki7',  # 작업 ID
	'TaskName': 'task A'  # 태스크 이름
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [태스크 정보 보기 API 문서](https://cloud.tencent.com/document/product/599/12684)를 참조하십시오.

## 태스크 인스턴스 종료

```
try:
    action = 'TerminateTaskInstance'
    action_params = {
        'Version': '2017-03-12',
	'JobId': 'job-8kwnzki7',  # 작업 ID
	'TaskName': 'task A',  # 태스크 이름
	'TaskInstanceIndex': 1  # 첫 번째 인스턴스
        }
    print(service.generateUrl(action, action_params))
    print(service.call(action, action_params))
except Exception as e:
    import traceback
    print('traceback.format_exc():\n%s' % traceback.format_exc())
```
더 많은 매개변수 설명 및 오류 정보는 [태스크 인스턴스 종료 API 문서](https://cloud.tencent.com/document/product/599/12688)를 참조하십시오.
