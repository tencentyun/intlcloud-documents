회사에 공중망 액세스에 대한 제한이 있는 경우 방화벽 얼로우리스트를 구성해야 액세스할 수 있습니다. 다음은 관련 규칙입니다.

### 클라이언트 Native SDK(v2.2 이상)

**방화벽 포트:**

|  포트 유형 | 얼로우리스트 항목 |
|---------|---------|
| TCP 포트 | 443 |
| UDP 포트 | 8000 |


**도메인 이름 얼로우리스트:**
```
tcloud.tim.qq.com
gmeconf.qcloud.com
yun.tim.qq.com
gmeosconf.qcloud.com
sg.global.gme.qcloud.com
```

>!
> - Tencent Cloud 서버 IP 주소는 동적으로 업데이트되므로 고정 IP 목록을 제공할 수 없습니다.
> - Windows XP에서 GME SDK를 사용하려면 방화벽 얼로우리스트에 다음 항목을 추가해야 합니다.

**방화벽 포트:**

|  포트 유형 | 얼로우리스트 항목 |
|---------|---------|
| TCP 포트 | 15000|

**도메인 이름 얼로우리스트:**

```
cloud.tim.qq.com
openmsf.3g.qq.com
```


### H5 SDK 사용

**방화벽 포트:**

| 포트 유형 | 얼로우리스트 항목 |
|---------|---------|
| TCP 포트 | 443, 8687 |
| UDP 포트 |8000; 8800; 843; 443|

**도메인 이름 얼로우리스트:**

```
qcloud.rtc.qq.com
rtc.qcloud.qq.com
```


### 음성 메시지 및 음성-텍스트 변환 서비스 사용

**방화벽 포트:**

| 포트 유형 | 얼로우리스트 항목 |
|---------|---------|
| TCP 포트 | 80, 443|

**도메인 이름 얼로우리스트:**

```
gmespeech.qcloud.com
yun.tim.qq.com
gmeconf.qcloud.com
```
