## 현상 설명

- **현상1**: 동일한 링크에 액세스하지만 다른 파일에 액세스되는 경우
- **현상2**: 파일을 업데이트했는데 이전 파일로 액세스되는 경우

## 예상 원인

- Content Delivery Network(CDN) 캐시가 만료되지 않은 경우
- 브라우저에서 로컬 캐시 사용을 비활성화하지 않은 경우
- 액세스하는 파일이 하이재킹되어 액세스하는 리소스 콘텐츠와 설정된 콘텐츠가 일치하지 않는 경우

## 처리 순서

### CDN 캐시 만료 여부 확인

[사용자 액세스가 CDN 캐시에 히트되었는지 확인하는 방법은 무엇인가요?](https://intl.cloud.tencent.com/document/product/228/11207) 문서를 참조하여 CDN 캐시 만료 여부를 확인합니다.
 - 예. [브라우저에서 로컬 캐시 사용 비활성화 여부를 확인](#DisableCaching)하십시오.
 - 아니요. [캐시 퍼지](https://intl.cloud.tencent.com/document/product/228/6299) 문서를 참조하여 CDN URL 또는 CDN 디렉터리를 퍼지합니다.

<span id="DisableCaching"></span>
### 브라우저에서 로컬 캐시 사용 비활성화 여부 확인

>? Google 브라우저 작업 예시
>
1. Google 브라우저를 실행합니다.
2. **F12** 키를 눌러 디버깅 창을 엽니다.
3. [Network] 탭에서 [Disable cache]를 선택했는지 확인합니다.
![](https://main.qcloudimg.com/raw/453ea5fdaa0d69be6f13fd809a815d22.png)
 - 예. [액세스하는 파일이 하이재킹되었는지 확인](#UseHTTPS)하십시오.
 - 아니요. [Disable cache]를 선택하고 브라우저를 재시작합니다.

<span id="UseHTTPS"></span>
### 액세스하는 파일이 하이재킹되었는지 확인

액세스하는 리소스 콘텐츠가 설정과 일치하지 않는 경우(예: 파일의 content-length 불일치, 응답 header 불일치 등) 하이재킹된 것입니다. HTTPS 프로토콜을 사용하여 해당 파일에 액세스하는 것을 권장합니다.




