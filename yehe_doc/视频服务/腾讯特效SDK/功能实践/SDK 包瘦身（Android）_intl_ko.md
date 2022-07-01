패키지의 크기를 줄이려면 온라인에서 SDK에 필요한 assets 리소스, so 라이브러리 그리고 애니메이션 효과 리소스 MotionRes(일부 기본 SDK에서는 사용할 수 없음)를 다운로드할 수 있습니다. 다운로드 성공 후 SDK에서 위 파일의 경로를 설정합니다.

Demo의 다운로드 로직을 재사용하는 것이 좋습니다. 기존 다운로드 서비스를 사용할 수도 있습니다.

Demo 다운로드 로직을 재사용하는 경우 체크포인트 재시작 기능은 Demo에서 기본적으로 활성화되어 있어 다운로드가 중단된 경우 나중에 다시 시작할 수 있습니다. 이 기능을 사용하려면 다운로드 서버가 체크포인트 재시작 기능을 지원하는지 확인하십시오. 

**확인 방법**

```java
Web 서버가 Range 요청을 지원하는지 확인하십시오. Range 요청이 지원되는 경우 서버는 체크포인트 재시작을 지원합니다. 명령줄에서 다음 curl 명령을 실행합니다.
curl -i --range 0-9 https://귀하의 서버 주소/다운로드할 파일 이름
예시:
curl -i --range 0-9 https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.119/xmagic_S1-04_android_2.4.1.119.zip
반환된 콘텐츠에 Content-Range 필드가 포함된 경우 서버는 체크포인트 재시작을 지원합니다.
```

[](id:so)
## so 라이브러리 동적 다운로드
so 라이브러리 패키지는 ` jniLibs/arm64-v8a` 및 `jniLibs/armeabi-v7a`에 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/785d9f1a64b556343ea8959f14fec646.png)


<dx-tabs>
:::  Demo에서 다운로드 서비스를 재사용하려면
1. 두 ZIP 패키지의 MD5 값을 계산합니다. Mac에서 그렇게 하려면 터미널에서 `md5 파일 경로/파일 이름'을 직접 실행하거나 해당 도구를 사용하십시오.
2. 패키지를 서버에 업로드하고 다운로드 URL을 가져옵니다.
3. Demo 프로젝트의 ResDownloadConfig에서 다음 상수 값을 업데이트합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2c6e6b4e36eca9a7b17181f567efe01c.png)
4. `ResDownloadUtil.checkOrDownloadFiles`를 호출하여 다운로드를 시작합니다.
:::
::: 자체 다운로드 서비스를 이용하려면
1. 패키지를 다운로드 및 압축 해제하고 SDK에서 경로를 설정합니다. 예를 들어 패키지를 압축 해제한 후 `so path = /data/data/com.tencent.pitumotionDemo.effects/files/xmagic_libs`로 설정합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c4ee096758d599be54310d740c5026d4.png" width=400px>
>! so 라이브러리를 외부 저장 장치가 아닌 App의 개인 디렉터리에 다운로드하여 so가 실수로 삭제되는 것을 방지하는 것이 좋습니다. 또한 빠른 다운로드를 위해 사용자 휴대폰의 CPU 아키텍처를 기반으로 하는 v8a 또는 v7a의 so 라이브러리를 다운로드하는 것이 좋습니다. Demo 프로젝트의 LaunchActivity를 참고하십시오.
2. 다음 코드를 호출하여 so 라이브러리를 로딩하고 Licence를 인증합니다.
```java
XmagicApi.setLibPathAndLoad(path);
auth();
```
:::
</dx-tabs>

>! 
>- SDK 버전이 업데이트되면 해당 so 라이브러리도 변경될 수 있으며, so 라이브러리를 다시 다운로드해야 합니다. Demo의 방법을 참고하여 MD5 값을 검증하는 것을 권장합니다.
>- so 라이브러리를 직접 다운로드하든 Demo에서 다운로드 서비스를 재사용하든 상관없이 SDK의 auth API를 호출하기 전에 다운로드되었는지 확인하십시오. ResDownloadUtil은 다음과 같은 확인 방법을 제공합니다. 다운로드한 경우 아래와 같이 SDK에서 경로를 설정합니다.
```java
String validLibsDirectory = ResDownloadUtil.getValidLibsDirectory(LaunchActivity.this,

isCpuV8a() ? ResDownloadConfig.DOWNLOAD_MD5_LIBS_V8A : ResDownloadConfig.DOWNLOAD_MD5_LIBS_V7A);
if (validLibsDirectory == null) {
     Toast.makeText(LaunchActivity.this,"libs는 다운로드되지 않습니다. 먼저 다운로드하십시오",Toast.LENGTH_LONG).show();
     return;
}
XmagicApi.setLibPathAndLoad(validLibsDirectory);
auth();
```


## assets 리소스 동적 다운로드
다음과 같이 assets 리소스를 동적으로 다운로드할 수 있습니다.

1. 로컬 프로젝트의 assets에서 다음을 구성합니다.
     - **2.4.0 이상**: 로컬 assets 디렉터리에 파일을 보관할 필요가 없습니다.
     - **2.4.0 이전 버전**: License 파일과 4개의 JSON 구성 파일인 `brand_name.json`, `device_config.json`, `phone_info.json`, `score_phone.json`을 유지해야 합니다.
2. SDK에서 `download_assets.zip` 패키지를 찾습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b04e8d991a4aef086229a8610ad8f883.png)
3. [so 파일](#so)에 대해 위에서 설명한 것과 같은 방법으로 ZIP 패키지의 MD5 값을 계산한 다음 서버에 패키지를 업로드하여 다운로드 주소를 가져옵니다.
<dx-tabs>
::: Demo에서 다운로드 서비스를 재사용하려면
1. 다음 그림에서 다운로드 주소와 MD5 값을 업데이트합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a59277a9a3a9d5c000b103fce7ea2885.png)
2. `ResDownloadUtil.checkOrDownloadFiles`를 호출하여 다운로드를 시작하고 `ResDownloadUtil.getValidAssetsDirectory`를 호출하여 다운로드한 assets의 path를 가져옵니다. 자세한 안내는 `LaunchActivity.java`를 참고하십시오.
:::
::: 자체 다운로드 서비스를 이용하려면
상기 ZIP 패키지를 다운로드 및 압축 해제한 후 파일 구조를 다음과 같이 재구성해야 합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8ad5eeb526671bea433967c91aa377bc.png" width=400px>
여기서 light_assets, light_material과 같이 빨간 박스 안의 이름은 임의로 변경할 수 없습니다. 구조를 구성하려면 ResDownloadUtil의 organizeAssetsDirectory 메소드를 직접 재사용하는 것이 좋습니다.
:::
</dx-tabs>

>! 
>- SDK 버전이 업데이트되면 해당 assets도 변경될 수 있으며, 호환성을 위해 assets을 다시 다운로드해야 합니다. Demo의 방법을 참고하여 MD5 값을 검증하는 것을 권장합니다.
>- assets을 직접 다운로드하거나 Demo에서 다운로드 서비스를 재사용하는지 여부에 관계없이 비디오를 캡처하기 전에 assets이 다운로드되었는지 확인하십시오. ResDownloadUtil은 다음과 같은 확인 방법을 제공합니다. 다운로드한 경우 SDK에서 경로를 설정합니다. 자세한 안내는 `LaunchActivity.java`를 참고하십시오.
```java
String validAssetsDirectory = ResDownloadUtil.getValidAssetsDirectory(LaunchActivity.this,ResDownloadConfig.DOWNLOAD_MD5_ASSETS);
if (validAssetsDirectory == null) {
      Toast.makeText(LaunchActivity.this,"assets이 다운로드되지 않았습니다. 먼저 다운로드하십시오",Toast.LENGTH_LONG).show();
      return;
}
XmagicResParser.setResPath(validAssetsDirectory);
startActivity(intent);
```

## 애니메이션 효과 리소스 MotionRes 다운로드
일부 기본 버전에는 애니메이션 효과 리소스가 없습니다. 실제 상황에 따라 이 섹션을 건너뛸 수 있습니다.

애니메이션 효과는 6가지 유형으로 나뉘며 각 유형에는 애니메이션 효과가 포함된 여러 ZIP 패키지가 있습니다. 파일 내용은 구입한 에디션에 따라 다릅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e289586793242d7a9b363b42cacb0f38.png)
애니메이션 효과 리소스는 필요에 따라 다운로드할 수 있습니다. 예를 들어 사용자가 관련 기능 페이지에 들어간 후 또는 애니메이션 효과의 아이콘을 클릭한 후 다운로드를 시작할 수 있습니다.

이러한 ZIP 패키지를 서버에 업로드하고 각 ZIP 패키지의 다운로드 주소를 가져와야 합니다.
>!**다운로드한 애니메이션 효과 리소스의 MotionRes 디렉터리는 이전 섹션에서 설명한 light_assets 및 light_material과 동일한 수준에 있어야 합니다**. 또한 각 애니메이션 효과는 추출해야 하며 동일한 ZIP 패키지에 넣을 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/96876dfb2d76901b4e20a3847b0be280.png) 

MotionRes를 다운로드하려면 ResDownloadUtil.checkOrDownloadMotions 메소드를 참고하십시오. 이러한 리소스를 하나씩 다운로드하는 것이 좋습니다.

**Demo에서 다운로드 서비스를 재사용하려면 ResDownloadConfig의 MOTION_RES_DOWNLOAD_PREFIX 상수 값을 다운로드 URL 접두사로 바꾸십시오.**