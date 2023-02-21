본문은 Unity 개발자를 위해 Tencent Cloud Game Multimedia Engine(GME) API용 Unity 프로젝트를 구성하는 방법을 안내합니다.


## SDK 다운로드

1. 해당 Demo 및 SDK를 다운로드하십시오. 자세한 내용은 [SDK 다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)를 참고하십시오.
2. 페이지에서 Unity용 SDK 리소스를 찾습니다.
3. **다운로드**를 클릭합니다. 압축 해제 후 다운로드한 SDK 리소스에는 다음 파일이 포함됩니다.
<table>
<thead>
<tr>
<th>파일 이름</th>
<th align="center">설명</th>
<th>용도</th>
</tr>
</thead>
<tbody><tr>
<td>Plugins</td>
<td align="center">SDK 라이브러리 파일</td>
<td>플랫폼별 라이브러리 파일 저장</td>
</tr>
<tr>
<td>GMESDK</td>
<td align="center">SDK 코드 파일</td>
<td>API 제공</td>
</tr>
</tbody></table>
4. HD 음질을 사용하려면 [Using HD Sound Quality](https://intl.cloud.tencent.com/document/product/607/46016)를 참고하십시오.

<dx-alert infotype="explain" title="지원되는 플랫폼">
Unity용 SDK는 Windows, Mac, Android, iOS, PlayStation, Xbox, Switch 및 WebGL 플랫폼 아키텍처를 동시에 통합했습니다.
</dx-alert>



## 프로젝트 구성

### 1단계: Plugins 파일 가져오기

아래와 같이 SDK의 Plugins 폴더에서 **Unity 프로젝트**>**Assets**>**Plugins** 아래의 폴더로 파일을 복사합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/ce8ba3561d43148971f1cbe9076be3a3.png"  width="65%" /></img>



<dx-alert infotype="explain" title="">
win32 아키텍처에서 실행 파일을 내보낼 필요가 없으면 Plugins 폴더 아래의 x86 폴더를 삭제하십시오.
</dx-alert>




### 2단계: 코드 파일 가져오기

아래와 같이 SDK의 Scripts 폴더에 있는 파일을 Unity 프로젝트의 코드를 저장하는 데 사용되는 폴더에 복사합니다.  
<img src="https://qcloudimg.tencent-cloud.cn/raw/5ab4509590a5effa9e8aadeee2456492.png"  width="65%" /></img>



## Unity 2021 구성
Unity Editor 2021 이상을 사용하는 경우 Plugins > Android > Opensdk.plugin 아래의 lib 폴더를 잘라내기 하고 Opensdk.plugin과 동일한 수준의 프로젝트의 Plugins 파일의 Android 디렉터리에 붙여넣어야 합니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/bc7156db71faf994654c824787bfb1a9.png"  width="65%" /></img>


## 오디오 설정

Unity 편집기에서 **Edit**>**Project Setting**>**Audio**로 이동하고 기본 시스템 설정을 사용합니다. 설정을 변경하면 아래와 같이 iOS 장치에 설정된 하드웨어 버퍼로 인해 Unity 재생 사운드 효과가 영향을 받습니다.
<img src="https://main.qcloudimg.com/raw/db8975fcaefa3dc71732ede1b5f979db.png"  width="50%" /></img>


<dx-alert infotype="forbid" title="Unity Audio Setting">
Project Setting에서 Audio 모듈을 설정하지 마십시오.
</dx-alert>

설정이 다음과 같으면 iOS 장치에 설정된 하드웨어 버퍼로 인해 Unity 재생 사운드 효과가 중단됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6eb910221b8a24289dcffe0a39d60573.png)

## MacOS에서의 작업

Unity를 사용하여 MacOS 10.15.x에서 GME SDK를 통합하는 경우 `com.apple.quarantine` 속성으로 인해 실행 중에 파일이 손상되었다는 오류가 표시됩니다.

가장 직접적인 해결책은 아래와 같이 `com.apple.quarantine` 속성을 삭제하는 것입니다.
1. 터미널에서 cd 명령을 실행하여 프로젝트의 `Unity_OpenSDK_Audio/Assets/Plugins/` 폴더로 이동합니다.
2. 다음 명령을 실행합니다.
```
$ xattr -d com.apple.quarantine gmesdk.bundle
```



<dx-alert infotype="explain" title="">
이 작업은 리스크가 있습니다. 액세스하려면 이전 버전의 MacOS를 사용하는 것이 좋습니다.
</dx-alert>


