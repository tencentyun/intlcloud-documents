CSS를 사용하면 기본적으로 원본 스트림의 비트 레이트가 재생에 사용됩니다. 다른 재생 비트 레이트를 사용하려면 트랜스코딩 또는 어댑티브 비트 레이트 템플릿을 사용하여 도메인을 바인딩할 수 있습니다. 이 문서는 템플릿을 재생 도메인에 바인딩하고 템플릿을 재생 도메인에서 바인딩 해제하는 방법을 보여줍니다.

## 주의 사항
- 템플릿 설정을 완료하면 약 5 - 10분 후 적용됩니다.
- 트랜스코딩 템플릿을 지정하면 백엔드에서 더 쉽게 사용할 수 있도록 다양한 비트 레이트로 다른 재생 주소를 생성합니다. 푸시 스트리밍 원본 해상도가 최대한 원본 비율과 비슷해야 화면이 늘어나거나 왜곡되지 않습니다.
- H.265의 호환성은 H.264보다 못하기 때문에, 플레이어가 H.265 인코딩을 지원하지 않아 재생에 실패하면, [트랜스코딩 템플릿](https://intl.cloud.tencent.com/document/product /267/31071) 설정을 통해 H.264 인코딩으로 변환하여 재생합니다.
- 새로운 비트 레이트 주소에 처음으로 액세스하는 경우, 처음 트리거된 링크에 접속한 사용자의 로딩 시간이 조금 길어지는 것은 정상적인 현상입니다.
- 도메인별로 여러 개의 트랜스코딩 템플릿을 연결할 수 있으며, 연결한 후 재생 비트 레이트는 설정된 트랜스코딩 포맷에 따라 트랜스코딩됩니다.
- 최대 **50개**의 트랜스 코딩 템플릿을 만들 수 있습니다.



## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 하며 [재생 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.
- [트랜스 코딩 템플릿](https://intl.cloud.tencent.com/document/product/267/31071) 또는 [어댑티브 비트 레이트 템플릿](https://cloud.tencent.com/document/product/267/78369) 생성을 완료해야 합니다.

[](id:conect)
## 트랜스코딩 템플릿 바인딩
1. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)로 이동합니다. **재생 도메인 이름**을 클릭하거나 오른쪽에서 **관리**를 클릭합니다.
2. **템플릿 구성** 탭을 선택하고, **트랜스코딩 구성** 영역에서 **편집**을 클릭합니다.
3. 트랜스코딩 템플릿을 선택합니다. 현재 도메인의 비디오는 템플릿에 지정된 코덱 및 비트 레이트를 사용하여 트랜스코딩됩니다.
4. **확인**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/2d8cb5be76debfbd04d60329891c5830.png)

[](id:descript)
## 트랜스코딩 재생 주소 설명
트랜스코딩 템플릿 설정 후 재생 URL에 트랜스코딩 템플릿 이름을 추가해야 합니다. 연결 방식은 **재생 주소_트랜스코딩 템플릿 이름**입니다. 트랜스코딩 템플릿 이름이 연결되지 않은 경우, 원본 라이브 방송 스트리밍 콘텐츠가 재생됩니다. 재생 주소에 대한 더 자세한 내용은 [재생 설정](https://intl.cloud.tencent.com/document/product/267/31058)을 참고하십시오.

**예시:** 재생 도메인과 연결한 트랜스코딩 템플릿 이름이 **hd**인 경우, 원본 재생 주소:
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
트랜스코딩 후의 비디오를 획득하고 재생할 경우 다음과 같은 새로 생성한 신규 재생 주소가 필요합니다.
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>
[](id:Untie)

## 트랜스코딩 템플릿 바인딩 해제
1. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)로 이동합니다. 설정의 재생 도메인 이름을 클릭하거나 오른쪽에서 **관리**를 클릭하여, 도메인 세부 정보 페이지로 이동합니다.
2. **템플릿 구성** 탭을 선택합니다. **트랜스코딩 구성**을 선택합니다.
3. 트랜스코딩 구성 영역에서 오른쪽의 **편집**을 클릭하고 바인딩을 해제할 템플릿을 선택 해제합니다.
4. **확인**을 클릭합니다. 템플릿과 도메인의 연결이 취소됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ff6e5f8038124c95fb29d0ffb5745890.png)

>? 템플릿을 삭제하려면 먼저 바인딩을 해제한 다음 **기능 구성** > [**트랜스코딩 설정**](https://console.cloud.tencent.com/live/config/transcode)으로 이동하여 템플릿을 삭제해야 합니다. 자세한 내용은 [템플릿 삭제](https://intl.cloud.tencent.com/document/product/267/31071#delect)를 참고하십시오.


## 어댑티브 비트 레이트 템플릿 바인딩

1. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)로 이동합니다. **재생 도메인 이름**을 클릭하거나 오른쪽에서 **관리**를 클릭합니다.
2. **템플릿 구성** 탭을 선택하고 **어댑티브 비트 레이트 구성** 영역에서 **편집**을 클릭합니다.
3. 어댑티브 비트 레이트 설정 템플릿을 선택합니다. 템플릿에 따라 현재 도메인의 비디오에 대해 다른 비트 레이트의 스트림이 생성됩니다.
4. **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/df2db1fd5b8f9beb5eda4eb989557c51.png)

## 어댑티브 비트 레이트 URL 형식
어댑티브 비트 레이트 재생에는 HLS 및 WebRTC만 지원됩니다. 두 프로토콜의 URL 형식은 다릅니다. 자세한 내용은 [재생 설정](https://intl.cloud.tencent.com/document/product/267/31058)을 참고하십시오.
**HLS URL:**
**예시:** 어댑티브 비트 레이트 템플릿 바인딩의 이름이 **autobitrate**이고 원래 재생 URL이 다음과 같다고 가정합니다.

<pre>
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
트랜스코딩 후의 비디오를 획득하고 재생할 경우 다음과 같은 새로 생성한 신규 재생 주소가 필요합니다.
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_autobitrate</b>.m3u8?txSecret=Md5(key+<b style="color:yellow;">StreamName_autobitrate</b>+hex(time))&txTime=hex(time)
</pre>
**WebRTC URL:**
**예시:** 어댑티브 비트 레이트 템플릿 바운드에 세 개의 스트림이 있다고 가정합니다. 이름은 test1, test2 및 test3이며 비트 레이트는 각각 200Kbps, 300Kbps 및 400Kbps입니다.
어댑티브 비트 레이트 재생 URL은 다음과 같습니다.

webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)&tabr_bitrates=test3,test2,test1&tabr_start_bitrate=test1&tabr_control=auto。

## 어댑티브 비트 레이트 템플릿 바인딩 해제
1. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)로 이동합니다. 재생 도메인 이름을 클릭하거나 오른쪽에서 **관리**를 클릭하여, 도메인 세부 정보페이지로 이동합니다.
2. **템플릿 구성** 탭을 선택합니다. **어댑티브 비트레이트 구성**을 선택합니다.
3. 어댑티브 비트레이트 구성 영역에서 오른쪽의 **편집**을 클릭하고 바인딩을 해제할 템플릿을 선택 해제합니다.
4. **확인**을 클릭합니다. 템플릿과 도메인의 연결이 취소됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/872b71589554e8d89abf50db40f75777.png)

>? 템플릿을 삭제하려면 먼저 바인딩을 해제한 다음 **기능 구성** > [**트랜스코딩 설정**](https://console.cloud.tencent.com/live/config/transcode)으로 이동하여 템플릿을 삭제해야 합니다. 자세한 내용은 [템플릿 삭제](https://intl.cloud.tencent.com/document/product/267/31071#delect)를 참고하십시오.
