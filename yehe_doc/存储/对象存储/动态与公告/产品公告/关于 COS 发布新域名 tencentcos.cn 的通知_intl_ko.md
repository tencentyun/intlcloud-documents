COS(Cloud Object Storage)는 2022년 7월 25일에 새로운 도메인 이름 tencentcos.cn을 출시할 예정입니다. 현재 도메인 이름 myqcloud.com은 계속 사용할 수 있지만 COS의 새로운 기능을 지원하지 않으므로 더 안전하고 신뢰할 수 있는 새 도메인 이름 tencentcos.cn으로 전환하는 것이 좋습니다.


>! 기존 도메인 이름 myqcloud.com은 계속 사용할 수 있으며 기존 기능은 ​​영향을 받지 않습니다. 단, 추후 제공되는 새로운 COS 기능은 지원되지 않습니다.
>

구체적으로 다음과 같은 변경 사항이 있습니다.

**1. 도메인 이름에 접미사 tencentcos.cn 사용**

기본 버킷 도메인 이름을 예로 들면 새 도메인 이름은 &lt;bucket-appid&gt;.cos.&lt;region&gt;.tencentcos.cn 형식입니다.

**2. 사설망 도메인 이름 제공**

사설망을 통해서만 액세스할 수 있으며 공중망 트래픽을 사용하지 않는 독립적인 사설망 도메인 이름이 제공됩니다.

기본 버킷 도메인 이름을 예로 들면 새 사설망 도메인 이름은 &lt;bucket-appid&gt;.cos-internal.&lt;region&gt;.tencentcos.cn 형식입니다.

**3. tencentcos.cn 도메인 이름 지원**
사설망 도메인 이름을 제외한 모든 새 도메인 이름은 스마트 DNS를 지원하므로 시스템은 액세스 환경에 따라 사설망과 공중망을 자동으로 전환합니다.

| 도메인 이름   |  예시              |
| -------------- | ---------------- |
| 기본 버킷 도메인 이름 | &lt;bucket-appid&gt;.cos.&lt;region&gt;.tencentcos.cn  |
| 기본 버킷 도메인 이름(사설망) | &lt;bucket-appid&gt;.cos-internal.&lt;region&gt;.tencentcos.cn  |
| 글로벌 가속 도메인 이름 | &lt;bucket-appid&gt;.cos.&lt;accelerate&gt;.tencentcos.cn  |
| 글로벌 가속 도메인 이름(사설망) | &lt;bucket-appid&gt;.cos-internal.&lt;accelerate&gt;.tencentcos.cn  |
| 정적 웹사이트 도메인 이름 | &lt;bucket-appid&gt;.cos-website.&lt;region&gt;.tencentcos.cn  |
| 정적 웹사이트 도메인 이름(사설망) | &lt;bucket-appid&gt;.cos-website-internal.&lt;region&gt;.tencentcos.cn  |   
