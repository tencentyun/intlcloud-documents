COS(Cloud Object Storage)는 2022년 03월 15일에 새로운 도메인인 tencentcos.cn을 출시합니다. 현재 도메인 myqcloud.com은 계속 사용할 수 있지만 COS의 새로운 기능을 지원하지 않으므로 더 안전하고 안정적인 새 도메인으로 전환하는 것이 좋습니다. 


>! 기존 도메인 myqcloud.com은 계속 사용할 수 있으며 기존 도메인의 기존 기능(예: 내부 및 외부 네트워크의 스마트 리졸브)은 ​​영향을 받지 않지만 신규 기능이 더 이상 지원되지 않습니다.
>

구체적으로 두 가지 변경 사항이 있습니다.

**1. 도메인 이름에 접미사 tencentcos.cn 사용**

다음은 기본 버킷 도메인 예시입니다.

- 기존 도메인 이름 형식: &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com 
- 신규 도메인 이름 형식: &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com 

**2. 비공개 및 공개 액세스에 서로 다른 도메인 이름 사용**

현재 비공개 및 공개 액세스를 위한 도메인 이름의 형식은 동일합니다. 예를 들어, 모든 기본 버킷 도메인은 &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com 형식입니다.

앞으로 공개 및 비공개 액세스를 위한 도메인 이름은 다른 형식을 사용할 것입니다. 기본 버킷 도메인을 예로 들어 보겠습니다.

- 공개 액세스 도메인 이름 형식: &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.tencentcos.cn 
- 비공개 액세스 도메인 이름 형식: &lt;BucketName-APPID&gt;.cos-internal.&lt;Region&gt;.tencentcos.cn 


아래 표는 현재 도메인과 새 도메인 비교표입니다.

| 도메인 형식   | 기존 도메인                    | 신규 도메인                |
| -------------- | ---------------------------------- | ---------------- |
| 기본 버킷 도메인 | &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com, 비공개 및 공개 액세스용 도메인 동일. | <ul  style="margin: 0;"><li>공개 액세스용 도메인: &lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.tencentcos.cn </li><li>비공개 액세스용 도메인: &lt;BucketName-APPID&gt;.cos-internal.&lt;Region&gt;.tencentcos.cn </li></ul>     |   
| 글로벌 가속 도메인 | &lt;BucketName-APPID&gt;.cos.accelerate.myqcloud.com, 비공개 및 공개 액세스용 도메인 동일.   |  <ul  style="margin: 0;"><li>공개 액세스용 도메인: &lt;BucketName-APPID&gt;.cos.accelerate.tencentcos.cn </li><li>비공개 액세스용 도메인: &lt;BucketName-APPID&gt;.cos-internal.accelerate.tencentcos.cn </li></ul>              |   
| 정적 웹사이트용 도메인 |&lt;BucketName-APPID&gt;.cos-website.&lt;Region&gt;.myqcloud.com, 비공개 및 공개 액세스용 도메인 동일. | <ul  style="margin: 0;"><li>공개 액세스 도메인: &lt;BucketName-APPID&gt;.cos-website.&lt;Region&gt;.tencentcos.cn </li><li>비공개 액세스용 도메인: &lt;BucketName-APPID&gt;.cos-website-internal.&lt;Region&gt;.tencentcos.cn</li></ul> |       


