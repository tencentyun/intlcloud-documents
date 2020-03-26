## 호출 준비
명령줄 스크립트로 API를 호출하려면 SecretId 및 SecretKey 설정이 필요합니다. Tencent Cloud에 로그인하여 [API Keys](https://console.cloud.tencent.com/capi)에 진입하면 API 호출에 필요한 SecretId 및 SecretKey를 확인할 수 있으며, 키를 안전하게 보관하시기 바랍니다.
![](https://mc.qcloudimg.com/static/img/6ca171d3f6662016a8f31cc5520ffaeb/1.png)

## 사용 설명
명령줄의 Python 스크립트 다운로드. [다운로드](https://github.com/zz-mars/CDN_API_DEMO/tree/master/Qcloud_CDN_API/python)

### 사용 준비
상술한 Python 스크립트 사용 시 requests 라이브러리 설치가 필요하며 다음 명령을 사용할 수 있습니다.
```
pip install requests
```
스크립트를 실행하면 현재 지원하는 인터페이스 인벤토리가 보여집니다.
![](https://mc.qcloudimg.com/static/img/813c521d24602315a8ddd18c644f56a6/2.png)
인터페이스 기능 설명은 [API 개요](https://intl.cloud.tencent.com/document/api/228/1723)를 참조하십시오.
### 도메인 상세 정보 조회
#### 모든 도메인 상세 정보 조회
1. 다음 명령어로 [DescribeCdnHosts](https://intl.cloud.tencent.com/document/api/228/3937) 인터페이스를 호출해 APPID 하의 모든 도메인 상세 정보를 조회할 수 있습니다.
```
python QcloudCdnTools_V2.py DescribeCdnHosts -u xxxxxx -p xxxxxxx
```
2. 매개변수 설명
 -  -u는 SecretId를 말합니다.
 -  -p는 SecretKey를 말합니다.
3. 결과 예시
```josn
{
    u'total': 1,
    u'hosts': [
        {
            u'origin': u'8.8.8.8',
            u'enable_overseas': u'no',
            u'disabled': 0,
            u'create_time': u'2016-07-2610: 34: 09',
            u'seo': u'off',
            u'message': u'\u90e8\u7f72\u4e2d',
            u'id': 279950,
            u'cache': [
                {
                    u'type': 0,
                    u'unit': u'd',
                    u'rule': u'all',
                    u'time': 2592000
                },
                {
                    u'type': 1,
                    u'unit': u's',
                    u'rule': u'.php;.jsp;.asp;.aspx',
                    u'time': 0
                }
            ],
            u'middle_resource': -1,
            u'fwd_host_type': u'default',
            u'readonly': 0,
            u'fwd_host': u'www.test.com',
            u'service_type': u'media',
            u'project_id': 0,
            u'refer': {
                u'list': [                  
                ],
                u'type': 0,
                u'null_flag': 0
            },
            u'status': 4,
            u'update_time': u'2016-08-1220: 36: 58',
            u'ssl_expire_time': None,
            u'deleted': u'no',
            u'ssl_type': 0,
            u'ssl_deploy_time': None,
            u'app_id': 1251991073,
            u'host': u'www.test.com',
            u'bucket_name': u'',
            u'host_id': 279950,
            u'pid_config': None,
            u'cache_mode': u'simple',
            u'furl_cache': u'on',
            u'host_type': u'cname',
            u'owner_uin': 78976504,
            u'cname': u'www.test.com.cdn.dnsv1.com'
        }
        ...
    ]
}
```

#### 도메인에 따라 도메인 상세 정보 조회
1. 다음 명령어로 [GetHostInfoByHost](https://intl.cloud.tencent.com/document/api/228/3938) 인터페이스를 호출해 특정 도메인에 대응하는 상세 정보를 조회할 수 있습니다.
```
python QcloudCdnTools_V2.py GetHostInfoByHost -u xxxxx -p xxxxxxx --hosts www.test.com --hosts www.test2.com
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 -  -p 는 SecretKey를 말합니다.
 -   --hosts는 조회할 도메인을 의미하며, 한 번에 여러 개를 조회할 수 있고 모두 --hosts를 사용합니다. 인터페이스 매개변수는 바 두 줄을 사용하니 주의하십시오.

3. 결과 예시
```json
{
    u'total': 2,
    u'hosts': [
        {
            u'origin': u'8.8.8.8',
            u'enable_overseas': u'no',
            u'disabled': 0,
            u'create_time': u'2016-07-2610: 34: 09',
            u'seo': u'off',
            u'message': u'\u5df2\u5f00\u542f',
            u'id': 1234,
            u'cache': [
                {
                    u'type': 0,
                    u'unit': u'd',
                    u'rule': u'all',
                    u'time': 2592000
                },
                {
                    u'type': 1,
                    u'unit': u's',
                    u'rule': u'.php;.jsp;.asp;.aspx',
                    u'time': 0
                }
            ],
            u'middle_resource': -1,
            u'fwd_host_type': u'default',
            u'readonly': 0,
            u'fwd_host': u'www.test.com',
            u'service_type': u'media',
            u'project_id': 0,
            u'refer': {
                u'list': [                 
                ],
                u'type': 0,
                u'null_flag': 0
            },
            u'status': 5,
            u'update_time': u'2016-08-1220: 36: 58',
            u'ssl_expire_time': None,
            u'deleted': u'no',
            u'ssl_type': 0,
            u'ssl_deploy_time': None,
            u'app_id': 1251991073,
            u'host': u'www.test.com',
            u'bucket_name': u'',
            u'host_id': 279950,
            u'pid_config': None,
            u'cache_mode': u'simple',
            u'furl_cache': u'on',
            u'host_type': u'cname',
            u'owner_uin': 78976504,
            u'cname': u'www.test.com.cdn.dnsv1.com'
        },
        ...
    ]
}
```


#### 도메인 ID에 따라 도메인 상세 정보 조회
1. 다음 명령어로 [GetHostInfoById](https://intl.cloud.tencent.com/document/api/228/3939) 인터페이스를 호출해 ID에 대응하는 도메인 상세 정보를 조회할 수 있습니다.
```
python QcloudCdnTools_V2.py GetHostInfoById -u xxxxx -p xxxxxxx --ids 1234
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - --ids는 조회할 도메인 ID를 의미하며, 한 번에 여러 개를 조회할 수 있고 모두 --ids를 사용합니다. 인터페이스 매개변수는 바 두 줄을 사용하니 주의하십시오.

3. 결과 예시
```json
{
    u'total': 1,
    u'hosts': [
        {
            u'origin': u'8.8.8.8',
            u'enable_overseas': u'no',
            u'disabled': 0,
            u'create_time': u'2016-07-2610: 34: 09',
            u'seo': u'off',
            u'message': u'\u5df2\u5f00\u542f',
            u'id': 1234,
            u'cache': [
                {
                    u'type': 0,
                    u'unit': u'd',
                    u'rule': u'all',
                    u'time': 2592000
                },
                {
                    u'type': 1,
                    u'unit': u's',
                    u'rule': u'.php;.jsp;.asp;.aspx',
                    u'time': 0
                }
            ],
            u'middle_resource': -1,
            u'fwd_host_type': u'default',
            u'readonly': 0,
            u'fwd_host': u'www.test.com',
            u'service_type': u'media',
            u'project_id': 0,
            u'refer': {
                u'list': [                 
                ],
                u'type': 0,
                u'null_flag': 0
            },
            u'status': 5,
            u'update_time': u'2016-08-1220: 36: 58',
            u'ssl_expire_time': None,
            u'deleted': u'no',
            u'ssl_type': 0,
            u'ssl_deploy_time': None,
            u'app_id': 1251991073,
            u'host': u'www.test.com',
            u'bucket_name': u'',
            u'host_id': 279950,
            u'pid_config': None,
            u'cache_mode': u'simple',
            u'furl_cache': u'on',
            u'host_type': u'cname',
            u'owner_uin': 78976504,
            u'cname': u'www.test.com.cdn.dnsv1.com'
        }
    ]
}
```

### 퍼지와 프리패치
#### URL 퍼지
1. 다음 명령어로 [RefreshCdnUrl](https://intl.cloud.tencent.com/document/api/228/3946) 인터페이스를 호출해 특정 URL을 갱신할 수 있습니다.
```
python QcloudCdnTools_V2.py RefreshCdnUrl -u xxxxx -p xxxxxxx --urls http://xxxxxxxtang.sp.oa.com/test.php --urls http://www.test.com/1.html
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - --urls는 갱신할 URL을 의미하며, 한 번에 여러 개를 조회할 수 있고 모두 --urls를 사용합니다.
 -  urls 매개변수 앞에 반드시 http:// 또는 https://의 접두사를 추가해야 합니다.
 - 모든 사용자는 매일 URL 10,000개를 갱신할 수 있고, 1번당 최대 1,000개까지 제출하여 갱신할 수 있습니다.

3. 결과 예시
```json
[
    {
        u'log_id': 220332,
        u'count': 1
    }
]
```
그중 log_id는 제출한 갱신 작업 ID를 말하며, 이 ID에 따라 해당 갱신 작업의 실행 상태를 조회할 수 있습니다. count는 이번에 제출한 URL 갱신 수를 말합니다.

#### 목록 갱신
1. 다음 명령어로 [RefreshCdnDir](https://intl.cloud.tencent.com/document/api/228/3947) 인터페이스를 호출해 특정 목록을 갱신할 수 있습니다.
```
python QcloudCdnTools_V2.py RefreshCdnDir -u xxxxx -p xxxxxxx --dirs http://www.test.com/abc/
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - --dirs는 갱신할 URL을 의미하며, 한 번에 여러 개를 조회할 수 있고 모두 --dirs를 사용합니다.
 -  dirs 매개변수 앞에 반드시 http:// 또는 https://의 접두사를 추가해야 합니다.
 - 모든 사용자는 매일 목록 100개를 갱신할 수 있고, 1번당 최대 20개까지 제출하여 갱신할 수 있습니다.

3. 결과 예시
```json
request is success.
```

#### 갱신 기록 조회
1. 다음 명령어를 사용해 갱신 기록을 조회할 수 있습니다.
```
python QcloudCdnTools_V2.py GetCdnRefreshLog -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-16
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - startDate는 조회 시작 일시를, endDate는 조회 종료 일시를 말하며, startDate는 endDate보다 작아야 합니다.

3. 결과 예시
```json
{
    u'total': 2,
    u'logs': [
        {
            u'status': 1,
            u'complete_time': u'2016-08-1510: 39: 16',
            u'url_list': [
                u'http: //www.test.org/1.html'
            ],
            u'app_id': 1251991073,
            u'datetime': u'2016-08-1510: 39: 14',
            u'host': u'www.test.org',
            u'project_id': 0,
            u'type': 0,
            u'id': 1234
        },
		...
	]
}
```
그중 status는 갱신 상태를, 1은 갱신 완료를 의미합니다. URL 갱신, 목록 갱신 기록은 모두 이 인터페이스를 통해 조회할 수 있습니다.

### 도메인설정
#### 캐시 설정 수정
1. 다음 명령어로 [UpdateCache](https://intl.cloud.tencent.com/document/api/228/3934) 인터페이스를 호출해 캐시 만료 설정을 수정할 수 있습니다.
```
python QcloudCdnTools_V2.py UpdateCache -u xxxxx -p xxxxxxx --hostId 1234 --cache [[0,\"all\",1000],[1,\".jpg;.js\",2000],[2,\"/www/html\",3000]]
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - hostId는 캐시 만료 설정 수정의 도메인 ID가 필요합니다.
 - cache는 목표 캐시 설정을 말하며 쌍 따옴표 확장이 필요하니 주의하십시오.

 **캐시 만료 설정**
도메인 1개의 캐시 만료 설정은 몇 줄의 캐시 만료 설정으로 구성되며, 각각의 캐시 만료 설정은 매개변수 3개로 구분됩니다. 첫 번째는 캐시 유형, 두 번째는 매칭 규칙, 세 번째는 설정의 만료 시간, 단위는 초입니다. CDN은 3가지 유형을 제공합니다.
 - 0: 모든 유형, 매칭된 모든 파일을 말하며 기본 캐시 설정입니다.
 - 1: 파일 유형, 파일 접미사에 따른 매칭을 말합니다. 매칭 내용 예시: jpg;.png
 - 2: 폴더 유형, 목록에 따른 매칭을 말합니다. 매칭 내용 예시: /abc;/def

3. 결과 예시
```json
request is success.
```

#### 도메인 세부 항목 수정
1. 다음 명령어로 [UpdateCdnProject](https://intl.cloud.tencent.com/document/api/228/3935) 인터페이스를 호출해 도메인 세부 항목을 수정할 수 있습니다.
```
python QcloudCdnTools_V2.py UpdateCdnProject -u xxxxx -p xxxxxxx --hostId 1234 --projectId 0
```
도메인 세부 항목 수정 시 항목에 대응하는 ID를 알아야 합니다. [항목 관리](https://console.cloud.tencent.com/project)에서 조회할 수 있으며, 기본 항목 ID는 0입니다.
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - hostId는 수정할 항목의 도메인 대응 ID를 말합니다.
 - projectId는 목표 항목 ID입니다.

3. 결과 예시
```json
request is success.
```

#### 도메인 설정 수정
1. 다음 명령어로 [UpdateCdnConfig](https://intl.cloud.tencent.com/document/api/228/1397) 인터페이스를 호출해 캐시 만료 설정, 링크 도용 방지, 호스트 헤더, 전체 경로 캐시 등을 포함한 도메인 설정을 수정할 수 있습니다.
```
python QcloudCdnTools_V2.py UpdateCdnConfig -u xxxxx -p xxxxxxx --hostId 1234 --projectId 0 --cacheMode custom --cache [[0,\"all\",1023448]] --refer [1,[\"www.baidu.com\",\"www.qq.com\"]] --fwdHost www.test.org --fullUrl off
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 -  -p는 SecretKey를 말합니다.
 -   hostId는 수정할 설정의 도메인 ID를 말합니다.
 -   projectId는 수정할 항목 ID를 말합니다.
 -   cacheMode는 고급 캐시 설정 활성화 여부를 말합니다.
 -   cache는 캐시 만료 설정을 말하며, UpdateCache 설명을 참조하십시오.
 -   refer는 링크 도용 방지 설정을 말합니다.
 -   fwdHost는 호스트 헤더 설정을 말합니다.
 -   fullUrl은 전체 경로 캐시 활성화 여부를 말하며, 전체 경로 캐시가 활성화된 경우 필터링 매개변수가 꺼짐 상태이고, 전체 경로 캐시가 비활성화인 경우 필터링 매개변수가 켜짐 상태라는 것을 의미합니다.

 **링크 도용 방지 설정**
링크 도용 방지는 두 개의 필드로 구성되며, 첫 번째 필드에 refer의 유형이 표시됩니다.
 - 0: 링크 도용 방지 설정 안 함.
 - 1: 블랙리스트 설정.
 - 2: 화이트리스트 설정.

 두 번째 필드에는 구체적인 명단, 목록이 표시됩니다.
3. 결과 예시
```json
request is success.
```

### 도메인 관리
#### 도메인 추가
1. 다음 명령어로 [AddCdnHost](https://intl.cloud.tencent.com/document/api/228/1406) 인터페이스를 호출해 CDN 가속 도메인을 추가할 수 있습니다.
```
python QcloudCdnTools_V2.py AddCdnHost -u xxxxx -p xxxxxxx --host www.test.com --projectId 0 --hostType cname --origin 1.1.1.1
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - host는 추가할 가속 도메인을 말하며, 도메인은 공업정보부 ICP비안을 통과해야 하고, Tencent Cloud CDN에 액세스한 적이 없어야 합니다.
 - projecctId는 도메인을 추가할 항목의 ID를 말하며, [항목 관리](https://console.cloud.tencent.com/project)에 진입하여 항목의 대응 ID를 조회할 수 있습니다.
 - hostType은 액세스 유형으로, 'cname'인 경우 외부 원본 액세스를, 'ftp'인 경우 FTP 원본 액세스를 말하며, 이때 원본 서버 매개변수가 무시될 수 있습니다.
 - origin은 원본 서버 설정을 말합니다.

3. 결과 예시
```
request is success.
```

#### 도메인 비활성화
1. 다음 명령어로 [OfflineHost](https://intl.cloud.tencent.com/document/api/228/1403) 인터페이스를 호출해 특정 도메인의 CDN 가속 서비스를 끌 수 있습니다.
```
python QcloudCdnTools_V2.py OfflineHost -u xxxxx -p xxxxxxx --hostId 1234
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - "활성" 상태의 도메인은 비활성화 명령어를 호출하여 완료할 수 있습니다.
 - hostId는 비활성화할 도메인 ID를 말하며, GetHostInfoByHost를 통해 도메인 대응 ID를 가져옵니다.

3. 결과 예시
```json
request is success.
```

#### 도메인 활성화
1. 다음 명령어로 [OnlineHost](https://intl.cloud.tencent.com/document/api/228/1402) 인터페이스를 호출해 특정 도메인의 CDN 가속 서비스를 켤 수 있습니다.
```
python QcloudCdnTools_V2.py OnlineHost -u xxxxx -p xxxxxxx --hostId 1234
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - "비활성" 상태의 도메인은 활성화 명령어를 호출하여 완료할 수 있습니다.
 - hostId는 비활성화할 도메인 ID를 말하며, GetHostInfoByHost를 통해 도메인 대응 ID를 가져옵니다.

3. 결과 예시
```json
request is success.
```

#### 도메인 삭제
1. 다음 명령어로 [DeleteCdnHost](https://intl.cloud.tencent.com/document/api/228/1396) 인터페이스를 호출해 특정 도메인을 삭제할 수 있습니다.
```
python QcloudCdnTools_V2.py DeleteCdnHost -u xxxxx -p xxxxxx -hostId 1234
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - "비활성" 상태의 도메인은 삭제 명령어를 호출하여 완료할 수 있습니다.
 - hostId는 비활성화할 도메인 ID를 말하며, GetHostInfoByHost를 통해 도메인 대응 ID를 가져옵니다.

### 로그 관련
#### 로그 다운로드 링크 가져오기
1. 다음 명령어로 [GenerateLogList](https://intl.cloud.tencent.com/document/api/228/3950) 인터페이스를 호출해 특정 도메인의 CDN 로그 다운로드 링크를 가져올 수 있습니다.
```
python QcloudCdnTools_V2.py GenerateLogList -u xxxxx -p xxxxxxx --hostId 1234
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - hostId는 조회할 로그 다운로드 링크의 도메인 ID를 말합니다.
 - 30일 이내의 일별 로그 다운로드 링크를 가져옵니다.

3. 결과 예시
```json
{
    u'now': 1471267882,
    u'list': [
        {
            u'date': u'2016-07-16',
            u'type': 0,
            u'name': u'20160716-test.com'
        },
        {
            u'date': u'2016-07-17',
            u'link': u'http: //log-download.cdn.qcloud.com/20160717/20160717-test.com.gz?st=xYeU1vW6N9UJlSc3hxM0lg&e=1472131882',
            u'type': 1,
            u'name': u'20160717-test.com'
        },
		...
	]
}
```
link 필드가 없는 경우 당일 생성된 로그 데이터가 없다는 것을 말합니다.

 

### 소모 조회

#### TOP 100 URL 조회
1. 다음 명령어로 [GetCdnStatTop](https://intl.cloud.tencent.com/document/api/228/3944) 인터페이스를 호출해 도메인 또는 항목의 TOP 100 트래픽/대역폭 소모 URL을 조회할 수 있습니다.
```
python QcloudCdnTools_V2.py GetCdnStatTop -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --statType bandwidth --projects 0 --hosts test.com
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - startDate는 조회 시작 시간을 말하며, 2016-08-15로 설정한 경우 실제 조회 시작 시간은 2016-08-15 00:00:00입니다.
 - endDate는 조회 종료 시간을 말하며, 2016-08-15로 설정한 경우 실제 조회 종료 시간은 2016-08-15 23:55:00입니다.
 - projects는 조회한 항목 ID를 말하며, 여러 개를 지원합니다.
 - hosts는 조회한 도메인을 말하며, 도메인 세부 항목을 반드시 참조해야 하고, 그렇지 않은 경우 오류가 발생하며, 여러 개를 지원합니다.
 - statType은 순위 근거이며, bandwidth는 대역폭을 flux는 트래픽을 말합니다.

3. 결과 예시
```json
{
    u'start_datetime': u'2016-08-15',
    u'url_data': [
        {
            u'name': u'test.com/uploads/20141218/1418891322.jpeg',
            u'value': 877
        },
        {
            u'name': u'test.com/uploads/20141218/1418891825.jpeg',
            u'value': 796
        },
        {
            u'name': u'test.com/uploads/20141218/1418896965.jpeg',
            u'value': 706
        },
		...
	]
}
```
value는 소모 값이며, flux 단위는 Byte, bandwidth 단위는 bps입니다.

#### 상태 코드 통계 조회
1. 다음 명령어로 [GetCdnStatusCode](https://intl.cloud.tencent.com/document/api/228/3943) 인터페이스를 호출해 도메인 또는 항목의 상태 코드 통계를 조회할 수 있습니다.
```
python QcloudCdnTools_V2.py GetCdnStatusCode -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --projects 0 --hosts test.com
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - startDate는 조회 시작 시간을 말하며, 2016-08-15로 설정한 경우 실제 조회 시작 시간은 2016-08-15 00:00:00입니다.
 - endDate는 조회 종료 시간을 말하며, 2016-08-15로 설정한 경우 실제 조회 종료 시간은 2016-08-15 23:55:00입니다.
 - projects는 조회한 항목 ID를 말하며, 여러 개를 지원합니다.
 - hosts는 조회한 도메인을 말하며, 도메인 세부 항목은 반드시 참조(projects)해야 하고, 그렇지 않은 경우 오류가 발생하며, 여러 개를 지원합니다.

3. 결과 예시
```json
[
    {
        u'200': [
            
        ],
        u'206': [
            
        ],
        u'304': [
            
        ],
        u'416': [
            
        ],
        u'404': [
            69,
			69,
            76,
            69,
            66,
            78,
            73,
            71,
            73,
            76,
      		...
     	],
      	u'500':[
          
      	]
    }
]
```



#### 소모 통계 내역 조회
1. 다음 명령어로 [DescribeCdnHostDetailedInfo](https://intl.cloud.tencent.com/document/api/228/3942) 인터페이스를 호출해 도메인 또는 항목의 소모 내역을 조회할 수 있습니다.
```
python QcloudCdnTools_V2.py DescribeCdnHostDetailedInfo -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-05-08 --endDate 2016-08-15 --projects 0 --hosts www.test.com --statType bandwidth
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - startDate는 조회 시작 시간을 말하며, 2016-08-15로 설정한 경우 실제 조회 시작 시간은 2016-08-15 00:00:00입니다.
 - endDate는 조회 종료 시간을 말하며, 2016-08-15로 설정한 경우 실제 조회 종료 시간은 2016-08-15 23:55:00입니다.
 - projects는 조회한 항목 ID를 말하며, 여러 개를 지원합니다.
 - hosts는 조회한 도메인을 말하며, 도메인 세부 항목은 반드시 참조(projects)해야 하고, 그렇지 않은 경우 오류가 발생하며, 여러 개를 지원합니다.
 - statType은 지정하여 조회한 소모 유형이며, flux는 트래픽, 단위는 Byte, bandwidth는 대역폭, 단위는 bps입니다.

3. 결과 예시
```json
{
    u'start_datetime': u'2016-08-1300: 00: 00',
    u'total_data': [
        35216,
        41875,
        42256,
        34333,
        40868,
        40906,
        38505,
        39487,
        39407,
  		...
  	],
    u'stat_type': u'flux',
    u'end_datetime': u'2016-08-1523: 55: 00',
    u'period': 5
}
```
period는 시간 데이터 분할 정도이며, 조회 시간 구간 길이에 따라 출력되는 시간 단위 데이터 세분화도 달라집니다. 1~3일의 내역 시간 데이터 분할 정도는 모두 5분, 4~7일의 시간 데이터 분할 정도는 1시간, 8일 이상의 시간 데이터 분할 정도는 1일입니다.

#### 소모량 통계 조회
1. 다음 명령어로 [DescribeCdnHostInfo](https://intl.cloud.tencent.com/document/api/228/3941) 인터페이스를 호출해 도메인 또는 항목의 소모 통계를 조회할 수 있습니다.
```
python QcloudCdnTools_V2.py DescribeCdnHostInfo -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --projects 0 --hosts www.test.com --statType bandwidth
```
2. 매개변수 설명
 - -u는 SecretId를 말합니다.
 - -p는 SecretKey를 말합니다.
 - startDate는 조회 시작 시간을 말하며, 2016-08-15로 설정한 경우 실제 조회 시작 시간은 2016-08-15 00:00:00입니다.
 - endDate는 조회 종료 시간을 말하며, 2016-08-15로 설정한 경우 실제 조회 종료 시간은 2016-08-15 23:55:00입니다.
 - projects는 조회한 항목 ID를 말하며, 여러 개를 지원합니다.
 - hosts는 조회한 도메인을 말하며, 도메인 세부 항목은 반드시 참조(projects)해야 하고, 그렇지 않은 경우 오류가 발생하며, 여러 개를 지원합니다.
 - statType은 지정하여 조회한 소모 유형이며, flux는 트래픽, 단위는 Byte, bandwidth는 대역폭, 단위는 bps입니다.

3. 결과 예시
```json
{
    u'start_datetime': u'2016-08-1300: 00: 00',
    u'stat_type': u'bandwidth',
    u'end_datetime': u'2016-08-1523: 55: 00',
    u'detail_data': [
        {
            u'host_id': u'www.test.com',
            u'host_type': u'cname',
            u'host_name': u'www.test.com',
            u'host_value': 2214
        }
    ],
    u'period': 5
}
```
조회 결과는 지정 시간 구간의 총량이며, host_type은 도메인 액세스 시간 유형, cname은 외부 원본 서버 액세스, ftp는 FTP 원본 액세스, cos는 COS 원본 액세스를 말합니다.


