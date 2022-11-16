**라이브 스트림 퍼블리싱 License**, **UGSV License** 및 **비디오 재생 License** 3가지 유형의 미디어 SDK(RT-Cube) License를 제공합니다. . 과금 세부 정보는 [가격 개요](https://www.tencentcloud.com/document/product/647/50553)를 참고하십시오. License를 구매한 후 [TRTC 콘솔](https://console.tencentcloud.com/trtc), [CSS 콘솔](https://console.tencentcloud.com/live/license) 또는 [VOD 콘솔](https://console.tencentcloud.com/vod/license)에서 바인딩하여 새로운 기능을 활성화하거나 기존 기능의 유효 기간을 연장할 수 있습니다. 각 License가 활성화할 수 있는 기능은 다음과 같습니다.

| License | 기능            |
| -------------------- | ----------------------- |
| 라이브 스트림 퍼블리싱 License     | 라이브 스트림 퍼블리싱 + 비디오 재생 |
| UGSV License       | UGSV(라이트/스탠다드) + 비디오 재생 |
| 비디오 재생 License | 비디오 재생 |

>! v10.1부터 라이브 스트림 퍼블리싱 License와 UGSV License도 비디오 재생 기능을 활성화할 수 있습니다. 즉, 이제 라이브 스트림 퍼블리싱 License 또는 UGSV License로 Player SDK의 비디오 재생 기능을 사용할 수 있습니다.

**본문은 라이브 스트림 퍼블리싱 License를 예시로** 평가판 또는 공식 License를 사용하여 기능을 활성화하는 방법과 기존 기능의 유효 기간을 연장하는 방법을 안내합니다.

[](id:test)
## 평가판 License

[](id:creat_test)
### 평가판 License 신청

라이브 스트리밍 기능에 대한 평가판 License(28일 동안 유효)를 무료로 신청할 수 있습니다.


>? 평가판 라이선스를 '2022-10-01 11:34:55'에 신청하면 28일 후인 '2022-10-28 00:00:00'에 만료됩니다.


콘솔에서 **새 애플리케이션에 대한 평가판 License를 생성**하거나 **기존 애플리케이션에 대한 평가판에 대한 새 기능을 활성화**할 수 있습니다.
<dx-tabs>
::: 옵션1: 새로운 평가판 License 생성
1. [TRTC 콘솔](https://console.tencentcloud.com/trtc), [CSS 콘솔](https://console.tencentcloud.com/live/license) 또는 [VOD 콘솔](https://console.tencentcloud.com/vod/license)에 로그인한 후 **평가판 License 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4507bd038c2a6e43cf91205383a1904f.png)
2. `App Name`, `Package Name`, `Bundle ID`를 입력하고 **라이브 스트리밍**(라이브 스트림 퍼블리싱 + 비디오 재생)을 선택한 후 **생성**을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/af9ee37d5d25af0dc63221ff13cac3d6.png" style="zoom:67%;" />
1. 평가판 License가 성공적으로 생성되면 **SDK를 초기화할 때 전달해야 하는 License URL과 Key가 표시됩니다. 정보 사본을 저장하십시오.**
![](https://qcloudimg.tencent-cloud.cn/raw/67b33614792136bb295b3f47a024291f.png)
:::
::: 옵션2: 기존 평가판 애플리케이션에 새로운 기능 활성화
기존 애플리케이션에 대해 **라이브 스트림 퍼블리싱**(라이브 스트림 퍼블리싱 + 비디오 재생)을 활성화하려면 아래 단계를 따르십시오.
1. 대상 평가판 애플리케이션을 선택하고 **새 기능 테스트**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/026830658f7815b3d43432a501f2327a.png)
2. **라이브 스트림 퍼블리싱**(라이브 스트림 퍼블리싱 + 비디오 재생)을 선택하고 **확인**을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/80d4dffff43aa6e299088d4a1b06db72.png" style="zoom:67%;" />
:::
</dx-tabs>

>? 
>- **편집**을 클릭하여 평가판 License에 바인딩된 Bundle ID 및 Package Name을 수정할 수 있습니다. 수정 후 **확인**을 클릭합니다.
>- 아직 바인딩할 Package Name 또는 Bundle Id가 없으면 ‘-’를 입력할 수 있습니다.
>- 평가판 License는 28일 동안 유효합니다. **각 기능에 대해 하나의 평가판 라이선스만 신청할 수 있습니다**. 평가판 라이선스가 만료된 후에도 기능을 계속 사용하려면 [공식 License](#formal)를 구매하십시오.

[](id:up_test)
### 공식 License로 업그레이드
평가판 License에서 공식 License(1년 동안 유효)로 업그레이드하려면 아래 단계를 따르십시오.
1. 기존 평가판 License를 선택하고 라이브 스트리밍 섹션에서 **업그레이드**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6daf850b30a29014ab8cbd0f1a3f500f.png)
2. **바인딩**을 클릭하고 구매한 CSS 트래픽 패키지 또는 라이브 스트림 퍼블리싱 License를 선택한 후 **확인**을 클릭합니다. 바인딩할 License 리소스가 없다면 [구매 페이지](https://buy.tencentcloud.com/license)로 이동하여 리소스를 구매하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/087fb89a73fa9cffd80e0da4840783f6.png" alt="image" style="zoom: 50%;" /><img src="https://qcloudimg.tencent-cloud.cn/raw/1ff7b009cbce37598521d43df2cdae61.png" style="zoom:50%;" />

[](id:formal)
## 공식 License
[](id:creat_formal)
### 공식 License 구매
1. 구매 방법:
    - [라이브 스트림 퍼블리싱 License](https://www.tencentcloud.com/document/product/647/50553)을 단독 [**구매**](https://buy.tencentcloud.com/license)하여 얻은 라이선스는 애플리케이션에 바인딩한 후 1년 동안 유효합니다(1년 후의 익일 00:00:00에 만료됨).
2. License를 바인딩합니다. **License를 새 애플리케이션에 바인딩**하거나 **이를 사용하여 기존 애플리케이션에 License를 활성화**할 수 있습니다.
<dx-tabs>
::: 옵션1: 애플리케이션 생성 및 프로덕션 License 바인딩
1. [TRTC 콘솔](https://console.tencentcloud.com/trtc), [CSS 콘솔](https://console.tencentcloud.com/live/license) 또는 [VOD 콘솔](https://console.tencentcloud.com/vod/license)로 이동하여 **공식 License 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c7689b0f319f616a5e5e3ecf47267b65.png)
2. `App Name`, `Package Name`, `Bundle ID`를 입력하고 **라이브 스트리밍**(라이브 스트림 퍼블리싱 + 비디오 재생)을 선택한 후 **다음**을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0ba8765431755c7807787782a157297.png" style="zoom:67%;" />
3. **바인딩**을 클릭하고 구매한 CSS 트래픽 패키지 또는 라이브 스트림 퍼블리싱 License를 선택한 후 **확인**을 클릭합니다. 바인딩할 License 리소스가 없다면 [구매 페이지](https://buy.tencentcloud.com/license)로 이동하여 리소스를 구매하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ddb304e3d9e35959c0ba93a4138189a.png" style="zoom:50%;" />

>? **확인**을 클릭하기 전에 Bundle ID와 Package Name을 다시 확인하고 앱 스토어에 제출한 것과 동일한지 확인하십시오. **제출 후에는 정보를 수정할 수 없습니다.**

4. 공식 License가 성공적으로 생성되면 SDK 초기화 시 전달해야 하는 License URL과 Key가 표시됩니다. 정보 사본을 저장하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/11fcae56bf1fcad8641ba789bdaaa517.png)
:::
::: 옵션2: 기존 애플리케이션에 대한 기능 활성화
1. **라이브 스트림 퍼블리싱** 기능(라이브 스트림 퍼블리싱 + 비디오 재생)을 추가할 기존 공식 라이선스를 선택하고 **추가 기능 활성화**를 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e1ab736ce2f80e74214dbca9a47f10fd.png" style="zoom:67%;" />
2. **라이브 스트림 퍼블리싱**(라이브 스트림 퍼블리싱 + 비디오 재생)을 선택하고 **다음**을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/1ff7b009cbce37598521d43df2cdae61.png" style="zoom: 67%;" />
3. **바인딩**을 클릭하고 구매한 CSS 트래픽 패키지 또는 라이브 스트림 퍼블리싱 License를 선택한 후 **확인**을 클릭합니다. 바인딩할 License 리소스가 없다면 [구매 페이지](https://buy.tencentcloud.com/license)로 이동하여 리소스를 구매하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/095e35fc6947c3399ca30d66d019b2f5.png" style="zoom:67%;" />
:::
</dx-tabs>

[](id:update_formal)
### 공식 License 기능 유효 기간 연장
[TRTC 콘솔](https://console.tencentcloud.com/trtc), [CSS 콘솔](https://console.tencentcloud.com/live/license) 또는 [VOD 콘솔](https://console.tencentcloud.com/vod/license)에서 바인딩된 License의 유효 기간을 확인할 수 있습니다. [메시지 구독](https://console.cloud.tencent.com/message/subscription)의 미디어 SDK에서 알림(**메시지 센터 메시지**/**이메일**/**SMS**/**WeChat**/**WeCom**)을 구독할 수도 있습니다. License 만료 30일, 15일, 7일 및 1일 전에 알림을 보내드립니다. 업무 중단을 방지하려면 적시에 기능의 유효 기간을 연장하십시오. License가 만료된 경우 아래 단계에 따라 해당 기능의 유효 기간을 연장할 수 있습니다.
1. 대상 License를 선택하고 라이브 스트리밍 섹션에서 **유효 기간 업데이트**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/534f5d02cb72a6950ad5d37fb3666c70.png)
2. **바인딩**을 클릭하고 **바인딩 되지 않은** CSS 트래픽 패키지 또는 라이브 스트림 퍼블리싱 License를 선택한 후 **확인**을 클릭합니다. 바인딩할 License 리소스가 없다면 [구매 페이지](https://buy.tencentcloud.com/license)로 이동하여 리소스를 구매하십시오.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6b1f279e5cd439386147c4f4aa96d852.png" style="zoom:50%;" />
3. 갱신된 유효 기간을 확인합니다.

>! **공식 License 정보는 수정할 수 없습니다**. 구매한 License 리소스를 새 애플리케이션에 사용하려면 **공식 License 생성**을 클릭하여 새 애플리케이션에 바인딩합니다.