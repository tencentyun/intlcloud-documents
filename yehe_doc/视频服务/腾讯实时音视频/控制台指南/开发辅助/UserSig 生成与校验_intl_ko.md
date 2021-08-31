TRTC 콘솔에서는 UserSig 서명 온라인 생성을 지원합니다. 그러나 해당 UserSig는 개발 단계에서의 신속한 테스트를 위해서만 사용할 수 있으며, 암호화 키가 노출되어 트래픽을 도용 당하지 않도록 정식 런칭 전 UserSig 계산 로직을 [백그라운드 서버에 마이그레이션](https://intl.cloud.tencent.com/document/product/647/35166)하십시오.


[](id:generate)
## 서명(UserSig) 생성 툴
개발자와 Tencent Cloud 서비스는 서명(UserSig) 인증을 통해 신뢰 관계를 구축합니다.

1. TRTC 콘솔에서 왼쪽 [Development Assistance]>[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)을 선택하여 [Signature (UserSig) Generator] 모듈을 확인합니다.
2. 드롭다운 목록을 클릭하여 생성한 애플리케이션(SDKAppID)을 선택하면 자동으로 해당 키(Key)가 생성됩니다.
3. 사용자 이름(UserID)을 입력합니다.
4. [Generate Signature(UserSig)]을 클릭하면 해당하는 UserSig 서명이 생성됩니다.


[](id:check)
## 서명(UserSig) 인증 툴
해당 툴은 사용하는 서명(UserSig)의 유효성을 인증합니다.

>! 해당 툴을 사용하는 경우 인증 요청 시 입력하는 SDKAppID, UserID는 UserSig의 SDKAppID, UserID와 동일해야 합니다.

1. TRTC 콘솔에서 왼쪽 [Development Assistance]>[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)을 선택하여 [Signature (UserSig) Generator] 모듈을 확인합니다.
2. 인증할 어플리케이션(SDKAppID)을 선택하면 자동으로 해당하는 키(Key)가 생성됩니다.
3. 사용자 이름(UserID)을 입력합니다.
4. 인증할 서명(UserSig)을 복사해 [서명(UserSig)]에 붙여넣은 후, [Verify Now]를 클릭합니다.
>? [Signature (UserSig) Generator] 모듈에서 UserSig를 생성한 경우 [Copy Signature(UserSig)]를 클릭하여 복사하는 것을 권장합니다.
>
5. 인증 완료 후, 하단에서 인증 결과를 확인할 수 있습니다.
	- 인증 성공 예시:
	- 인증 실패 예시:


## 관련 문서
UserSig과 관련된 추가 문의사항은 [UserSig 관련 FAQ](https://intl.cloud.tencent.com/document/product/647/35166)를 참조하십시오.
