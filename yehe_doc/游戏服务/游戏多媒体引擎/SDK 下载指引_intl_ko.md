본문에서는 Tencent Cloud Game Multimedia Engine(GME)용 SDK를 다운로드하는 방법을 설명합니다.

## 릴리스 기록
SDK를 다운로드하기 전에 [릴리스 노트](https://intl.cloud.tencent.com/document/product/607/35323)를 먼저 확인하십시오.

## 시작하기

SDK를 처음 사용하는 경우 [사용자 튜토리얼](https://intl.cloud.tencent.com/document/product/607/39696)을 참고하십시오.

## Sample Project 가이드

### Sample Project 사용

다운로드한 SDK 또는 Sample Project 사용 중 문제가 발생하면 [Sample Project 사용 문제](https://www.tencentcloud.com/document/product/607/39521)를 참고하거나 [온라인 문의](https://intl.cloud.tencent.com/contact-sales)를 통하여 도움을 받으십시오.

> ?다운로드한 Sample Project를 컴파일하고 실행하려면 관련 문자열을 신청한 SDKAppid 및 Key로 바꿔야 합니다. 예를 들어 Unity Demo를 사용하려면 코드 파일 **UserConfig.cs**를 수정해야 합니다. 서비스 신청에 대한 자세한 내용은 [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.

### Sample Project 디버깅

Sample Project를 사용하여 디버깅을 진행할 때 다음 문서를 참고하십시오.

- 방 입장 실패 문제는 [방 입장 실패](https://intl.cloud.tencent.com/document/product/607/39523)를 참고하십시오.
- 소리가 나오지 않는 문제는 [사운드 및 오디오](https://intl.cloud.tencent.com/document/product/607/39524)를 참고하십시오.
- 서비스 호출 오류는 [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223)를 참고하십시오.
- 문제가 지속되면 로그를 받은 후 [문의하기](https://intl.cloud.tencent.com/document/product/607/49702)를 통해 GME 개발자에게 문의할 수 있습니다.



### Sample Project 내보내기

Sample Project를 실행 파일로 내보낼 때 발생하는 문제는 [프로그램 내보내기](https://intl.cloud.tencent.com/document/product/607/39522)를 참고하십시오.



## 버전 업데이트

v2.9.6은 다음과 같이 업데이트됩니다.

<table >
<thead>
<tr>
<th width="18%">업데이트 명칭</th>
<th width="44%">업데이트 설명</th>
 <th width="14%">배포일</th>  
<th width="24%">관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>SDK v2.9.6 출시</td>
<td ><ul style="margin:0;">
<li >음성 채팅에 대한 역할 설정 기능을 추가하여 클랜전, SLG 게임에 대한 지원을 늘렸습니다.</li>
<li >두 개의 반주 스트림을 동시에 재생할 수 있습니다.</li>
<li >온라인 MP3 파일을 반주로 사용할 때 반주 진행 설정을 지원했습니다.</li>
<li >언어 감지 결과는 텍스트 번역 기능에서 반환될 수 있습니다.</li>
<li >음성-텍스트 변환 API에 번역 기능이 추가되었습니다.</li>
<li >VR 시나리오에 더 잘 적응할 수 있도록 로컬 3D 위치를 입력하기 위한 API를 추가했습니다.</li>
<li >다른 게이머 음성의 3D 음향 효과를 제거하는 데 사용되는 3D 음성 블록리스트용 API를 추가했습니다.</li>
<li >3D 음성 기능을 최적화하여 SDK에 내장된 3D 오디오 모델을 사용하면 개발자가 모델 경로를 전달하기 위해 API를 호출할 필요가 없습니다.</li>
<li >GME SDK는 Unity WebGL, xbox gamecore 및 UnrealEngine5를 지원합니다.</li>
<li >GME SDK는 최신 버전의 Playstation 5와 호환됩니다.</li>
<li >Mac용 GME SDK는 M1 Arm64를 지원합니다.</li>
<li >GME SDK는 Android 12의 블루투스 권한과 호환됩니다.</li>
<li >Android 5.1의 호환성 문제를 수정했습니다.</li>
<li >반복되는 음성 메시지로 인해 발생하는 메모리 문제를 수정했습니다.</li>
<li >SDK의 메모리 사용량이 줄어듭니다.</li>
<li >방 입장 시간을 단축하기 위해 하드웨어 장치의 실행 시간을 최적화했습니다.</li>
</ul ></td>
<td>2023-01-18</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218">3D 음향 효과</td>
</tr>
</tbody></table>



<dx-alert infotype="notice" title="업데이트 주의">
-  v2.9.6으로 업그레이드하려면 [SDK Version Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/32363)를 참고하십시오.
</dx-alert>



## SDK 다운로드

| OS/엔진  |   버전          | 업데이트 시간   | SDK 다운로드| Sample Project 다운로드| 문서|
| ----------------- | ---------- | ---------- | ---------------------------- | ---------------------------- | -------------------------------- |
| Unity   | v2.9.6    | 2023-01-18 | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unity_Audio_SDK_2.9.6.09d06620.zip) | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unity_Audio_Demo_2.9.6.09d06620.zip) | [Unity SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44544) |
| Unreal Engine 4.x | v2.9.6 | 2023-01-18 | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal422_Audio_SDK_2.9.6.09d06620.zip) | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal422_Audio_Demo_2.9.6.09d06620.zip) | [Unreal SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44545) |
| Unreal Engine 5.x | v2.9.6 |  2023-01-18 | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal5_Audio_SDK_2.9.6.97b107ed.zip) | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Unreal5_Audio_Demo_2.9.6.97b107ed.zip) | [Unreal SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44545) |
| Cocos2D      |v2.9.6       |  2023-01-18 | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Cocos_Audio_SDK_2.9.6.09d06620.zip) | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Other/GME_Cocos_Audio_Demo_2.9.6.09d06620.zip) | [Getting Started](https://intl.cloud.tencent.com/document/product/607/18292) |
| Windows      | v2.9.6       | 2023-01-18 | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Windows/GME_Windows_audio_sdk_2.9.6.92a797e4.zip) | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Windows/GME_Windows_audio_example_project_2.9.6.92a797e4.zip) | [Native SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/40858) |
| iOS        | v2.9.6         | 2023-01-18 | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/iOS/GME_ios_audio_sdk_2.9.6.92a797e4.zip) | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/iOS/GME_ios_audio_example_2.9.6.92a797e4.zip) | [Native SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/40858) |
| Android    | v2.9.6        | 2023-01-18 | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Android/GME_android_audio_sdk_2.9.6.92a797e4.zip) | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Android/GME_android_audio_example_2.9.6.92a797e4.zip) | [Native SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/40858) |
| macOS     | v2.9.6          | 2023-01-18 | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Mac/GME_mac_audio_sdk_2.9.6.92a797e4.zip) | [다운로드](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.6.intl/Mac/GME_mac_audio_demo_2.9.6.92a797e4.zip) | [Native SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/40858) |
| Web      | -          | 2022-06-20 | [다운로드](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.1/H5/GME_Web_SDK_2.8.1.47.zip) | [다운로드](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.8.1/H5/GME_Web_Demo_2.8.1.47.zip) | [API Documentation](https://intl.cloud.tencent.com/document/product/607/30263) |





> ?
> - GME SDK는 **게임 콘솔**(PlayStation, Xbox 및 Nintendo Switch) 또한 지원합니다. 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하십시오.
> - 모든 플랫폼의 SDK 컴파일 툴 체인은 [Toolchain](https://intl.cloud.tencent.com/document/product/607/46711)을 참고하십시오.
> - 현재 ITMG_ROOM_TYPE_FLUENCY 음질 유형만 기본적으로 제공됩니다. 다른 음질 유형을 사용하려면 [티켓 제출](https://www.tencentcloud.com/document/product/607/18521#:~:text=%E6%97%A5%E5%BF%97%E5%90%8E%EF%BC%8C%E9%80%9A%E8%BF%87-,%E6%8F%90%E4%BA%A4%E5%B7%A5%E5%8D%95,-%E8%81%94%E7%B3%BB%20GME%20%E5%BC%80%E5%8F%91)하십시오.



