## SDK 준비
관련 [Demo 및 SDK](https://main.qcloudimg.com/raw/5ef28eba111891591f576dbbbaed601c.zip) 다운로드. 본문은 주로 Android, iOS와 Windows 세 가지 버전의 액세스 가이드를 포함하고 있습니다.

## Android 액세스
### 예비 작업
- SDK에 액세스하려면 다음 절차를 완료해야 합니다.
 1. 실행 플랫폼에 따라 상응하는 so 파일을 선택하고, so 파일과 jar 파일을 프로세스 디렉터리에 복사하고 의존 라이브러리를 추가합니다.
 2. SDK 인터페이스 함수를 호출하고, 워터마크 정보를 생성합니다.
 3. 메시지 발송 시, 20바이트의 워터마크 정보가 정보체 앞에 놓입니다.
- SDK 파일은 so 파일과 jar 파일을 포함하며, 디렉터리 구조는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/917fa4204160a4def749d5c71a98f810.png)
- SDK API 설명
 - 프로그램 패키지: com.gamesec
 - 유형: Mark
- 인터페이스 설명: 
<table>
<tbody>
<tr>
<th>인터페이스 이름</th>
<th>설명</th></tr>
<tr>
<td>CreateSDKBuffFromStr</td>
<td>워터마크 생성</td></tr></tbody></table>

### 액세스 절차(Android Studio)
1. sdk/android 폴더 내용을 프로세스 디렉터리의 libs 폴더에 복사합니다.
 ![](https://main.qcloudimg.com/raw/10957eeaba136e56d53528d4cedc4001.png)
2. 프로젝트의 build.gradle 파일을 수정하고, jni 파일 디렉터리를 설정하며, jar 의존을 추가합니다.
```
android {
		sourceSets {
				main {
						jniLibs.srcDirs =['libs/jni'] // jni 디렉터리 설정
					 }
				   }
			}
		dependencies {
						implementation files('libs/gamesec.jar') // 의존 추가
				     }
```
3. Eclipse 액세스 방법은 이와 유사하며, build.gradle 파일을 구성할 필요가 없습니다.

### 인터페이스 호출
1. 프로그램 패키지를 가져옵니다.
```
import com.gamesec.*;
```
2. Mark 개체를 인스턴스화합니다.
```
Mark mark = new Mark();
```
3. CreateSDKBuffFromStr를 호출하여 워터마크를 생성합니다.
```
byte [ ] CreateSDKBuffFromStr (String pSDKinfo, String buffer, String uDesIp, int uDesPort)
```
 - **매개변수 설명:**
<table>
<tr>
<th>매개변수</th>
<th>유형</th>
<th>의미</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>String</td>
<td>워터마크 방어 키</td>
</tr>
<tr>
<td>buffer</td>
<td>String</td>
<td>자리채우미 매개변수입니다. 빈 문자열을 가져오면 됩니다.</td>
</tr>
<tr>
<td>uDeslp</td>
<td>String</td>
<td>서버 IP, 예: “1.2.3.4”</td>
</tr>
<tr>
<td>uDesPort</td>
<td>int</td>
<td>서버 포트</td>
</tr>
</table>
 - **반환값**
<table>
<tr>
<th>유형</th>
<th>의미</th>
</tr>
<tr>
<td>byte[]</td>
<td>컴퓨팅 워터마크 정보, 20바이트 추출</td>
</tr>
</table>
 - **호출 예시: **
```
String pSDKinfo = "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
String uDesIp = "115.159.147.198";
int uDesPort = 8899 ;
byte[] bytes = mark.CreateSDKBuffFromStr(pSDKinfo, "", uDesIp, uDesPort);
```

4. 워터마크 정보를 정보체에 추가합니다. 코드 예시는 다음과 같습니다.
```
Socket s = new Socket(uDesIp, uDesPort);
OutputStream out = s.getOutputStream();
PrintWriter output = new PrintWriter(out, true);
// 우선 워터마크 정보를 입력합니다.
output.print(bytes); 
output.println("msg msg msg");
BufferedReader input = new BufferedReader(new InputStreamReader(s.getInputStream()));
String msg = input.readLine();
s.close();
```

## iOS 액세스

### 예비 작업
- SDK에 액세스하려면 다음 절차를 완료해야 합니다.
	1. SDK 파일을 프로세스 디렉터리에 복사합니다. Swift 프로세스에는 브리지 파일을 추가해야 합니다.
	2. SDK 인터페이스 함수를 호출하고, 워터마크 정보를 생성합니다.
	3. 메시지 발송 시, 20바이트의 워터마크 정보가 정보체 앞에 놓입니다.
- SDK 파일은 a 파일과 h 파일을 포함합니다. 디렉터리 구조는 다음과 같습니다.
 ![](https://main.qcloudimg.com/raw/64126dc978ed27a9c4c5d02ad906a250.png)
- 인터페이스 설명:
<table>
<tbody>
<tr>
<th>인터페이스 이름</th>
<th>설명</th></tr>
<tr>
<td>CreateSDKBuffFromStr</td>
<td>워터마크 생성</td></tr></tbody></table>

### 액세스 절차(Xcode)
1. SDK/ios 폴더의 내용을 프로세스 디렉터리에 복사합니다.
![](https://main.qcloudimg.com/raw/1e6284a08a2d17c9138e4442cb7204b1.png)
2. SDK 파일을 Xcode에 추가합니다. 프로세스 이름을 마우스 우클릭하고, “Add Files to”를 클릭합니다.
![](https://main.qcloudimg.com/raw/d2dc416312ca9c2b244c7a0ba75ce841.png)
3. 대화 상자에서 “Create folder references”를 선택하고, SDK의 두 파일을 선택한 뒤, 추가를 클릭합니다.
![](https://main.qcloudimg.com/raw/2a7bf9fb066bd7c4ab584eb4287a5f1b.png)
4. 프로세스 이름을 좌클릭하고 General을 선택한 뒤, a 파일을 “Linked Framews and Libraries”에 추가합니다.
![](https://main.qcloudimg.com/raw/b509d322e2cb7485c848f4226ed9ccfd.png)
5. Swift 프로젝트의 경우, 브리지 파일을 생성해야 하며, Object-C 프로젝트의 경우, 해당 절차를 넘어갈 수 있습니다. Header File 1개를 생성하여 bridge.h라 명명합니다. 파일에 아래 코드를 추가합니다.
			# import "gamesec.h";
6. 프로세스 이름을 좌클릭하고 Build Settings를 선택하여 bridge.h를 Object-C Bridging Header에 추가합니다.
![](https://main.qcloudimg.com/raw/2a7bf9fb066bd7c4ab584eb4287a5f1b.png)

### 인터페이스 호출

1. Swift 프로젝트는 워터마크 생성 함수를 직접 호출할 수 있으며, Object-C 프로젝트는 사용하는 파일에 헤더 파일을 추가해야 합니다.
```
# import "gamesec.h";
```
2. CreateSDKBuffFromStr를 호출하여 워터마크를 생성합니다.
```
uint32_t CreateSDKBuffFromStr(char *pSDKinfo, uint8_t *buffer, char* uDstIp, uint16_tuDstPort);
```
**매개변수 설명:**
<table>
<tr>
<th>매개변수</th>
<th>유형</th>
<th>의미</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>char *</td>
<td>워터마크 방어 키</td>
</tr>
<tr>
<td>buffer</td>
<td>uint8_t *</td>
<td>워터마크 포인터, 워터마크 결과 출력</td>
</tr>
<tr>
<td>uDeslp</td>
<td>char *</td>
<td>서버 IP, 예: “1.2.3.4”</td>
</tr>
<tr>
<td>uDesPort</td>
<td>uint16_t</td>
<td>서버 포트</td>
</tr>
</table>
 
 >**주의:**
 >워터마크 결과는 매개변수 buffer에 저장되며 20바이트를 추출합니다.
3. 예시를 호출합니다
**Swift 호출**
```
	let pSDKinfo = UnsafeMutablePointer<Int8>(mutating: (
			"566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c" 
			as NSString).utf8String);
					var buffer = UnsafeMutablePointer<UInt8>.allocate(capacity: 20);
			let uDstIp = UnsafeMutablePointer<Int8>(mutating: (
			"115.159.147.198" as NSString).utf8String);
					let uDstport = UInt16.init("8899")!;

			CreateSDKBuffFromStr(pSDKinfo, buffer, uDstIp, uDstport);

					for i in 0 ..< 20 {
							let b = (buffer+i).pointee;
							// 워터마크 정보는 앞 20바이트입니다. 출력은 uint8이니 주의하십시오.
							print(" \(b)");
					}
**Object-C 호출:** 

			char *pSDKinfo = "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
					uint8_t buffer[20];
					char *uDstIp = "115.159.147.198";
					uint16_t uDstPort = 8899;

					CreateSDKBuffFromStr(pSDKinfo, buffer, uDstIp, uDstPort);

					for(int i=0;i<20;i++)
			{
					// 워터마크 정보는 앞 20바이트입니다.
							NSLog(@"%d", (int8_t)buffer[i]); 
			}
```
4. 메시지 발송 전, 20바이트의 워터마크 정보를 정보체 앞쪽에 추가합니다.

## Windows 액세스
### 예비 작업
SDK는 gamesec.dll 파일이며, 워터마크 생성 함수가 1개 있습니다.
```
uint32_t CreateSDKBuffFromStr(char *pSDKinfo, uint8_t *buffer, char* uDstIp, uint16_t uDstPort);
```
**매개변수 설명:**
<table>
<tr>
<th>매개변수</th>
<th>유형</th>
<th>의미</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>char *</td>
<td>워터마크 방어 키</td>
</tr>
<tr>
<td>buffer</td>
<td>uint8_t *</td>
<td>워터마크 포인터, 워터마크 결과 출력</td>
</tr>
<tr>
<td>uDeslp</td>
<td>char *</td>
<td>서버 IP, 예: “1.2.3.4”</td>
</tr>
<tr>
<td>uDesPort</td>
<td>uint16_t</td>
<td>서버 포트</td>
</tr>
</table>

 >**주의:**
>워터마크 결과는 매개변수 buffer에 저장되며 20바이트를 추출합니다.


### 인터페이스 호출

워터마크 함수를 사용할 때, 우선 dll 파일을 가져옵니다. LoadLibrary 함수를 사용할 수 있습니다(Windows.h 추가해야 함).
```
 // 함수 포인터 정의
    typedef int(*FUNC)(char *, uint8_t *, char* , uint16_t );
    // dll 경로 설정
    HINSTANCE Hint = ::LoadLibrary(L"E:\\sdk\\gamesec.dll");
    FUNC CreateSDKBuffFromStr = (FUNC)GetProcAddress(Hint, "CreateSDKBuffFromStr");
```
완전한 호출 예시:
```
 // 워터마크 저장
    uint8_t buffer[BUFFER_SIZE];
    memset(buffer, 0, BUFFER_SIZE);
    
    int UDP_TEST_PORT = 8899;
    
    const char * CONST_UDP_SERVER_IP  = "115.159.147.198";
    char * UDP_SERVER_IP = new char[strlen(CONST_UDP_SERVER_IP)];
    strcpy(UDP_SERVER_IP, CONST_UDP_SERVER_IP);
    
    const char * CONST_pSDKinfo = 
    "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
    char * pSDKinfo = new char[strlen(CONST_pSDKinfo)];
    strcpy(pSDKinfo, CONST_pSDKinfo);
    
    // 10회 호출
    for (int i = 0; i < 5; i++) {
    CreateSDKBuffFromStr(pSDKinfo, buffer, (char *)UDP_SERVER_IP, UDP_TEST_PORT);
    
    for (int i = 0; i <= 20; i++)
    {
    // 워터마크는 앞쪽 20바이트에 있습니다.
    printf("%d ", (int8_t)buffer[i]);
    }
    printf("\n\n");
    }
```

