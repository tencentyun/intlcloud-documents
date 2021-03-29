[](id:q1)
### Tencent Cloud CDN 노드의 기본 타임아웃 시간은 몇 초인가요?
Tencent Cloud CDN 노드의 기본 타임아웃 시간은 10초입니다.

[](id:q2)
### CDN 관리에서 도메인 액세스를 비활성화하면 CDN 노드의 파일은 어떻게 되나요?
CDN에 액세스한 도메인 가속화 서비스를 비활성화하면 CDN 노드는 해당 도메인의 액세스 설정을 유지하지만, 더 이상 CDN 트래픽을 생성하지 않으며 해당 도메인에 접속할 수 없게 됩니다.

[](id:q3)
### CDN에 액세스한 후 웹 사이트를 열 수 없을 때, 어떻게 진단하나요?
액세스한 도메인의 CDN 상태가 ‘비활성화 상태’인지 확인하십시오. ‘비활성화 상태’인 경우 해당 웹 페이지를 열 수 없습니다. 만약 ‘비활성화’ 상태가 아니라면 다음 단계에 따라 추가로 확인할 수 있습니다.
+ ping 또는 nslookup 검사를 통해 해당 도메인의 CNAME 리졸브가 적용되었는지 확인합니다. CNAME이 바인딩되지 않은 경우 [CNAME 설정](https://intl.cloud.tencent.com/document/product/228/3121)의 설명을 참조하여 DNS 서비스 제공 업체 측에서 CNAME을 바인딩할 수 있습니다.
+ CNAME이 적용된 후 원본 서버에 정상적으로 액세스되는지 확인하십시오.

만약 위 단계를 통해 문제를 해결할 수 없는 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 문의해 주시면 감사하겠습니다.

[](id:q4)
### 사용자가 액세스하는 CDN 노드를 확인하는 방법은 무엇인가요?
사용자는 nslookup 및 ping 명령을 사용하여 사용자가 액세스한 CDN 노드의 IP 및 지연된 패킷 손실과 같은 기본 문제 해결 정보를 얻을 수 있습니다.

[](id:q5)
### 히트율이 낮은 이유는 무엇인가요?
다음과 같은 이유로 히트율이 낮을 수 있습니다.
+ Cache Configuration 문제, 예를 들어 캐시 시간이 비교적 짧은 경우입니다.
+ HTTP header로 인해 캐시를 진행할 수 없을 때, 원본 서버 Cache-Control 혹은 Expires의 설정을 확인하십시오.
+ 원본 서버 유형의 문제, 캐시 가능한 콘텐츠가 적은 경우입니다.
+ 웹 사이트에 액세스가 적고 만료 시간이 짧으며 도달한 파일이 적어 자주 원본 가져오기가 진행됩니다.

[](id:q6)
### 사용자가 CDN 액세스가 느리다고 생각할 때 어떻게 하나요?
용량이 큰 파일은 다운로드 속도에 중점을 두고 용량이 작은 파일은 대기 시간에 중점을 둡니다. 먼저, 속도 측정 웹 사이트 (권장 툴: [17ce] (http://www.17ce.com))를 통해 사용자가 느리다고 생각하는 URL의 액세스 속도를 판단하십시오.
측정 결과 속도가 실제로 느리고, 원본 서버가 외부 원본에 속하는 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 해주시면 사용자가 원본 서버 기기 부하와 대역폭에 제한 받지 않도록 지원하겠습니다.

[](id:q7)
### 사용자 액세스가 CDN 캐시에 도달하는지 확인하는 방법은 무엇인가요?
액세스 패킷의 헤더에서 X-Cache-Lookup 정보를 확인합니다. 만약 여러 X-Cache-Lookup이 동시에 리턴되는 경우 Cache Hit/Hit From MemCache/Hit From Disktank를 리턴할 때 CDN 캐시에 도달한 것입니다.
![](https://mc.qcloudimg.com/static/img/64ac912c895b36f0241a927df6da3543/image.png)
+ X-Cache-Lookup:Hit From MemCache는 CDN 노드에 도달하는 메모리를 나타냅니다.
+ X-Cache-Lookup:Hit From Disktank는 CDN 노드에 도달하는 디스크를 나타냅니다.

[](id:q8)
### 동일한 이름의 파일 노드에서 리턴한 파일 크기가 일치하지 않는 이유는 무엇인가요?
모든 파일 유형이 기본적으로 캐시되므로 CDN 노드에 다른 버전의 파일이 존재할 수 있습니다. 해결 방법은 다음과 같습니다.
+ 파일을 강제로 새로고침하고 즉시 캐시를 업데이트하십시오.
+ 버전 번호를 가져옵니다. 예: ```http://www.xxx.com/xxx.js?version=1```.
+ 동일한 이름의 파일을 사용하지 않고 다른 파일명으로 바꾸십시오.

만약 위 단계를 통해 문제를 해결할 수 없는 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 문의해 주시면 감사하겠습니다.

[](id:q9)
### CDN에 링크 도용 방지 화이트리스트를 설정한 후, 웹 사이트에 정상적으로 액세스할 수 없는 경우 어떻게 하나요?

링크 도용 방지 설정에서 화이트리스트를 활성화할 때 [비어있는 referer 포함]을 선택해야 브라우저를 통해 웹 사이트에 바로 액세스할 수 있습니다. 브라우저에서 바로 액세스 시 referer는 비어 있습니다.
![이미지 설명](https://main.qcloudimg.com/raw/3ec77732d4f5266278af2e8f569b08a2.png)

[](id:q10)
### 트래픽 상한 설정으로 DDOS 공격을 막을 수 있습니까?

CDN의 주요 기능은 DDOS 방어가 아닌 가속입니다. CDN 대역폭 상한 기능을 사용할 경우 5분 이내에 대역폭 사용 현황을 자동으로 집계할 수 있습니다. 상한 임계 값에 도달했을 경우 CDN은 설정에 따라 다르게 반응합니다. **임계 값 최대치는 10000Tbps입니다**.

[](id:q11)
### Tencent Cloud CDN에서는 모든 노드 IP를 제공하나요? 
보안상의 이유로 현재 플랫폼에서는 CDN 노드의 IP 리스트를 지원하지 않고 있으나, 노드의 IP 바인딩 현황은 IP 바인딩 조회 페이지에서 조회할 수 있습니다. 자세한 내용은 [IP 바인딩 조회](https://intl.cloud.tencent.com/document/product/228/10747)를 참조하십시오.
