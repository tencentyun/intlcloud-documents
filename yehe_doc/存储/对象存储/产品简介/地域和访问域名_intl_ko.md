## 소개

<b>리전(Region)</b>은 Tencent Cloud 호스팅 데이터 센터의 분포 지역을 의미하며, COS(Cloud Object Storage)의 데이터를 해당 리전의 버킷에 저장합니다. 사용자는 COS를 통해 데이터를 여러 리전에 저장할 수 있으며, 일반적으로 저지연, 저비용, 컴플라이언스 요건을 충족할 수 있도록 사용자의 비즈니스 지역과 가장 근접한 리전에 버킷을 생성하는 것을 권장합니다.

예를 들어, 비즈니스가 화남지역에 분포되어 있는 경우 광저우 리전을 선택해 버킷을 생성하면 객체의 업로드 및 다운로드 속도를 더욱 향상시킬 수 있습니다.

**기본 설정 도메인**은 COS의 기본 버킷 도메인을 말하며, 사용자가 버킷을 생성하면 시스템에서 버킷 이름과 리전에 따라 자동으로 생성합니다. 다른 리전의 버킷은 각각 다른 기본 도메인이 있습니다. [COS 콘솔](https://console.cloud.tencent.com/cos5)로 이동하여 버킷의 **개요 > 도메인 정보**에서 확인하실 수 있습니다.




### 중국대륙 리전

<table>
   <tr>
	 <th colspan=3><center>리전</center></th>
      <th>리전 약칭</th>
      <th>기본 도메인(업로드/다운로드/관리)</th>
   </tr>
   <tr>
      <td rowspan=10>중국대륙</td>
      <td rowspan=7 nowrap="nowrap">퍼블릭 클라우드 리전</td>
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
      <td rowspan=7>아시아 태평양</td>
      <td rowspan=13 nowrap="nowrap">퍼블릭 클라우드 리전</td>
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
      <td  nowrap="nowrap">자카르타</td>
      <td>ap-jakarta</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-jakarta.myqcloud.com</td>
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
      <td  nowrap="nowrap">실리콘밸리(미국 서부)</td>
      <td>na-siliconvalley</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-siliconvalley.myqcloud.com</td>
   </tr>
   <tr>
      <td  nowrap="nowrap">버지니아(미국 동부)</td>
      <td>na-ashburn</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-ashburn.myqcloud.com</td>
   </tr>
   <tr>
      <td>토론토</td>
      <td>na-toronto</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=1>남미</td>
      <td>상파울루</td>
      <td>sa-saopaulo</td>
      <td>&lt;BucketName-APPID&gt;.cos.sa-saopaulo.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=2>유럽</td>
      <td>프랑크푸르트</td>
      <td>eu-frankfurt</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-frankfurt.myqcloud.com</td>
   </tr>
</table>



### 글로벌 가속 도메인

글로벌 가속 도메인 포맷은 &lt;BucketName-APPID&gt;.cos.accelerate.myqcloud.com입니다. 글로벌 가속 도메인에 대한 소개 및 사용 예시는 [글로벌 가속 개요](https://intl.cloud.tencent.com/document/product/436/33409)를 참고하십시오.


### 예시

루트 계정(APPID: 1250000000)으로 COS 콘솔에 로그인하여 소속 리전이 **광저우**, 이름이 **examplebucket**인 버킷을 생성한 경우, 버킷의 기본 도메인은 다음과 같습니다.

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

>?
>
>- examplebucket-1250000000: 해당 버킷이 APPID가 1250000000인 사용자에게 귀속되어 있다는 것을 의미합니다. APPID는 Tencent Cloud 계정 신청 후 획득하게 되는 계정으로 시스템에서 자동으로 할당합니다. 변경 불가능한 고유 ID로 [계정 정보](https://console.cloud.tencent.com/developer)에서 확인할 수 있습니다.
>- cos: Cloud Object Storage.
>- ap-guangzhou: 버킷의 리전 약칭.
>- myqcloud.com: Tencent Cloud 도메인, 고정 문자 부호.

버킷을 생성한 후 이미지 파일 picture.jpg를 해당 버킷에 업로드하는 경우, 이미지 picture.jpg의 액세스 주소는 다음과 같습니다.

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/picture.jpg
```

>? 이미지 액세스 권한을 **공개 읽기 및 개인 쓰기**로 설정하고 이미지 액세스 주소를 브라우저에 붙여넣으면 이미지 상세 정보를 확인할 수 있습니다.
>



## 내부 네트워크 및 공인 네트워크 액세스

동일 리전 내 CVM(Cloud Virtual Machine)에서는, COS 기본 도메인을 통해 파일에 액세스할 때 기본적으로 내부 네트워크 링크를 사용하는데 이때 파일 업로드 및 다운로드는 내부 네트워크 트래픽을 발생시키며 트래픽 요금은 발생하지 않으나, 요청 수에 대한 요금은 부과됩니다.

Tencent Cloud COS의 액세스 도메인은 스마트 DNS 리졸브를 사용하여 각 통신사 환경의 인터넷에서 COS 액세스를 검증하고 최적의 링크를 제공합니다.

Tencent Cloud 내부에 서비스를 배포하여 COS 액세스에 사용하는 경우, 리전 내 액세스가 자동으로 내부 네트워크 주소로 안내됩니다. 현재 리전 간에는 내부 네트워크 액세스를 지원하지 않으며, 기본적으로 외부 네트워크 주소로 리졸브됩니다. 리전 간 내부 네트워크 통신이 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 문의하십시오.

내부 네트워크 및 공인 네트워크 액세스에 대한 자세한 내용은 [요청 생성 개요](https://intl.cloud.tencent.com/document/product/436/30613) 문서를 참고하십시오.

