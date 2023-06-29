
[](id:q1)
### Tencent Cloud CDN 노드의 기본 타임아웃 시간은 얼마나 됩니까?
기본 제한 시간은 10초입니다.

[](id:q2)
### CDN 콘솔에서 연결된 도메인 이름을 비활성화하면 CDN 노드의 파일은 어떻게 됩니까?
연결된 도메인 이름의 CDN 서비스를 비활성화하면 CDN 노드가 도메인 이름의 연결 구성을 유지하고 CDN 트래픽이 더 이상 생성되지 않으며 도메인 이름에 액세스할 수 없게 됩니다.

[](id:q3)
### CDN에 연결한 후 웹사이트를 열 수 없으면 어떻게 해야 합니까?
먼저 연결된 도메인 이름의 CDN 상태가 비활성화인 경우 웹사이트를 열 수 없으므로 상태를 확인하고, 비활성화가 아닌 경우 다음과 같이 확인을 진행할 수 있습니다.
+ ping 또는 nslookup 검사를 통해 해당 도메인의 CNAME 리졸브가 적용되었는지 확인합니다. CNAME이 바인딩되지 않은 경우 [CNAME 설정](https://intl.cloud.tencent.com/document/product/228/3121)의 설명을 참조하여 DNS 서비스 제공 업체 측에서 CNAME을 바인딩할 수 있습니다.
+ CNAME이 적용된 후 원본 서버에 정상적으로 액세스되는지 확인하십시오.

만약 상기 단계를 통해 문제를 해결할 수 없는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 문의하십시오.

[](id:q4)
### 사용자가 액세스하는 CDN 노드를 어떻게 확인합니까?
사용자는 nslookup 및 ping 명령을 사용하여 사용자가 액세스한 CDN 노드의 IP, 대기 시간 및 패킷 손실과 같은 기본 문제 해결 정보를 얻을 수 있습니다.

[](id:q5)
### 히트율이 낮은 이유는 무엇인가요?
다음과 같은 이유로 히트율이 낮을 수 있습니다.
+ Cache Configuration 문제, 예를 들어 캐시 시간이 비교적 짧은 경우입니다.
+ HTTP 헤더로 인해 캐시를 진행할 수 없을 때, 원본 서버 Cache-Control 혹은 Expires의 설정을 확인하십시오.
+ 원본 서버 유형의 문제, 캐시 가능한 콘텐츠가 적은 경우입니다.
+ 사이트 방문 횟수가 적고 유효 기간이 짧고 파일 히트율이 낮아 Origin-Pull 요청이 잦습니다.

[](id:q6)
### 사용자가 CDN에 액세스할 때 연결 속도가 느린 이유는 무엇입니까?
용량이 큰 파일은 다운로드 속도에 중점을 두고 용량이 작은 파일은 대기 시간에 중점을 둡니다. 먼저, 속도 측정 웹 사이트 (권장 툴: [17ce] (http://www.17ce.com))를 통해 사용자가 느리다고 생각하는 URL의 액세스 속도를 판단하십시오.
테스트 결과 속도가 실제로 느리고, 원본 서버가 외부 원본 서버인 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 해주시면 원본 서버 컴퓨터에서 부하와 대역폭이 제한되어 있는지 확인할 수 있도록 도와드립니다.

[](id:q7)
### 사용자 액세스가 CDN 캐시에 도달했는지 어떻게 알 수 있습니까?
요청 반환 헤더에서 X-Cache-Lookup 정보를 확인합니다. 만약 여러 X-Cache-Lookup이 동시에 반환되면 정상입니다. Cache Hit/Hit From MemCache/Hit From Disktank가 반환되면 CDN Cache가 히트되었음을 의미합니다.
![](https://mc.qcloudimg.com/static/img/64ac912c895b36f0241a927df6da3543/image.png)
+ X-Cache-Lookup:Hit From MemCache: CDN 노드의 메모리가 히트되었습니다.
+ X-Cache-Lookup:Hit From Disktank: CDN 노드의 디스크가 히트되었습니다.

[](id:q8)
### 노드에서 반환한 이름이 같은 파일의 크기가 다른 이유는 무엇입니까?
모든 파일 유형이 기본적으로 캐시되므로 CDN 노드에 다른 버전의 파일이 존재할 수 있습니다. 해결 방법은 다음과 같습니다.
+ 수동으로 파일을 퍼지하고 캐시를 즉시 업데이트하십시오.
+ 버전 번호를 사용하십시오. 예: `http://www.xxx.com/xxx.js?version=1`
+ 같은 이름의 파일을 사용하지 않도록 파일 이름을 변경하십시오.

만약 상기 단계를 통해 문제를 해결할 수 없는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 문의하십시오.

[](id:q9)
### CDN에 링크 도용 방지 화이트리스트를 설정한 후, 웹 사이트에 액세스할 수 없으면 어떻게 해야 합니까?

웹사이트가 브라우저에서 정상적으로 열릴 수 있도록 링크 도용 방지 허용 목록을 구성할 때 [빈 referer 허용]을 선택하십시오(빈 referer 사용).
![이미지 설명](https://main.qcloudimg.com/raw/3ec77732d4f5266278af2e8f569b08a2.png)

[](id:q10)
### 트래픽 상한 설정이 DDOS 공격을 방어할 수 있습니까?

CDN은 DDoS 방어보다는 콘텐츠 전송 가속화에 중점을 두고 있습니다. CDN의 대역폭 상한 기능을 사용하여 5분 안에 대역폭 사용 통계를 자동으로 수집할 수 있습니다. 상한 임계값에 도달하면 CDN은 구성에 따라 응답하며 **최대 임계값은 10,000Tbps입니다**. DDOS로부터 사이트를 보호하려면 [Secure Content Delivery Network](https://intl.cloud.tencent.com/products/scdn)를 사용하여 방어할 수 있습니다.

[](id:q11)
### CDN이 모든 노드 IP를 제공할 수 있습니까? 
보안상의 이유로 CDN은 전체 노드 IP 목록을 제공할 수 없지만 Tencent Cloud CDN IP 확인 페이지에서 IP 지역을 쿼리할 수 있습니다. 자세한 내용은 [IP 소속 조회](https://intl.cloud.tencent.com/document/product/228/10747)를 참고하십시오.
