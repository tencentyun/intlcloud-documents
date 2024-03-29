StreamLive는 채널에 워터마크 추가 기능을 제공하며 StreamLive 콘솔의 Watermark Management 페이지에서 텍스트 또는 워터마크 템플릿을 추가할 수 있습니다. 생성된 템플릿은 채널 관리 페이지에서 설정할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2be49fa4bd0ee5ec87a5dbb2f1281c3b.jpg)


### 워터마크 템플릿 생성

[Watermark Management] 메뉴를 선택하고 [Create Watermark Template]을 클릭하면 워터마크 템플릿이 생성됩니다.



#### Ⅰ. 텍스트 형식의 워터마크 템플릿 생성

시스템은 기본적으로 텍스트 유형의 워터마크 템플릿을 선택합니다. 드롭다운 목록 Watermark Type에서 이미지 유형의 워터마크 템플릿을 선택할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/d7bc227e5d28378e849ce2a544be957e.jpg)

텍스트 템플릿을 생성하려면 워터마크 템플릿 이름(Template Name)을 입력하고 표시할 워터마크의 워터마크 콘텐츠(Watermark Text)를 입력해야 합니다. 워터마크 템플릿은 글꼴 크기(25 - 50px)와 워터마크 색상 설정 기능을 제공합니다.

워터마크 위치를 설정할 수 있는 경우 먼저 워터마크의 초기 위치를 정하고 수직 오프셋(Vertical Offset)과 수평 오프셋(Horizontal Offset)을 통해 위치를 세부 조정합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/f05a8121f13d086a2073077188bcbed7.jpg)



#### Ⅱ. 이미지 유형 워터마크 템플릿 생성

이미지 템플릿을 생성하려면 워터마크 템플릿 이름(Template Name)을 입력하고 표시할 워터마크 이미지를 업로드해야 합니다. 워터마크 템플릿은 글꼴 크기(25 - 50px)와 워터마크 색상 설정 기능을 제공합니다.

시스템은 워터마크 이미지의 크기, 높이/너비 비율 설정을 요청하며, 해당 비율에 따라 이미지가 화면에 나타나게 됩니다. 기존 워터마크의 종횡비를 유지하려면 높이 또는 너비 중 하나만 조정합니다. 이 경우 같은 비율로 확대/축소됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ad8955e56c150811433b4045e488af5e.jpg)

예시:
- 너비가 50%이고 높이가 25%인 경우 워터마크는 전체 화면 너비의 절반으로 늘어나고 높이는 전체 화면 높이의 1/4로 확대/축소됩니다.
- 너비가 50%이고 높이가 0%인 경우 워터마크가 전체 화면 너비의 절반으로 늘어나며, 높이는 워터마크 이미지의 기존 종횡비에 따라 변경됩니다.



### 채널에 워터마크 템플릿 바인딩

워터마크 템플릿을 생성한 후 채널 관리 페이지에서 지정된 채널에 워터마크 템플릿을 바인딩할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/81b30d06e27aa8ab19ec3433356a82bd.jpg)

설정 방법: 워터마크를 설정할 채널을 선택하고, Output Group Setting에서 워터마크 스위치를 활성화한 후, 생성된 워터마크 템플릿을 선택합니다.
>!  설정 변경 사항은 다음 라이브 방송부터 적용됩니다.




### 워터마크 템플릿 관리

워터마크 템플릿 관리 페이지에서 언제든지 워터마크 템플릿을 추가, 수정 또는 삭제할 수 있습니다.

워터마크 템플릿 제거 시 모든 채널에서 해당 템플릿의 바인딩 해제 여부를 확인해야 합니다. Template Binding에서 현재 워터마크 템플릿에 바인딩된 채널을 볼 수 있으며, 바인딩 개수가 0일 때만 워터마크 템플릿을 삭제할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/291d919592bb7c66ef63015bd154c851.jpg)



