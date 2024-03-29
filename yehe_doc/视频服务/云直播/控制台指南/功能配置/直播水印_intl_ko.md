CSS는 라이브 방송 화면에 워터마크 이미지를 겹쳐 영상 도용을 방지하는 워터마크 기능을 제공합니다. 본 문서에서는 콘솔을 통해 워터마크 템플릿을 생성, 바인딩, 바인딩 해제, 수정 및 삭제하는 방법에 대해 소개합니다.
**라이브 방송 워터마크 템플릿을 생성하는 방법으로는 다음 두 가지 방식이 있습니다**

- CSS 콘솔을 통한 워터마크 템플릿 생성에 대한 자세한 방법은 [워터마크 템플릿 생성](#Watermark)을 참조하십시오.
- API호출을 통해 워터마크를 생성하는 자세한 작업 방식은 [워터마크 추가](https://intl.cloud.tencent.com/document/product/267/30826)를 참조 바랍니다.


## 주의 사항
- 템플릿 생성이 완료되면 푸시 도메인에 연결할 수 있습니다. 연결 성공 후 약 5~10분 뒤에 적용됩니다.
- 콘솔의 워터마크 템플릿은 현재 도메인 차원에서 관리되며, 연결 인터페이스에서 생성된 규칙은 당분간 취소할 수 없습니다. 워터마크 관리 인터페이스를 통해 지정한 스트림과 연결하고 있는 경우, [워터마크 규칙 삭제](https://intl.cloud.tencent.com/document/product/267/30823)를 참조하여 연결을 해제해야 합니다.
- 템플릿 바인딩 및 수정, 바인딩 해제는 업데이트 이후의 라이브 방송 스트리밍에만 적용되며, 현재 라이브 방송 중인 스트리밍에는 적용되지 않습니다. 라이브 방송 중인 스트리밍을 중단하고 다시 시작해야만 새로운 규칙이 적용됩니다.


## 전제 조건

Tencent CSS 서비스를 활성화하고 [푸시 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가된 상태여야 합니다.

<span id="Watermark"></span>

## 워터마크 템플릿 생성

1.CSS 콘솔에 로그인하여 [기능 설정]>[[라이브 방송 워터마크]](https://console.cloud.tencent.com/live/config/watermark) 페이지로 이동합니다.
2. [워터마크 템플릿 생성]을 클릭하여 워터마크 템플릿 생성 페이지로 이동합니다.
3. 워터마크 이름을 입력합니다. 워터마크 이름은 중문, 영문, 숫자, _, - 만 지원되며, 30자를 초과할 수 없습니다.
4. [이미지 선택]을 클릭하여 워터마크 이미지를 업로드합니다.
>! 최적의 시각적 효과를 위해 워터마크는 투명 이미지 png 포맷을 사용하고, 이미지 크기는 2M 미만이어야 합니다.
5. 워터마크 이미지를 표시할 위치를 설정합니다. 위치는 다음 두 가지 방식으로 조절할 수 있습니다.
  - 워터마크 이미지 설정바에서 이미지 위치를 드래그합니다.
  - 설정 위치는 X축 방향과 Y축 방향을 나타냅니다.
6. [저장]을 클릭합니다.
![](https://main.qcloudimg.com/raw/aea9634d78972f2f72fd2c4c74d90f35.png)

<span id="conect"></span>
## 도메인 연결
1.CSS 콘솔에 로그인하여 [기능 설정]>[[라이브 방송 워터마크]](https://console.cloud.tencent.com/live/config/watermark) 페이지로 이동합니다.
2. 다음과 같은 방식을 통해 도메인 바인딩 창으로 이동합니다.
  - **도메인 직접 연결**: 왼쪽 상단에 있는 [도메인 바인딩]을 클릭합니다.
![](https://main.qcloudimg.com/raw/f28cd640fdd290b2c2ee60a1669860ac.png)
  -  **신규 워터마크 템플릿 생성 완료 후 도메인 연결**: [워터마크 템플릿 생성](#Watermark) 완료 후 안내창의 [도메인 바인딩]을 클릭합니다.
![](https://main.qcloudimg.com/raw/ea00262e98e51ebdf0d92d99d23c8a2d.png)
3. 도메인 바인딩 창에서 바인딩할 **워터마크 템플릿**과 **푸시 도메인**을 선택하고 [Confirm]을 클릭하면 바인딩이 완료됩니다.
![](https://main.qcloudimg.com/raw/e8197d5a79656a0692b0d5f9e84191da.png)
>? [추가]를 클릭하여 현재 템플릿에 여러 개의 푸시 도메인을 추가할 수 있습니다.

<span id="untie"></span>
## 바인딩 해제
1.CSS 콘솔에 로그인하여 [기능 설정]>[[라이브 방송 워터마크]](https://console.cloud.tencent.com/live/config/watermark) 페이지로 이동합니다.
2. 연결되어 있는 도메인의 워터마크 템플릿을 선택하고 [바인딩 해제]를 클릭합니다.
    ![](https://main.qcloudimg.com/raw/7c1b81f6df67607321355d654f3f9eec.png)
3. 현재 연결된 도메인의 바인딩 해제 여부를 확인하고 [확인]을 클릭하면 바인딩 해제가 완료됩니다.
    ![](https://main.qcloudimg.com/raw/3b845efa0aae58546955a2bd06841eca.png)

<span id="change"></span>
## 템플릿 수정

1. [기능 설정]>[[라이브 방송 워터마크]](https://console.cloud.tencent.com/live/config/watermark) 페이지로 이동합니다.
2. 생성된 워터마크 템플릿을 선택하고 오른쪽에 있는 [편집]을 클릭하면 템플릿 정보 수정 페이지로 이동합니다.
3. [저장]을 클릭합니다.

![](https://main.qcloudimg.com/raw/7a8c0d24f6d813244b4f4d1b5a333f87.png)

>? 화면에서 워터마크 템플릿 효과를 보려면 [미리보기]를 클릭합니다.

<span id="delete"></span>
## 템플릿 삭제
템플릿이 이미 연결되어 있는 경우 먼저 템플릿 바인딩 해제를 진행해야 삭제할 수 있습니다. 자세한 바인딩 해제 작업 방법은 [바인딩 해제](#untie)를 참조하십시오.
1. [기능 설정]>[[라이브 방송 워터마크]](https://console.cloud.tencent.com/live/config/watermark) 페이지로 이동합니다.
2. 생성된 워터마크 템플릿을 선택하고 상단에 있는 ![img](https://main.qcloudimg.com/raw/220ada95a4b631349543cc8cde96226e.png) 삭제 버튼을 클릭합니다.
3. 현재 워터마크 템플릿의 삭제 여부를 확인하고 [확인]을 클릭하면 삭제가 완료됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/7a405987e7494de1f4551b3e90d00408.png)

## 관련 작업
워터마크 템플릿에 대한 **도메인 차원의 바인딩** 및 **바인딩 해제**의 자세한 방법 및 관련 설명은 [워터마크 설정](https://intl.cloud.tencent.com/document/product/267/31064)을 참조하십시오.

