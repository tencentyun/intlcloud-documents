## 소개
자체 도메인(사용자 정의 도메인, 예: `test.cos.com`)을 통해 버킷(Bucket)의 객체(Object)에 액세스할 수 있습니다. 구체적인 작업 가이드는 다음과 같습니다.
- [CDN 가속 활성화 시 사용자 정의 도메인에 HTTPS 액세스 지원 설정](#.E5.BC.80.E5.90.AF-cdn-.E5.8A.A0.E9.80.9F)
- [CDN 가속 비활성화 시 사용자 정의 도메인에 HTTPS 액세스 지원 설정](#.E5.85.B3.E9.97.AD-cdn-.E5.8A.A0.E9.80.9F)


## 작업 단계
### CDN 가속 활성화

#### 1단계: 사용자 정의 도메인 바인딩
버킷을 자체 도메인에 바인딩하고 CDN 가속을 활성화합니다. 자세한 작업 가이드는 [사용자 정의 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31506) 문서를 참고하십시오.

#### 2단계: HTTPS 액세스 설정
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에서 HTTPS를 설정합니다. 자세한 작업 가이드는 [HTTPS 가속 설정 가이드](https://intl.cloud.tencent.com/document/product/228/35213)를 참고하십시오.


### CDN 가속 비활성화

본 챕터에서는 Cloud Object Storage(COS)에서 리버스 프록시를 통해 사용자 정의 도메인(CDN 가속 비활성화)을 설정하고 HTTPS 액세스를 지원하는 작업을 예시를 통해 소개합니다. 본 예시에서는 CDN 가속이 비활성화된 상태에서 직접 사용자 정의 도메인 `https://test.cos.com`을 통해 소속 리전이 광저우이고 이름이 testhttps-1250000000인 버킷에 액세스하게 됩니다. 구체적인 작업 순서는 다음과 같습니다.

#### 1단계: 사용자 정의 도메인 바인딩

COS 중국 내 공유 클라우드 리전과 싱가포르 리전은 이미 사용자 정의 원본 서버 도메인 호스팅을 위한 HTTPS 인증서를 지원하고 있으며, 추가된 사용자 정의 원본 서버 도메인은 콘솔을 통해 인증서를 바인딩 할 수 있습니다. 자세한 내용은 [방법1](#1)을 참고하십시오. 도메인에 HTTPS 인증서가 없는 경우 [Tencent Cloud 인증서 신청](https://console.cloud.tencent.com/ssl)을 클릭할 수 있습니다.

기타 해외 리전의 경우 현재 HTTPS 인증서 호스팅이 지원되지 않으며, HTTPS 인증서를 사용해야 하는 경우 [방법2](#2)를 참고하십시오.

<span id="1"></span>
- 방법1: COS 콘솔을 통해 사용자 정의 원본 서버 도메인 바인딩
버킷 testhttps-1250000000를 `https://test.cos.com` 도메인에 바인딩하고, CDN 가속을 비활성화합니다. 자세한 작업 가이드는 [사용자 정의 원본 서버 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31507) 문서를 참고하십시오.

<span id="2"></span>
- 방법2: 도메인에 리버스 프록시 설정
서버 상의 `https://test.cos.com` 도메인에 리버스 프록시를 설정합니다. 구체적인 설정 방법은 다음을 참고하십시오(Nginx 설정은 참고용으로만 제공).
```shell
server {
    listen        443;
    server_name  test.cos.com ;

    ssl on;
    ssl_certificate /usr/local/nginx/conf/server.crt;
    ssl_certificate_key /usr/local/nginx/conf/server.key;

    error_log logs/test.cos.com.error_log;
    access_log logs/test.cos.com.access_log;
    location / {
        root /data/www/;
        proxy_pass  http://testhttps-1250000000.cos.ap-guangzhou.myqcloud.com; //버킷(Bucket)의 기본 다운로드 도메인 설정 
    }
}
```
`server.crt;`, `server.key`는 귀하의 자체(사용자 정의) 도메인 HTTPS 인증서입니다. 귀하의 도메인에 HTTPS 인증서가 없는 경우 [Tencent Cloud SSL 인증서](https://intl.cloud.tencent.com/products/ssl) 페이지에서 신청하십시오.
현재 인증서가 없는 경우 다음과 같은 설정 정보를 삭제할 수 있습니다. 액세스 시 알람이 뜰 수 있으나 계속을 클릭하면 액세스할 수 있습니다.
```shell
ssl on;
ssl_certificate /usr/local/nginx/conf/server.crt;
ssl_certificate_key /usr/local/nginx/conf/server.key;
```

#### 2단계: 서버로 도메인 리졸브

도메인 DNS 리졸브 서비스 제공 업체에서 사용자의 도메인을 리졸브합니다.

#### 3단계: 고급 설정

- **브라우저로 직접 웹 페이지 열기**
사용자 정의 도메인의 HTTPS 액세스 지원 설정을 완료하면 사용자의 도메인을 통해 버킷(Bucket)에 있는 객체(Object)를 다운로드할 수 있습니다. 비즈니스 수요에 따라 브라우저에서 직접 웹 페이지 및 이미지 등을 액세스해야 하는 경우 정적 웹 사이트 기능을 통해 실행할 수 있습니다. 자세한 작업 가이드는 [정적 웹 사이트 설정](https://intl.cloud.tencent.com/document/product/436/14984)을 참고하십시오.
설정 완료 후, Nginx 설정에 정보를 한 행 추가한 다음 Nginx를 재시작해 브라우저 캐시를 새로 고칩니다.
```bash
proxy_set_header Host $http_host;
```
- **refer 링크 도용 방지 설정**
버킷(Bucket)이 공용인 경우 링크 도용 리스크가 있습니다. 링크 도용 방지 설정을 통해 Referer 얼로우리스트를 활성화하여 악성 링크 도용을 방지할 수 있습니다. 구체적인 작업 순서는 다음과 같습니다.
 1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후, 링크 도용 방지 설정 기능을 활성화하여 얼로우리스트를 선택합니다. 자세한 작업 가이드는 [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/436/13319)을 참고하십시오.
 2. Nginx 구성 파일에 정보를 한 행 추가한 다음 Nginx를 재시작해 브라우저 캐시를 새로 고칩니다.
```bash
proxy_set_header   Referer www.test.com;
```
 3. 설정 완료 후, 바로 파일을 열면 `errorcode: -46616` 오류 알림이 뜹니다. 오류 알림: refer 얼로우리스트가 미스되었으나 프록시를 통해 사용자 정의 도메인에 액세스하면 정상적으로 웹 페이지를 열 수 있습니다.
```json
{
	errorcode: -46616,
	errormsg: "not hit white refer, retcode:-46616"
}
```


