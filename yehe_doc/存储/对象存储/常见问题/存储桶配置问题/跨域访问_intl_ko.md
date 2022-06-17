### 크로스 도메인 액세스란 무엇인가요? 어떻게 설정하나요?

크로스 도메인 액세스는 HTTP 요청을 통해 도메인에서 다른 도메인의 리소스를 요청하는 것을 의미합니다. 프로토콜, 도메인, 포트 중 하나라도 다른 경우 다른 도메인으로 인식합니다. 콘솔 작업 방법은 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/13318) 또는 [크로스 도메인 액세스](https://intl.cloud.tencent.com/document/product/436/11488) 모범 사례 문서를 참고하십시오.

### 크로스 도메인 액세스 설정 후 얼로우리스트에 헤더가 있는 데도 COS 액세스가 거부됩니다. 어떻게 해야 하나요?

액세스가 거부되는 예상 원인은 다음과 같습니다.
1. 설정이 헤더와 동일한지, 보이지 않는 문자(예: 공백)가 있는지 확인합니다.
2. 전송한 요청의 도메인 정보를 확인합니다. CDN 가속 도메인으로 액세스하는 경우 CDN 콘솔에서 크로스 도메인을 설정해야 합니다. 자세한 내용은 [사용자 정의 응답 헤더 설정](https://intl.cloud.tencent.com/document/product/228/35320)을 참고하십시오.
3. 버킷 권한 상태를 확인하고 액세스가 버킷 권한에 부합하는지 확인합니다.
4. 브라우저 캐시 상태를 확인합니다. 브라우저 캐시로 인해 오류가 발생할 수 있으며, Ctrl+F5 키로 브라우저를 강제로 새로고침 하거나 브라우저 **Network** 탭에서 Disable cache를 선택하여 문제를 해결할 수 있습니다.


### 버킷의 파일 headers가 'Access-Control-Allow-Origin:*'을 반환하도록 설정하려면 어떻게 해야 하나요?

크로스 도메인을 설정하여 Origin을 `*`로 설정합니다. 자세한 내용은 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/11488) 모범 사례 문서를 참고하십시오.

### 업로드 시 "get ETag error, please add "ETag" to CORS ExposeHeader setting." 오류가 보고됩니다. 어떻게 처리해야 하나요?

다음 이미지에 따라 크로스 도메인 규칙을 설정하고 브라우저를 전환하여 실행되는지 확인합니다. 자세한 내용은 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/11488)을 참고하십시오.
![](https://main.qcloudimg.com/raw/e2cb8ce626ceaba0058423bb5eb72327.png)

### Tencent Cloud COS와 CDN 동시 사용 시 COS 크로스 도메인이 정상적으로 작동되지 않습니다. 어떻게 처리해야 하나요?

사용하는 도메인이 CDN 가속 도메인인 경우 CDN 콘솔에서 크로스 도메인을 설정합니다. 자세한 내용은 [HTTP 응답 헤더 설정](https://intl.cloud.tencent.com/document/product/228/35320) 문서를 참고하십시오.

### 크로스 도메인 설정에서 출처 Origin 퍼지 매칭을 지원하나요?

콘솔에서 하위 도메인의 퍼지 매칭을 지원합니다.

### COS 크로스 도메인 액세스 시 오류가 보고됩니다. 어떻게 처리해야 하나요?

다음 순서에 따라 확인하십시오.
1. COS 콘솔에 크로스 도메인 규칙이 설정되어 있는지 확인합니다. 자세한 작업 방법은 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/13318)을 참고하십시오.
2. CDN 가속 도메인을 사용 여부를 확인합니다. CDN 가속 도메인을 사용 중인 경우 CDN 측에서 크로스 도메인 규칙을 설정해야 합니다. [HTTP 응답 헤더 설정](https://intl.cloud.tencent.com/document/product/228/35320)을 참고하십시오.
3. 크로스 도메인이 설정되어 있다면 명령 라인을 사용해 규칙이 적용되고 있는지 확인합니다. 명령어 포맷: `curl -Lvo /dev/null "<객체 주소>" -H "origin:<도메인>"`. 비즈니스 상황에 따라 <> 안의 값을 변경합니다. 예: `curl -Lvo /dev/null "https://bucketname-1250000000.cos.ap-guangzhou.myqcloud.com/test.png" -H "origin:https://www.baidu.com"`. 상태 코드 200이 반환되는 경우 규칙이 적용되어 있는 상태로, 브라우저의 캐시를 삭제한 후 다시 시도하십시오.
4. 여전히 문제가 해결되지 않는다면 크로스 도메인 액세스 규칙을 max-age=0으로 설정해 보십시오.

### 크로스 도메인 액세스 CORS 규칙에 IP 주소를 추가할 수 있나요?
크로스 도메인 규칙은 IP 주소 형식을 지원합니다. 자세한 소개 내용은 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/13318) 문서를 참고하십시오.

### COS에 CDN을 설정한 후 CDN을 통해 COS의 파일에 액세스하면 크로스 도메인 오류가 보고됩니다. 어떻게 처리해야 하나요?

CDN을 사용해 COS에 액세스 시 크로스 도메인 오류가 보고된다면 [HTTP 응답 헤더 설정](https://intl.cloud.tencent.com/document/product/228/35320) 문서의 CDN 콘솔에서 크로스 도메인 허용하기를 참고하십시오.

### 파일 URL 액세스 시 크로스 도메인 액세스 오류가 보고됩니다. 어떻게 해결해야 하나요?

크로스 도메인을 설정했는지 확인합니다. 크로스 도메인을 정확하게 설정했다면 브라우저 캐시를 정리한 후 다시 시도해 보시기 바랍니다. 여전히 문제가 해결되지 않는다면 크로스 도메인 규칙을 max-age=0으로 설정해 보십시오. 크로스 도메인 액세스 설정 가이드는 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/13318)을 참고하십시오.
