본문은 Unity 개발자를 위해 Tencent Cloud Game Multimedia Engine(GME) API용 Unity 실시간 음성 채팅 HD 음질 방의 사용 방법을 안내합니다.

## 전제 조건

GME SDK v2.9부터 GME Unity SDK는 기본적으로 실시간 음성 채팅 HD 음질 방의 사용을 지원하지 않습니다. 버전 2.9 이상이 아닌 경우 다음 작업이 필요하지 않습니다.

## 관련된 기능

조정하지 않으면 Unity SDK에서 다음 기능이 누락됩니다.

실시간 음성 채팅 HD 음질 방은 [음질](https://intl.cloud.tencent.com/document/product/607/18522)을 참고하십시오.
반주 기능 재생은 [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504)을 참고하십시오.
실시간 음성 변조 및 음성 메시지 음성 변조 기능은 [실시간 음성 효과](https://intl.cloud.tencent.com/document/product/607/31503)를 참고하십시오.

## SDK 업데이트

### 다운로드 링크

[다운로드 가이드](https://intl.cloud.tencent.com/document/product/607/18521)를 통해 Unity SDK의 표준 버전을 다운로드한 경우 다른 라이브러리 파일을 다운로드해야 하므로 티켓을 제출하거나 [문의하기](https://intl.cloud.tencent.com/contact-sales)을 통해 Tencent Cloud 직원에게 문의하십시오.

### 라이브러리 파일 교체

기존 GME 라이브러리 파일을 삭제하고 다운로드한 라이브러리 파일을 사용하십시오. 추가된 라이브러리 파일의 예시는 아래 이미지와 같습니다.

![](https://write-document-release-1258344699.cos-internal.ap-guangzhou.tencentcos.cn/100022348635/381764c1a91e11ed9e14525400088f3a.png?q-sign-algorithm=sha1&q-ak=AKIDN6qb1L53Nhiq33ZJMVD92KUQFqA6DU8R4TO5oUTHuofQc3lesTi3gHalRJdThQ67&q-sign-time=1677046269;1677049869&q-key-time=1677046269;1677049869&q-header-list=&q-url-param-list=&q-signature=9ed29d0b57091c652ad6d2adb641c76e0342c90a&x-cos-security-token=QcdgxUzvwKDlGrTz03GrDg7qrpgsHS0a3a7e7cc62b57075d84b23551f57120aefg2RQVrX4jNxEze67BjnFx_O5mJtp6mBxi0FRHmqiSedLjqAkERWjsz1ol9oBJ3zRZ8lnDMddpq0ccK79BLgiV8vAhtfS1CwUjswI_L1M9KdOrdyRgs_M3sUILdPFpT7qOaY9I90d6OMBAjmC5R8lGeY6AUP9GZ9LUANeay6b7H-yVzvjg71vPRLBZhOAP9Dz8sZqvg137_p3-wmLOsQEEFlGz9pgCg_9vvK9HYfYRgDqLEY6ZKdTkNVSC1WFUAnVIvUU9jyO_-Dfz-Q7urwHgpQbcDwf87TgXntHS4xT4X3RusvqYYmzWPHdl0rTlr153EyoaxkprnXxSV4hCmlcXfBmTstlko5A19ET_Zn-juXBZJWUc3X9-hseBQT3076)

### 라이브러리 파일의 해당 기능

자신의 필요에 따라 해당 라이브러리 파일만 가져올 수 있습니다. 예를 들어 음성 변조 기능만 필요한 경우 libgme_soundtouch만 가져오면 됩니다.
<table>
<tr>
<td rowspan="1" colSpan="1" >라이브러리 파일</td>
<td rowspan="1" colSpan="1" >해당 기능</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >libgme_fdkaac</td>
<td rowspan="1" colSpan="1" >1. 표준, HD 음질 방 입장 시 사용 2. acc 형식의 반주 파일 재생 시 사용</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >libgme_faad2</td>
<td rowspan="1" colSpan="1" >mp4 형식의 반주 파일 재생 시 사용</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >libgme_ogg</td>
<td rowspan="1" colSpan="1" >ogg 형식의 반주 파일 재생 시 사용</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >libgme_lamemp3</td>
<td rowspan="1" colSpan="1" >mp3 형식의 반주 파일 재생 시 사용</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >libgme_soundtouch</td>
<td rowspan="1" colSpan="1" >음성 및 피치 변경에 사용</td>
</tr>
</table>


## 내보내기 구성

필요한 라이브러리 파일을 구성한 후 내보내기 시 iOS 플랫폼 패키지 동적 라이브러리를 구성해야 하며 다른 플랫폼은 기본적으로 내보내기 할 수 있습니다.

### Unity 2019 이상

#### 구성 원리

Editor OnPostprocessBuild 스크립트를 생성하고 UnityEditor.iOS.Xcode.Extensions.PBXProjectExtensions.AddFileToEmbedFrameworks를 사용하면 이 API가 자동으로 동적 라이브러리를 최종 패키지 번들의 프레임워크 디렉터리에 복사하고 서명합니다.

#### 예시 코드

Demo 프로젝트의 add_dylib.cs 스크립트 파일을 참고하여 자신의 프로젝트 요구 사항에 따라 이 부분의 코드를 프로젝트의 Editor 폴더 아래에 넣을 수 있습니다.
``` c#
    [UnityEditor.Callbacks.PostProcessBuild(1002)]
    public  static void OnPostprocessBuild (UnityEditor.BuildTarget BuildTarget, string path){  
        if (BuildTarget == UnityEditor.BuildTarget.iOS) {
            UnityEngine.Debug.Log ("OnPostprocessBuild add_dylib:" + path);
#if UNITY_EDITOR_OSX || UNITY_STANDALONE_OSX
            {
                string projPath = UnityEditor.iOS.Xcode.PBXProject.GetPBXProjectPath (path);  
                UnityEditor.iOS.Xcode.PBXProject proj = new UnityEditor.iOS.Xcode.PBXProject ();  

                proj.ReadFromString (System.IO.File.ReadAllText (projPath));  
                // string targetGuid = proj.TargetGuidByName (UnityEditor.iOS.Xcode.PBXProject.GetUnityTargetName ()); // 2018
                string targetGuid = proj.GetUnityMainTargetGuid();	// 2019

                // 가져오기한 framework에 따라 삭제
                string[] framework_names = {
                    "libgme_fdkaac.framework",
                    "libgme_lamemp3.framework",
                    "libgme_ogg.framework",
                    "libgme_soundtouch.framework"
                };

                for (int i = 0; i < framework_names.Length; i++)
                {
                    string framework_name = framework_names[i];
                    string dylibGuid = null;
                    dylibGuid = proj.FindFileGuidByProjectPath("Frameworks/Plugins/iOS/" + framework_name);

                    if (dylibGuid == null) {
                        UnityEngine.Debug.LogWarning (framework_name + " guid not found");
                    } else  {
                        UnityEngine.Debug.LogWarning (framework_name + " guid:" + dylibGuid);
                        // proj.AddDynamicFramework (targetGuid, dylibGuid);
                        UnityEditor.iOS.Xcode.Extensions.PBXProjectExtensions.AddFileToEmbedFrameworks(proj, targetGuid, dylibGuid);

                        proj.AddBuildProperty(targetGuid, "LD_RUNPATH_SEARCH_PATHS", "@executable_path/Frameworks");
                        System.IO.File.WriteAllText (projPath, proj.WriteToString ());
                    }
                }
            }
#endif
        }
    }
```

### Unity 2019보다 낮은 버전

현재 Unity 2019 이상 버전에서만 UnityEditor.iOS.Xcode.Extensions를 사용할 수 있으며, Unity 이전 버전인 경우 Unity 상위 버전에서 하위 버전 Unity로 UnityEditor.iOS.Xcode 패키지를 내보내거나 [UnityEditorAV.iOS.XCode.zip](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.0/Other/UnityEditorAV.iOS.XCode.zip) 첨부 파일을 직접 참고하여 이 파일의 압축을 풀어 프로젝트 디렉터리의 Editor 폴더 아래에 넣습니다.

![](https://write-document-release-1258344699.cos-internal.ap-guangzhou.tencentcos.cn/100022348635/383311cda91e11ed9e14525400088f3a.png?q-sign-algorithm=sha1&q-ak=AKIDifFDt6RJzclvQ8NcPZTV5fjwrONY8Cno2bA6f8WuxESnhu61K5IDNlfUJFTeNaLt&q-sign-time=1677046269;1677049869&q-key-time=1677046269;1677049869&q-header-list=&q-url-param-list=&q-signature=3d4bbe46177884791b0584a4d4edcd7f71bef7cc&x-cos-security-token=ywFiZBiXaTn63GMKHdwvBZH6h4tfPSba1b2d77d24bb9b33b37d2b3a491fb2b14-oUSsr3rmwYinKtv9tnvWruLQ2RuwoUqK7r05xErnISmqAZxo9rqMct-nPu1NZNTkvEpk2DLtgFYtkn9hsw80z7tXBqGR0vFqj_ycw0Zoo7uYFyX04mt-jSJK9qkUpSlCPcaZWQU-qDe25NPpF7nBz1ogNbiV4phwMM_yZCTt42760GDFyiuqlzx2sxju9WMtYsAtn4pJlTkdEw92XhPMRaxTA2nm6vRoFk2zfcejdf1vlpNexpYDbRUZWVgyksbbSm3iGhlzCe5Mdr3gDp79X1GI8wedZmwMomojPGyx5JzZcArRhQ2bg674Hnp9bNn6Aq6Xsc2KB6zgTurcex_Wip-EHfO5SxoaKyh2LvPEhg1Y7qdfAFIBKZVVZMD4Urr)