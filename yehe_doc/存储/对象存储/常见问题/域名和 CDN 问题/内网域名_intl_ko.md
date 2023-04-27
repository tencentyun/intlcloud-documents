### COS에는 사설망 도메인이 있습니까?

Cloud Object Storage(COS)의 기본 오리진 도메인 이름은: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com 형식입니다. 기본적으로 공중망 및 리전 내 사설망 액세스가 지원됩니다(예시: `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`). 도메인 이름에 대한 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.

이 도메인을 사용하여 사설망을 통해 COS에 액세스할 수 있습니다. COS는 사설망 IP로 지능적으로 확인됩니다.

이 경우 다음이 생성됩니다.
- 사설망 트래픽: 사설망 업스트림 트래픽과 다운스트림 트래픽 모두 무료입니다. 자세한 내용은 [트래픽 요금](https://intl.cloud.tencent.com/document/product/436/33776)을 참고하십시오.
- 요청: 읽기 요청 및 쓰기 요청의 총 수는 요청 명령이 전송된 횟수에 따라 매일 계산되며, 최소 단위는 1만 회입니다. 자세한 내용은 [읽기/쓰기 요청 비용](https://intl.cloud.tencent.com/document/product/436/40100)을 참고하십시오.







