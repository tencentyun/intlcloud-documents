본 문서에서는 VOD 기능을 빠르게 이해하고 사용할 수 있도록 Tencent Cloud RT-Cube Player(이하 Player라고 함)의 VOD 재생 시나리오와 관련된 기본 개념을 설명합니다.

[](id:basicConception)
## 기본 개념
Player는 Superplayer 또는 Superplayer Adapter를 통해 Tencent Cloud VOD에 연결할 수 있습니다.

### Superplayer
Superplayer는 비디오 암호화, 썸네일 미리보기 및 해상도 전환과 같은 모든 범위의 비디오 재생 기능을 갖춘 독립 실행형 완전한 비디오 플레이어입니다. 완전한 UI 및 Demo와 함께 제공되며 VOD와 긴밀하게 통합되며 FileId로 VOD의 리소스를 재생할 수 있습니다. 또한 Full Linkage VOD 재생 품질의 데이터 서비스를 제공합니다. Superplayer를 빠르게 연결하려면 [Superplayer Guide](https://intl.cloud.tencent.com/document/product/266/38098)를 참고하십시오.


### Superplayer Adapter
Superplayer Adapter는 타사 플레이어를 VOD의 리소스와 연결하는 데 사용되는 플레이어 플러그 인입니다. 비디오 재생 및 암호화를 포함한 다양한 기능을 제공하므로 타사 플레이어에 통합하여 FileId별로 VOD의 리소스를 재생할 수 있습니다. Superplayer Adapter를 빠르게 연결하려면 다양한 플랫폼에 대한 통합 문서를 참고하십시오.


[](id:choosePlayer)
## 플레이어 선택 방법
연결을 단순화하고 비즈니스 시나리오에 맞게 플레이어 서비스를 연결할 때 가장 적합한 플레이어 유형을 선택하는 것이 좋습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f793f98980f8f0adb38ee4292ed10d67.png)

- **Superplayer**: 플레이어를 통합하지 않았지만 VOD 재생 기능을 빠르게 구축해야 하는 사용자에게 적합합니다. Player는 모든 기능을 갖추고 있으며 쉽게 연결할 수 있습니다. VOD는 Superplayer를 통해 연결하는 방법에 대한 자세한 [Superplayer Guide](https://intl.cloud.tencent.com/document/product/266/38098)를 제공합니다.
- **Superplayer Adapter**: 독점 또는 타사 플레이어로 VOD 리소스를 재생해야 하는 사용자에게 적합합니다. VOD는 VOD의 리소스를 원활하게 연결하고 사용할 수 있도록 Superplayer Adapter를 제공합니다.

Player에서 지원하는 플랫폼은 다음과 같습니다.

| Player 유형     | Superplayer | Superplayer Adapter |
| --------- | ----- | ------------- |
| Web      | &#10003     | &#10003             |
| iOS      | &#10003     | &#10003             |
| Android | &#10003     | &#10003             |
| Flutter  | &#10003     | \-            |
| UI        | &#10003     | \-            |
| Demo      | &#10003     | \-            |


