## 현상

- **현상1**: 동일한 링크에 액세스하였는데 다른 파일에 연결됩니다.
- **현상2**: 파일을 업데이트했는데 이전 파일로 연결됩니다.

## 가능한 원인

- Content Delivery Network(CDN) 캐시가 만료되지 않았습니다.
- 브라우저에서 로컬 캐시 사용을 비활성화하지 않았습니다.
- 액세스하는 파일이 하이재킹되어 액세스하는 리소스 콘텐츠와 설정된 콘텐츠가 일치하지 않습니다.

## 처리 단계

### CDN 캐시 만료 여부 확인

[CDN 캐시 설정](https://intl.cloud.tencent.com/document/product/228/11203) FAQ를 참고하여 CDN 캐시 만료 여부를 확인합니다.
 - 만료된 경우, [브라우저에서 로컬 캐시 사용 비활성화 여부를 확인](#DisableCaching)하십시오.
 - 만료되지 않은 경우, [캐시 퍼지](https://intl.cloud.tencent.com/document/product/228/6299) 문서를 참조하여 CDN URL 또는 CDN 디렉터리를 퍼지하십시오.

<span id="DisableCaching"></span>
### 브라우저에서 로컬 캐시 사용 비활성화 여부 확인

>? 다음은 Google 브라우저 작업 예시입니다.
>
1. Google 브라우저를 실행합니다.
2. **F12** 키를 눌러 디버깅 창을 엽니다.
3. **Network** 탭에서 **Disable cache**가 선택되었는지 확인합니다.
![](https://main.qcloudimg.com/raw/453ea5fdaa0d69be6f13fd809a815d22.png)
 - 선택된 경우, [액세스하는 파일이 하이재킹되었는지 확인](#UseHTTPS)하십시오.
 - 선택되지 않은 경우, **Disable cache**를 선택하고 브라우저를 재시작 하십시오.

<span id="UseHTTPS"></span>
### 액세스하는 파일이 하이재킹되었는지 확인

액세스하는 리소스 콘텐츠가 설정과 일치하지 않는 경우(예: 파일의 content-length 불일치, 응답 header 불일치 등) 하이재킹된 것입니다. HTTPS 프로토콜을 사용하여 해당 파일에 액세스할 것을 권장합니다.


