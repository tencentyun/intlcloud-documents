Tencent Cloud COS(Cloud Object Storage)는 다중 지역 소토리지를 지원하며 다른 지역의 기본 액세스 도메인 이름이 다릅니다. 버킷을 생성할 때 선택한 지역은 수정할 수 없습니다. 업로드 및 다운로드 속도를 향상시키기 위해 자신의 비즈니스 시나리오에 따라 가장 가까운 지역을 선택하여 소토리지를 배포하는 것이 좋습니다.

## 사용 가능한 지역 및 액세스 도메인 이름
>!
>- 버킷이 생성된 후 해당 기본 도메인 이름이 생성됩니다. [COS 콘솔](https://console.cloud.tencent.com/cos5)로 이동하여 버킷의 [도메인 이름 관리]에서 볼 수 있습니다.
>- BucketName은 버킷을 만들 때 입력한 사용자 지정의 이름입니다. 자세한 내용은 [버킷 명명 규칙](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83)을 참조하십시오.
>- APPID는 사용자가 Tencent Cloud 계정을 성공적으로 신청한 후 받은 계정이며 시스템에서 자동적으로 활당되어 고유성을 지닙니다. [Tencent Cloud 콘솔]의 [계정 정보](https://console.cloud.tencent.com)를 통해 볼 수 있습니다.
>- 이전 버전에 지원하는 지역 정보는 [이전 버전 지역 리스트](https://cloud.tencent.com/document/product/436/7777)를 참조하십시오.


| 지역       | 약칭         | 기본 도메인 이름(업로드/다운로드/관리)                          |
| -------- | ------------ | ---------------------------------------- |
| 베이징 1지역(매진됨)| ap-beijing-1 | &lt;BucketName-APPID&gt;.cos.ap-beijing-1.myqcloud.com |
| 베이징       | ap-beijing   | &lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com |
| 상하이(화동)   | ap-shanghai  | &lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com |
| 광저우(화남)   | ap-guangzhou | &lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com |
| 청두(서남)   | ap-chengdu   | &lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com |
| 충칭       | ap-chongqing | &lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com |
| 싱가포르      | ap-singapore | &lt;BucketName-APPID&gt;.cos.ap-singapore.myqcloud.com |
| 홍콩       | ap-hongkong  | &lt;BucketName-APPID&gt;.cos.ap-hongkong.myqcloud.com |
| 토론토      | na-toronto   | &lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com |
| 프랑크푸르트     | eu-frankfurt | &lt;BucketName-APPID&gt;.cos.eu-frankfurt.myqcloud.com |
| 뭄바이       | ap-mumbai    | &lt;BucketName-APPID&gt;.cos.ap-mumbai.myqcloud.com |
| 서울       | ap-seoul     | &lt;BucketName-APPID&gt;.cos.ap-seoul.myqcloud.com |
| 실리콘 밸리       | na-siliconvalley     | &lt;BucketName-APPID&gt;.cos.na-siliconvalley.myqcloud.com |
| 버지니아       | na-ashburn     | &lt;BucketName-APPID&gt;.cos.na-ashburn.myqcloud.com |
| 방콕       | ap-bangkok     | &lt;BucketName-APPID&gt;.cos.ap-bangkok.myqcloud.com |
| 모스크바       | eu-moscow     | &lt;BucketName-APPID&gt;.cos.eu-moscow.myqcloud.com |
|도쿄       |ap-tokyo  |     &lt;BucketName-APPID&gt;.cos.ap-tokyo.myqcloud.com |

> 예시:
> 사용자가 소속 지역이 광저우인 버킷 하나를 만들고 examplebucket이라는 이름을 지정하였습니다. 사용자 APPID는 1250000000이면 버킷의 기본 도메인 이름은 다음과 같습니다.
```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

## 사설망 및 공중망 액세스
Tencent Cloud COS의 액세스 도메인 이름은 지능형 DNS 확인을 사용합니다. 다른 ISP 환경에서의 인터넷에 따라 COS에 액세스하는 데 최적의 링크를 찾아 제공합니다.

Tencent Cloud에서 COS에 액세스하기 위해 서비스를 배포한 경우 동일한 지역 내 액세스가 자동으로 사설망 주소로 리디렉션됩니다. 크로스 지역의 경우, 현재 사설망 액세스가 지원되지 않으며 공중망 주소로 연결됩니다.

사설망 및 공중망 액세스에 대한 자세한 내용은 [요청 작성 개요](https://cloud.tencent.com/document/product/436/31315) 문서를 참조하십시오.
