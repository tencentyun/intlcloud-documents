## CLB(Cloud Load Balancer)에서 클라이언트 리얼 IP 가져오기 관련 참고 사항
모든 레이어 4(TCP/UDP/TCP SSL) 및 레이어 7(HTTP/HTTPS) CLB 서비스는 추가 구성 없이 백엔드 CVM 인스턴스에서 직접 실제 클라이언트 IP 가져오기를 지원합니다.
- 레이어 4 CLB의 경우 백엔드 CVM 인스턴스에서 얻은 원본 IP는 클라이언트 IP입니다.
- 레이어 7 CLB의 경우 `X-Forwarded-For` 또는 `remote_addr` 필드를 사용하여 클라이언트 IP를 직접 가져올 수 있습니다. 레이어 7 CLB의 액세스 로그는 [Configuring Access Logs](https://intl.cloud.tencent.com/document/product/214/35063)를 참고하십시오. 

>?
>- 레이어 4 CLB의 경우 백엔드 CVM 인스턴스에서 추가 구성 없이 클라이언트 IP를 직접 가져올 수 있습니다.
>- SNAT가 활성화된 다른 레이어 7 로드 밸런싱 서비스의 경우 백엔드 CVM 인스턴스를 구성한 다음 X-Forwarded-For를 사용하여 실제 클라이언트 IP를 가져와야 합니다.
>

다음은 일반적으로 사용되는 애플리케이션 서버 구성 스키마입니다.

## IIS 6 구성 스키마
1. [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers) 플러그인 모듈을 다운로드하여 설치하고 서버 운영 체제 버전에 따라 `x86\Release` 또는 `x64\Release` 디렉터리의 `F5XForwardedFor.dll`을 특정 디렉터리(예시: 본문의 `C:\ISAPIFilters`)에 복사하고 IIS 프로세스에 이 디렉터리에 대한 읽기 권한이 있는지 확인합니다.
2. IIS 관리자를 열고 현재 열려 있는 웹 사이트를 찾은 다음 웹 사이트를 우클릭하고 **속성**을 선택하여 속성 페이지를 엽니다.
3. 속성 페이지에서 **ISAPI 필터**로 전환하고 **추가**를 클릭하면 필터 속성 추가/편집 창이 팝업됩니다.
4. 필터 속성 추가/편집 창에서 ‘필터 이름’에 ‘F5XForwardedFor’를 입력하고 ‘실행 파일’에 `F5XForwardedFor.dll`의 전체 경로를 입력한 다음 **확인**을 클릭합니다.
5. 구성을 적용하려면 IIS 서버를 다시 시작합니다.

## IIS 7 구성 스키마
1. [F5XForwardedFor](https://devcentral.f5.com/s/articles/x-forwarded-for-log-filter-for-windows-servers) 플러그인 모듈을 다운로드하여 설치하고 서버 운영 체제 버전에 따라 `x86\Release` 또는 `x64\Release` 디렉터리의 `F5XFFHttpModule.dll` 및 `F5XFFHttpModule.ini`를 특정 디렉터리(예시: 본문의 `C:\x_forwarded_for`)에 복사하고 IIS 프로세스에 이 디렉터리에 대한 읽기 권한이 있는지 확인합니다.
2. **IIS 서버**를 선택하고 **모듈**을 더블클릭합니다.
![](https://main.qcloudimg.com/raw/21372379584488e72ae3d22af44a5017.png)
3. **네이티브 모듈 구성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/280f11e95b7ac8cd4a754d98ad0cd2b7.png)
4. 팝업 창에서 **등록**을 클릭합니다.
![](https://main.qcloudimg.com/raw/1d6f7bd38077f2c9f089eb84a1995aa1.png)
5. 다운로드한 DLL 파일을 아래와 같이 추가합니다.
![](https://main.qcloudimg.com/raw/354a35a203c24d802d59782c91dfe02a.png)
6. 파일을 추가한 후 파일을 선택하고 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/9fffdfa02fba225f13090ef2598e1c0e.png)
7. ‘ISAPI 및 CGI 제한’에 위의 두 DLL 파일을 추가하고 제한을 허용으로 설정합니다.
![](https://main.qcloudimg.com/raw/8585122da39f14d734eb9d6ded7e486c.png)
8. 구성을 적용하려면 IIS 서버를 다시 시작하십시오.

## Apache 구성 스키마
1. 타사 Apache 모듈 ‘mod_rpaf’를 설치합니다.
```
wget http://stderr.net/apache/rpaf/download/mod_rpaf-0.6.tar.gz
tar zxvf mod_rpaf-0.6.tar.gz
cd mod_rpaf-0.6
/usr/bin/apxs -i -c -n mod_rpaf-2.0.so mod_rpaf-2.0.c
```
2. 파일 끝에 다음을 추가하여 Apache 구성 `/etc/httpd/conf/httpd.conf`를 수정합니다.
```
LoadModule rpaf_module modules/mod_rpaf-2.0.so
RPAFenable On
RPAFsethostname On
RPAFproxy_ips IP 주소(CLB에서 제공하는 공중망 IP가 아니며, 특정 IP에 대해서는 Apache 로그를 조회하고, 일반적으로 두 개의 IP 주소가 있으며 둘 다 입력해야 함)
RPAFheader X-Forwarded-For
```
3. 위의 내용을 추가한 후 Apache를 다시 시작합니다.
```
/usr/sbin/apachectl restart
```

## Nginx 구성 스키마
1. Nginx를 서버로 사용할 때 http_realip_module을 사용하여 실제 클라이언트 IP를 가져올 수 있습니다. 그러나 이 모듈은 기본적으로 Nginx에 설치되어 있지 않으며 `--with-http_realip_module`을 추가하려면 Nginx를 다시 컴파일해야 합니다.
```
yum -y install gcc pcre pcre-devel zlib zlib-devel openssl openssl-devel
wget http://nginx.org/download/nginx-1.17.0.tar.gz
tar zxvf nginx-1.17.0.tar.gz
cd nginx-1.17.0
./configure --prefix=/path/server/nginx --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_realip_module
make
make install
```
2. nginx.conf 파일을 수정합니다.
```
vi /etc/nginx/nginx.conf
```
빨간색으로 표시된 구성 필드 및 정보를 다음과 같이 수정합니다.
>?여기서 `xx.xx.xx.xx`를 리얼 IP 주소(CLB에서 제공하는 공중망 IP가 아님)로 변경해야 합니다. 특정 IP 주소에 대해 이전 Nginx 로그를 쿼리합니다. IP 주소가 여러 개인 경우 모든 IP 주소를 입력해야 합니다.
<div class="code">
<p>
</p>
<pre>  
fastcgi connect_timeout 300;
fastcgi send_timeout 300;
fastcgi read_timeout 300;
fastcgi buffer_size 64k;
fastcgi buffers 4 64k;
fastcgi busy_buffers_size 128k;
fastcgi temp_file_write_size 128k;
<font color="#f2777a">
set_real_ip_from xx.xx.xx.xx;
real_ip_header X-Forwarded-For;
 </font>
</pre>
</div>
3. Nginx를 다시 시작합니다.
```
service nginx restart
```
4. 실제 클라이언트 IP를 가져오려면 Nginx 액세스 로그를 조회합니다.
```
cat /path/server/nginx/logs/access.log
```
