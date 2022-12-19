## 소개

COS 콘솔을 사용하여 버킷의 단일 객체 또는 여러 객체를 원본 경로에서 대상 경로로 복사할 수 있습니다.

>?
> - ARCHIVE 스토리지 클래스의 객체에 대해 복사 및 붙여넣기가 지원되지 않습니다.
> - MAZ_STANDARD(다중AZ STANDARD) 스토리지 클래스는 STANDARD, STANDARD_IA 또는 ARCHIVE 스토리지 클래스가 아닌 정확히 동일한 클래스로의 복제만 지원합니다.
> - MAZ_STANDARD_IA 스토리지 클래스는 STANDARD, STANDARD_IA 및 ARCHIVE 스토리지 클래스가 아닌 완전히 동일한 클래스로의 복제만 지원합니다.
> - 객체를 복사하려면 서브 계정에 PutObject, GetObject, GetObjectACL의 3개 권한이 부여되어야 합니다.
> 

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 대상 버킷의 이름을 클릭하여 파일 목록 페이지로 이동합니다.
4. 객체 또는 폴더를 하나 이상 선택하고 상단의 **추가 작업 > 복사**를 클릭합니다.
5. 복사에 성공했다는 메시지가 표시되면 대상 경로를 선택하고 상단의 **추가 작업 > 붙여넣기**를 클릭합니다.
예를 들어 examplebucket1-1250000000 버킷의 target 폴더에 붙여넣을 수 있습니다.
![](https://main.qcloudimg.com/raw/c5ced94c2d09085efb55bf39a87a258b.png)
>! 대상 경로는 원본 경로와 같을 수 없습니다. 동일한 경우 붙여넣기가 실패합니다.
>

