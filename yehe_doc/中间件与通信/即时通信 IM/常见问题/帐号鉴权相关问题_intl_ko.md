>### JNI 방식으로 APl를 사용할 때 다음과 같은 문제가 발생하면 어떻게 해야 합니까?
>
>```
>Exception in thread “main” java.lang.UnsatisfiedLinkError:
>com.tls.tls_sigcheck.tls_gen_signature_ex2(Ljava/lang/String;Ljava/lang/String;Ljava/lang/String;)I
>        at com.tls.tls_sigcheck.tls_gen_signature_ex2(Native Method)
>        at Demo.main(Demo.java:31)
>```
>
>동적 라이브러리 경로의 잘못된 요소를 배제한 후, 코드의 package 경로가 올바른지 확인합니다. API 이름은 JNI 동적 라이브러리 컴파일 중 package 경로를 통해 생성됩니다. 따라서 tls_sigcheck.java에서 package 경로를 수정하여 컴파일하지 마십시오. 그렇지 않으면 위와 같은 문제가 발생합니다.
>
>### JNI 방식으로 APl를 사용할 때 다음과 같은 문제가 발생하면 어떻게 해야 합니까?
>
>```
>Exception in thread “main” java.lang.UnsatisfiedLinkError: *** Can't load IA 32-bit *** on a AMD 64-bit platform
>```
>
>이는 전형적인 JVM과 동적 라이브러리 간의 불일치를 나타냅니다. 이를 수정하려면 32비트 동적 라이브러리를 사용하여 32비트 JVM을 로딩하십시오.
>
>
>### UserSig는 어떻게 생성합니까?
>자세한 내용은 [UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.
>
>### UserSig의 유효 기간은 어떻게 됩니까?
>
>IM 로그인 인증을 위한 중요한 자격 증명인 UserSig의 기본 유효 기간은 180일이며 기본 API를 통해서만 수정할 수 있습니다. 다른 API 및 도구는 유효 기간을 수정할 수 없습니다. UserSig의 유효 기간은 최대 50년까지 설정할 수 있습니다. 계정 보안을 위해 유효 기간을 2개월로 설정할 것을 권장합니다. 자세한 내용은 [UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.
>
>### 계정은 삭제할 수 있습니까?
>
>- **프로 버전**의 계정은 삭제할 수 없습니다. 계정을 비활성화하려면 [v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957) API를 호출하여 계정 소유자의 로그인 상태를 무효화할 수 있습니다.
>- **체험판**의 계정은 삭제할 수 있습니다. [v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955) API를 호출하여 더 이상 필요하지 않은 계정을 삭제할 수 있습니다. **계정 삭제 후에는 사용자 데이터를 복구할 수 없습니다.**
>
>### 로그인 시 오류 코드 70009가 발생하는 이유는 무엇입니까?
>공개키와 개인키가 일치하는지 확인하십시오. IM Demo의 개인 키를 사용하여 UserSig를 생성하지 마십시오.
>
>### IM 계정을 가져오지 않았을 때 다음과 같은 문제가 발생하면 어떻게 해야 하나요?
>- **오류 코드 10019가 발생하는 경우**
>요청의 UserID가 존재하지 않습니다. MemberList의 각 Member_Account가 올바른지 확인하십시오.
>- **오류 10007가 발생하는 경우**
>작업 권한이 없습니다. (예: Public 그룹의 일반 구성원이 그룹에서 구성원을 제거하려고 시도하지만 권한은 App 관리자에게만 있음)
>- **오류 20003가 발생하는 경우**
>메시지 수신자 또는 발신자의 User ID가 잘못되었거나 존재하지 않습니다. UserID를 IM 콘솔로 가져왔는지 확인하십시오.
>
>>?계정을 생성하고 API 호출을 통해 계정을 IM으로 가져와야 합니다. 계정은 가져오기 후에만 사용할 수 있습니다.
