## 1. CLB(Cloud Load Balancer) 기능 설명

프로토콜 스택과 서버를 심층적으로 최적화함으로써 Tencent Cloud CLB는 HTTPS 성능을 크게 향상시킵니다. 한편, Tencent Cloud는 국제 인증 기관과의 협업을 통해 인증서 비용을 크게 절감합니다. CLB는 다음과 같은 측면에서 귀하의 비즈니스에 상당한 이점을 제공할 수 있습니다.

1. HTTPS 사용은 Client의 액세스 속도에 영향을 미치지 않습니다.
2. 클러스터에 있는 단일 서버의 SSL 암호화 및 암호 해독 성능은 고성능 CPU보다 최소 3.5배 높은 초당 최대 6.5W cps의 전체 핸드셰이크를 유지할 수 있습니다. 이를 통해 서버 비용이 절감되고 비즈니스 피크 및 트래픽 급증 시 서비스 기능이 크게 향상되며 컴퓨팅 기반 공격 방지 기능이 강화됩니다.
3. 여러 프로토콜의 오프로딩 및 변환이 지원되어 다양한 클라이언트 프로토콜에 적응하는 비즈니스의 스트레스를 줄입니다. 비즈니스 백엔드는 HTTP2, SPDY, SSL 3.0 및 TLS 1.2와 같은 다른 프로토콜을 사용하기 위해 HTTP1.1만 지원하면 됩니다.
4. 원스톱 SSL 인증서 신청, 모니터링, 교체 서비스를 제공합니다. Tencent Cloud는 두 개의 선도적인 글로벌 인증 기관인 Comodo 및 SecureSite와 협력하여 인증서 신청 프로세스를 크게 간소화하고 신청 비용을 절감합니다.
5. Anti-CC 및 WAF 기능을 제공하여 느린 HTTP 공격, 고빈도 표적 공격, SQL 인젝션 및 웹 사이트 트로이 목마와 같은 애플리케이션 레이어 공격을 효과적으로 제거합니다.

## 2. HTTP 및 HTTPS 헤더 식별자

CLB는 HTTPS에 대한 프록시 역할을 합니다. HTTP 및 HTTPS 요청은 모두 CLB에서 백엔드 CVM 인스턴스로 포워딩할 때 HTTP 요청이 됩니다. 이 경우 프런트엔드 요청이 HTTP인지 HTTPS인지 구분할 수 없습니다.

CLB는 요청을 리얼 서버로 포워딩할 때 X-Client-Proto를 header에 삽입합니다.

X-Client-Proto: http(프런트엔드의 HTTP 요청)
X-Client-Proto: https(프런트엔드의 HTTPS 요청)

## 3. 시작하기


최종 사용자가 브라우저에서 `www.example.com`을 직접 입력할 때 HTTPS를 통해 안전하게 액세스할 수 있도록 `https://example.com` 웹 사이트를 구성해야 한다고 가정합니다.

이 경우 최종 사용자가 입력한 `www.example.com` 엑세스 요청은 아래와 같이 포워딩됩니다.

1. 요청은 HTTP를 통해 전송되고 VIP를 통해 CLB 수신기의 포트 80에 액세스합니다. 그러면 리얼 서버의 8080번 포트로 포워딩됩니다.

2. 리얼 서버의 Nginx에서 rewrite를 구성하면 요청이 포트 8080을 통해 전달되고 `https://example.com` 페이지에 다시 작성됩니다.

3. 그런 다음 브라우저는 `https://example.com` 요청을 해당 HTTPS 사이트로 다시 보냅니다. 요청은 VIP를 통해 CLB 수신기의 포트 443에 액세스한 다음 리얼 서버의 포트 80으로 포워딩됩니다.

이제 요청 포워딩 프로세스가 완료되었습니다.

이 작업은 브라우저 사용자의 HTTP 요청을 보다 안전한 HTTPS 요청으로 다시 작성하고 사용자가 감지할 수 없습니다. 위의 요청 포워딩 작업을 구현하기 위해 리얼 서버를 다음과 같이 구성할 수 있습니다.

```
server {

	listen 8080; 
	server_name example.qcloud.com;

	location / {

		#! customized_conf_begin;
		client_max_body_size 200m;
		rewrite ^/.(.*) https://$host/$1 redirect;

} 
}
```

또는 새 버전의 Nginx에서 권장되는 301 리디렉션 메소드를 사용하여 Nginx HTTP 페이지를 HTTPS 페이지로 리디렉션합니다.

```
server { 	
  	listen	  80;
  	server_name    example.qcloud.com;
  	return	  301 https://$server_name$request_uri;
}

server {
  	listen	  443 ssl;
 	server_name    example.qcloud.com;
	[....]
}
```
