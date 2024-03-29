## 작업 시나리오
본 문서는 리소스의 태그 편집 작업을 안내합니다.

## 사용 제한

태그를 편집할 때 다음의 제한 조건을 유의하십시오.
- 수량 제한: 각 클라우드 리소스마다 허용되는 최대 태그 수량은 50입니다.
- 태그 키 제한:
  - ‘qcloud’, ‘tencent’, ‘project’로 시작하는 시스템 예약 태그 키는 생성을 금지합니다.
  - ‘숫자’, ‘알파벳’, ‘+=.@-’만 사용 가능하며, 태그 키의 최대 길이는 255자로 제한합니다.
- 태그 값 제한: ‘공백 문자 혹은 숫자’, ‘알파벳’, ‘+=.@-’만 사용 가능하며, 태그 값의 최대 길이는 127자로 제한합니다.


## 전제 조건
[CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인되어 있어야 합니다.

## 작업 단계

<dx-tabs>
::: 단일 인스턴스의 태그 편집

1. 인스턴스의 관리 페이지의 실제 뷰 모드에 따라 작업합니다.
   - **리스트 뷰**: 아래 이미지와 같이 태그를 편집할 인스턴스를 선택하고 **더보기** > **인스턴스 설정** > **태그 편집**을 선택합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7f5ff3c9a726569805f3d085ffd8f8dd.png)
   - **탭 뷰**: 아래 이미지와 같이 태그 편집할 인스턴스를 선택하고 오른쪽 상단의 **더보기** > **인스턴스 설정** > **태그 편집**을 선택합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e558f115b9e41be9afd18c7649c9a823.png)
2. 팝업된 "1개의 클라우드 리소스를 선택하셨습니다." 창에서 실제 필요에 따라, 태그를 추가, 수정 또는 삭제합니다.
:::
::: 여러 인스턴스의 태그 편집


<dx-alert infotype="explain" title="">
최대 20개의 리소스에 대한 태그 일괄 편집을 지원합니다.
</dx-alert>


1. 아래 이미지와 같이 인스턴스 관리 페이지에서 태그를 편집할 인스턴스를 모두 선택하고 상단의 **더보기** > **태그 편집**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d07d2ab7830b9f4431bd23826892938c.png)
2. 팝업된 "n개의 클라우드 리소스를 선택하셨습니다." 창에서 실제 필요에 따라, 태그를 추가, 수정 또는 삭제하십시오.
:::
</dx-tabs>

## 작업 사례

태그 사용 방법과 관련된 내용은 [태그를 사용해 인스턴스 관리](https://intl.cloud.tencent.com/document/product/213/19548)를 참조하십시오.

