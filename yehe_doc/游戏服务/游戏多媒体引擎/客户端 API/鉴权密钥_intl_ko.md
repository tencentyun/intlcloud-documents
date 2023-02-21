
이 문서는 개발자가 GME를 쉽게 디버깅하고 통합할 수 있도록 모든 플랫폼에 대한 인증 키를 설명합니다.


## 음성 키 백엔드 배포
GME는 음성 채팅 및 오프라인 음성에 대한 인증 키를 제공합니다. 이 문서는 백엔드 배포 체계에 대해 설명합니다.
인증에 사용되는 서명 생성 프로세스에는 **플레인 텍스트**, **키** 및 **알고리즘**이 포함됩니다.

### 플레인 텍스트
플레인 텍스트는 네트워크 순서대로 다음 필드를 사용하여 구성됩니다.

|필드 설명   | 유형/길이|  값 정의/비고|
| ---------------- |-------------------|--------------|
| cVer|unsigned char(1)|버전 번호, 입력값: 1|
| wOpenIDLen|unsigned short(2)|사용자 계정 길이|
| strOpenID|wOpenIDLen|사용자의 계정 문자수|
| dwSdkAppid|unsigned short(4)|개발자 SDKappid|
| dwReserved1|unsigned int(4)|입력값: 0|
| dwExpTime|unsigned int(4)|만료 시각(현재시간+유효기간[단위: 초, 권장값 300 초])|
| dwReserved2|unsigned int(4)|입력값: -1 또는 0xFFFFFFFF|
| dwReserved3|unsigned int(4)|입력값: 0|
| wRoomIDLen|unsigned short(2)|사용자가 입장하고자 하는 방 ID의 길이. 오프라인 음성의 경우 0을 입력하십시오.|
| strRoomID|wRoomIDLen|사용자가 입장하고자 하는 방 ID의 문자수|

### 키
권한 키는 GME 콘솔에서 얻을 수 있습니다.

### 알고리즘
TEA 대칭 암호화 알고리즘이 사용됩니다.
초기 단계에서 클라이언트에 인증 기능을 배포하고 나중에 게임 App의 백엔드에 배포하는 것을 권장합니다.

|방안       | 장점        | 단점|
| ------------- |-------------|-------------| 
| 백엔드 배포    |보안성 높음|백엔드 개발자 공동 테스트 필요|
| 클라이언트 배포      |빠른 통합|보안성 낮음|

#### 백엔드 배포 구현 방법
백엔드에서 생성된 암호화된 문자열은 클라이언트로 전송되어 다음 시나리오에 사용됩니다. 방 입장을 위해 EnterRoom API가 호출되면 암호화된 문자열이 방 입장용 매개변수의 authBuffer 필드로 전송됩니다.




### 암호화 알고리즘 상세 정보
- 키: APPID에 해당하는 인증 키의 MD5 값으로 길이는 16바이트입니다.
- 암호화 알고리즘: TEA
- 암호화 라이브러리 및 샘플: [authbuffer.zip](https://main.qcloudimg.com/raw/c8be793e20c85114499f52e0f8c29190.zip) 참조

>!수정된 키는 15분에서 1시간 이내에 적용됩니다. 빈번한 수정은 권장하지 않습니다.



#### 암호화 메소드	
1. 플레인 텍스트의 숫자를 네트워크 바이트 순서로 변환합니다.
2. 플레인 텍스트를 순서대로(플레인 텍스트 필드가 선언된 순서) 문자열로 구성합니다.
3. tea를 사용하여 스티칭된 문자열을 암호화합니다. symmetry_encrypt 함수가 출력한 문자열은 암호화된 권한 문자열입니다.

>!이진법 문자열을 16진법으로 변환하지 마십시오.


## 예시 코드
C++ 언어를 예로 들면 인증 키의 예시 코드는 다음과 같습니다.
```C++
unsigned char pInBuf[512]={0};
    xel::byte_writer bw(pInBuf, sizeof(pInBuf));
    
    char cVer = 1;
    unsigned short wOpenIDLen = (unsigned short)strlen((const char *)strOpenID);
        if (wOpenIDLen > 127) wOpenIDLen = 127;
    unsigned short wRoomIDLen = (unsigned short)strlen((const char *)strRoomID);
        if (wRoomIDLen > 127) wRoomIDLen = 127;
    
    bw.write_byte(cVer);
    bw.write_int16(wOpenIDLen);
    bw.write_bytes(strOpenID, wOpenIDLen);
    bw.write_int32(dwSdkAppId);
    bw.write_int32(0 /*dwRoomID*/);
    bw.write_int32(expTime);
    bw.write_int32(nAuthBits);
    bw.write_int32(0 /*dwAccountType*/);
    bw.write_int16(wRoomIDLen);
    bw.write_bytes(strRoomID, wRoomIDLen);
    
    int pInLen = bw.bytes_write();
    
        unsigned char pEncryptOutBuf[512] = { 0 };
    int iEncrptyLen = 0;
    
        symmetry_encrypt((const unsigned char*)pInBuf, pInLen, (const unsigned char*)key, (unsigned char*)pEncryptOutBuf, &iEncrptyLen);
```

Java 및 Go 언어 예시 코드 또한 제공합니다. [다운로드하려면 클릭 >>](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/authbuffer_go_java.zip)하십시오.

