3. ### TUIKit 소스 코드는 Androidx를 지원합니까?
   네. TUIKit 소스 코드는 Androidx를 지원합니다.

   ### 로그인 시 6012 오류 또는 “TLSSDK exchange ticket fail”이 발생하는 이유는 무엇입니까?

   - 초기화 API와 로그인 API는 별도로 호출해야 하며 연속적으로 호출할 수 없습니다(초기화 메소드에 비동기 작업이 있기 때문에).
   - IM 체험판을 사용 중이고 프로 버전으로 업그레이드하려는 경우, 업그레이드 후 콘솔에서 SDKAppID를 구성하여 정상적으로 로그인할 수 있습니다. 요금 정보는 [제품 가격](https://intl.cloud.tencent.com/document/product/1047/34350)을 참고하십시오.

   ### 6013 "SDK가 초기화되지 않음" 오류가 발생하는 이유는 무엇입니까?

   6013 "SDK가 초기화되지 않음" 오류가 발생하면 다음 문제 해결 방법을 시도하십시오.
   1. 로그인하기 전에 메시지 수발신 등 다른 작업을 수행했는지 확인합니다.
   2. 동일 계정이 다른 디바이스에서 이미 로그인되어 있는지 확인합니다. IM SDK는 기본적으로 하나의 계정으로 하나의 디바이스에 로그인할 수 있으며, 중복 로그인 시 강제 오프라인됩니다. 자세한 내용은 [멀티 단말 동시 로그인](https://intl.cloud.tencent.com/document/product/1047/33518) 문서를 참고하십시오.
   3. Android의 경우, 사용 도중 시스템에서 모든 라이브러리 파일을 로딩하거나 회수했는지 확인합니다.

   ### "code: 6205 desc: QALSERVICE not ready"가 발생하는 이유는 무엇입니까?

   초기화 후 `stopQALService`를 호출하면 이 오류가 발생합니다. 고객 중 한 명이 공유한 [구성 방법](https://blog.csdn.net/qq_16131393/article/details/54895733)을 참고하십시오.

   ### 이모티콘이 나타나지 않거나 깨짐 현상이 나타나는 이유는 무엇입니까?

   IM은 이모티콘 패키지를 제공하지 않습니다. 실질적인 파싱은 자체 정렬해야 합니다.
   이모티콘을 사용하는 방법에는 두 가지가 있습니다.
   - TIMFaceElem의 index를 사용하여 이모티콘의 인덱스를 식별합니다. 예를 들어, Android 디바이스와 iOS 디바이스에 동일한 이모티콘 세트가 있고, 인덱스 2는 웃음 이모티콘을 나타내는 경우, index=2일 때, 두 디바이스 모두 동일하게 색인된 이모티콘을 수/발신 합니다.
   - TIMFaceElem의 data를 사용합니다. 예를 들어, 이모티콘 이미지의 이름은 문자열 형식이며, smile 이라는 단어를 사용하여 웃음 이모티콘을 나타내고, smile을 data 에 저장합니다. 그런 다음 iOS 및 Android 디바이스 모두 data를 key로 사용하여 해당 이모티콘을 검색하고 표시합니다.

   두 필드를 동시에 사용할 수도 있습니다. 예를 들어. data를 사용하여 이모티콘 세트를 지정하고, index를 사용하여 해당 이모티콘 세트의 특정 인덱스를 나타냅니다. 이런 식으로 QQ에서와 같이 다양한 이모티콘 효과를 구현할 수 있습니다. 디바이스가 동일한 파싱 규칙을 따른다면, 더 복잡한 데이터 구조를 data 데이터에 저장할 수 있습니다.

   

   ### 작업 중에 오류 10002가 발생하는 이유는 무엇입니까?

   이 상태 코드는 서버 측 인증 중에 네트워크 예외, 시간 초과 또는 티켓 전환 실패가 발생할 때 반환됩니다. 이 상태 코드가 표시되면 잠시 기다렸다가 다시 시도하십시오.

   ### 메시지 수발신 시 오류 코드 6200 또는 6201이 발생하는 이유는 무엇입니까?

   이 상태 코드는 클라이언트 오프라인, 타임 아웃, 연결 끊김 시 반환됩니다. 오류 6200은 요청 전송 중 네트워크 연결 없음을, 오류 6201은 응답 전송 중 네트워크 연결 없음을 나타냅니다. 이 상태 코드가 표시되면 네트워크 상태를 확인하거나 네트워크가 복원될 때까지 기다렸다가 다시 시도하십시오.

   ### 메시지 수발신 시 오류 코드 20003이 발생하는 이유는 무엇입니까?

   이 오류 코드는 사용자 계정(UserID)이 유효하지 않거나, UserID를 IM으로 가져오지 않은 경우 반환됩니다. 이를 수정하려면 UserID를 Tencent Cloud로 가져왔는지 확인하십시오.

   ### 음성 메시지 재생 시 오류 코드 6010이 발생하는 이유는 무엇입니까?

   로밍 서버에서 더 이상 저장하지 않는 음성 메시지를 요청하면 이 오류 코드가 반환됩니다. [로밍 시간 연장](https://intl.cloud.tencent.com/document/product/1047/34419)을 통해 이를 수정하거나, 오디오 파일을 로컬 저장소에 다운로드하여 재생합니다. 만료된 파일은 복원할 수 없습니다. 다양한 SDK 버전을 통해 다양한 메시지 유형에 대한 저장 기간을 늘릴 수 있습니다. 자세한 내용은 [메시지 저장](https://intl.cloud.tencent.com/document/product/1047/33524)을 참고하십시오.

   ### 계정 인증 중 오류 코드 70001, 70003, 70009 또는 70013이 발생하는 이유는 무엇입니까?

   이러한 오류는 UserID와 UserSig가 일치하지 않기 때문에 발생합니다. 이를 수정하려면 UserID 및 UserSig의 유효성을 확인하십시오. 오류 코드 70001은 UserSig 만료, 오류 코드 70003은 잘린 UserSig로 인한 인증 실패, 오류 70009는 UserSig 공개키 확인 실패, 오류 70013은 UserID 불일치를 나타냅니다.

   ### Web 클라이언트 애플리케이션의 IM SDK 사용 시 오류 코드 -2 또는 -5가 발생하는 이유는 무엇입니까?

   - \-2: 일반적으로 네트워크 문제로 인해 서버에 대한 Web 애플리케이션 요청이 실패했음을 나타냅니다. Web 애플리케이션이 HTTP Long Polling 방법을 사용하여 서버에 요청 발송 시, 네트워크 문제가 발생하면 이 상태 코드가 반환됩니다. 문제를 해결하려면 네트워크를 확인하거나 다시 시도하십시오.
   - \-5: 로그인 작업이 완료되지 않았으며, SDK가 서버에서 반환된 a2key 및 tinyID를 수신하지 못한 경우, 다른 API를 직접 호출하면 "tinyid or a2 is empty" 오류 메시지와 -5 오류 코드가 반환됩니다.

   ### armeabi 플랫폼의 SDK가 "java.lang.UnsatisfiedLinkError: No implementation found for"의 오류 보고 시 어떻게 해결합니까?
   IM SDK의 aar 파일에 있는 jni/armeabi-v7a/libImSDK.so를 소스 코드 프로젝트의 src/main/jniLibs/armeabi 디렉터리에 복사하고 build.gradle에 로딩합니다.

   ### 애플리케이션 App Store 런칭 시, x86_64 및 i386 아키텍처 오류가 발생하면 어떻게 해결합니까?
   이 오류는 App Store가 x86_64 및 i386 아키텍처를 지원하지 않기 때문에 발생합니다. 해결방법은 다음과 같습니다.
   1. 프로젝트 컴파일 캐시 지우기:
    [Product]>[clean]을 선택하고 "clean build Folder..."가 나타날 때까지 Alt를 누른 다음 작업이 완료될 때까지 기다립니다.
   2. App Store에서 지원하지 않는 x86_64 및 i386 아키텍처를 제거합니다.
    a. [TARGETS]>[Build Phases]를 선택합니다.
     b. 덧셈 부호를 클릭하고, [New Run Script Phase]를 선택합니다.
     c. 다음 코드를 추가합니다.

   ```
   APP_PATH="${TARGET_BUILD_DIR}/${WRAPPER_NAME}"  
   
   # This script loops through the frameworks embedded in the application and  
   
   # removes unused architectures.  
   
    find "$APP_PATH" -name '*.framework' -type d | while read -r FRAMEWORK  
    do  
    FRAMEWORK_EXECUTABLE_NAME=$(defaults read "$FRAMEWORK/Info.plist" CFBundleExecutable)  
    FRAMEWORK_EXECUTABLE_PATH="$FRAMEWORK/$FRAMEWORK_EXECUTABLE_NAME"  
    echo "Executable is $FRAMEWORK_EXECUTABLE_PATH"  
   
    EXTRACTED_ARCHS=()  
   
    for ARCH in $ARCHS  
    do  
    echo "Extracting $ARCH from $FRAMEWORK_EXECUTABLE_NAME"  
    lipo -extract "$ARCH" "$FRAMEWORK_EXECUTABLE_PATH" -o "$FRAMEWORK_EXECUTABLE_PATH-$ARCH"  
    EXTRACTED_ARCHS+=("$FRAMEWORK_EXECUTABLE_PATH-$ARCH")  
    done  
   
    echo "Merging extracted architectures: ${ARCHS}"  
    lipo -o "$FRAMEWORK_EXECUTABLE_PATH-merged" -create "${EXTRACTED_ARCHS[@]}"  
    rm "${EXTRACTED_ARCHS[@]}"  
   
    echo "Replacing original executable with thinned version"  
    rm "$FRAMEWORK_EXECUTABLE_PATH"  
    mv "$FRAMEWORK_EXECUTABLE_PATH-merged" "$FRAMEWORK_EXECUTABLE_PATH"  
   
    done
   ```

    ![](https://main.qcloudimg.com/raw/f343cb4d7674d58623dfa0097d2c6484.png)

   3. 애플리케이션을 패키징하고 다시 업로드합니다.
