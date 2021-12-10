CSS 재생은 기본적으로 원래 비트 레이트로 출력됩니다. 재생 비트 레이트를 제한하거나 설정하려는 경우 재생 도메인 이름을 트랜스코딩 템플릿에 바인딩할 수 있습니다. 이 문서는 재생 도메인 이름을 트랜스코딩 템플릿에 바인딩/바인딩 해제하는 방법을 설명합니다.

## 주의 사항
- 템플릿 설정을 완료하면 약 5 - 10분 후 적용됩니다.
- 트랜스코딩 템플릿을 지정하면 백엔드에서 더 쉽게 사용할 수 있도록 다양한 비트 레이트로 다른 재생 주소를 생성합니다. 푸시 스트리밍 원본 해상도가 최대한 원본 비율과 비슷해야 화면이 늘어나거나 왜곡되지 않습니다.
- H.265의 호환성은 H.264보다 못하기 때문에, 플레이어가 H.265 인코딩을 지원하지 않아 재생에 실패하면, [트랜스코딩 템플릿](https://intl.cloud.tencent.com/document/product /267/31071) 설정을 통해 H.264 인코딩으로 변환하여 재생합니다.
- 새로운 비트 레이트 주소에 처음으로 액세스하는 경우, 처음 트리거된 링크에 접속한 사용자의 로딩 시간이 조금 길어지는 것은 정상적인 현상입니다.
- 도메인별로 여러 개의 트랜스코딩 템플릿을 연결할 수 있으며, 연결한 후 재생 비트 레이트는 설정된 트랜스코딩 포맷에 따라 트랜스코딩됩니다.
- 트랜스코딩 템플릿의 최대 설정 수량은 **50개**입니다.



## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 하며 [재생 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.
- [트랜스코딩 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31071)이 완료되어 있어야 합니다.

[](id:conect)
## 트랜스코딩 템플릿 연결
1. [[도메인 이름 관리]](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **재생 도메인** 또는 오른쪽에 있는 [관리]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [템플릿 설정] 탭을 선택해 [트랜스코딩 설정] 부분 오른쪽 상단의 [편집]을 클릭합니다.
3. 각 트랜스코딩을 선택하여 템플릿을 설정하고, 해당 도메인의 재생 주소에 컴파일 방식과 비트 레이트가 설정된 템플릿을 지정합니다.
4. [저장]을 클릭합니다.

![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

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
1. [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 재생 도메인 또는 오른쪽에 있는 [관리]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [템플릿 설정] 탭을 선택해 [트랜스코딩 설정]을 선택합니다.
3. 오른쪽 [편집]을 클릭하여 해당 템플릿 선택을 해제합니다.
4. [저장]을 클릭하면 템플릿과 도메인 연결이 취소됩니다.
![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

>? 템플릿을 삭제하려면 템플릿 바인딩 해제 후 [기능 템플릿]>[[트랜스코딩 설정]](https://console.cloud.tencent.com/live/config/transcode) 페이지로 이동하여 삭제할 수 있습니다. 자세한 내용은 [템플릿 삭제](https://intl.cloud.tencent.com/document/product/267/31071#delect)를 참고하십시오.
