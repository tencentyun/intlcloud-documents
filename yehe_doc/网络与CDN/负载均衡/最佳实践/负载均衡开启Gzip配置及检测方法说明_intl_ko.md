**공중망 CLB 또는 고정 IP가 있는 공중망 CLB**의 경우 기본적으로 **HTTP/HTTPS 프로토콜**에 대해 Gzip 압축이 활성화됩니다. Gzip 기능은 웹사이트를 압축하여 네트워크 전송에서 데이터 볼륨을 효과적으로 줄이고 클라이언트 브라우저의 액세스 속도를 높입니다. 다음에 주의하십시오.

### 주의 사항
- **동기화된 CVM 인스턴스에서 Gzip 압축을 활성화해야 합니다.**
일반적인 Nginx 서비스 컨테이너의 경우 구성 파일(기본적으로 nginx.conf)에서 Gzip을 활성화하고 서비스를 다시 시작해야 합니다.
```
gzip on;
```
- **현재 CLB는 다음 파일 형식을 지원하며, Gzip_types 구성 항목에서 압축을 위한 파일 형식을 지정할 수 있습니다.**
```
application/atom+xml application/javascript application/json application/rss+xml application/vnd.ms-fontobject application/x-font-ttf application/x-web-app-manifest+json application/xhtml+xml application/xml font/opentype image/svg+xml image/x-icon text/css text/plain text/x-component;
```
>!CLB의 CVM 인스턴스 비즈니스 소프트웨어에서 위의 파일 형식에 대해 동기화된 Gzip을 활성화해야 합니다.
>
- **클라이언트 요청은 압축 요청 식별자가 있어야 합니다.**
Gzip 압축을 활성화하려면 클라이언트 요청에 다음 식별자가 있어야 합니다.
```
Accept-Encoding: gzip,deflate,sdch
```

### CVM 인스턴스 Gzip 활성화 예시
CVM 실행 환경 예시: Debian 6
1. vim을 사용하여 사용자 경로를 기반으로 Nginx 구성 파일을 엽니다.
```
vim /etc/nginx/nginx.conf
```
2. 다음 코드를 찾습니다.
```
gzip on;
gzip_min_length 1k;
gzip_buffers 4 16k;
gzip_http_version 1.1;
gzip_comp_level 2;
gzip_types text/html application/json;
```
상기 코드 구문에 대한 설명:

- Gzip: Gzip 모듈을 활성화 또는 비활성화할지 여부입니다.
구문: `gzip on/off`
범위: http, server, location	

- gzip_min_length: 페이지를 압축할 수 있는 최소 바이트 수를 지정합니다. 바이트 수는 HTTP  header의 Content-Length에서 얻을 수 있습니다. 기본값은 1k입니다.
구문: `gzip_min_length length`
범위: http, server, location	

- gzip_buffers: Gzip 압축 결과의 데이터 스트림을 저장하기 위한 버퍼의 단위를 지정합니다. 16k는 16k가 단위로 사용됨을 의미하며 메모리는 원래 데이터 크기의 4배(16k)가 적용됩니다.
구문: `gzip_buffers number size`
범위: http, server, location	

- gzip_http_version: Gzip을 사용할 수 있는 가장 낮은 HTTP 버전을 지정합니다. HTTP/1.0 구성은 Gzip이 필요한 가장 낮은 HTTP 버전이 1.0임을 의미하므로 Gzip은 HTTP/1.1 이상과 호환될 수 있습니다. Tencent Cloud는 전체 네트워크에서 HTTP/1.1을 지원하므로 변경할 필요가 없습니다.
구문: `gzip_http_version 1.0 | 1.1;`
범위: http, server, location

- gzip_comp_level: 값 범위가 1 – 9인 Gzip 압축 비율을 지정합니다. 1은 가장 빠른 처리 속도의 가장 작은 압축 비율이고 9는 가장 느린 처리 속도(높은 cpu 소비와 빠른 전송)의 가장 큰 압축 비율입니다.
구문: `gzip_comp_level 1..9`
범위: http，server，location

- gzip_types: 압축을 위한 MIME(Multipurpose Internet Mail Extensions) 유형을 나타내며 기본적으로 "text/html" 유형이 압축됩니다. 또한 Nginx용 Gzip은 기본적으로 javascript 및 이미지와 같은 정적 리소스 파일을 압축하지 않습니다. 압축할 MIME 유형을 지정하도록 gzip_types를 구성할 수 있습니다. 지정되지 않은 유형은 압축되지 않습니다. **예를 들어 json 형식으로 데이터를 압축하려면 이 문장에 application/json을 추가해야 합니다.**

지원되는 유형은 다음과 같습니다.
```
text/html text/plain text/css application/x-javascript text/javascript application/xml
```
구문: `gzip_types mime-type [mime-type ...]`
범위: http, server, location

3. 구성을 수정하려면 파일을 저장하고 종료하고 Nginx bin 파일 디렉터리를 입력하고 다음 명령을 실행하여 Nginx를 다시 로딩합니다.
```
./nginx -s reload
```
4. curl 명령을 사용하여 Gzip이 성공적으로 활성화되었는지 테스트합니다.
```
curl -I -H "Accept-Encoding: gzip, deflate" "http://cloud.tencent.com/example/"
```
