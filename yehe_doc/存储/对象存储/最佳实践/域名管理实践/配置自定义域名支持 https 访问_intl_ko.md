## 소개
사용자는 자체 도메인(사용자 정의 도메인, 예: `test.cos.com`)을 통해 버킷(Bucket)의 객체(Object)에 액세스할 수 있습니다. 구체적인 작업 가이드는 다음과 같습니다.
- [CDN 가속 활성화 시 사용자 정의 도메인 설정으로 HTTPS 액세스 지원](#.E5.BC.80.E5.90.AF-cdn-.E5.8A.A0.E9.80.9F)
- [CDN 가속 비활성화 시 사용자 정의 도메인 설정으로 HTTPS 액세스 지원](#.E5.85.B3.E9.97.AD-cdn-.E5.8A.A0.E9.80.9F)


## 작업 순서

### CDN 가속 활성화

#### 1. 사용자 정의 도메인 바인딩
버킷을 귀하의 자체 도메인에 바인딩하고 CDN 가속을 활성화합니다. 자세한 작업 가이드는 [도메인 관리](https://intl.cloud.tencent.com/document/product/436/31506) 문서의 사용자 정의 도메인 설정 부분을 참조하십시오.
#### 2. HTTPS 액세스 설정
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에서 HTTPS를 설정합니다. 자세한 작업 가이드는 [HTTPS 설정](https://intl.cloud.tencent.com/document/product/228/6295)을 참조하십시오.



### CDN 가속 비활성화
여기에서는 COS에서 리버스 프록시를 통해 사용자 정의 도메인(CDN 가속 비활성화)을 설정하고 HTTPS 액세스를 지원하는 작업 순서를 예시를 보여주는 방식으로 소개합니다. 본 예시는 CDN 가속 비활성화 상태에서 사용자 정의 도메인 `https://test.cos.com`을 통해 소속 리전이 Huanan이고 이름이 testhttps-12345678인 버킷에 액세스하게 됩니다. 구체적인 작업 순서는 다음과 같습니다.

#### 1. 사용자 정의 도메인 바인딩
버킷 testhttps를 도메인 `https://test.cos.com`에 바인딩하고, CDN 가속을 비활성화합니다. 자세한 작업 가이드는 [도메인 관리](https://intl.cloud.tencent.com/document/product/436/31506) 문서의 사용자 정의 도메인 설정 부분을 참조하십시오.
#### 2. 도메인을 위한 리버스 프록시 설정
서버에서 도메인 `https://test.cos.com`을 위한 리버스 프록시를 설정합니다. 구체적인 설정은 다음을 참조하십시오(Nginx 설정은 참고용으로만 제공).
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
        proxy_pass  http://testhttps-12345678.cos.ap-guangzhou.myqcloud.com; //버킷(Bucket)의 기본 다운로드 도메인 설정 
    }
}
```
`server.crt;`, `server.key`는 귀하의 자체(사용자 정의) 도메인 HTTPS 인증서입니다. 귀하의 도메인에 HTTPS 인증서가 없는 경우 [Tencent Cloud SSL 인증서](https://intl.cloud.tencent.com/product/ssl) 페이지에서 신청하십시오.
현재 인증서가 없는 경우 다음과 같은 설정 정보를 삭제할 수 있습니다. 액세스 시 알람이 뜰 수 있으나 '계속'을 클릭하면 액세스할 수 있습니다.
```shell
ssl on;
ssl_certificate /usr/local/nginx/conf/server.crt;
ssl_certificate_key /usr/local/nginx/conf/server.key;
```
#### 3. 서버로 도메인 리졸브
DNS 리졸브 서비스 제공 업체에서 귀하의 도메인을 리졸브합니다. Tencent Cloud DNS를 사용하는 경우 [Tencent Cloud DNS 콘솔](https://console.cloud.tencent.com/cns/domains)에서 도메인 `test.cos.com`을 2단계의 서버 IP로 리졸브하십시오.

#### 고급 설정
#### 브라우저로 웹 페이지 열기
HTTPS 액세스를 지원하는 사용자 정의 도메인 설정을 완료하면 귀하의 도메인을 통해 버킷(Bucket)의 객체(Object)를 다운로드할 수 있습니다. 필요에 따라 브라우저에서 웹 페이지, 이미지 등을 바로 액세스해야 할 경우 정적 웹 사이트 기능을 통해 실행할 수 있습니다. 자세한 작업 가이드는 [정적 웹 사이트 설정](https://intl.cloud.tencent.com/document/product/436/14984) 문서를 참조하십시오.
설정 완료 후, Nginx 설정에 정보를 한 행 추가한 다음 Nginx를 재시작해 브라우저 캐시를 새로 고치면 됩니다.
```bash
proxy_set_header Host $http_host;
```
#### refer 링크 도용 방지 설정
버킷(Bucket)이 공용인 경우 링크 도용 리스크가 있습니다. 사용자는 링크 도용 방지 설정을 통해 Referer 화이트리스트를 활성화하여 악성 링크 도용을 방지할 수 있습니다. 구체적인 작업 순서는 다음과 같습니다.
1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후 링크 도용 방지 설정 기능을 활성화하여 화이트리스트를 선택합니다. 자세한 작업 가이드는 [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/436/13319)을 참조하십시오.
2. Nginx 구성 파일에 정보를 한 행 추가한 다음 Nginx를 재시작해 브라우저 캐시를 새로 고칩니다.
```bash
proxy_set_header   Referer www.test.com;
```
3. 설정 완료 후 바로 파일을 열면 `errorcode: -46616` 오류 알림이 뜹니다. 오류 알림: refer 화이트리스트가 미스되었으나 프록시를 통해 사용자 정의 도메인에 액세스하면 정상적으로 웹 페이지를 열 수 있습니다.
```json
{
	errorcode: -46616,
	errormsg: "not hit white refer, retcode:-46616"
}
```
