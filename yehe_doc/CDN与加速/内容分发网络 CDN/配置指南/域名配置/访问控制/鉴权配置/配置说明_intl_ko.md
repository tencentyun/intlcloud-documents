
## 설정 시나리오
일반적으로 CDN에 배포된 콘텐츠는 기본 오픈 리소스로, 사용자가 URL을 획득하여 액세스할 수 있습니다. referer 블랙리스트/화이트리스트, IP 블랙리스트/화이트리스트, IP 액세스 빈도 제한 등의 액세스 제어 외에도, 고급 타임스탬프 인증 설정을 통해 악성 사용자의 도용을 방지할 수 있습니다.

> !타임스탬프 링크 도용 방지 설정 후에는, 클라이언트가 요청을 보낼 때 설정에 따라 서명을 계산하고 서버로 가져오며, CDN 노드가 서버를 인증하여 통과한 후에만 통과 허가를 계속할 수 있습니다.

## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴에서 [도메인 관리]를 선택한 후, 오른쪽의 [관리]를 클릭하면 도메인 설정 페이지로 이동할 수 있습니다. 그중 [액세스 제어]에서 인증 설정을 확인할 수 있으며 비활성화 상태로 기본 설정되어 있습니다.
![](https://main.qcloudimg.com/raw/1efe407c5a9f2fc8f8837d5b1cdbb3d7.png)

### 설정 변경
#### 1. 설정 변경
CDN은 네 가지 인증 서명 계산 방식을 제공하며, 상단의 [인증 계산기]를 통해 각각의 인증 모드, 설정 후 효과를 조회할 수 있습니다. 자세한 설명은 [TypeA](https://intl.cloud.tencent.com/document/product/228/35222), [TypeB](https://intl.cloud.tencent.com/document/product/228/35223), [TypeC](https://intl.cloud.tencent.com/document/product/228/35224), [TypeD](https://intl.cloud.tencent.com/document/product/228/35225) 등의 알고리즘 설명 문서를 참조 바랍니다.
![](https://main.qcloudimg.com/raw/ffd60184fa759b4c7a82a5a49634b8c3.png)

#### 2. 설정 비활성화
인증 설정 스위치를 통해 원클릭으로 설정을 비활성화할 수 있습니다. 스위치가 비활성화 상태일 때 하단에 기존 설정이 존재하더라도 현재 네트워크에 적용되지 않습니다. 이후에 활성화를 클릭하면 전체 네트워크에 적용되지 않도록 즉시 배포하지 않으며, 설정에 대해 2차 확인을 먼저 진행합니다.
![](https://main.qcloudimg.com/raw/f892392e86acae153ef7821944888155.png)

#### 3. 지역 특수 설정
사용자의 가속 도메인 서비스 지역이 글로벌 가속이고 중국 내, 중국 외 지역의 인증 설정을 다르게 하길 원한다면 설정 하단의 [특수 설정 추가]를 클릭하여 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/8e6e0e08ef230322f4366a4fa92288e0.png)

> !지역 특수 설정을 추가한 후에는 현재로서는 직접 삭제할 수 없으니 비활성화를 통해 사용하지 않도록 설정할 수 있습니다.

## 설정 예시
도메인이 'cloud.tencent.com'인 글로벌 가속 도메인의 인증 설정이 아래와 같을 경우,
![](https://main.qcloudimg.com/raw/1d82f89f383aa35f5d7ae679f19669fb.png)
실제 적용 시나리오는 다음과 같습니다.

1. 중국 내 사용자가 실제로 리소스 'http://cloud.tencent.com/1.jpg'에 액세스할 때, 바로 요청을 보낼 수 있습니다.
2. 중국 외 사용자가 실제로 리소스 'http://cloud.tencent.com/1.jpg'에 액세스할 때, 요청 URL 형식은 'http://cloud.tencent.com/509301d10da7b862052927ed7a947f43/5e561139/1.jpg' 입니다.


### 예시 코드

 각 인증 계산 방식은 아래와 같으며,  Python 데모 예시는 아래와 같습니다:

```
import requests
import json
import sys
import time
import hashlib

def generate_url(category, ts=None):
    url = 'http://www.test.com'              # 테스트 도메인
    path = '/1.txt'                                     # 액세스 경로
    suffix = '?a=1&b=2'                                 # URL 매개변수
    key = 'abc123456789'                                # 인증 키
    now = int(time.mktime(time.strptime(ts, "%Y%m%d%H%M%S")) if ts else time.time())                # 시간을 새로 입력했다면 입력한 ts를 사용하고, 그렇지 않다면 기존 ts를 사용합니다
    sign_key = 'key'                                    # url 서명 필드
    time_key = 't'                                      # url 시간 필드
    ttl_format = 10                                     # 시간의 진법, 10 또는 16을 쓰며 typeD만 지원
    if category == 'A':                                 #Type A
        ts = now
        rand_str = '123abc'
        sign = hashlib.md5('%s-%s-%s-%s-%s' % (path, ts, rand_str, 0, key)).hexdigest()
        request_url = '%s%s?%s=%s' % (url, path, sign_key, '%s-%s-%s-%s' % (ts, rand_str, 0, sign))
        print(request_url)
    elif category == 'B':                               #Type B
        ts = time.strftime('%Y%m%d%H%M', time.localtime(now))
        sign = hashlib.md5('%s%s%s' % (key, ts, path)).hexdigest()
        request_url = '%s/%s/%s%s%s' % (url, ts, sign, path, suffix)
        print(request_url)
    elif category == 'C':                               #Type C
        ts = hex(now)[2:]
        sign = hashlib.md5('%s%s%s' % (key, path, ts)).hexdigest()
        request_url = '%s/%s/%s%s%s' % (url, sign, ts, path, suffix)
        print(request_url)
    elif category == 'D':                               #Type D
        ts = now if ttl_format == 10 else hex(now)[2:]
        sign = hashlib.md5('%s%s%s' % (key, path, ts)).hexdigest()
        request_url = '%s%s?%s=%s&%s=%s' % (url, path, sign_key, sign, time_key, ts)
        print(request_url)


if __name__ == '__main__':
    if len(sys.argv) == 1:
        print('usage: python generate_url.py A 20200501000000')
    args = sys.argv[1:]
    generate_url(*args)
```
