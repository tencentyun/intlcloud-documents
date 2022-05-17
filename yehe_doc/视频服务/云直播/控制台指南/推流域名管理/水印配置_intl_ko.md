라이브 방송 푸시 스트리밍은 기본적으로 워터마크 기능이 비활성화되어 있으며, 본 문서에서는 푸시 스트리밍 도메인을 워터마크 템플릿에 연결하여 워터마크 기능을 활성화하는 방법과 연결 완료 후 템플릿 바인딩을 해제해 워터마크 기능을 비활성화하는 방법을 소개합니다.
 
## 주의 사항
- 템플릿 설정을 완료하면 약 5~10분 후 적용됩니다.
- 템플릿 연결 완료 후 지정한 푸시 스트리밍 도메인의 푸시 스트리밍 주소에 워터마크 기능을 활성화할 수 있습니다.
- 도매인당 워터마크 템플릿은 1개만 연결할 수 있으며, 연결 후 해당 도메인의 모든 스트리밍은 해당 템플릿에 따라 워터마크가 추가됩니다.

## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 하며 [푸시 스트리밍 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가되어 있어야 합니다.
- [워터마크 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31073)이 완료되어 있어야 합니다.


## 워터마크 템플릿 연결
1.	[Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **푸시 스트리밍 도메인** 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. 	[Template Configuration] 탭을 선택해 [Watermark configuration] 부분 오른쪽 상단의 [Edit]를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c9a415b0848a1d22b6e236c0ab4771ba.png)
4.	설정할 워터마크 템플릿을 선택하고 [Save]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b597758441bcabcbb3f38d74e649b4da.png)
>? 작업 열의 [미리보기]를 클릭하여 워터마크 효과를 확인할 수 있습니다.

## 워터마크 템플릿 바인딩 해제
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **푸시 스트리밍 도메인** 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
2. [Template Configuration] 탭을 선택해 [Watermark configuration] 부분 오른쪽 상단의 [Edit]를 클릭합니다.
3. 해당 템플릿의 선택을 해제하고 [Save]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7a009d4780d4c91f0f06707abd9e22d9.png)
