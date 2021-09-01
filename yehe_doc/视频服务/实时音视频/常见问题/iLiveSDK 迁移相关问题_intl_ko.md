### TRTC V1(iLiveSDK)과 V2(LiteAVSDK) 버전은 무엇이 다른가요?
![](https://main.qcloudimg.com/raw/798eb3618bc87eea647e77a97ae48ca7.png)

| 차이 항목 | 구버전 V1 |  최신 버전 V2 |
|:-------:|:-------:|:-------:|
| 커널 아키텍처 | iLiveSDK | LiteAVSDK |
| IM SDK   |  내장형        |  비내장형       |
| API 인터페이스 |  V1 |  V2 |
| CDN 푸시 스트리밍 | REST API으로 활성화 |  클라이언트 활성화 지원 |
| 클라우드 회선  |  V1 회선 |   V2 회선  |

### TRTC V1(iLiveSDK)을 어떻게 V2(LiteAVSDK)로 업그레이드 하나요?
- 사용자의 **프로젝트가 TRTC SDK를 통합한 적이 없는 경우**, 통화 품질, 회선 사양, 액세스 난도 및 기능 확장에 장점이 있는 V2(LiteAVSDK)를 사용하는 것을 강력히 권장합니다.
- 사용자의 **프로젝트가 문제 없이 안정적인 경우**, V1과 V2의 클라우드 회선은 현재 통신이 되지 않으므로 사용자의 프로젝트가 이미 안정적인 운영 단계에 진입했다면 즉시 업그레이드하지 않아도 됩니다.
- 사용자의 **프로젝트가 구버전 V1과 연결된 경우**, V2 버전으로 직접 연결하는 것을 권장합니다. V2 버전의 API 인터페이스는 최신 설계를 도입하여 연결 시간이 구버전에 비해 훨씬 짧습니다.
- 사용자가 **이미 구버전 V1을 사용 중이며 통화 품질을 향상하려는 경우**, V1과 V2의 클라우드 회선은 현재 통신이 되지 않으므로 최신 버전 SDK로 업그레이드하려면 'SDK 통합', '모두 펼치기', '클라우드 전환'의 과정을 거쳐야 합니다. 대략적인 순서는 다음과 같습니다.
 1. 현재 프로젝트 중 최신 버전 SDK를 통합하여 테스트를 통과합니다.
 2. 방 리스트에 SDK 버전 넘버 필드를 추가하면 App에서 서버의 필드에 따라 V1 버전과 V2 버전 중 사용할 버전을 선택합니다.
 3. 최신 버전 App을 배포하고 버전이 사용자 그룹을 커버하길 기다립니다.
 4. 방 리스트의 SDK 버전 넘버 필드를 V1에서 V2로 전환하여 회선 전환을 완료합니다.


### Android의 LiteAVSDK와 iLiveSDK는 어떻게 동시에 호환 통합되나요?

iLiveSDK와 LiteAVSDK 모두 TRAE를 사용해 메아리 제거와 노이즈 감소 등 음성 처리를 진행했습니다. LiteAVSDK에서 사용한 TRAE 버전은 업데이트되면서 iLiveSDK에서 사용한 모든 기능 인터페이스를 포함했으므로 사용자는 설정 항목에서 LiteAVSDK의 TRAE 라이브러리를 사용하면 됩니다.
aar 방식을 사용해서 프로그램을 통합합니다. 서브 프로젝트(app 디렉터리)의 build.gradle을 수정하고, android{} 노드에서 다음과 같이 설정하십시오.
>!참조 테이블 추가 시 LiteAVSDK는 반드시 iLiveSDK 앞에 있어야 합니다.

```java
android{
//1. gradle에서 packagingoptions 설정
packagingOptions {
pickFirst 'lib/armeabi-v7a/libTRAECodec.so'
pickFirst 'lib/armeabi-v7a/libstlport_shared.so'
pickFirst 'lib/armeabi/libTRAECodec.so'
pickFirst 'lib/armeabi/libstlport_shared.so'
}
//2. dempendencies 가져오기
implementation(name:'LiteAVSDK_TRTC_6.4.7108', ext:'aar')  // 주의사항: TRTC는 반드시 iLiveSDK 앞에 있어야 함
implementation 'com.tencent.ilivesdk:ilivesdk:1.9.4.6.4'
}
```

### iOS의 LiteAVSDK + iLiveSDK + BeautySDK는 어떻게 동시에 호환 통합되나요?
TRTC V1 버전에서 BeautySDK를 사용하여 뷰티 필터 및 동적 효과 등의 기능을 구현했습니다. TRTC V2 버전에서는 사용자의 편리한 사용을 위해 BeautySDK의 기능을 LiteAVSDK에 탑재했습니다. 이미 iLiveSDK를 통합하고 사용자의 프로그램에 BeautySDK를 탑재한 경우, 파일 충돌이 일어날 수 있으며 해결 방법은 다음과 같습니다.

| 버전                                   | 처리 방법                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| BeautySDK 기본 버전(P 이미지 없는 버전) | Xcode 프로그램에 BeautySDK의 헤더 파일 검색 경로를 설정하고, BeautySDK 링크를 취소해야 합니다. |
| BeautySDK 고급 버전(P 이미지 있는 버전)    | LiteAVSDK 엔터프라이즈 버전을 사용하여 Xcode 프로그램에 BeautySDK 헤더 파일 검색 경로를 설정하고, BeautySDK 링크를 취소해야 합니다. LiteAVSDK 엔터프라이즈 버전에 P 이미지 모듈이 있기 때문에 다시 요금을 지불할 필요 없이 이전에 구매한 P 이미지 licence를 사용하면 됩니다. |

### Windows의 LiteAVSDK와 iLiveSDK는 어떻게 동시에 호환 통합되나요?

Windows의 LiteAVSDK와 iLiveSDK 모두 TRAE를 사용해 메아리 제거와 노이즈 감소 등 음성 처리를 진행했습니다. 그러나 LiteAVSDK에서 사용한 TRAE 버전이 업데이트되었고 기능 사용에 차이가 있으므로 직접 변경할 수는 없으며, 다음의 방법으로 처리할 수 있습니다.

#### 프로그램 구조

프로그램에 다음과 같은 구조 적용을 권장합니다.

	|
	|- 주요 프로그램.exe
	|- 주요 프로그램.exe가 종속된 다른 파일
	|- iLiveSDK.dll
	|- iLiveSDK.dll이 종속된 다른 파일
	|- LiteAV
	|        |- liteav.dll
	|        |- liteav.dll이 종속된 다른 파일

#### 초기화 방법

iLiveSDK는 .lib 링크를 직접 사용할 수 있으며, 다음과 같은 코드를 사용한 동적 로딩도 가능합니다.
```cpp
HMODULE hiLive = LoadLibrary("iLiveSDK.dll");
```

LiteAVSDK를 사용해야 하는 경우, 다음 코드로 로딩 및 초기화를 진행합니다.

<dx-codeblock>
::: cpp cpp
typedef ITRTCCloud* (*getTRTCShareInstanceMtd)();
typedef void(*destroyTRTCShareInstanceMtd)();

TCHAR dllPath[MAX_PATH];
GetModuleFileName(nullptr, dllPath, MAX_PATH);
PathRemoveFileSpec(dllPath);
wcscat(dllPath, L"\\LiteAV\\");
SetDllDirectory(dllPath);
HMODULE hLiteAV = LoadLibrary(L"liteav.dll");
if (!hLiteAV) {
printf("liteav.dll 로딩 실패: %d", GetLastError());
return;
}

getTRTCShareInstanceMtd pGetTRTCShareInstance = (getTRTCShareInstanceMtd)GetProcAddress(hLiteAV, "getTRTCShareInstance");
if (!pGetTRTCShareInstance) {
printf("getTRTCShareInstance 함수 로딩 실패");
return;
}

destroyTRTCShareInstanceMtd pDestroyTRTCShareInstance = (destroyTRTCShareInstanceMtd)GetProcAddress(hLiteAV, "destroyTRTCShareInstance");
if (!pDestroyTRTCShareInstance) {
printf("destroyTRTCShareInstance 함수 로딩 실패");
return;
}

ITRTCCloud *pTrtcCloud = m_pGetTRTCShareInstance();
if (!pTrtcCloud) {
printf("TRTC 인스턴스 생성 실패");
return;
}
SetDllDirectory(nullptr);

pTrtcCloud->enterRoom(...);
:::
</dx-codeblock>



