## 소개

**리전(Region)**은 Tencent Cloud 호스팅 데이터센터의 분포 지역으로, COS의 데이터가 해당 리전의 버킷에 저장됩니다. COS를 통해 데이터를 멀티 리전에 저장할 수 있으며, 일반적으로 낮은 딜레이, 저렴한 비용, 컴플라이언스 요구에 만족하기 위해 귀하의 비즈니스 지역과 가장 가까운 리전에 버킷을 생성하는 것을 권장합니다.

예를 들어 귀하의 비즈니스가 화난 지역에 분포되어 있을 경우 광저우 리전에 버킷을 생성하면 객체 업로드 및 다운로드 속도를 더욱 향상시킬 수 있습니다.

**기본 도메인**이란 COS의 기본 버킷 도메인으로, 버킷 생성 시 시스템이 버킷 이름 및 리전에 따라 자동으로 생성합니다. 각 리전별 버킷에는 서로 다른 기본 도메인이 존재합니다.


> ?버킷 생성 후에는 상응하는 기본 도메인이 생성되며, [COS 콘솔](https://console.cloud.tencent.com/cos5)에서 버킷의 [기본 설정]을 확인할 수 있습니다.


### 중국대륙 리전

<table>
   <tr>
	 <th colspan=3><center>리전</center></th>
      <th>리전 약칭</th>
      <th>기본 도메인(업로드/다운로드/관리)</th>
   </tr>
   <tr>
      <td rowspan=10>중국대륙</td>
      <td rowspan=7 nowrap="nowrap">공유 클라우드 리전</td>
      <td nowrap="nowrap">베이징 1존(품절)</td>
      <td>ap-beijing-1</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-beijing-1.myqcloud.com</td>
   </tr>
   <tr>
      <td>베이징</td>
      <td>ap-beijing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com</td>
   </tr>
   <tr>
      <td>난징</td>
      <td>ap-nanjing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-nanjing.myqcloud.com</td>
   </tr>
   <tr>
      <td>상하이</td>
      <td>ap-shanghai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com</td>
   </tr>
   <tr>
      <td>광저우</td>
      <td>ap-guangzhou</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com</td>
   </tr>
   <tr>
      <td>청두</td>
      <td>ap-chengdu</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com</td>
   </tr>
   <tr>
      <td>충칭</td>
      <td>ap-chongqing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com</td>
   </tr>
</table>




### 중국홍콩 및 해외 리전

<table>
   <tr>
	 <th colspan=3><center>리전</center></th>
      <th>리전 약칭</th>
      <th>기본 도메인(업로드/다운로드/관리)</th>
   </tr>
   <tr>
      <td rowspan=6>아시아 태평양</td>
      <td rowspan=11 nowrap="nowrap">공유 클라우드 리전</td>
      <td>중국홍콩</td>
      <td>ap-hongkong</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-hongkong.myqcloud.com</td>
   </tr>
   <tr>
      <td>싱가포르</td>
      <td>ap-singapore</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-singapore.myqcloud.com</td>
   </tr>
   <tr>
      <td>뭄바이</td>
      <td>ap-mumbai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-mumbai.myqcloud.com</td>
   </tr>
   <tr>
      <td>서울</td>
      <td>ap-seoul</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-seoul.myqcloud.com</td>
   </tr>
   <tr>
      <td>방콕</td>
      <td>ap-bangkok</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-bangkok.myqcloud.com</td>
   </tr>
   <tr>
      <td>도쿄</td>
      <td>ap-tokyo</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-tokyo.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=3>북미</td>
      <td>실리콘밸리(미국 서부)</td>
      <td>na-siliconvalley</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-siliconvalley.myqcloud.com</td>
   </tr>
   <tr>
      <td>버지니아주(미국 동부)</td>
      <td>na-ashburn</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-ashburn.myqcloud.com</td>
   </tr>
   <tr>
      <td>토론토</td>
      <td>na-toronto</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=2>유럽</td>
      <td>프랑크푸르트</td>
      <td>eu-frankfurt</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-frankfurt.myqcloud.com</td>
   </tr>
   <tr>
      <td>모스크바</td>
      <td>eu-moscow</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-moscow.myqcloud.com</td>
   </tr>
</table>


### 글로벌 가속 도메인

글로벌 가속 도메인 포맷은 `<BucketName-APPID>.cos.accelerate.myqcloud.com`입니다. 글로벌 가속 도메인에 대한 소개 및 이용 사례는 [글로벌 가속 개요](https://intl.cloud.tencent.com/document/product/436/33409)를 참조하십시오.


### 예시

루트 계정(APPID: 1250000000)으로 COS 콘솔에 로그인하여 버킷을 생성하였고, 해당 버킷의 소속 리전이 **광저우**, 버킷 이름이 **examplebucket**인 경우, 버킷의 기본 도메인은 다음과 같습니다.

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

>?
>
>- examplebucket-1250000000: 해당 버킷이 APPID가 1250000000인 사용자에게 귀속되어 있다는 것을 의미합니다. APPID는 Tencent Cloud 계정 신청 후 획득하게 되는 계정으로 시스템에서 자동으로 할당합니다. 변경 불가능한 고유 ID로 [계정 정보](https://console.cloud.tencent.com/developer)에서 확인할 수 있습니다.
>- cos: 객체 스토리지 COS
>- ap-guangzhou: 버킷의 리전 약칭
>- myqcloud.com: Tencent Cloud 도메인, 고정 문자열

버킷을 생성한 후, 이미지 파일 picture.jpg를 해당 버킷에 업로드하는 경우, 이미지 picture.jpg의 액세스 주소는 다음과 같습니다.

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/picture.jpg
```

>?이미지 액세스 제한을 **공개 읽기, 쓰기 제한**으로 설정하고 이미지 액세스 주소를 브라우저에 붙여 넣으면 이미지 상세 정보를 확인할 수 있습니다.



## 내부 네트워크 및 외부 네트워크 액세스

Tencent Cloud COS의 액세스 도메인은 스마트 DNS 리졸브를 사용하여 인터넷을 통해 각각의 통신사 환경에서의 COS 액세스를 점검하고 최적의 링크를 제공합니다.

Tencent Cloud 내부에 서비스를 배포하여 COS 액세스에 사용하는 경우 리전 내 액세스가 자동으로 내부 네트워크 주소로 바인딩됩니다. 현재 리전 간에는 내부 네트워크 액세스를 지원하지 않으며, 기본적으로 외부 네트워크 주소로 리졸브됩니다.

내부 네트워크 및 외부 네트워크에 관한 자세한 정보는 [요청 생성 개요](https://intl.cloud.tencent.com/document/product/436/30613) 문서를 참조하십시오.