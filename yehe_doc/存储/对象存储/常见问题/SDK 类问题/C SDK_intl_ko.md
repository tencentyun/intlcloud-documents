### C SDK 사용 시 어떻게 중단 후 업로드를 재개하나요?

[C SDK 고급 업로드](https://intl.cloud.tencent.com/document/product/436/31518) 인터페이스를 사용해 중단 후 업로드 재개 기능을 구현할 수 있습니다. 중단 후 업로드 재개 시, 업로드 제어 매개변수를 **COS_TRUE**로 설정해야 합니다. 예시: `clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_TRUE, NULL)`.

