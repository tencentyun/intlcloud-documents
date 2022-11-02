## 소개

WordPress는 인기 있는 오픈 소스 블로그 프레임워크 및 콘텐츠 관리 시스템입니다. 어려움을 크게 줄이고 웹 사이트 구축의 효율성을 높일 수 있습니다. WordPress의 사전 설정 플랜을 사용하면 몇 분 만에 작은 웹사이트를 만들고 실행할 수 있습니다. 그러나 웹 사이트에 이미지, 오디오/비디오를 추가하면 대역폭과 저장 공간에 대한 요구 사항이 점점 더 많아지고 웹 사이트 성능에 영향을 미치기 시작할 수 있습니다. 미디어 파일의 관리는 웹사이트의 장기적인 운영에 매우 중요합니다.

### VOD를 사용해야 하는 이유

장기적으로 운영하려는 웹사이트를 구축할 때 WordPress의 사전 설정 플랜을 사용하지 않는 것이 좋습니다. 사전 설정 플랜은 미디어 파일을 웹 서버에 저장하기 때문에 다음과 같은 단점이 있습니다.
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:10px">No.</td>
<th>상세 정보</td>
</tr>
<tr  ><td>1</td>
<td>사용자가 웹 서버에서 호스팅되는 미디어 파일에 액세스하면 동영상이 끊길 수 있고 이미지가 느리게 로딩될 수 있습니다.</td>
</tr>
<tr  ><td>2</td>
<td>웹 서버에서 호스팅되는 미디어 파일에 액세스하면 대역폭 리소스가 소모되고 대역폭을 모두 차지할 수 있습니다.</td>
</tr>
<tr  ><td>3</td>
<td>웹사이트가 성장함에 따라 미디어 파일이 서버의 모든 스토리지 공간을 차지할 수 있습니다.</td>
</tr>
<tr  ><td>4</td>
<td>다른 서버로 마이그레이션할 때 미디어 파일 전송이 어려울 수 있습니다.</td>
</tr>
</tbody>
</table>

VOD는 미디어 저장, 트랜스코딩, 배포/재생 가속 서비스를 제공합니다. 이를 사용하여 웹 사이트를 구축하면 다음과 같은 장점이 있습니다.
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:10px">No.</td>
<th>상세 정보</td>
</tr>
<tr  ><td>1</td>
<td>WordPress 플러그인 또는 SDK를 사용하여 웹사이트의 미디어 파일을 VOD에 업로드하고 저장할 수 있습니다. 이렇게 하면 서버의 스토리지 공간을 확보하고 서버 마이그레이션을 용이하게 할 수 있습니다. 또한 실수로 파일을 삭제하는 문제를 방지합니다.</td>
</tr>
<tr  ><td>2</td>
<td>VOD는 미디어 파일에 대한 CDN 주소를 제공합니다. 이미지, 오디오/비디오에 대한 액세스가 더 빨라지고 더 이상 서버의 대역폭을 소모하지 않습니다.</td>
</tr>
</tbody>
</table>


VOD는 또한 액세스 제어, 미디어 처리 및 콘텐츠 조정 기능을 제공합니다. 자세한 내용은 [Feature Overview](https://intl.cloud.tencent.com/document/product/266/49084)를 참고하십시오.

### VOD WordPress 플러그인

VOD는 [WordPress 플러그인](https://wordpress.org/plugins/tencentcloud-vod/)을 제공합니다. 이 플러그인을 사용하면 [VOD 서브 애플리케이션](https://intl.cloud.tencent.com/document/product/266/33987)을 바인딩하여 VOD에서 WordPress 미디어 파일을 호스팅할 수 있습니다. 웹사이트 방문자는 VOD에서 제공하는 CDN 주소를 통해 파일에 액세스할 수 있습니다. 현재 플러그인은 다음 기능을 제공합니다.

- VOD 서브 애플리케이션을 WordPress에 바인딩할 수 있습니다.
- WordPress에 업로드한 동영상 파일은 VOD 서브 애플리케이션에 자동으로 저장될 수 있습니다.
- 웹페이지에 동영상을 삽입하면 VOD에서 제공하는 주소로 동영상이 재생됩니다.

## 준비 작업
### 1. VOD 서브 애플리케이션 생성

VOD 애플리케이션은 리소스 격리 구현에 도움이 됩니다. 서로 다른 웹사이트를 서로 다른 VOD 서브 애플리케이션에 바인딩하여 미디어 파일을 개별적으로 관리할 수 있습니다. 서브 애플리케이션 생성 방법에 대한 자세한 내용은 [서브 애플리케이션 기능 활성화](https://intl.cloud.tencent.com/document/product/266/33987#.E5.BC.80.E9.80.9A.E5.AD.90.E5.BA.94.E7.94.A8)를 참고하십시오.

### 2. WordPress를 사용하여 웹사이트 구축
다음 두 가지 방법 중 하나로 WordPress 웹 사이트를 구축할 수 있습니다.
<dx-tabs>
::: 방법1(권장)
TencentCloud Lighthouse 또는 Cloud Virtual Machine의 WordPress 이미지를 사용하여 웹사이트를 구축합니다.
:::
::: 방법2
최신 버전의 WordPress를 [다운로드](https://cn.wordpress.org/download/)하여 설치합니다. 자세한 내용은 [WordPress 설치 방법](https://wordpress.org/support/article/how-to-install-wordpress/)을 참고하십시오.
:::
</dx-tabs>


## 작업 단계

### 1단계: 플러그인 설치

<dx-tabs>
::: 방법1
검색 창에 **tencentcloud-vod**를 입력하고 **설치 > 활성화**를 클릭합니다.

![온라인 설치](https://qcloudimg.tencent-cloud.cn/raw/1dea0a047d5df7dc67eedb907dbaf586.png)
:::
::: 방법2
최신 버전의 플러그인 ZIP 파일을 [다운로드](https://github.com/Tencent-Cloud-Plugins/tencentcloud-wordpress-plugin-vod/releases/latest/download/tencentcloud-wordpress-plugin-vod.zip)하여 설치합니다. WordPress에서 **플러그인 업로드 > 파일 선택 > 지금 설치 > 플러그인 활성화**를 클릭합니다.

![다운로드 및 설치](https://qcloudimg.tencent-cloud.cn/raw/3e16ee19f1dcf3a5734e67e293e72f2f.png)
:::
</dx-tabs>


### 2단계: 플러그인 구성

WordPress 왼쪽 사이드바에서 **Tencent Cloud 설정 > [VOD](https://intl.cloud.tencent.com/document/product/266/33897)**를 선택합니다.

다음 구성을 완료합니다.

| **항목**           | **설명**                                                     |
| -------------------- | ------------------------------------------------------------ |
| 사용자 정의 키           이 기능을 끄면 **Tencent Cloud 설정**용으로 구성된 키가 사용되며, 이는 VOD 플러그인이 다른 Tencent Cloud 플러그인과 동일한 키를 사용한다는 것을 의미합니다. 이 기능을 켜면 아래에 구성된 키가 사용됩니다. |
| SecretId、SecretKey | 액세스 키입니다. 콘솔의 [API Keys](https://console.cloud.tencent.com/cam/capi) 페이지로 이동하여 액세스 키를 생성하고 볼 수 있습니다. |
| SubAppID             | 바인딩하려는 VOD 서브 애플리케이션의 ID입니다. [애플리케이션 관리](https://console.cloud.tencent.com/vod/app-manage)에서 VOD 애플리케이션을 볼 수 있습니다. |
| 어댑티브 비트레이트 | 이 기능을 활성화하면 업로드된 비디오가 여러 비트레이트로 인코딩됩니다. 자세한 내용은 [Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/49258)을 참고하십시오. |

**저장**을 클릭합니다.

### 3단계: 웹페이지에 VOD 동영상 업로드 및 사용
1. 플러그인 설정이 완료되면 WordPress 미디어 라이브러리에 있는 동영상과 글이나 웹페이지를 편집하면서 업로드한 동영상이 자동으로 VOD에 저장됩니다.
2. 예를 들어 WordPress에서 게시물을 편집할 때 더하기 아이콘을 클릭하고 ‘동영상’을 선택한 다음 **업로드**를 클릭하여 동영상을 업로드합니다. 동영상이 업로드된 후 오른쪽 상단의 **미리보기**를 클릭합니다. VOD의 URL을 통해 동영상이 재생되는 것을 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0d5cd195f0d9db5c0e4cb9161601823f.png)
3. 아래에서 볼 수 있듯이 왼쪽의 동영상은 웹 서버에 저장되어 대역폭이 제한되어 끊김 현상이 발생합니다. CDN을 사용하여 비디오 배포를 가속화하는 VOD를 사용하면 문제가 되지 않습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c336d83417e255868fe58338413a9325.gif)

## 확장
### HTTPS 사용

VOD는 기본적으로 HTTP를 사용합니다. HTTPS를 사용하려면 VOD 콘솔에서 서브 애플리케이션을 선택하고 **시스템 설정 > 배포 및 재생 > 기본 배포 도메인**에서 HTTPS를 선택합니다.
