사용자는 자체 도메인 이름(사용자 지정 도메인 이름, 예: `test.cos.com`)을 통해 버킷하의 객체에 접근할 수 있습니다. 자세한 조작 안내는 아래와 같습니다.
- [CDN 가속을 시작할 때 사용자 지정 도메인 이름을 구성하여 HTTPS 접근을 지원합니다](# CDN 가속 시작)
- [CDN 가속을 종료할 때 사용자 지정 도메인 이름을 구성하여 HTTPS 접근을 지원합니다](# CDN 가속 종료)

<span id="CDN 가속 시작"></span>
## CDN 가속 시작
### A. 사용자 지정 도메인 이름 바인딩
버킷을 자체 도메인 이름에 바인딩하고 CDN 가속을 시작합니다. 작업 가이드는 [도메인 이름 관리 -- 사용자 지정 도메인 이름](/doc/product/436/6252#开启 CDN 加速)을 참조하십시오.
### B. HTTPS 접근 구성
CDN 콘솔에서 HTTPS를 구성합니다. 작업 가이드는 [HTTPS 구성](/doc/product/228/6295)을 참조하십시오.
<span id="CDN 가속 종료"></span>
## CDN 가속 종료
본 문서에서는 주로 예시의 방식으로 COS 중 리버스 프록시를 통해 사용자 지정 도메인 이름(CDN 가속 종료)을 구성하여 https 접근을 지원하는 조작 절차를 소개합니다. 본 예시는 CDN 가속을 시작하지 않은 상황에서 직접 사용자 지정 도메인 이름 `https://test.cos.com`으로 소재 지역이 화남이고 이름이 testhttps-12345678인 버킷에 접근하는 것을 구현합니다. 자세한 조작 절차는 아래와 같습니다.

### A. 사용자 지정 도메인 이름 바인딩
버킷 testhttps를 도메인 이름 `https://test.cos.com`에 바인딩하고 CDN 가속을 종료합니다. 작업 가이드는 [도메인 이름 관리--사용자 지정 도메인 이름](/doc/product/436/6252# CDN 가속 종료)을 참조하십시오.
### B. 도메인 이름의 리버스 프록시 구성
서버에서 도메인 이름 `https://test.cos.com`에 리버스 프록시를 구성합니다. 자세한 구성은 아래와 같습니다(이하 Nginx 구성은 참조용으로만 제공).
```
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
        proxy_pass  http://testhttps-12345678.cos.ap-guangzhou.myqcloud.com; //버킷(Bucket)의 기본 다운로드 도메인 이름 구성 
    }
        
}
```
그 중 `server.crt;`, `server.key`는 사용자의 자체(사용자 지정) 도메인 이름의 HTTPS 인증서입니다. 도메인 이름이 아직 HTTPS 인증서가 없다면 [Tencent Cloud SSL 인증서](https://cloud.tencent.com/product/ssl) 페이지에서 신청할 수 있습니다.
잠시 인증서가 없을 경우 아래 구성 정보를 삭제할 수 있습니다. 그러나 접근 시 알람이 나타날 수 있으며 계속을 클릭하면 접근할 수 있습니다.
```
    ssl on;
    ssl_certificate /usr/local/nginx/conf/server.crt;
    ssl_certificate_key /usr/local/nginx/conf/server.key;
```

### C. 도메인 이름을 서버에 해석
도메인 이름의 DNS 해석 서비스 제공업체에서 도메인 이름을 해석합니다. Tencent Cloud의 DNS를 사용하는 경우 [DNS 콘솔](https://console.cloud.tencent.com/cns/domains)로 이동하여 도메인 이름 `test.cos.com`을 절차 2의 서버의 IP에 해석합니다. 작업 가이드는 [도메인 이름 해석](/doc/product/302/3446)을 참조하십시오.
### 업그레이드 구성
#### 브라우저로 페이지 열기
HTTPS 접근을 지원하도록 사용자 지정 도메인 이름을 구성한 후 도메인 이름으로 버킷 중의 객체를 다운로드할 수 있습니다. 비즈니스의 수요에 따라 브라우저에서 직접 페이지, 이미지 등에 접근하고자 할 경우 정적 웹사이트 기능으로 구현할 수 있습니다. 작업 가이드는 [정적 웹사이트 설정](/doc/product/436/6249)을 참조하십시오.
![이미지1](//mc.qcloudimg.com/static/img/bdd63d54f805e4975e82c95b37f675f0/image.png)
구성한 후 Nginx 구성에 한 줄의 정보를 추가하고 Nginx를 다시 시작한 다음 브라우저 캐시를 새로고침하면 됩니다.
```
proxy_set_header Host $http_host;
```
#### Referer 핫 링크 보호 구성
공유 버킷일 경우 링크가 도난될 위험이 있습니다. 사용자는 핫 링크 보호를 설정하고 Referer 화이트리스트를 시작하여 악의적인 링크 도난을 방지할 수 있습니다. 자세한 조작 절차는 아래와 같습니다.
1. [COS 콘솔](https://console.cloud.tencent.com/cos5/index)에서 핫 링크 보호 설정 기능을 시작하고 화이트리스트를 선택합니다. 작업 가이드는 [핫 링크 보호 설정](/doc/product/436/6250)을 참조하십시오.
![이미지2](//mc.qcloudimg.com/static/img/788556013c4d3ebd6b728d8c22a8adb5/image.png)
2. Nginx 구성에 한 줄의 정보를 추가하고 Nginx를 다시 시작한 다음 브라우저 캐시를 새로고침하면 됩니다.
```
proxy_set_header   Referer www.test.com;
```
3. 설정한 후 파일을 직접적으로 열 경우 `errorcode：-46616`이라는 오류 메시지가 나타납니다. 오류 메시지: refer 화이트리스트 미적중. 그러나 프록시에 의해 사용자 지정 도메인 이름에 접근할 경우 정상적으로 페이지를 열 수 있습니다.
![이미지 3](//mc.qcloudimg.com/static/img/005099e6a30398c600bb945b6b1c34e7/image.png)

