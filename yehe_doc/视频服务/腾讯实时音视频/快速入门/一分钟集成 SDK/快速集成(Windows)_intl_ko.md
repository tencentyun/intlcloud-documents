본 문서에서는 Tencent Cloud TRTC SDK(Windows C# 및 C++ 버전)를 프로젝트에 빠르게 통합하는 방법을 소개합니다.

## 개발 환경 요구사항

- 운영 체제: Windows 7 이상 버전
- 개발 환경: Visual Studio 2010 이상 버전, Visual Studio 2015 사용 권장
- 개발 프레임워크: .Net Framework 4.0 이상 버전

## TRTC C# SDK 통합

본 장에서는 간단한 Winform 프로젝트를 생성하는 예시를 통해 Visual Studio에 C# SDK를 통합하는 방법을 소개합니다.

[](id:step1)
### 1단계: Windows SDK 다운로드 
[SDK 다운로드](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip) 후 압축을 해제하고 파일을 열어줍니다. 파일에는 다음이 포함되어 있습니다.

| 디렉터리명  | 설명                                   |
| ------- | -------------------------------------- |
| xxxDemo | C++ Demo 소스코드, C# Demo 소스코드 |
| CPlusPlus | C++ 32비트/64비트 종속 SDK 라이브러리 파일 |
| CSharp | C# 32비트/64비트 종속 SDK 라이브러리 파일 |

본 문서 예시에서는 SDK 레퍼런스 디렉터리의 C# SDK 파일만 필요합니다.

[](id:step2)
### 2단계: 프로젝트 생성
Visual Studio를 열어 `TRTCCSharpDemo` 이름의 Winform 응용 프로그램을 생성합니다.

[](id:step3)
### 3단계: 파일 복사
압축 해제한 SDK 파일을 `TRTCCSharpDemo.csproj`가 있는 디렉터리에 복사합니다.
>?C# SDK만 필요한 경우, SDK 경로에 있는 CPlusPlus 디렉터리를 삭제할 수 있습니다.



[](id:step4)
### 4단계: 프로젝트 설정 수정
#### 4.1단계: 레퍼런스 추가
1. Visual Studio의 [생성] 디렉터리에서 [설정 관리자]를 찾아 열어줍니다. [](id:step4_1_2)
2. [이벤트 솔루션 플랫폼] 드롭다운 목록에서 [생성]을 선택하면 [솔루션 플랫폼 생성] 대화 상자가 팝업됩니다. [](id:step4_1_3)
3. 신규 플랫폼을 입력하거나 선택한 후 [확인]을 클릭합니다.

4. 필요에 따라 [2단계](#step4_1_2) ~ [3단계](#step4_1_3)를 반복해 지원이 필요한 솔루션 플랫폼을 생성합니다.

5. TRTCCSharpDemo가 있는 폴더를 열고 본문 편집기를 사용해 `TRTCCSharpDemo.csproj` 파일을 편집합니다.
6. `TRTCCSharpDemo.csproj` 파일의 `<itemGroup>` 태그에 다음 내용을 추가합니다.
```
  //각각의 플랫폼에 있는 레퍼런스 추가
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'x64'">
		<HintPath>SDK\CSharp\Win64\lib\ManageLiteAV.dll</HintPath>
  </Reference>
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'AnyCPU'">
		<HintPath>SDK\CSharp\Win64\lib\ManageLiteAV.dll</HintPath>
  </Reference>
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'x86'">
		<HintPath>SDK\CSharp\Win32\lib\ManageLiteAV.dll</HintPath>
  </Reference>
```


#### 4.2단계: copy 명령어 추가
1. TRTCCSharpDemo 속성 페이지를 열어 [솔루션 리소스 관리자] > [TRTCCSharpDemo 프로젝트 오른쪽 메뉴] > [속성]을 선택합니다.
2. [이벤트 생성] > [이후 이벤트 생성 명령 라인]에 다음 명령어를 추가하면, 다음 이미지와 같이 컴파일링 완료 후 자동으로 각 플랫폼별 SDK의 .dll 파일이 프로그램 실행 디렉터리에 복사됩니다.
```
set Platform=Win64
SETLOCAL ENABLEDELAYEDEXPANSION
if $(PlatformName)==x86 ( 
  set Platform=Win32
)
copy /Y "$(ProjectDir)SDK\CSharp\!Platform!\lib\*.dll" "$(ProjectDir)$(OutDir)"
ENDLOCAL
```


#### 4.3단계: 디버깅 환경 수정
다음 이미지와 같이 TRTCDemo 속성 페이지를 열어 [생성]을 선택해 [플랫폼(M)]과 상부 메뉴바 상의 솔루션 플랫폼을 동일하게 설정합니다.


[](id:step5)
### 5단계: SDK 버전 출력
1. 다음 이미지와 같이 Form1.cs 디자이너에서 label 제어 파일 1개를 추가합니다.
2. Form1.cs 코드 파일을 열고 다음 코드를 추가합니다.
```c#
	using System.Windows.Forms;
	using ManageLiteAV;   // 1. 네임스페이스 레퍼런스 추가

	namespace TRTCCSharpDemo
	{
			public partial class Form1 : Form
			{
					public Form1()
					{
							InitializeComponent();
							// 2. ITRTCCloud 인스턴스 획득, SDK 버전 출력
							ITRTCCloud lTRTCCloud = ITRTCCloud.getTRTCShareInstance(); 
							this.label1.Text = "SDK version : " + lTRTCCloud.getSDKVersion();
							// 3. 사용 완료 시 수동으로 ITRTCCloud 인스턴스 삭제 필요
							ITRTCCloud.destroyTRTCShareInstance();
					}
			}
	}
```
3. F5를 눌러 실행하여 SDK 버전을 출력합니다. (다음 이미지 참조)
 ![](https://main.qcloudimg.com/raw/9bfebaac4fa339af6b7c74b0413cde1d.png)


[](id:using_cpp)
## TRTC C++ SDK 통합

본 장에서는 간단한 MFC 프로젝트를 생성하는 예시를 통해 Visual Studio에 C++ SDK를 통합하는 방법을 소개합니다.

[](id:using_cpp_step1)
### 1단계: SDK 다운로드
[SDK 다운로드](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip) 후 압축을 해제하고 열어줍니다. 파일에는 다음이 포함되어 있습니다.

| 디렉터리명  | 설명                                   |
| ------- | -------------------------------------- |
| include | 상세한 인터페이스 주석이 포함되어 있는 API 헤더 파일           |
| lib     | 컴파일용 .lib 파일 및 실행 시 로딩하는 .dll 파일 |


[](id:using_cpp_step2)
### 2단계: 프로젝트 생성
다음 이미지와 같이 Visual Studio를 열어 TRTCDemo 이름의 MFC 응용 프로그램을 생성합니다.


본 문서에서는 빠른 통합 설명을 위해 **응용 프로그램 유형** 선택 페이지에서 비교적 간단한 **대화 상자 기반** 유형을 선택하겠습니다. 다음 이미지와 같습니다.


기타 가이드 설정은 기본 설정으로 두면 됩니다.


[](id:using_cpp_step3)
### 3단계: 파일 복사
다음 이미지와 같이 압축 해제한 LiteAVSDK 파일을 TRTCDemo.vcxproj가 있는 디렉터리에 복사합니다.



[](id:using_cpp_step4)
### 4단계: 프로젝트 설정 수정
TRTCDemo 속성 페이지를 열어 [솔루션 리소스 관리자] > [TRTCDemo 프로젝트 오른쪽 메뉴] > [속성]을 선택하고 다음 순서에 따라 설정합니다.

1. **포함 디렉터리 추가**
다음 이미지와 같이 [C/C++] > [일반] > [포함 디렉터리 추가]에서 SDK 헤더 디렉터리 `$(ProjectDir)LiteAVSDK\include`와 `$(ProjectDir)LiteAVSDK\include\TRTC`를 추가합니다.

2. **라이브러리 디렉터리 추가**
다음 이미지와 같이 [링커] > [일반] > [라이브러리 디렉터리 추가]에서 SDK 라이브러리 디렉터리 `$(ProjectDir)LiteAVSDK\lib`를 추가합니다.

3. **라이브러리 파일 추가**
다음 이미지와 같이 [링커] > [가져오기] > [종속 항목 추가]에서 SDK 라이브러리 파일 `liteav.lib`를 추가합니다.

4. **copy 명령어 추가**
[이벤트 생성] > [이후 이벤트 생성] > [명령 라인]에 명령어 `copy /Y "$(ProjectDir)LiteAVSDK\lib\\\*.dll" "\$(OutDir)"`을 복사 및 추가하면 컴파일 완료 후 자동으로 SDK의 .dll 파일이 프로그램 실행 디렉터리에 복사됩니다. 다음 이미지와 같습니다.



[](id:using_cpp_step5)
### 5단계: SDK 버전 출력
- `CTRTCDemoDlg::OnInitDialog` 함수에 다음 테스트 코드를 추가합니다.
<dx-codeblock>
:::  c++  c++
ITRTCCloud * pTRTCCloud = getTRTCShareInstance();
std::string version(pTRTCCloud->getSDKVersion());
CString szText;
szText.Format(L"SDK version: %hs", version.c_str());

CWnd *pStatic = GetDlgItem(IDC_STATIC);
pStatic->SetWindowTextW(szText);
:::
</dx-codeblock>
- F5를 눌러 실행하면 다음 이미지와 같이 SDK 버전이 출력됩니다.  
![](https://main.qcloudimg.com/raw/6851ab7f24d95ae8115fdf5f69e36a3b.png)


## FAQ
- 다음 오류가 발생하는 경우 [프로젝트 설정 수정](#step4)에 따라 SDK 레퍼런스가 프로젝트에 추가되었는지 확인합니다.
```
오류 CS0246은 유형 또는 네임스페이스명 “ManageLiteAV”(using 명령 또는 어셈블리 레퍼런스가 있는지 확인)를 찾을 수 없는 경우입니다.
```

- 다음 오류가 발생하는 경우 [프로젝트 설정 수정](#step4)에 따라 프로젝트 실행 플랫폼 환경을 솔루션의 현재 타깃 플랫폼으로 수정했는지 확인합니다.
```
System.BadImageFormatException:“파일 또는 어셈블리의 “ManageLiteAV, Version=2.0.7152.18518, Culture=neutral, PublicKeyToken=null” 또는 해당 종속 항목을 로딩할 수 없습니다. 정확하지 않은 포맷의 프로그램이 로딩되었습니다.”
```

- 다음 오류가 발생하는 경우 [프로젝트 설정 수정](#step4)에 따라 생성 이벤트를 실행 디렉터리에 정확하게 추가했는지 확인합니다.
```
System.IO.FileNotFoundException:“파일 또는 어셈블리의 “ManageLiteAV.dll” 또는 해당 종속 항목을 로딩할 수 없습니다. 지정한 모듈을 찾을 수 없습니다.”
```

- Windows 버전별 호환성 문제로, 현재 C# SDK에 호환성 문제 해결을 위한 dll 파일을 신규 추가하였습니다. 추가된 파일 리스트는 다음 이미지와 같습니다.

- 다음 오류가 발생하는 경우 상기 프로그램 설정에 따라 SDK 헤더 파일의 디렉터리를 정확하게 추가했는지 확인합니다.
```
fatal error C1083: 포함된 파일을 열 수 없습니다. “TRTCCloud.h”: No such file or directory
```

- 다음 오류가 발생하는 경우 상기 프로그램 설정에 따라 SDK 라이브러리 디렉터리 및 라이브러리 파일을 정확하게 추가했는지 확인합니다.
```
error LNK2019: 리졸브할 수 없는 외부 부호 "__declspec(dllimport) public: static class TXString __cdecl TRTCCloud::getSDKVersion(void)" (__imp_?getSDKVersion@TRTCCloud@@SA?AVTXString@@XZ), 해당 부호는 "protected: virtual int __thiscall CTRTCDemoDlg::OnInitDialog(void)" (?OnInitDialog@CTRTCDemoDlg@@MAEHXZ) 함수에 참조됩니다.
```
