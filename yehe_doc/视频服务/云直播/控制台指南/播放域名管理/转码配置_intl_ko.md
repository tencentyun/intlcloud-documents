라이브 방송 재생은 기본적으로 원본 비트레이트를 통해 출력되며, 재생 비트레이트를 제한하거나 설정하고 싶은 경우 재생 도메인에 트랜스 코딩 템플릿을 연결할 수 있습니다. 본 문서에서는 재생 도메인에 트랜스 코딩 템플릿을 연결하는 방법과 바인딩을 해제하는 방법을 소개합니다.

## 주의 사항
- 템플릿 설정을 완료하면 약 5~10분 후 적용됩니다.
- 트랜스 코딩 템플릿을 지정하면 백그라운드에서 해당 비트레이트의 서로 다른 재생 주소를 생성하여 편리하게 선택하여 호출할 수 있습니다. 푸시 스트리밍 원본 해상도가 최대한 원본 비율과 비슷해야 화면이 늘어나는 변형이 발생하지 않습니다.
- 처음 새로운 비트레이트 주소에 액세스하는 경우, 처음 트리거된 링크에 접속한 사용자의 로딩 시간이 조금 길어지는 것은 정상적인 현상입니다.
- 도메인별로 여러 개의 트랜스 코딩 템플릿을 연결할 수 있으며, 연결한 후 재생 비트레이트는 설정된 트랜스 코딩 포맷에 따라 트랜스 코딩됩니다.



## 전제 조건
- [LVB 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 하며 [재생 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.
- [트랜스 코딩 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31071)이 완료되어 있어야 합니다.


## 트랜스 코딩 템플릿 연결
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **재생 도메인** 또는 오른쪽에 있는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Template Configuration] 탭을 선택해 [Transcoding Configuration] 부분 오른쪽 상단의 [Edit]를 클릭합니다.
3. 각 트랜스 코딩을 선택하여 템플릿을 설정하고, 해당 도메인의 재생 주소에 컴파일 방식과 비트레이트가 설정된 템플릿을 지정합니다.
4. [Save]를 클릭합니다.

![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

## 트랜스 코딩 재생 주소 설명
트랜스 코딩 템플릿을 설정한 후 재생 URL에는 트랜스 코딩 템플릿 이름이 필요합니다. URL은 **재생 주소_트랜스 코딩 템플릿 이름** 방식으로 조합되며, 트랜스 코딩 템플릿 이름을 조합하지 않는 경우 원본 라이브 방송 스트리밍 콘텐츠가 재생됩니다. 재생 주소에 대한 자세한 내용은 [재생 설정](https://intl.cloud.tencent.com/document/product/267/31058)을 참조하십시오.

**예시: **재생 도메인과 연결한 트랜스 코딩 템플릿 이름이 **hd**인 경우, 원본 재생 주소:
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
트랜스 코딩 후의 비디오를 획득하고 재생할 경우 다음과 같은 새로 생성한 새로운 재생 주소가 필요합니다.
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>

<span id="Untie"></span>
## 트랜스 코딩 템플릿 바인딩 해제
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 재생 도메인 또는 오른쪽에 있는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Template Configuration] 탭을 선택해 [Transcoding Configuration]을 선택합니다.
3. 오른쪽 [Edit]를 클릭하여 해당 템플릿 선택을 해제합니다.
4. [Save]를 누르면 템플릿과 도메인 연결이 취소됩니다.
![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

>?템플릿 삭제가 필요한 경우, 템플릿 바인딩 해제 후 [기능 템플릿]>[트랜스 코딩 설정](https://console.cloud.tencent.com/live/config/transcode) 페이지로 이동하여 삭제할 수 있습니다. 자세한 내용은 [템플릿 삭제](https://intl.cloud.tencent.com/document/product/267/31071#delect)를 참조하십시오.
