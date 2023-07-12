### JavaScript SDK를 사용한 멀티파트 업로드 시, 처음 업로드 완료 후 이어지는 요청은 모두 403입니다. 어떻게 처리해야 하나요?

요청에 403 오류 보고가 나타나는 경우, [COS 액세스 시 403 에러 코드 반환](https://intl.cloud.tencent.com/document/product/436/40105) 문서를 참조해 진단합니다. 임시 키를 사용한 멀티파트 업로드 시 [멀티파트 업로드 권한](https://intl.cloud.tencent.com/document/product/436/30580)이 부여되었는지, 권한 부여 경로가 정확한지 확인하는 것을 권장합니다.

### JavaScript SDK 업로드 속도가 최대 대역폭에 미치지 못합니다. 어떻게 처리해야 하나요?

멀티파트 업로드 인터페이스로 각 멀티파트의 크기를 늘려 해결할 수 있습니다. 예를 들어 현재 각 멀티파트의 크기가 1MB로 설정된 경우, 사용자는 멀티파트 크기를 5MB 또는 기타 크기로 적당히 바꿔보면서 대역폭 사용 상황을 모니터링할 수 있습니다. 자세한 내용은 [멀티파트 업로드 가이드](https://intl.cloud.tencent.com/document/product/436/31538)를 참조하십시오.

### JavaScript SDK에서 파일 업로드 진행률은 어떻게 획득하나요?

JavaScript SDK의 간편한 객체 업로드 인터페이스와 멀티파트 업로드 객체 인터페이스가 진행률을 반환합니다. 자세한 내용은 [객체 작업](https://intl.cloud.tencent.com/document/product/436/31538)을 참조하십시오.

### JavaScript SDK의 List Multipart Uploads에서 진행률을 직접 획득할 수 있나요?

현재 List Multipart Uploads 인터페이스는 콜백 함수로 반환해야 하며, 직접 획득할 수 없습니다.

