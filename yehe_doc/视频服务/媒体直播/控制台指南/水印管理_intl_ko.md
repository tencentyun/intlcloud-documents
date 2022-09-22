StreamLive의 비디오 출력에 정적 이미지나 텍스트를 추가할 수 있습니다. 워터마크 이미지는 PNG 또는 JPG 형식이어야 합니다.

## 워터마크 보기
왼쪽 사이드바에서 **Watermark Management**를 선택합니다. 이 페이지에서 추가된 워터마크를 미리 볼 수 있을 뿐만 아니라 이미지 크기 및 너비/높이와 같은 정보를 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0cd3973c8d34202dff84257a9ae3eddc.png)

## 워터마크 추가
워터마크를 추가하려면 **Watermark Management** 페이지에서 **Create Template**을 클릭하고 다음 설정을 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a919f169397bef249904ae88c3a08b23.png)
일반 설정:

- **Template Name**: 템플릿 이름은 최대 16자이며 숫자, 대소문자 및 언더바(_)를 포함할 수 있습니다.
- **Watermark Type**: 드롭다운 목록에서 Text Watermark 또는 Image Watermark를 선택합니다.
- **Origin**: 드롭다운 목록에서 Top Left, Bottom Left, Top Right 또는 Bottom Right 모서리를 Origin으로 사용할지 선택합니다.
- **Vertical Offset**: Origin을 기준으로 한 워터마크의 수직 오프셋입니다.
- **Horizontal Offset**: Origin을 기준으로 한 워터마크의 수평 오프셋입니다.

### 텍스트 워터마크 추가
- **Watermark Text**: 비디오에 추가할 텍스트입니다. 이것은 텍스트 워터마크를 추가하는 경우에 필요합니다.
- **Front Size**: 글꼴 크기입니다.
- **Coloer**: 글꼴 색입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/41770c54a01cb9b2eebeaf48c266a981.png)
**Confirm**을 클릭합니다.

### 이미지 워터마크 추가
- **Watermark Image**: 이미지 워터마크를 추가하는 경우 필요합니다. **Click to upload**하거나 업로드할 이미지 파일을 끌어다 놓습니다.
- **Watermark Size**: 이미지의 원래 크기에 대한 백분율로 나타낸 워터마크의 너비와 높이입니다. 비워 두거나 0으로 설정하면 원본 이미지 크기가 사용됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0bc5a62b8fbe88edca116802414ae9be.png)
**Confirm**을 클릭합니다.

## 워터마크 쿼리
워터마크 관리 페이지 우측 상단의 검색창에 워터마크 템플릿 이름 또는 워터마크 ID를 입력하여 워터마크를 검색하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/17bba7c53601f53fb2daa46d227146b5.png)

## 워터마크 편집
워터마크 관리 페이지에서 대상 워터마크를 찾고 **Operation** 열에서 **Edit**을 클릭하여 워터마크를 편집합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e9485a741dc02eb763022d34e111a2d3.png)

## 워터마크 삭제
워터마크 관리 페이지에서 대상 워터마크를 찾고 **Operation** 열에서 **Delete**를 클릭하여 워터마크를 삭제합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6770bdf42d44e9f2b01d4b880c4ebdca.png)
채널에 바인딩된 워터마크는 삭제할 수 없습니다. **Template Binding** 열은 워터마크가 바인딩된 채널의 수를 보여줍니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f5cbff44d5f19a16a721e7d9d5d49933.png)

## 채널에 워터마크 바인딩하기
워터마크 템플릿을 만든 후 채널에 바인딩할 수 있습니다. 채널 관리 페이지에서 타깃 채널을 찾아 편집을 클릭합니다. **Output Group Setting**에서 **Video Watermark**를 켜고 **Video Watermark Template**의 드롭다운 목록에서 생성된 워터마크 템플릿을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/00b231219d0e51cfb4004c018a64ff15.jpg)

>! 구성 변경 사항은 다음 라이브 스트리밍까지 적용되지 않습니다.




