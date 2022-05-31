### COS에 내부 네트워크 도메인이 있나요?

COS의 기본 원본 서버 도메인 포맷은 &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com이며, 기본적으로 공용 네트워크 액세스 및 리전 내 내부 네트워크 액세스를 지원합니다. 내부 네트워크 환경에서 해당 도메인을 통한 COS 액세스 시, COS는 내부 IP에 스마트하게 리졸브됩니다. 이 때 발생하는 트래픽은 모두 내부 네트워크 트래픽으로 트래픽 요금이 부과되지 않습니다.
예시: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com. 도메인에 대한 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.



